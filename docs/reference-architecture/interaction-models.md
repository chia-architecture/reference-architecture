# Interaction models
Interaction models describe how building blocks coordinate and interact to function as an integrated system. They define the sequence of actions and information flows between components, such as verifying a user’s identity before granting access to data or ensuring a patient is uniquely identified before records are linked across systems. By specifying how building blocks work together, interaction models support consistent, secure, and reliable interoperability across organisations and countries.

## Identity record linkage
This model defines the mandatory logical sequence for establishing a unique and verifiable identity for all entities (Patients, Providers, and Facilities) within the cross-border healthcare ecosystem. Its primary goal is to ensure that every interaction is anchored to a Regional Unique Identifier (patient: RUPI, provider: RUPID, or facility: RUFID), thereby preventing data fragmentation, duplicate records, and unauthorized access due to identity ambiguity.

**Core**

- Uniqueness First: No care relationship (Client Record) can be established until a valid Regional Unique Identifier is resolved for the Patient, Provider, and Facility involved.
- Deterministic Ordering: Identity resolution must complete successfully before linkage; linkage must complete successfully before authorization.
- Conflict Suspension: If probabilistic matching yields ambiguous results (potential duplicates), the process must halt automatically for manual adjudication. No automated merging or splitting occurs without human intervention.
- Tripartite Validation: A valid care relationship requires simultaneous validation of three distinct identities: the Patient (RUPI), the Provider (RUPID), and the Facility (RUFID).

**Building blocks involved**

**Sequence**

The interaction follows a strict four-phase dependency chain:

Phase 1: Entity Ingestion & Matching

Input: Demographic and credential data is submitted for a Patient, Provider, and/or Facility.
Action: The respective Registration Blocks (Resident, Provider, Facility) query the regional registry to perform a match against existing records.
Logic:
Exact/Probabilistic Match: The system retrieves the existing Regional Unique Identifier (RUPI/RUPID/RUFID).
No Match: The system generates a new, persistent Regional Unique Identifier.
Conflict: If multiple potential matches exist with insufficient confidence, the state transitions to PENDING_ADJUDICATION.

Phase 3: Relationship Binding (Linkage)

Prerequisite: All entities are identified and verified as ACTIVE.
Action: The Client Registration block creates a new Client Record (or updates an existing one) that logically binds the RUPI, RUPID, and RUFID together.
Outcome: A persistent record is created representing the specific care relationship (e.g., "Dr. Smith [RUPID] is treating Patient X [RUPI] at Hospital Y [RUFID]").

Phase 4: State Propagation

Prerequisite: The Client Record is successfully created.
Action: A ClientLinked event is published to the regional event bus.
Effect: All peer Registration Blocks receive the event and update their local indexes to recognize the new relationship, ensuring that future queries from any jurisdiction can resolve the relationship immediately.


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


