![Crypto Commons](https://raw.githubusercontent.com/BlockchainCommons/crypto-commons/master/images/logos/crypto-commons-logo.png)

### _by Wolf McNally and Christopher Allen_

_Crypto Commons is the Gordian reference code & CLI utilities. It collects together all of Blockchain Commons' wallet libraries and the utilities built from them._

It includes reference libraries (mostly in C), which can be used to build wallets; and demos & tools, which exercise and exemplify those wallet libraries.

## Documents

_See the [complete listing](Docs/README.md)._

### SSKR

1. **[SSKR for Users](Docs/sskr-users.md)**
   * **[SSKR Cold Storage](Docs/sskr-cold-storage.md)**
   * **[SSKR Video Example](Docs/sskr-video.md)**
1. **[SSKR for Developers](Docs/sskr-developers.md)**
   * **[SSKR Test Vector](Docs/sskr-test-vector.md)**

### URs

1. **[URs: An Overview](Docs/ur-1-overview.md)**
   * **[A Guide to Using URs for PSBTs](Docs/ur-4-psbt.md)** [our biggest success story]
   * **[A Guide to Using URs for Key Material](Docs/ur-2-keys.md)**
   * **[A Guide to Using URs for SSKRs](Docs/ur-3-sskrs.md)**
   * **[A Guide to Using UR Request & Response](Docs/ur-99-request-response.md)**
1. **[crypto-request and crypto-response vs Signing via crypto-psbt](Docs/crypto-request-or-crypto-psbt.md)**
1. **[crypto-request test vectors](https://github.com/BlockchainCommons/crypto-commons/blob/master/Docs/crypto-request-test-vectors.md)**
1. **[crypto-seed test vectors](https://github.com/BlockchainCommons/crypto-commons/blob/master/Docs/crypto-seed-test-vectors.md)**
1. **[Animated QRs](https://www.blockchaincommons.com/devs/animated-qrs.html)**
1. **[Animated QRs Video](https://www.youtube.com/watch?v=HsFF5HPKQIk)**

### Envelopes (Videos)

1. **[Envelope Introduction](https://www.youtube.com/watch?v=OcnpYqHn8NQ)**
1. **[Envelope Overview](https://www.youtube.com/watch?v=K2gFTyjbiYk)**
1. **[Envelope & SSKR](https://www.youtube.com/watch?v=ERRhMDSEFm8)**
   * **[Seed Tool & SSKR](https://www.youtube.com/watch?v=aciTNh402Co)**
1. **[Envelope MVA](https://www.youtube.com/watch?v=S0deyIHXukk)**
1. **[Envelope Non-Correlation & Elision](https://www.youtube.com/watch?v=ubqKJAizayU)**
1. **[Envelope-CLI](https://www.youtube.com/watch?v=JowheoEIGmE)**
1. **[Envelope-CLI Q&A](https://www.youtube.com/watch?v=2MjcrKLEsSE)**

### Video Overview

<a href="https://www.youtube.com/watch?v=RYgOFSdUqWY"><img src="images/video-tech-overview.png"></a>

## Gordian Tools & Demos

_Blockchain Commons has released a number of kits and CLI tools that exercise the Gordian reference libraries._

* **[Bytewords](https://github.com/BlockchainCommons/bc-bytewords-cli) \(CLI\).** A tool for testing bytewords.
   * _Exercises [bc-crypto-base](https://github.com/BlockchainCommons/crypto-commons/blob/master/README.md#bc-crypto-base) and [bc-bytewords](https://github.com/blockchaincommons/bc-bytewords)._
* **[dCBOR](https://github.com/BlockchainCommons/dcbor-cli) \(CLI\).** A tool for parsing & validating deterministic CBOR.
   * _Exercises [bc-dcbor-rust](https://github.com/BlockchainCommons/bc-dcbor-rust)._
* **[Keytool](https://github.com/BlockchainCommons/bc-keytool-cli) \(CLI\).** A tool for deriving keys and addresses from seeds. 
  * _Uses [bc-crypto-base](https://github.com/BlockchainCommons/crypto-commons/blob/master/README.md#bc-crypto-base)._
* **[LetheKit](https://github.com/BlockchainCommons/bc-lethekit) \(Hardware Kit\).** A do-it-yourself hardware kit for generating and translating seeds in an airgapped manner. Cotains its own version of seedtool built using the Arduino IDE.
  * _LetheKit's Seedtool exercises [bc-crypto-base](https://github.com/BlockchainCommons/crypto-commons/blob/master/README.md#bc-crypto-base), [bc-bip-39](https://github.com/BlockchainCommons/crypto-commons/blob/master/README.md#bc-bip-39), [bc-bytewords](https://github.com/BlockchainCommons/crypto-commons/blob/master/README.md#bc-bytewords), [bc-shamir](https://github.com/BlockchainCommons/crypto-commons/blob/master/README.md#bc-shamir), [bc-sskr](https://github.com/BlockchainCommons/crypto-commons/blob/master/README.md#bc-sskr), and [bc-ur](https://github.com/BlockchainCommons/crypto-commons/blob/master/README.md#bc-ur) (the last through a bc-ur-arduino port)._
* **[LifeHashTool](https://github.com/BlockchainCommons/LifeHashTool) \(Swift CLI\).** A tool for generating Lifehash PNGs from the command line.
  * _LifeHashTool uses [LifeHash](https://github.com/BlockchainCommons/LifeHash)._
* **[Seedtool](https://github.com/BlockchainCommons/bc-seedtool-cli) \(CLI\).** A tool for generating seeds from a variety of random inputs and for translating seeds among formats like BIP39, [SSKR](https://github.com/blockchaincommons/bc-sskr), hex, and [Bytewords](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-012-bytewords.md).
   * _Exercises [bc-crypto-base](https://github.com/BlockchainCommons/crypto-commons/blob/master/README.md#bc-crypto-base), [bc-bip-39](https://github.com/BlockchainCommons/crypto-commons/blob/master/README.md#bc-bip-39), [bc-shamir](https://github.com/BlockchainCommons/crypto-commons/blob/master/README.md#bc-shamir), [bc-sskr](https://github.com/BlockchainCommons/crypto-commons/blob/master/README.md#bc-sskr), and [bc-ur](https://github.com/BlockchainCommons/crypto-commons/blob/master/README.md#bc-ur)._
* **[URDemo](https://github.com/BlockchainCommons/URDemo) \(iOS Demo\).** A demonstration of the [URKit](https://github.com/BlockchainCommons/crypto-commons/blob/master/README.md#bc-ur) that can be compiled and run in Xcode using Swift. It demonstrates multi-part animated QRs.

See also our [Gordian repo](https://github.com/BlockchainCommons/Gordian/blob/master/README.md#quick-links-for-reference-apps) for our complete list of reference apps, including other CLIs, mobile apps, and web servers.

## Gordian Reference Libraries

_The Crypto Commons libraries are reference implementations, meant to be examples of how to standardly implement these various crypto functions._

### *bc-crypto-base*

_Well-reviewed, audited, and optimized crypto functions. Includes CRC32, HMAC-SHA-256, HMAC-SHA-512, PBKDF2-SHA-256, PBKDF2-SHA-512, SHA-256, and SHA-512 algorithms, and memzero functions._

| Language | Repo | Contributor | Status |
|----------|------|-------------|--------|
| C | [bc-crypto-base](https://github.com/BlockchainCommons/bc-crypto-base) | Blockchain Commons |
| Java | [bc-libs-java](https://github.com/BlockchainCommons/bc-libs-java) | Bitmark | 
| Rust | [bc-crypto-rust](https://github.com/BlockchainCommons/bc-crypto-rust) | Blockchain Commons |
| Swift | [BCLibsSwift](https://github.com/BlockchainCommons/BCLibsSwift) | Blockchain Commons |

### *bc-bech32*

**Specification:** [BIP-173](https://github.com/bitcoin/bips/blob/master/bip-0173.mediawiki)

_Implementation of Bech32 address format. No longer being actively supported._

| Language | Repo | Contributor | Status |
|----------|------|-------------|--------|
| C | [bc-bech32](https://github.com/BlockchainCommons/bc-bech32) | Blockchain Commons | Unsupported |

### *bc-bip-39*

**Specification:** [BIP-39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki)

_Implementation of BIP-39 mnemonic codes._

| Language | Repo | Contributor | Status |
|----------|------|-------------|--------|
| C | [bc-bip39](https://github.com/blockchaincommons/bc-bip39) | Blockchain Commons | |
| Java | [bc-libs-java](https://github.com/BlockchainCommons/bc-libs-java) | Bitmark | 

### *bc-bytewords*

**Specification:** [bcr-2020-012](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-012-bytewords.md)

_The Bytewords methodology encodes binary data as English words, using a set of 256 four-letter words, each of which can be recovering using just the first two letters. Bytewords are also used in [bc-sskr](https://github.com/blockchaincommons/bc-sskr) and [bc-ur](https://github.com/BlockchainCommons/bc-ur)._

| Language | Repo | Contributor | Status |
|----------|------|-------------|--------|
| C | [bc-bytewords](https://github.com/BlockchainCommons/bc-bytewords) | Blockchain Commons | |
| Java | [bc-libs-java](https://github.com/BlockchainCommons/bc-libs-java) | Bitmark | 


### *bc-dcbor*

**Specification:** [RFC8949](https://www.rfc-editor.org/rfc/rfc8949.html) / [dCBOR I-D](https://datatracker.ietf.org/doc/draft-mcnally-deterministic-cbor/)

_Libraries for CBOR compliant with the [deterministic options](https://www.rfc-editor.org/rfc/rfc8949.html#name-deterministically-encoded-c). For more, see our [dCBOR page](dcbor.md)._

| Language | Repo | Contributor | Status |
|----------|------|-------------|--------|
| Rust | [bc-dcbor-rust](https://github.com/BlockchainCommons/bc-dcbor-rust) | Blockchain Commons | |
| Swift | [BCSwiftDCBOR](https://github.com/BlockchainCommons/BCSwiftDCBOR) | Blockchain Commons | |


### *bc-envelope*

**Specification:** [Envelope Structured Data Format I-D](https://datatracker.ietf.org/doc/draft-mcnally-envelope/)

_Libraries for [Gordian Envelope](https://www.blockchaincommons.com/introduction/Envelope-Intro/)._

| Language | Repo | Contributor | Status |
|----------|------|-------------|--------|
| Rust | [bc-envelope-rust](https://github.com/BlockchainCommons/bc-envelope-rust) | Blockchain Commons | |
| Swift | [BCSwiftEnvelope](https://github.com/BlockchainCommons/BCSwiftEnvelope) | Blockchain Commons | |


### *bc-lifehash*

**Overview:** [Lifehash.info](https://github.com/BlockchainCommons/lifehash.info)

_A library for creating LifeHash visual hashes._

| Language | Repo | Contributor | Status |
|----------|------|-------------|--------|
| C/C++ | [bc-lifehash](https://github.com/BlockchainCommons/bc-lifehash) | Blockchain Commons |
| Python | [bc-lifehash-python](https://github.com/BlockchainCommons/bc-lifehash-python) | CrossBar |
| Swift | [LifeHash](https://github.com/BlockchainCommons/LifeHash) | Blockchain Commons |

### *bc-shamir*

**Specification:** ["How to Share a Secret"](https://dl.acm.org/doi/pdf/10.1145/359168.359176)

_Implementation of Shamir's Secret Sharing._

| Language | Repo | Contributor | Status |
|----------|------|-------------|--------|
| C | [bc-shamir](https://github.com/BlockchainCommons/bc-shamir) | Blockchain Commons | [Security Reviewed](https://github.com/BlockchainCommons/bc-shamir/blob/master/SECURITY-REVIEW.md) |
| Java | [bc-libs-java](https://github.com/BlockchainCommons/bc-libs-java) | Bitmark | 
| Rust | [bc-shamir-rust](https://github.com/BlockchainCommons/bc-shamir-rust) | Blockchain Commons |
| Swift | [BCLibsSwift](https://github.com/BlockchainCommons/BCLibsSwift) | Blockchain Commons |

### *bc-slip39*

**Specification:** [SLIP-39](https://github.com/satoshilabs/slips/blob/master/slip-0039.md).

_Implementation of Satoshi Labs' SLIP-39. Largely deprected due to discovery of [round-trip failure with BIP-39](https://github.com/BlockchainCommons/bc-lethekit/issues/38). Blockchain Commons projects use [bc-sskr](https://github.com/blockchaincommons/bc-sskr) instead._

| Language | Repo | Contributor | Status |
|----------|------|-------------|--------|
| C | [bc-slip39](https://github.com/BlockchainCommons/bc-slip39) | Blockchain Commons | Deprecated |

### *bc-sskr*

**Specification:** [bcr-2020-011](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-011-sskr.md)

_The SSKR (Sharded Secret Key Reconstruction) methodology is an alternative to SLIP-39 that converts Shamir shares to [URs](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-012-bytewords.md) or [bytewords](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-012-bytewords.md). Its main improvement over SLIP-39 is that it round trips with BIP-39, whereas [SLIP-39 does not](https://github.com/BlockchainCommons/bc-lethekit/issues/38)._

| Language | Repo | Contributor | Status |
|----------|------|-------------|--------|
| C | [bc-sskr](https://github.com/blockchaincommons/bc-sskr) | Blockchain Commons | [Security Reviewed](https://github.com/BlockchainCommons/bc-sskr/blob/master/SECURITY-REVIEW.md) |
| Java | [bc-libs-java](https://github.com/BlockchainCommons/bc-libs-java) | Bitmark | 
| JavaCard | [jc-sskr](https://github.com/proxyco/jc-sskr) | Proxy |
| Rust | [bc-sskr-rust](https://github.com/BlockchainCommons/bc-sskr-rust) | Blockchain Commons |
| Swift | [BCLibsSwift](https://github.com/BlockchainCommons/BCLibsSwift) | Blockchain Commons |

### *bc-ur*

**Specification:** [bcr-2020-005](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-005-ur.md)

_The UR methodology allows the encoding of binary data of arbitrary content and length and their transportation using one or more URIs or QR codes (or alternatively animated QR codes). It also integrates with [bytewords](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-012-bytewords.md)._

| Language | Repo | Contributor | Status |
|----------|------|-------------|--------|
| C++ | [bc-ur](https://github.com/BlockchainCommons/bc-ur) | Blockchain Commons |
| Java | [bc-ur-java](https://github.com/BlockchainCommons/bc-ur-java) | Bitmark |
| Java | [Hummingbird](https://github.com/sparrowwallet/hummingbird) | Craig Raw |
| Python | [foundation-ur-py](https://github.com/Foundation-Devices/foundation-ur-py) | Foundation |
| Rust | [bc-ur-rust](https://github.com/BlockchainCommons/bc-ur-rust) | Blockchain Commons | 
| Rust | [ur-rust](https://github.com/dspicher/ur-rs) | Dominik Spicher |
| Swift | [URKit](https://github.com/BlockchainCommons/URKit) + [URUI](https://github.com/BlockchainCommons/URUI) | Blockchain Commons |

## Third-Party Libraries

Blockchain Commons also uses well-supported libraries from third parties. In particular, we make strong usage of The Elements Project [libwally wallet library](https://github.com/ElementsProject/libwally-core). We are further supporting it with wrappers for [Swift](https://github.com/BlockchainCommons/BCLibwallySwift) and [Java](https://github.com/BlockchainCommons/bc-bclibwally-java).

## Status - Varied

Please see individual projects for their exact status. The C libraries are largely in feature-complete beta status.

## Origin, Authors, Copyright & Licenses

Unless otherwise noted (either in this [/README.md](./README.md) or in the file's header comments) the contents of this repository are Copyright © 2020 by Blockchain Commons, LLC, and are [licensed](./LICENSE) under the [spdx:BSD-2-Clause Plus Patent License](https://spdx.org/licenses/BSD-2-Clause-Patent.html).

In most cases, the authors, copyright, and license for each file reside in header comments in the source code. When it does not, we have attempted to attribute it accurately in the table below.

## Financial Support

Crypto Commons is a project of [Blockchain Commons](https://www.blockchaincommons.com/). We are proudly a "not-for-profit" social benefit corporation committed to open source & open development. Our work is funded entirely by donations and collaborative partnerships with people like you. Every contribution will be spent on building open tools, technologies, and techniques that sustain and advance blockchain and internet security infrastructure and promote an open web.

To financially support further development of Crypto Commons and other projects, please consider becoming a Patron of Blockchain Commons through ongoing monthly patronage as a [GitHub Sponsor](https://github.com/sponsors/BlockchainCommons). You can also support Blockchain Commons with bitcoins at our [BTCPay Server](https://btcpay.blockchaincommons.com/).

## Contributing

We encourage public contributions through issues and pull requests! Please review [CONTRIBUTING.md](./CONTRIBUTING.md) for details on our development process. All contributions to this repository require a GPG signed [Contributor License Agreement](./CLA.md).

### Discussions

The best place to talk about Blockchain Commons and its projects is in our GitHub Discussions areas.

[**Gordian Developer Community**](https://github.com/BlockchainCommons/Gordian-Developer-Community/discussions). For standards and open-source developers who want to talk about interoperable wallet specifications, please use the Discussions area of the [Gordian Developer Community repo](https://github.com/BlockchainCommons/Gordian-Developer-Community/discussions). This is where you talk about Gordian specifications such as [Gordian Envelope](https://github.com/BlockchainCommons/Gordian/tree/master/Envelope#articles), [bc-shamir](https://github.com/BlockchainCommons/bc-shamir), [Sharded Secret Key Reconstruction](https://github.com/BlockchainCommons/bc-sskr), and [bc-ur](https://github.com/BlockchainCommons/bc-ur) as well as the larger [Gordian Architecture](https://github.com/BlockchainCommons/Gordian/blob/master/Docs/Overview-Architecture.md), its [Principles](https://github.com/BlockchainCommons/Gordian#gordian-principles) of independence, privacy, resilience, and openness, and its macro-architectural ideas such as functional partition (including airgapping, the original name of this community).

[**Blockchain Commons Discussions**](https://github.com/BlockchainCommons/Community/discussions). For developers, interns, and patrons of Blockchain Commons, please use the discussions area of the [Community repo](https://github.com/BlockchainCommons/Community) to talk about general Blockchain Commons issues, the intern program, or topics other than those covered by the [Gordian Developer Community](https://github.com/BlockchainCommons/Gordian-Developer-Community/discussions) or the 
[Gordian User Community](https://github.com/BlockchainCommons/Gordian/discussions).### Other Questions & Problems

As an open-source, open-development community, Blockchain Commons does not have the resources to provide direct support of our projects. Please consider the discussions area as a locale where you might get answers to questions. Alternatively, please use this repository's [issues](./issues) feature. Unfortunately, we can not make any promises on response time.

If your company requires support to use our projects, please feel free to contact us directly about options. We may be able to offer you a contract for support from one of our contributors, or we might be able to point you to another entity who can offer the contractual support that you need.

### Credits

The following people directly contributed to this repository. You can add your name here by getting involved. The first step is learning how to contribute from our [CONTRIBUTING.md](./CONTRIBUTING.md) documentation.

| Name              | Role                | Github                                            | Email                                 | GPG Fingerprint                                    |
| ----------------- | ------------------- | ------------------------------------------------- | ------------------------------------- | -------------------------------------------------- |
| Christopher Allen | Principal Architect | [@ChristopherA](https://github.com/ChristopherA) | \<ChristopherA@LifeWithAlacrity.com\> | FDFE 14A5 4ECB 30FC 5D22  74EF F8D3 6C91 3574 05ED |
| Wolf McNally      | Lead Researcher       | [@WolfMcNally](https://github.com/wolfmcnally)    | \<Wolf@WolfMcNally.com\>              | 9436 52EE 3844 1760 C3DC  3536 4B6C 2FCF 8947 80AE |

## Responsible Disclosure

We want to keep all of our software safe for everyone. If you have discovered a security vulnerability, we appreciate your help in disclosing it to us in a responsible manner. We are unfortunately not able to offer bug bounties at this time.

We do ask that you offer us good faith and use best efforts not to leak information or harm any user, their data, or our developer community. Please give us a reasonable amount of time to fix the issue before you publish it. Do not defraud our users or us in the process of discovery. We promise not to bring legal action against researchers who point out a problem provided they do their best to follow the these guidelines.

### Reporting a Vulnerability

Please report suspected security vulnerabilities in private via email to ChristopherA@BlockchainCommons.com (do not use this email for support). Please do NOT create publicly viewable issues for suspected security vulnerabilities.

The following keys may be used to communicate sensitive information to developers:

| Name              | Fingerprint                                        |
| ----------------- | -------------------------------------------------- |
| Christopher Allen | FDFE 14A5 4ECB 30FC 5D22  74EF F8D3 6C91 3574 05ED |

You can import a key by running the following command with that individual’s fingerprint: `gpg --recv-keys "<fingerprint>"` Ensure that you put quotes around fingerprints that contain spaces.
