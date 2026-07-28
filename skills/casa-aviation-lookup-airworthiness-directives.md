---
name: Look up Australian Airworthiness Directives and fetch the AD document
description: Pull CASA's full Airworthiness Directive listing, filter it correctly by status and type series, and resolve any directive to its real PDF using the undocumented AD document URL template.
api: casa-aviation:casa-airworthiness-directives-data
generated: '2026-07-28'
method: generated
grounding: >-
  There is no OpenAPI for this surface, so this skill is grounded in real HTTP
  requests and real field values verified live on 2026-07-28 rather than in
  operationIds. The AD document URL template was derived by API Evangelist and
  verified against records spanning multiple groups; CASA does not publish it.
operations:
  - GET https://services.casa.gov.au/JSON/combinedadweb.json
  - GET https://services.casa.gov.au/airworth/airwd/data/adweb.csv
  - GET https://services.casa.gov.au/airworth/airwd/data/folder.csv
  - GET https://services.casa.gov.au/airworth/airwd/ADfiles/{grouptitle}/{foldername}/{ADFILE}
artifacts:
  - json-schema/casa-aviation-airworthiness-directive.schema.json
  - vocabulary/casa-aviation-vocabulary.yml
  - examples/casa-aviation-airworthiness-directives-examples.json
  - conventions/casa-aviation-conventions.yml
  - data-model/casa-aviation-data-model.yml
---

# Look up Australian Airworthiness Directives

## 1. Take the JSON, not the CSVs

`combinedadweb.json` is exactly `adweb.csv` joined to `folder.csv` — verified
field-by-field across all 17,738 records with zero mismatches. If you consume
the JSON you never need either CSV. If you consume the CSVs you have to do that
join yourself, on `FOLDERNAME`.

```
GET https://services.casa.gov.au/JSON/combinedadweb.json
User-Agent: <your application>
If-None-Match: "<etag you stored>"
```

A missing `User-Agent` gets you a **403** (edge filtering, not auth). A matching
`ETag` gets you a **304** with an empty body — poll conditionally rather than
pulling 7.3MB. There is no gzip on this host and no zipped equivalent of the AD
JSON, so a real change always costs the full 7.3MB.

## 2. Read the envelope

The document is `{"DATA": [ ... ]}` — a single top-level array with no record
count, no generated-at timestamp and no metadata. 17,738 records on 2026-07-28.
Validate against `json-schema/casa-aviation-airworthiness-directive.schema.json`
before use; CASA states on its own data-files page that *"the format of this
file is subject to change"* and provides no notice channel.

## 3. Filter on `Status` — and get it right

`Status` has exactly three values:

| Value | Count | Meaning |
|---|---|---|
| `Active` | 12,993 | In force |
| `Cancelled` | 4,326 | Withdrawn — still published in the file |
| `Urgent` | 419 | Urgent AD, **in force** |

Two failure modes, both silent:

* Not filtering at all means **24.4% of what you show is withdrawn regulation**.
* Filtering `Status == "Active"` **drops all 419 urgent directives**, which are
  the ones that matter most. The correct in-force filter is
  `Status in ("Active", "Urgent")`.

## 4. Handle the empty and null fields

* `EffectiveDate` is an empty string in 10,893 of 17,738 records; `PublishedDate`
  in 10,817. Date parsers that assume a value will throw on most of the file.
* `ADIssueNumber` is `null` in 4,566 records and also carries the literal string
  `"NK"` (not known). Treat `null`, `""` and `"NK"` as absence.
* Dates that are present are ISO `YYYY-MM-DD` — unlike the aircraft register,
  which uses `DD/MM/YYYY`.
* `GROUPS` is a comma-and-space delimited **string** (`"AIRGEN, ROTOR, UNDER,
  OVER"`), not an array. Split it.
* `Authority` is free text with 25 spellings for far fewer regulators — `FAA`
  and `USA - FAA`, `EASA` and `EASa`, `Canada` and `CANADA` and the typo
  `Candada`. Only 11,940 of 17,738 directives are CASA's own; the rest are
  adopted from EASA, the FAA and others. Normalisation groups are in
  `vocabulary/casa-aviation-vocabulary.yml`.

## 5. Cite a directive correctly

The public citation is **not** a field. Build it by concatenating `SeriesNumber`
and `ADNUMBER`:

```
"AD/B747/" + "100"  ->  AD/B747/100
```

`ID` is CASA's opaque internal integer. It is stable across both the JSON and
CSV projections (so the two files join on it) but it is not a citation — never
show it to a user.

## 6. Fetch the actual directive document

The regulatory text — affected serial ranges, modification states, compliance
times — exists **only** as prose inside the PDF. None of it is in the JSON.

CASA documents that AD PDFs live under `/airworth/airwd/ADfiles/` but does not
publish the addressing template. It is:

```
https://services.casa.gov.au/airworth/airwd/ADfiles/{GROUPTITLE|lowercase}/{FOLDERNAME|lowercase}/{ADFILE}
```

**Lower-case both path segments; keep the filename's original case.** Getting
the case wrong returns a 1,245-byte IIS HTML 404 page, not a JSON error — that
byte count is the signature of a case bug rather than a missing directive.

Verified 200 on 2026-07-28:

| Record | URL |
|---|---|
| `AIRGEN`/`GEN`/`GEN-001.pdf` | `.../ADfiles/airgen/gen/GEN-001.pdf` |
| `AIRGEN`/`GEN`/`GEN-037.pdf` | `.../ADfiles/airgen/gen/GEN-037.pdf` |
| `EQUIP`/`FPE`/`2009-0251-E.pdf` | `.../ADfiles/equip/fpe/2009-0251-E.pdf` |
| `OVER`/`B747`/`B747-100.pdf` | `.../ADfiles/over/b747/B747-100.pdf` |

## 7. Know the limit you are about to hit

**There is no key shared between the AD data and the aircraft register.** A
directive identifies applicability by `FOLDERNAME` (a CASA type-series code such
as `B747`); a registered aircraft identifies its type by `Manu`/`Model` and the
ICAO Doc 8643 designator. CASA publishes no mapping between the two.

So "which directives apply to VH-XYZ" is **not answerable from the published
data**. You must build and maintain your own `FOLDERNAME` → aircraft-type
mapping, then read the applicability prose inside each PDF for serial-number and
configuration conditions. Do not claim AD applicability for a specific aircraft
from these files alone — say what you matched on and what you could not.

`folder.csv` publishes 426 series; 425 have at least one directive (`CT58` has
none). Use it as the authoritative series list.
