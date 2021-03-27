# KeySend Protocols

Descriptions of Lightning Network KeySend Service Protocol TLV records.

## KeySend-Protocol-1 PushPayment

*Description*

Send a push payment that the receiver can claim using an encoded preimage.

*Records*

- `5482373484`: 32 Byte Preimage Corresponding to HTLC Preimage Hash

## KeySend-Protocol-2 Basic Messages

*Description*

Send a text message to a destination.

*Records*

- `34349334`: Message Contents UTF8 Encoded Bytes
- `34349337`: Message Signature Bytes
- `34349339`: Message Signer Public Key Bytes
- `34349343`: Epoch Time In Nanoseconds, Big-Endian Encoded
- `5482373484`: 32 Byte Preimage Corresponding to HTLC Preimage Hash

## KeySend-Protocol-3 Ping

*Description*

Send a request to a destination to receive a response payment to a payment request.

*Records*

- `34349334`: Message Contents UTF8 Encoded Bytes
- `5482373484`: 32 Byte Preimage Corresponding to HTLC Preimage Hash
- `8470534167946609795`: UTF8 Encoded Payment Request

## KeySend-Protocol-4 Dual Funding

*Description*

Negotiate Dual Funding of a new channel with a peer.

A dual-funded transit transaction will be formed which will pay into the channel funding transaction.

Request - Push KeySend with the following data:

- Proposed Channel Capacity
- Funding Transaction Fee Rate
- Channel Funding MultiSig Output Local Public Key
- Transit Transaction Id
- Transit Transaction Vout
- Accept Proposal Payment Request

Response - Responder Pays Accept Request with the following data:

- MultiSig Public Key
- Transit Transaction Id
- Transit Transaction Vout
- Funding Signature
- Transit Public Key

This allows the original requesting party to propose a channel.

*Records*

- `80501`: Initial Request Response BOLT 11 Payment Request
- `80502`: Base 16 Channel Capacity Tokens Number
- `80503`: Funding Transaction Signature Bytes
- `80504`: Base 16 Funding Transaction Fee Rate Per VByte
- `80505`: Channel MultiSig Public Key
- `80506`: Transit MultiSig Public Key
- `80507`: Transit Transaction Id Bytes
- `80508`: Transit Transaction Output Number
- `5482373484`: 32 Byte Preimage Corresponding to HTLC Preimage Hash
