# Modular and decoupled

## Statement

Solutions are built from independent building blocks with clear interfaces, so each can be replaced or extended without affecting the others.

## Rationale

Countries move at different speeds and use different systems. Loose coupling lets each country change its systems without breaking cross-border exchange. Modularity also simplifies change, reduces complexity and improves maintainability and scalability.

## Implications

- Data is separated from functionality.
- Building blocks communicate only through published, standardised interfaces.
- Functions, data structures and technologies are decoupled, so each can change on its own.
- Applications can use external data and functions.
- We avoid vendor lock-in.

<small>Source: Merges the former *Flexible* and *Decouplable* principles, based on ZiRA/Sigra *Flexibel* and *Ontkoppelbaar* ([Sigra 2025](../references.md#ref-sigra2025)). Aligned with the CumuluZ concept of separating data and functionality ([VWS 2025](../references.md#ref-vws2025)) and the modular building blocks of the WHO SMART reference architecture ([WHO n.d.](../references.md#ref-whosmart)).</small>
