# Enhanced Transaction Propogation including ISLock Signature

* Date: 2024-02-01
* Participants: pasta
* Scope(s): Core, Light Clients(mobile, electrum)

## Status

Proposed

## Context

The process of broadcasting transactions and the associated Instant Send Locks (ISLocks) in the network is
bandwidth-intensive. Currently, an ISLock, which ensures that a transaction is instantly locked and cannot be
double-spent, is sent separately from the transaction itself. This separation leads to redundancy as the transaction
inputs are included both in the transaction and the ISLock. To optimize bandwidth usage and improve network efficiency,
a proposal has been made to append the Instant Send Lock signature directly to the transaction broadcast message,
rather than sending it as a separate message.

## Decision

It is proposed that a BLS signature of 96 bytes, representing the Instant Send Lock, be appended to every transaction
broadcast message when an Instant Send Lock is available. This will be activated via a new Protocol Version to be
documented when decided. If an Instant Send Lock is not available for a particular
transaction, this 96-byte field should be filled with zeros or a predefined placeholder. When a node requests a
transaction and an Instant Send Lock is available, the node will receive the serialized transaction appended with
the serialized signature of the Instant Send Lock. This approach will enable the reconstruction of the actual Instant
Send Lock from the transaction and its appended signature, eliminating the need to broadcast the inputs of the
transaction again as part of the ISLock.

## Consequences

1. **Bandwidth Efficiency:** By bundling the transaction and its corresponding Instant Send Lock signature, the
bandwidth used for broadcasting transactions will be significantly reduced, as there will be no need to send a 
separate message for the ISLock.

2. **Improved Network Performance:** The reduction in the amount of data sent across the network for each transaction
will lead to overall improved network performance, potentially reducing latency and increasing throughput.

3. **Simplified Transaction Processing:** Nodes will be able to process transactions and their corresponding ISLocks
more efficiently, as they will receive all necessary information in a single message, reducing the complexity and time
required for transaction validation.

4. **Compatibility and Transition Considerations:** This change will require careful consideration regarding backward
compatibility and the transition mechanism. Nodes running older versions of the software may not understand the new
5. format, so a clear strategy will need to be developed to ensure a smooth network-wide transition.

By appending the Instant Send Lock signature directly to the transaction broadcast message, the network will operate 
more efficiently, with reduced bandwidth requirements and improved transaction processing times. However, careful 
planning and implementation will be necessary to manage the transition and ensure compatibility across the network.
