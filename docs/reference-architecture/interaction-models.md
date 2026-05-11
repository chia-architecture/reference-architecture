# Interaction models
Interaction models describe how building blocks coordinate and interact to function as an integrated system. They define the sequence of actions and information flows between components, such as verifying a user’s identity before granting access to data or ensuring a patient is uniquely identified before records are linked across systems. By specifying how building blocks work together, interaction models support consistent, secure, and reliable interoperability across organisations and countries.

## Identity record linkage
This model defines the mandatory logical sequence for establishing a unique and verifiable identity for all entities (Clients, Providers, and Facilities) within the cross-border healthcare ecosystem. Its primary goal is to ensure that every interaction is anchored to a Regional Unique Identifier (patient: RUCID, provider: RUPID, or facility: RUFID), thereby preventing data fragmentation, duplicate records, and unauthorized access due to identity ambiguity.


**Requirements**

- Each entity (client, healthcare provider, and healthcare facility) must be identifiable through a unique regional identifier.
- Regional identifiers are linked to regional provider and facility identifiers, establishing care relationships. 
- Regional identifiers must remain linked to authoritative national registries, such as resident registries where available, ensuring alignment with nationally managed identity information.
- Access to client information requires authentication of the client (RUCID), healthcare provider (RUPID), and healthcare facility (RUFID) involved.
- Access to client information requires confirming care relationships.
- If identity matching produces ambiguous or conflicting results, the process must automatically stop for human review.

**Building blocks involved**

Client registration; provider registration; facility registration; resident registration

**Sequence**

## Authentication and autorisation
This model defines the mandatory logical sequence for verifying the identity of data consumer and determining the specific scope of data access permitted. Its primary goal is to enforce secure and robust principles.

**Requirements**

- Authentication and authorization must be completed before any data retrieval request is processed.
- Access/autorisation decisions consider the context of the patient, taking into account purpose of use (e.g., emergency vs. routine), the healthcare provider, the facility, and the patient's consent status.
- Authentication and authorization is logged for audit tracebility.

**Sequence**

The interaction follows a strict three-phase dependency chain:

Phase 1: Identity & Credential Verification (Authentication)

Input: A request containing ProviderID, PatientID (Local), and PurposeOfUse.

Action: The Authenticator queries the Health Provider Registration and Resident Registration.

Logic:
Provider Check: Verify the provider's license is ACTIVE and they are GOOD_STANDING.
Patient Check: Resolve the local PatientID to a valid RUPI.
Failure: If either check fails, the sequence terminates with 403 Forbidden.

Phase 2: Relationship & Policy Evaluation (Authorization)

Prerequisite: Both Provider and Patient identities are verified.

Action: The Authenticator invokes the Authorization Block with the context (RUPI, RUPID, PurposeOfUse).

Logic:
Relationship Check: Verify a valid Client Record exists (from Model 3.1) OR that an "Emergency Override" condition applies.
Policy Check: Evaluate rules against the provider's specialty (e.g., "Psychiatrist cannot access unrelated dental records") and patient consent flags.
Outcome: A set of Allowed_Scopes (e.g., read:allergies, read:medications) or DENIED.

Phase 3: Token Issuance & Handoff

Prerequisite: Allowed_Scopes is not empty.
Action: The Authenticator generates a signed JWT Token containing the Allowed_Scopes, Expiry, and Audience.
Outcome: The token is returned to the Data Consumer.
Constraint: The token is valid only for the specific PurposeOfUse and Scopes defined. It cannot be reused for other patients or purposes.

## Data exchange

This model defines the mandatory logical sequence for retrieving, filtering, and delivering clinical data from a source system to a requesting provider. Its primary goal is to ensure that data is delivered only within the strict boundaries of the previously issued authorization token, while maintaining system resilience against network failures through asynchronous store-and-forward mechanisms.

**Core**

**Sequence**


