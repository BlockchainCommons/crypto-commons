# SSKR for Developers

SSKR is Sharded Secret Key Reconstruction. It's a methodology for secret sharing 
that allows for the sharding of a master seed into multiple shares, which may then be combined with a certain threshold to reconstruct that secret. Major expansions of the SSKR specification over previous standards include:

1. Compatibility with BIP-39.
2. Implementation of two-level shards.
3. Encoding of shards as ByteWords.
4. Integration with URs.

Currently, SSKR supports one secret-sharing algorithm: Shamir's Secret Sharing, which is version `0` of SSKR types. As such, it's intended to replace SLIP-39 as a specification for Shamir's Secret Sharing.

## Where Can I Find SSKR?

**Specification:** 

SSKR is described in a Blockchain Commons research paper.

* [BCR-0011: UR Type Definition for Sharded Secret Key Reconstruction (SSKR)](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-011-sskr.md)

**Code Libraries:**

The core of SSKR is in the `bc-sskr` library:

* [bc-sskr](https://github.com/blockchaincommons/bc-sskr) (C library)

However, SSKR was built with a modular design allowing developers to choose both the underlying secret sharing and the encoding that they use.

The Shamir's Secret Sharing used by default with SSKR is found in the `bc-shamir` library, which is supported by the `bc-crypto-base` library:

* [bc-crypto-base](https://github.com/blockchaincommons/bc-crypto-base) (C library)
* [bc-shamir](https://github.com/blockchaincommons/bc-shamir) (C library)

SSKR's default encoding method is ByteWords, which is available in the `bc-bytewords` library:

* [bc-bytewords](https://github.com/BlockchainCommons/bc-bytewords) (C library)

Many of these libraries are available in the following conversions:

* [bc-libs-java](https://github.com/BlockchainCommons/bc-libs-java) (Java library for crypto-base, shamir, sskr, and bytewords)
* [BCLibsSwift](https://github.com/BlockchainCommons/BCLibsSwift) (Swift library for crypto-base, shamir, and sskr)

**Sample Code:**

The following applications demonstrate the usage of SSKR:

* [Gordian Guardian](https://github.com/BlockchainCommons/GordianGuardian-iOS) (app implementation)
* [LetheKit](https://github.com/BlockchainCommons/bc-lethekit) (hardware implementation)
* [SeedTool](https://github.com/BlockchainCommons/bc-seedtool-cli) (CLI implementation)

## How Do I Use SSKR?

SSKR allows you to protect a 32-byte seed. You will also need to think about a few other things when utilizing SSKR:

* The seed being encrypted must be truly random, with high entropy.
* The shares are non-deterministic due to a random factor in their creation. This means that shares will look different every time you generate them.
* If you need to protect more than 32 bytes, you will need to either create muktiple SSKR objects or else encrypt the additional data using the 32-byte value being protected by SSKR as an encryption key. 

The last point is particularly notable because multilayered encryption of this type is required to protect a standard BIP-32 HD wallet, which is typically built with a 32-byte private key and its 32-byte chain code; it is also necessary to preserve metadata related to any 32-byte key. It may also be required in other situations where more than 32 bytes are being preserved for later reconstruction.

## Why Use Shamir's Secret Sharing?

Shamir's Secret Sharing (SSS) is built on an old, well-respected cryptographic proof, and so we have faith in its foundational concepts. 

Though we believe that [the usage of multisig](https://github.com/BlockchainCommons/Gordian/blob/master/Docs/Multisig.md) is superior to SSS, because Shamir's Secret Sharing can expose the user to vulnerability on the machine where a key is reconstructed, we nonetheless acknowledge that many users prefer Shamir's Secret Sharing, in large part for compatibility with last-generation single-signature addresses. 

So, while we're leading the way in using multisig to better protect our digital wealth, we're also interested in improving the interoperability of resilient, single-signature addresses, and that primarily means improving the interoperability of Shamir's Secret Sharing.

## What are Two-Level Shards?

Using SSKR, you can implement Shamir's Secret Sharing as normal, using a group of shards with a threshold for reconstruction. However, you can also implement a two-level hierarchy with multiple groups, each of which contain some shards. You can then specify a threshold for both groups and shards.

For example, you could create shares for 2 groups: the first group might require 2 of 3 shares and the second group might require 3 of 5 shares. With a group threshold of 2, individual thresholds from both groups must be met.

## What are ByteWords?

SSKR shards can be output as [Bytewords](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-012-bytewords.md), which is a specification for outputting encoded binary data as English words. We purposefully differentiated it from the BIP-39 mnemonics to avoid confusion: we wanted to make it obvious that the shards were SSKR, as evidenced by the ByteWords encoding, as opposed to SLIP-39, which would use BIP-39 encoding.

ByteWords also has several advantages. It's as efficient as hex, the words are all a uniform four letters, there are no homophones, and the first and last characters of each word differ from other words. Words were also specifically chosen to either be concrete or else to have valence. All around, the goal was to make ByteWords very easy to distinguish.

## What are URs?

URs are [Uniform Resources](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-005-ur.md), another Blockchain Commons specification. They describe a methodology for efficient, self-describing resources, and are easily interoperable with ByteWords. We choose them as another output format for SSKR.

See [A Guide to Using URs for SSKRs](ur-3-sskrs.md) for how ByteWord SSKRs and UR SSKRs are encoded, and how they slightly differ.

## Why Did We Create a New Standard?

We are well aware of the problems of creating yet more standards, as depicted by the ever-insightful Randall Munroe:

![](https://imgs.xkcd.com/comics/standards.png)

In the case of SSKR we felt that the creation of a new specification for Shamir's Secret Sharing was critical due to problems that we identified with the previous implementations, primarily SLIP-39, which we discovered [did not round trip with BIP-39](https://github.com/BlockchainCommons/bc-lethekit/issues/38).

The result is SSKR, which is similar to SLIP-39, but not compatible. It includes the same Shamir's Secret Sharing technology, but uses a different key-derivation methodology, for compatibility with BIP-39.

Seeing the need for a new specification that roundtripped with BIP-39 also allowed the possibility for expansion, which permitted us to introduce two-level shards as a major new feature.

## Why Did We Create New Libraries?

Obviously, with a new specification, we also needed libraries for that specification. We created C reference libraries for SSS and SSKR and modularizing the contents to allow a developer to pick and choose how they were put together. These libraries were later converted to Java, then our [contributing sponsor Bitmark](https://bitmark.com/) converted them to Swift.

Our new libraries also resolve one of our long-standing problems with SSS: we've always felt that Shamir's Secret Sharing looked deceptively easy to code, which has resulted in more than one implementation incorporating fundamental problems, from the lack of round-tripping in SLIP-39, to incorrect use of entropy in other implementations. Thus, we were happy to offer our own implementation, building on the cryptographic expertise of Blockchain Commons members and other experts in the field such as Daan Sprenkels.

## What is the Foundation of SSKR?

SSKR is the end-result of over two years of effort. It most immediately grew out of workgroups at the Rebooting the Web of Trust design workshops. At [RWOT8 in Barcelona](https://github.com/WebOfTrustInfo/rwot8-barcelona), a group of experts worked on "Shamir's Secret Sharing Best Practices" and the foundation of a new library, while at [RWOT9 in Prague](https://github.com/WebOfTrustInfo/rwot9-prague), a new cohort further discussed use cases, formats, and the two-level scheme. These workgroups included experts such as Christopher Allen, Bryan Bishop, Laurence Chen, Hank Chiu, Mark Friedenbach, Chris Howe, Yancy Ribbens, Daan Sprenkels, ChiaWei Tang, and  others. Initial work on Blockchain Common's `bc-shamir` library grew from Daan's work on his own [SSS library](https://github.com/dsprenkels/sss). Further encouragement to produce the new SSKR specification came from Ken Sedgwick, who identified the round-tripping problems between BIP-39 and SLIP-39.

## What is the Future of SSKR?

SSKR was designed from the beginning to work with different types of secret sharing. The first expansion is likely to be into VSS.

_Also see the [SSKR Example & Test Vector](sskr-test-vector.md) for a ready-to-use seed and [A Guide to Using URs for SSKRs](https://github.com/BlockchainCommons/crypto-commons/blob/shannona-docs-sskr-request-response/Docs/ur-3-sskrs.md) for discussions of a variety of SSKR formatting._
