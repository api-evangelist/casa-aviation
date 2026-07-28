---
name: Qualify for CASA RPAS Digital Platform access
description: Work out whether an application can get credentials for the CASA RPAS Digital Platform partner API, and what the full approval path costs, before writing any integration code.
api: casa-aviation:casa-rpas-digital-platform
generated: '2026-07-28'
method: generated
grounding: >-
  Grounded in CASA's published RPAS Platform reference PDFs (Concept of
  Operations, Operating Rules, Test Procedure, Declaration of Compliance, Terms
  and Conditions) and in live probes of data.casa.rpasplatform.net on
  2026-07-28. The endpoints named below come from the Operating Rules, not from
  probing - every path on that host returns an identical 403 to anonymous
  clients, so probing reveals nothing.
operations:
  - GET https://data.casa.rpasplatform.net/casa/data/advisories.geojson
  - GET https://data.casa.rpasplatform.net/casa/data/notifications.json
  - GET https://data.casa.rpasplatform.net/casa/gcd
  - GET https://data.casa.rpasplatform.net/asa/gcd
artifacts:
  - authentication/casa-aviation-authentication.yml
  - lifecycle/casa-aviation-lifecycle.yml
  - errors/casa-aviation-problem-types.yml
  - conformance/casa-aviation-conformance.yml
---

# Qualify for CASA RPAS Digital Platform access

**Read this before you write code.** This is not a self-serve API. There is no
sign-up, no console, no key issuance and no free tier. If you cannot clear every
gate below, no amount of integration work will get you a response other than
`403`.

## 1. Confirm the surface actually exists

Four feeds are named in the RPAS Platform Operating Rules, Attachment A:

| Feed | Path | Refresh obligation |
|---|---|---|
| CASA Advisories | `/casa/data/advisories.geojson` | at least every 15 minutes |
| CASA Notifications | `/casa/data/notifications.json` | — |
| CASA geospatial content | `/casa/gcd` | at least every 24 hours |
| Airservices facility maps | `/asa/gcd` | at least every 24 hours |

`data.casa.rpasplatform.net` is a Google Cloud Storage bucket with a
deny-by-default ACL. **Every** path returns the same XML body —
`<Error><Code>AccessDenied</Code><Message>Access denied.</Message></Error>` —
including paths that do not exist. A 403 here tells you nothing about whether an
endpoint is real. Never probe to discover structure, and never infer a schema
from a 403.

The Operating Rules state plainly that the notifications URL *"needs
authentication with a service account"*.

## 2. Check the four gates, in cost order

1. **A paid Airservices Australia aeronautical/airspace data licence** must
   already be in place — sourced independently of CASA, at your expense (Concept
   of Operations, clause 13.1). CASA will not consider an application without it.
2. **A written application to CASA** and acceptance of the RPAS Platform Terms
   and Conditions — a **four-year initial term**.
3. **A Declaration of Compliance** against the Operating Rules, plus
   demonstrable compliance with Australian Government security and privacy
   requirements including the **ASD Essential Eight**, at your expense.
4. **A live onboarding check-out** against the RPAS Platform Test Procedure.
   **Two attempts are permitted.** CASA runs it as Test Director using its
   InterUSS Platform-derived automated test suite.

Only after all four does CASA issue staging and then production credentials.
There is no development environment for you — `development` is CASA-internal.

## 3. Check what is currently open

Onboarding is **partially paused**. As published:

* **Open**: new app providers may apply for Sydney Harbour Automated Airspace
  Authorisation (R405A/R405B) and airspace awareness maps.
* **Paused**: onboarding of new providers for the ten trial controlled
  aerodromes, pending Airservices Australia's Flight Information Management
  System (FIMS).

If your use case is the trial aerodromes, the correct answer today is "wait",
not "apply".

## 4. Understand what you are signing

Terms and Conditions clause 45.1: CASA *"may terminate or reduce the scope of
this Agreement (including by reducing or removing any CASA Data or Data Sources
from the RPAS Platform) at any time, by giving the Software Provider eight
weeks' Notice"*, and under 45.2 you *"will not be entitled to any
compensation"*. Eight weeks' notice and no compensation is the real deprecation
policy for this API — there is no public one.

There is also no SLA and no uptime target. The Operating Rules set data
**refresh** obligations, which describe how current the data must be, not how
available the service must be. The CASA status page at `my.casa.gov.au/outage/`
covers the myCASA portal only — nothing on it covers this platform.

## 5. Do not model the payloads until you have credentials

No schema is published for `advisories.geojson`, `notifications.json` or either
`gcd` surface, and none can be observed anonymously. The advisories feed is
GeoJSON (RFC 7946) per the Operating Rules; beyond that, anything you write down
about field structure before you hold a service account is a guess. Model it
after your first authenticated response, not before.

## Start here

<https://www.casa.gov.au/drones/industry-initiatives/digital-platform>
