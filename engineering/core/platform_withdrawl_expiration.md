# Platform Withdrawl Expiration
Date: 2024-01-31
Participants: Ody, shumkov, knst, quantumexplorer, Pasta, Igor Markin
Scope(s): Core, Platform

## Status
Proposed

## Context
The handling of asset unlock transactions in the Dash core code has been a subject of discussion. Initially, it was thought that asset unlock transactions should not expire, aligning with the perspective that if a transaction is valid and complies with consensus rules, it should be considered valid indefinitely. However, concerns were raised regarding the complexity and security implications of not having an expiration for these transactions. Specifically, it was debated whether a transaction, once signed, should be valid indefinitely or if it should expire after a certain period or under specific conditions.

## Decision
It has been decided that asset unlock transactions will expire in core 48 blocks after the signing height (requestedHeight). The platform may reissue these transactions with the same index in the case of expiration. This decision is driven by the need to manage transaction validity efficiently and to ensure the security and integrity of the transaction process. By having transactions expire, it prevents the indefinite validity of transactions which could lead to potential security risks or complications in transaction management. The reissuing mechanism by the platform ensures that transactions that are still valid from a business logic perspective can be reattempted without changing their fundamental identity, as indicated by the index.

## Consequences
Simplification of Validation: By having transactions expire after a set number of blocks, the validation of asset unlocks becomes simpler and more predictable. Validators only need to consider a finite set of quorums for validation, rather than potentially thousands if transactions did not expire.

### Security:
Expiration of transactions mitigates the risk of old transactions being used inappropriately or maliciously. It ensures that the authority of a quorum is time-bound, aligning with the security model of other transaction types like ISLocks and CLSigs.

### Operational Complexity:
The platform will need to handle the reissuing of expired transactions, which adds a layer of operational complexity. However, this complexity is justified by the benefits in terms of security and manageability.

### Consistency with Expectations:
The decision aligns with the initial expectations and understanding of most participants in the discussion, ensuring that there is clarity and consensus on how asset unlock transactions are handled.

This decision reflects a balanced approach to managing asset unlock transactions, considering both operational practicality and the need to maintain a secure and robust transaction handling mechanism.
