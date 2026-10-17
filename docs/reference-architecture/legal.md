# Legal

Cross-border health data exchange always rests on legal conditions: why data may be shared, with whom, under which agreements, and with what safeguards. This page describes these conditions as requirements. It starts from one central set of client data that is used in different contexts. Generic requirements (authentication, authorisation, contracts, governance, data protection, security and logging) apply to every context; each context then adds its own specific requirements.

!!! note "Draft — not legal advice"
    The requirements describe common legal conditions, using the GDPR and EHDS as reference formulation. National legislation differs between Caribbean countries, so each exchange still needs to be checked against the law of the countries involved. When several countries are involved, the strictest requirement applies.

## Central client data

The architecture is built around one central set of personal and medical data about a client (patient). The data stays at its source ([principle 9](../principles/09-principle.md)) and the client is identified consistently across borders.

| Category | Examples |
|---|---|
| Identification | Identifiers, name, date of birth, sex |
| Contact and administrative data | Address, phone, next of kin, insurance |
| Consent and preferences | Consent for sharing, objections, preferred language |
| Patient summary | Allergies, problems and diagnoses, current medication, vaccinations |
| Clinical results | Laboratory results, imaging reports, screening results |
| Care documents | Referral letters, consultation reports, discharge letters, care plans |
| Medication data | Prescriptions, dispensations, adverse drug reactions |

The same data is used in different **contexts**. Each context has its own purpose, legal basis, users and safeguards, and therefore its own requirements. The context determines which part of the data is shared and in what form: identified, pseudonymised or aggregated.

## Contexts

