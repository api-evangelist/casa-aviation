# Civil Aviation Safety Authority (CASA) (casa-aviation)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

The Civil Aviation Safety Authority (CASA) is Australia's independent statutory aviation safety regulator, established under the Civil Aviation Act 1988. It maintains the Australian Civil Aircraft Register (VH- marks), issues Airworthiness Directives, licenses flight crew and maintenance organisations, certifies air operators, and regulates drone and RPAS operations. CASA sits entirely OUTSIDE the travel distribution chain — it is a safety regulator, not a distributor, so it has no GDS, NDC, channel-manager or OTA position, and airline fare distribution, full-content agreements and consumer disclosure are not CASA functions. Its API posture is split and honest: two genuinely open, no-key, documented bulk data products (the full Airworthiness Directives listing as JSON/CSV and the complete civil aircraft register as a daily CSV, both served from services.casa.gov.au), and one approval-gated partner API — the CASA RPAS Digital Platform at data.casa.rpasplatform.net — whose endpoints are named in public PDFs but require a service account, a signed four-year agreement, a CASA onboarding check-out and a paid Airservices Australia airspace data licence. There is no self-serve developer portal, no OpenAPI, and new RPAS Platform onboarding is currently paused pending Airservices' Flight Information Management System.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/casa-aviation/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/casa-aviation/refs/heads/main/apis.yml)

## Tags

- Travel
- Australia
- Aviation
- Airports
- Government
- Regulator
- Aviation Safety
- Open Data
- Drones

## Timestamps

- **Created:** 2026-07-28
- **Modified:** 2026-07-28

## APIs

### CASA Airworthiness Directives Data Files

Open, unauthenticated bulk data files covering every current Australian Airworthiness Directive (AD). combinedadweb.json lists all current ADs with aircraft and equipment references; adweb.csv lists all current ADs and folder.csv lists the aircraft and equipment types. Individual AD documents are addressable as PDFs under /airworth/airwd/ADfiles/ by folder and file number. CASA states the JSON file format is subject to change. No API key, no registration and no terms acceptance are required to download.

