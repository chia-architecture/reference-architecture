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

1. The data consumer building block (human/system) requests access to client information for a specific purpose of use (e.g., treatment or emergency care).
2. The identity of the data consumer is verified by the data distributer through the authentication building block using the the provider and facility registration building blocks.
3. If identity verification fails, the request is denied and the process stops.
4. The data distributer then evaluates using the authorisation building block whether the data consumer is allowed to access the requested information. This evaluation may consider:
   - the care relationship between the client, provider, and facility
   - the provider’s role or specialty
   - the purpose of use
   - the client’s consent status
   - emergency access policies
5. If authorization is approved, an authorization decision is issued with the permitted access scope to the data distributer.
6. The data distributer grants the permitted client information.
7. All authentication, authorization, and access events are logged for audit and traceability purposes.

## Data exchange

This model defines the mandatory logical sequence for retrieving, filtering, and delivering clinical data from a source system to a requesting provider. Its primary goal is to ensure that data is delivered only within the strict boundaries of the previously issued authorization token, while maintaining system resilience against network failures through asynchronous store-and-forward mechanisms.

**Core**

**Sequence**


