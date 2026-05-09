# Interaction models

## Identity record linkage
This model defines the mandatory logical sequence for establishing a unique and verifiable identity for all entities (Patients, Providers, and Facilities) within the cross-border healthcare ecosystem. Its primary goal is to ensure that every interaction is anchored to a Regional Unique Identifier (patient: RUPI, provider: RUPID, or facility: RUFID), thereby preventing data fragmentation, duplicate records, and unauthorized access due to identity ambiguity.

### Core 

- Uniqueness First: No care relationship (Client Record) can be established until a valid Regional Unique Identifier is resolved for the Patient, Provider, and Facility involved.
- Deterministic Ordering: Identity resolution must complete successfully before linkage; linkage must complete successfully before authorization.
- Conflict Suspension: If probabilistic matching yields ambiguous results (potential duplicates), the process must halt automatically for manual adjudication. No automated merging or splitting occurs without human intervention.
- Tripartite Validation: A valid care relationship requires simultaneous validation of three distinct identities: the Patient (RUPI), the Provider (RUPID), and the Facility (RUFID).

### Sequence
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

## Data exchange



