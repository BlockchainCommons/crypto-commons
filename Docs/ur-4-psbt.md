# A Guide to Using URs for PSBTs

Uniform Resources (URs) allow for the encoding of a variety of information, including a variety of crypto-data. This document describes how they are used to encode PSBTs, or Partially Signed Bitcoin Transactions.

As usual, this will typically be done for you automatically using Blockchain Commons' [libraries](https://github.com/BlockchainCommons/crypto-commons/blob/master/README.md#bc-ur), but what follows is an explanation of how everything works.

## Why Use URs for PSBTs?

PSBTs are perhaps the ultimate interoperable data type in Bitcoin Core. They were explicitly built to allow different devices to create and/or sign Bitocin transmissions. As such, they are crucial to [Gordian](https://github.com/BlockchainCommons/Gordian) best practices, which advocate for the storage or seeds and other vulnerable data on non-networked devices. Using PSBTs, transactions can be created on networked devices, shipped to non-networked devices for signing, then shipped back to the networked devices for transmission. 

So why do you need URs rather than PSBT's standard data format? Quite simply, because PSBTs are too big. If you're just sending around a PSBT's mass of data as base64, no problem. But when transmitting to non-networked devices, for maximum resiliency of your seeds and keys, you probably need to use QRs, and even if you can jam a PSBT into a QR, it may not be readable by a computer camera.

This is especially true when PSBTs are used for multisigs, which is a prime use case for PSBTs: they can allow a transaction to be easily passed around until it's signed by a threshold of people required to authenticate a UTXO. However, as signatures accrue, a PSBT gets ever bigger, to the point where it may be too large for a QR code entirely.

URs resolve this by using fountain codes to enable Animated QRs. A single UR is turned into a sequence or URs, each preceded by its type and by its place in a sequence. Each individual frame is not just small enough to fit into a QR, but small enough to be read by a lower-resolution camera. (Best practice is to allow a user to dynamically downsize an animated QR if they're having troubles transmitting it.) The reading device then reads the animation until it's put together enough frames to reconstruct the original data.

## PRBTs: `[crypto-psbt]`
