# Services

This section describes how different layers of services enable cross-border healthcare interoperability.[@adr_serviceoriented]

![Services overview](../assets/views/services-overview.svg)

This architecture distinguishes between different categories of services that together enable interoperable healthcare across borders. These services are defined as follows:

- **National healthcare delivery services**: The actual provision of care to clients and patients by healthcare professionals and organisations
- **Cross-border healthcare services**: Cross-border healthcare capabilities, such as integrated clinical workflows, patient management, and care coordination.
- **Cross-border integration services**: Mechanisms that enable integration and standardisation of data between systems
- **Data distribution services**: Inherently distributed sources of healthcare data and can be used a source for delivery
- **Shared services**: Reusable services that support multiple healthcare applications for cross-cross-border data sharing (e.g. patient indentification, consent, registries)  
- **Foundational services**: Cross-sector services such as digital identity, financial transaction, energy management, transportation, and other infrastructure used across domains  
- **Trust frameworks**: Legal, organizational, and governance agreements that enable trusted cross-border collaboration  
- **Terminology & semantics services**: Standards and services that ensure consistent meaning and interpretation of health data

These service categories of services are consistent with the WHO's Digital Public Services, the WHO's Digital Public Services for Health, and Sigra's Reference Architecture.

**Scope and positioning**

Not all service categories are defined in detail.

National healthcare delivery services are not described in detail in the architecture. Instead, the architecture is designed to support and enable effective healthcare delivery, which is reflected in the architecture principles.

Terminology and semantics services are used as input for defining standards within the building blocks. The architecture aims to align with internationally recognized standards wherever possible.

Trust agreement frameworks are not specified within the reference architecture itself. They are treated as a prerequisite and constraint, shaping how cross-border interoperability can be realized.

Similarly, foundational digital public services are not defined in detail. Their availability and maturity vary across countries and are considered an important constraint for the realization of interoperable solutions.

## Cross-border healthcare services
Cross-border healthcare services enable healthcare organisations, professionals, and supporting institutions in different countries to collaborate and exchange information as part of healthcare delivery. These services support processes such as referrals, diagnostics, laboratory testing, medicines monitoring, and public health coordination by allowing relevant healthcare information to be securely shared, interpreted, and acted upon across organisational and national boundaries.

By integrating information from multiple systems and jurisdictions, cross-border healthcare services provide healthcare professionals with a more complete view of the client’s health context. This supports better clinical decision-making, continuity of care, operational coordination, and regional public health response.

**Service users**  
Cross-border healthcare services are primarily used by healthcare provider within healthcare organisations and professionals involved in delivering care across national boundaries. This includes hospitals, primary care providers, laboratories, pharmacies, public health organisations, regulatory authorities, and emergency response organisations.

**Outputs**  
Outputs describe the integrated healthcare information over different jurisdictions.

**Building blocks**  
Data consumers

**Constraints**  
Relevant legal, organizational, or technical constraints.

## Cross-border integration services

Cross-border integration services support the integration, transformation, and routing of healthcare information between organisations, systems, and jurisdictions. Their primary function is to establish interoperable integration points (“knooppunten”) that enable different systems and services to exchange information in a coordinated and reliable manner.

These services are commonly implemented through integration platforms that mediate between systems with different technical capabilities, standards, or data structures. In addition to routing and orchestration, they may also function as adapters for non-compliant or legacy systems, enabling participation in cross-border interoperability without requiring complete replacement of existing infrastructure.

**Service users**  
These services may also be used by (non-compliant) digital systems such as electronic health records, laboratory information systems, referral systems, medicine registries, and public health surveillance platforms. 

**Outputs**  
Outputs describe the integrated healthcare information over different jurisdictions.


**Building blocks**  
Data integrstors & adapters

**Constraints**  
Relevant legal, organizational, or technical constraints.

## Data distribution services

Data distribution services enable the secure sharing of healthcare information cross-border organisations and systems. They support the controlled sharing of data across jurisdictions, ensuring that relevant information becomes available to authorised consumers at the right place and time. These services may distribute information contained in national systems such as EHRs, LIMSs, RISs, PACSs, public health systems, and integration platforms.

**Service users**  
Data distribution services are used by healthcare providers involved in delivering care across national boundaries. This includes roles within cross-border hospitals, primary care providers, laboratories, pharmacies, public health organisations, regulatory authorities, and emergency response organisations.

These services may also be used by supporting digital systems such as electronic health records, laboratory information systems, referral systems, medicine registries, and public health surveillance platforms. 

**Outputs**  
Outputs describe the local/national healthcare information within a jurisdiction.

**Building blocks**  
Data distributers

**Constraints**  
Relevant legal, organizational, or technical constraints.

## Shared services
**Capabilities**  
What the service enables (functional behavior).

**Consumers**  
Who uses the service (systems, organizations, or people).

**Outputs**  
What data goes in and what comes out.

**Building blocks**
Authentication; Autorisation; Client registration; Provider registration; Facility registration; Consent registration

**Constraints**  
Relevant legal, organizational, or technical constraints.
