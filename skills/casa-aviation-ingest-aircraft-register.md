---
name: Ingest the Australian civil aircraft register
description: Download, validate and refresh the complete Australian Civil Aircraft Register from CASA, without re-downloading unchanged data and without the four parsing bugs that silently corrupt this file.
api: casa-aviation:casa-aircraft-register-data
generated: '2026-07-28'
method: generated
grounding: >-
  There is no OpenAPI for this surface, so this skill is grounded in real HTTP
  requests verified live on 2026-07-28 rather than in operationIds. Every URL,
  header, status code and column name below was observed on the wire; none is
  invented.
operations:
  - GET https://services.casa.gov.au/CSV/acrftreg.csv
  - GET https://services.casa.gov.au/CSV/acrftreg.zip
  - HEAD https://services.casa.gov.au/CSV/acrftreg.csv
artifacts:
  - json-schema/casa-aviation-aircraft-register-row.schema.json
  - vocabulary/casa-aviation-vocabulary.yml
  - examples/casa-aviation-aircraft-register-examples.json
  - conventions/casa-aviation-conventions.yml
  - errors/casa-aviation-problem-types.yml
---

# Ingest the Australian civil aircraft register

CASA publishes the whole register as one file. There is no query API, no
pagination, no per-aircraft endpoint and no key. You download the file, you
parse it, you filter locally.

## 1. Send a User-Agent, or you get a 403

`services.casa.gov.au` returns **403** to unadorned programmatic clients and
**200** to a browser-style `User-Agent`. This is edge filtering, not
authentication and not a rate limit. Set a descriptive User-Agent that names
your application and retry once. Do **not** back off exponentially and do
**not** treat it as a permission error.

## 2. Poll conditionally

Both validators are served and both conditional headers are honoured (verified
2026-07-28 — a conditional poll returns `304` with a zero-byte body):

```
GET /CSV/acrftreg.csv
If-None-Match: "<etag you stored>"
If-Modified-Since: <Last-Modified you stored>
```

* `304` → nothing changed, stop.
* `200` → store the new `ETag` and `Last-Modified`, then continue to step 3.

The file is regenerated daily. Poll once a day. There is no changelog, no
version field and no generated-at timestamp inside the file, so `Last-Modified`
is your only freshness signal.

Prefer `acrftreg.zip` (~1.3MB) over `acrftreg.csv` (~6.7MB): the host does
**not** offer gzip, so the pre-zipped file is the only compression available.
`HEAD` and `Range: bytes=0-200` both work if you only need the header row.

## 3. Parse it correctly — four bugs that bite

1. **The file has a UTF-8 BOM.** Open it with `encoding='utf-8-sig'` or the
   first column parses as `﻿Mark` and your primary key silently vanishes.
2. **Dates are `DD/MM/YYYY`**, Australian order — `regholdCommdate`,
   `regopCommdate`, `Datefirstreg`, `Regexpirydate`, `suspenddate`. Parsing them
   as US `MM/DD/YYYY` corrupts every day-of-month above 12 without erroring.
   (The AD product uses ISO `YYYY-MM-DD`. The two CASA products disagree.)
3. **`Content-Type` is `application/octet-stream`, not `text/csv`.** Do not
   content-type sniff.
4. **`Mark` has no `VH-` prefix.** `87X` is aircraft VH-87X. Add the prefix
   yourself when displaying or joining to any other aviation dataset.

## 4. Validate before you replace your copy

Validate each row against
`json-schema/casa-aviation-aircraft-register-row.schema.json` (44 columns).
CASA gives no notice of format changes, so schema validation on every ingest is
the only defence you have. Fail the ingest and keep the previous snapshot rather
than half-loading a changed file.

## 5. Know what the data does and does not say

* **It is a snapshot, not a history.** Only currently registered aircraft are in
  the file (16,660 rows on 2026-07-28). Deregistered aircraft simply disappear —
  if you need history, diff your own snapshots.
* **`gear` and `CoAcatc` are empty in every row.** Do not build features on them.
* **`CoAcata`/`CoAcatb` are composite**, shaped `State (Category; Category)`.
  Parse them; do not string-match. The experimental, amateur-built, light-sport
  and ex-military fleets live almost entirely in `CoAcatb`, which is empty in
  13,987 of 16,660 rows — reading only `CoAcata` will miss them.
* **State fields are free text** with 94 distinct values across 8 real states
  (`NSW` and `New South Wales` and `.` all appear). Normalise before any
  geographic rollup.
* **Holder and operator are denormalised free text with no party identifier.**
  Entity resolution is your problem, and the same legal entity appears once per
  aircraft.
* **The file contains personal data.** Roughly a third of registration holders
  are private individuals, with name and full postal address. Treat it as
  personal information under Australian privacy law: do not republish rows
  wholesale, and redact holder/operator address lines in anything you publish.

The complete, exhaustive value set for every enumerable column is in
`vocabulary/casa-aviation-vocabulary.yml`.

## 6. Joining out

`ICAOtypedesig` (ICAO Doc 8643) is the only field that joins cleanly to FAA,
EASA, ADS-B, MRO and insurance datasets. `Serial` and `Typecert` are useful
secondary keys. Nothing in this file joins to the Airworthiness Directives
product — see the AD skill for why.
