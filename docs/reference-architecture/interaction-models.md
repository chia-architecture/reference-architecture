# Interaction models
Interaction models describe how building blocks coordinate and interact to function as an integrated system. They define the sequence of actions and information flows between components, such as verifying a user’s identity before granting access to data or ensuring a patient is uniquely identified before records are linked across systems. By specifying how building blocks work together, interaction models support consistent, secure, and reliable interoperability across organisations and countries.

## Identity record linkage
This model defines the mandatory logical sequence for establishing a unique and verifiable identity for all entities (Clients, Providers, and Facilities) within the cross-border healthcare ecosystem. Its primary goal is to ensure that every interaction is anchored to a Regional Unique Identifier (patient: RUCID, provider: RUPID, or facility: RUFID), thereby preventing data fragmentation, duplicate records, and unauthorized access due to identity ambiguity.


**Requirements**

- Each entity (client, healthcare provider, and healthcare facility) must be identifiable through a unique regional identifier.
- Regional identifiers must remain linked to authoritative national registries, such as resident registries where available, ensuring alignment with nationally managed identity information.
- Clients are linked to providers and facilities establishing care relationships.
- Access to client information requires verification of the client (RUCID), healthcare provider (RUPID), and healthcare facility (RUFID) involved.
- If identity matching produces ambiguous or conflicting results, the process must automatically stop for human review.

**Building blocks involved**

**Sequence**

## Authentication and autorisation
This model defines the mandatory logical sequence for verifying the identity of a requesting entity (Provider) and determining the specific scope of data access permitted for a target entity (Patient). Its primary goal is to enforce Zero-Trust principles by ensuring that no clinical data is retrieved unless a valid, scoped token has been issued based on real-time verification of credentials, relationships, and consent policies.

**Core**

- Verification Before Access: Authentication (Who are you?) and Authorization (What can you see?) must be completed and validated before any data retrieval request is processed.
- Token-Based Delegation: The Authorization block does not participate in the data flow. It issues a scoped token; the Data Distributor enforces the token's scope.
- Context-Aware Policy: Access decisions must dynamically consider the Purpose of Use (e.g., Emergency vs. Routine), the Provider's Specialty, and the Patient's Consent status.
Immutable Audit: Every authorization decision must be logged with full context (Who, What, Why, When) before the token is issued.

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