- **Human URL:** [https://www.casa.gov.au/aircraft/airworthiness/airworthiness-directives/data-files-all-airworthiness-directives](https://www.casa.gov.au/aircraft/airworthiness/airworthiness-directives/data-files-all-airworthiness-directives)
- **Base URL:** `https://services.casa.gov.au`

#### Tags

- Aviation
- Airworthiness
- Safety
- Open Data
- Australia

#### Properties

- [Documentation](https://www.casa.gov.au/aircraft/airworthiness/airworthiness-directives/data-files-all-airworthiness-directives)
- [Documentation](https://www.casa.gov.au/aircraft/airworthiness/airworthiness-directives)
- [JSON](https://services.casa.gov.au/JSON/combinedadweb.json)
- [CSV](https://services.casa.gov.au/airworth/airwd/data/adweb.csv)
- [CSV](https://services.casa.gov.au/airworth/airwd/data/folder.csv)

### Australian Civil Aircraft Register Data Files

The complete Australian Civil Aircraft Register published as a daily comma-delimited data file (acrftreg.csv, approximately 7.6MB) and a zip compressed equivalent (acrftreg.zip, approximately 1MB). CASR 47.030 requires CASA to publish or make available data relating to the civil register; only aircraft currently registered in Australia are included. Records carry VH- registration marks, manufacturer, model, serial number, MTOW, year and country of manufacture, engine and propeller details, ICAO Doc 8643 type designator, type certificate, registration holder and registered operator with address and commencement dates. Coded fields are documented on separate CASA pages. No API key or registration required.

- **Human URL:** [https://www.casa.gov.au/aircraft/aircraft-registration/data-files-registered-aircraft](https://www.casa.gov.au/aircraft/aircraft-registration/data-files-registered-aircraft)
- **Base URL:** `https://services.casa.gov.au/CSV`

#### Tags

- Aviation
- Aircraft
- Registration
- Open Data
- Australia

#### Properties

- [Documentation](https://www.casa.gov.au/aircraft/aircraft-registration/data-files-registered-aircraft)
- [Documentation](https://www.casa.gov.au/aircraft/aircraft-registration/data-files-registered-aircraft/downloading-and-using-our-data-files)
- [Documentation](https://www.casa.gov.au/aircraft/aircraft-registration/data-files-registered-aircraft/meaning-coded-fields-registered-aircraft)
- [Documentation](https://www.casa.gov.au/aircraft/aircraft-registration/data-files-registered-aircraft/list-coded-fields-registered-aircraft)
- [CSV](https://services.casa.gov.au/CSV/acrftreg.csv)
- [Archive](https://services.casa.gov.au/CSV/acrftreg.zip)
- [Documentation](https://www.casa.gov.au/search-centre/aircraft-register)

### CASA RPAS Digital Platform API

A partner-only API that supplies CASA advisories, notifications and geospatial map data to drone safety applications, and processes Automated Airspace Authorisations for Sydney Harbour (R405A/B) and ten trial controlled aerodromes. Endpoints are named in the public RPAS Platform Operating Rules — advisories.geojson and notifications.json under /casa/data/, plus /casa/gcd and /asa/gcd for geospatial content — and the Operating Rules state the URLs need authentication with a service account. Access requires a written application, acceptance of the RPAS Platform Terms and Conditions, a formal onboarding check-out against the RPAS Platform Test Procedure (two attempts allowed), staging then production credentials issued by CASA, and a paid Airservices Australia airspace data licence sourced independently. CASA has paused onboarding of new providers for the ten trial aerodromes pending Airservices' Flight Information Management System. Not a self-serve API.

- **Human URL:** [https://www.casa.gov.au/drones/industry-initiatives/digital-platform](https://www.casa.gov.au/drones/industry-initiatives/digital-platform)
- **Base URL:** `https://data.casa.rpasplatform.net`

#### Tags

- Aviation
- Drones
- RPAS
- Airspace
- Partner API
- Australia

#### Properties

- [Documentation](https://www.casa.gov.au/drones/industry-initiatives/digital-platform)
- [Documentation](https://www.casa.gov.au/sites/default/files/2021-09/rpas-platform-concept-of-operations.pdf)
- [Documentation](https://www.casa.gov.au/sites/default/files/2022-06/rpas-platform-operating-rules.pdf)
- [Documentation](https://www.casa.gov.au/sites/default/files/2026-06/rpas-platform-test-procedure.pdf)
- [Documentation](https://www.casa.gov.au/sites/default/files/2026-06/rpas-platform-declaration-compliance.pdf)
- [Terms Of Service](https://www.casa.gov.au/sites/default/files/2021-09/rpas-platform-terms-conditions.pdf)
- [Documentation](https://www.casa.gov.au/knowyourdrone/drone-safety-apps)

## Common Properties

- [Website](https://www.casa.gov.au/)
- [Documentation](https://www.casa.gov.au/aircraft/aircraft-registration/data-files-registered-aircraft)
- [Portal](https://my.casa.gov.au/)
- [Terms Of Service](https://www.casa.gov.au/sites/default/files/2021-09/rpas-platform-terms-conditions.pdf)
- [Blog](https://www.casa.gov.au/about-us/news-media-releases-and-speeches)
- [Blog RSS](https://www.casa.gov.au/rss.xml)
- [Contact](https://www.casa.gov.au/about-us/contact-us)
- [LinkedIn](https://www.linkedin.com/company/civil-aviation-safety-authority-casa-/)
- [YouTube](http://www.youtube.com/user/casabriefing)
- [Facebook](https://www.facebook.com/CivilAviationSafetyAuthority)
- [Instagram](https://www.instagram.com/casabriefing)

## Switching Cost

Recorded in full in [review.yml](review.yml).

- **Interface shape:** `proprietary-documented` — CASA-specific CSV and JSON file schemas documented only in prose; no OpenAPI anywhere. The one open standard in play is the InterUSS Platform, used for the RPAS Platform's automated conformance test suite, not for the data contract.
- **Second source:** `no-alternative` — for the Australian civil aircraft register and Australian Airworthiness Directives, CASA is the only route. Third-party register APIs are mirrors of CASA's own published files.
- **Exit path:** `bulk-export-documented` — the whole dataset is the export. The asymmetry is on the gated side, where RPAS Platform Terms and Conditions clause 47.1 obliges a departing provider to strip CASA data from its product and tell its users it has done so.
- **Identifier portability:** VH- registration marks, ICAO Doc 8643 type designators, manufacturer serial numbers and AD series numbers — all shared industry keys that travel anywhere. Only the numeric `ID` in combinedadweb.json is CASA-internal.
- **Contractual lock-in:** nothing published for the open files. For the RPAS Platform: four-year initial term plus a two-year option, six weeks' notice out for the provider, eight weeks' termination for convenience by CASA with no compensation, and a revocable, non-exclusive, non-transferable licence.
- **Access gate:** open files need nothing at all; the RPAS Platform needs a written application, signed terms, a Declaration of Compliance, a live onboarding check-out with two attempts, and a paid Airservices airspace data licence — and new onboarding is currently paused.
- **Distribution model:** `not-applicable`. **NDC posture:** not applicable.

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