| Context | Purpose | Example use cases |
|---|---|---|
| [Direct care](#direct-care) | Treating a specific client | [Planned referral](../use-cases/planned-referral.md), [specialist consultation](../use-cases/specialist-consultation.md), [laboratory services](../use-cases/laboratoryservices-microbiology.md), [screening](../use-cases/screening-cervicalcancer.md) |
| [Emergency care](#emergency-care) | Treating a client in an urgent situation | [Cross-border emergency care](../use-cases/cross-border-emergency-care.md) |
| [Personal access](#personal-access) | The client viewing and managing their own data | Client portal or app |
| [Public health](#public-health) | Surveillance, outbreak response and notification | [Emergency response](../use-cases/publichealth-emergencyresponse.md) |
| [Medicines regulation and monitoring](#medicines-regulation-and-monitoring) | Safety and quality of medicines | [Regulatory approval](../use-cases/medicines-regulatory-approval.md), [quality testing](../use-cases/medicines-quality-testing.md), [pharmacovigilance](../use-cases/pharmacovigilance.md) |
| [Secondary use](#secondary-use) | Research, policy and statistics | Regional health statistics |

## Overview of requirements per context

| Requirement | Direct care | Emergency care | Personal access | Public health | Medicines | Secondary use |
|---|---|---|---|---|---|---|
| Legal basis | Provision of care | Vital interests | Right of access | Legal obligation / public interest | Legal obligation / public interest | Public interest or consent, with permit |
| Client consent | Required (opt-in) | Not required; known objections respected | Not applicable | Not required | Not required | Not required; opt-out respected |
| Who may access | Licensed professional with a care relationship | Licensed professional on duty | The client (or legal representative) | Accredited public health authority | Accredited regulatory authority or laboratory | Approved researcher or institution |
| Authentication | High, multi-factor | High, multi-factor | High, multi-factor | High, organisation and person | High, organisation and person | High, organisation and person |
| Data identifiability | Identified | Identified | Identified | Identified only where needed, otherwise pseudonymised or aggregated | Pseudonymised; product data | Pseudonymised or anonymised |
| Data scope | What is needed for the treatment | Patient summary | All own data | Notifiable data set | Report data set | Data set in the permit |
| Agreements | Mutual data sharing agreement | Same as direct care | Terms of use | Data sharing agreement and mandate | Data sharing agreement and mandate | Data permit and access agreement |
| Logging and transparency | Logged; visible to client | Logged; reviewed afterwards; client informed | Logged | Logged | Logged | Logged; results published |

## Generic requirements

The following requirements apply to all contexts. The context sections below add the requirements that are specific to each context.

### Authentication

| ID | Requirement |
|---|---|
| AU-01 | Healthcare professionals and staff of participating organisations have a personal account and authenticate with at least two factors, at assurance level *substantial* or higher ([eIDAS](../references.md#ref-eidas2014)). Shared accounts are not allowed. |
| AU-02 | The identity of a professional is verified against the professional register before an account is issued, and access is revoked when the registration ends. |
| AU-03 | Clients authenticate with a national eID or an equivalent means at assurance level *substantial* or higher, after their identity has been verified (e.g. against a national identity document). |
| AU-04 | Participating organisations are identified by an organisation certificate issued under the trust framework. |
| AU-05 | Systems exchange data only over mutually authenticated and encrypted connections. |
| AU-06 | National authentication means are mutually recognised across borders when they meet the agreed assurance level. |
| AU-07 | Every request carries the identity and role of the person, the organisation and the purpose of use, so the receiving party can make its own access decision. |

### Authorisation

| ID | Requirement |
|---|---|
| AZ-01 | Access decisions are based on the role of the requester, their organisation, the context (purpose of use), the care relationship and the consent status of the client. |
| AZ-02 | The source holder makes the final access decision for its data. |
| AZ-03 | Deviations from the normal access rules (e.g. emergency access) follow a defined procedure and are always logged and reviewed. |

### Contractual

| ID | Requirement |
|---|---|
| CA-01 | All participating organisations sign a trust framework participation agreement. It sets out the roles, obligations, applicable law, dispute resolution, liability, and the conditions for suspension and exit. |
| CA-02 | Each type of exchange is covered by a data sharing agreement that states the purpose, legal basis, data set, recipients, retention period and the prohibition of onward sharing. |
| CA-03 | Where an organisation processes data on behalf of another (e.g. hosting), a processing agreement defines the instructions and safeguards. |
| CA-04 | Facilities that one party provides to others are covered by service level agreements for availability, support and incident handling ([principle 11](../principles/11-principle.md)). |
| CA-05 | Agreements include the safeguards required for transferring personal data to another country. |
| CA-06 | Subcontractors are bound by the same obligations as the participant that engages them. |
| CA-07 | Agreements are reviewed periodically, and describe the return or deletion of data when a participant leaves. |

### Governance and accreditation

| ID | Requirement |
|---|---|
| GO-01 | Organisations are admitted to the trust framework only after showing that they meet its legal, security and technical requirements (accreditation). |
| GO-02 | Compliance of participants can be audited, and participants can be suspended when they do not comply. |
| GO-03 | There is a procedure for complaints and questions from clients, regardless of the country where the data is held. |

### Data protection

| ID | Requirement |
|---|---|
| DP-01 | Every request states its context (purpose of use), and data is used only for that purpose. |
| DP-02 | Only the data needed for the purpose is exchanged; no bulk exchange ([GDPR](../references.md#ref-gdpr) art. 5(1)(c)). |
| DP-03 | Corrections are made at the source and passed on to recipients. |
| DP-04 | Received data is kept no longer than needed, within the retention periods of national medical records legislation. |
| DP-05 | A data protection impact assessment is carried out before a new context or use case is introduced ([GDPR](../references.md#ref-gdpr) art. 35). |
| DP-06 | Clients are informed about the cross-border exchange of their data: purposes, recipients and countries involved. |

### Security

| ID | Requirement |
|---|---|
| SE-01 | Data is encrypted in transit and at rest ([GDPR](../references.md#ref-gdpr) art. 32). |
| SE-02 | Participants manage information security according to a recognised information security standard. |
| SE-03 | Security incidents and data breaches are reported to the trust framework, the supervisory authorities and affected clients, within the shortest applicable period. |

### Logging and audit

| ID | Requirement |
|---|---|
| LG-01 | Every access and exchange is logged: who, from which organisation, which data, when and for what purpose. |
| LG-02 | Logs are protected against changes and kept for an agreed period. |
| LG-03 | Logs are reviewed periodically for unauthorised access. |
| LG-04 | Clients can see who has accessed their data ([EHDS](../references.md#ref-ehds2025)). |

## Direct care

A healthcare professional in one country needs data about a client to treat them, for example after a referral to another island.

**Legal basis:** provision of care ([GDPR](../references.md#ref-gdpr) art. 9(2)(h)).

| ID | Requirement |
|---|---|
| DC-01 | The client has given consent (opt-in) for the cross-border sharing of their data. Consent is recorded, can be withdrawn, and is checked before every exchange. |
| DC-02 | Only licensed healthcare professionals with a care relationship with the client can access the data, and only what they need for that treatment (need-to-know). |
| DC-03 | The client is reliably identified before data is exchanged. |
| DC-04 | The participating organisations have signed a mutual data sharing agreement for direct care (CA-02). |
| DC-05 | Professionals in the receiving country are bound by medical professional secrecy. |
| DC-06 | Data is viewed at the source where possible; copies are stored only when needed for the treatment record. |

## Emergency care

A client needs urgent care in another country and cannot give consent, for example after an accident while travelling or during evacuation after a hurricane.

**Legal basis:** vital interests of the client ([GDPR](../references.md#ref-gdpr) art. 9(2)(c)).

| ID | Requirement |
|---|---|
| EC-01 | Prior consent is not required when the client cannot give it. An explicit objection recorded by the client is respected. |
| EC-02 | Access is limited to licensed professionals on duty, and to an emergency data set (patient summary). |
| EC-03 | Professionals state the reason for emergency access ("break the glass", AZ-03). |
| EC-04 | Every emergency access is reviewed afterwards and reported to the client. |
| EC-05 | The data sharing agreement for direct care also covers emergency care. |

## Personal access

The client views their own data from different countries, shares it with a professional, or asks for corrections.

**Legal basis:** right of access ([GDPR](../references.md#ref-gdpr) art. 15; [EHDS](../references.md#ref-ehds2025)).

| ID | Requirement |
|---|---|
| PA-01 | A legal representative (e.g. a parent or guardian) can act on behalf of the client, based on a registered authorisation. |
| PA-02 | The client can see their data, who has accessed it (LG-04), and manage their consent and objections. |
| PA-03 | Requests for corrections are forwarded to the source holder. |
| PA-04 | Information is understandable and offered in the client's language where possible. |

## Public health

Public health authorities need data to detect and respond to outbreaks and to notify events of international concern.

**Legal basis:** legal obligation or public interest in public health ([GDPR](../references.md#ref-gdpr) art. 9(2)(i)); [International Health Regulations](../references.md#ref-ihr2005).

| ID | Requirement |
|---|---|
| PH-01 | Client consent is not required. Clients are informed in general terms about public health reporting. |
| PH-02 | Only accredited public health organisations with a legal mandate (e.g. the national public health authority, CARPHA) receive the data. |
| PH-03 | Identified data is shared only where needed (e.g. case notification, contact tracing); otherwise data is pseudonymised or aggregated. |
| PH-04 | Only the agreed notifiable data set is shared. |
| PH-05 | A data sharing agreement for public health (CA-02) refers to the legal mandate of the receiving organisation. |
| PH-06 | Events that may be a public health emergency of international concern are notified to WHO through the National IHR Focal Point. |

## Medicines regulation and monitoring

Regulatory authorities and laboratories share data on medicines, their quality and adverse reactions.

**Legal basis:** legal obligation or public interest in the safety of medicines ([GDPR](../references.md#ref-gdpr) art. 9(2)(i)).

| ID | Requirement |
|---|---|
| MR-01 | Client consent is not required for reporting adverse reactions. |
| MR-02 | Only accredited regulatory authorities and laboratories receive the data. |
| MR-03 | Reports contain the minimum personal data needed and are pseudonymised. Product data contains no personal data. |
| MR-04 | A data sharing agreement for medicines monitoring (CA-02) refers to the legal mandate of the receiving organisation. |

## Secondary use

Researchers and policy makers use health data for research, policy and statistics.

**Legal basis:** public interest or consent, with an approved data permit ([GDPR](../references.md#ref-gdpr) art. 89; [EHDS](../references.md#ref-ehds2025)).

| ID | Requirement |
|---|---|
| SU-01 | Use requires a data permit from an approved body and, for research, ethical approval. |
| SU-02 | Clients can object (opt-out) to the secondary use of their data. |
| SU-03 | Data is anonymised where possible, otherwise pseudonymised; re-identification is prohibited. |
| SU-04 | Data is processed in a secure processing environment and is not downloaded. |
| SU-05 | Results are never used for decisions about individual clients. |
| SU-06 | Results are published. |
