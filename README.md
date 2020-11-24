# Crypto Commons

_Crypto Commons is the Gordian reference code & CLI utilities. It collects together all of Blockchain Commons' wallet libraries and the utilities built from them._

## Additional Information

The Crypto Commons includes reference libraries (mostly in C), which can be used to build wallets; and demos & tools, which exercise and exemplify those wallet libraries.

### Gordian Tools & Demos

_Blockchain Commons has released a number of kits and CLI tools that exercise the Gordian reference libraries._

* **[Keytool](https://github.com/BlockchainCommons/bc-keytool-cli) \(CLI\).** A tool for deriving keys and addresses from seeds. 
  * _Uses [bc-crypto-base](https://github.com/BlockchainCommons/bc-crypto-base)._
* **[LetheKit](https://github.com/BlockchainCommons/bc-lethekit) \(Hardware Kit\).** A do-it-yourself hardware kit for generating and translating seeds in an airgapped manner. Cotains its own version of seedtool built using the Arduino IDE.
  * _LetheKit's Seedtool exercises [bc-crypto-base](https://github.com/BlockchainCommons/bc-crypto-base), [bc-bip-39](https://github.com/blockchaincommons/bc-bip39), [bc-bytewords](https://github.com/BlockchainCommons/bc-bytewords), [bc-shamir](https://github.com/BlockchainCommons/bc-shamir), [bc-sskr](https://github.com/blockchaincommons/bc-sskr), and [bc-ur](https://github.com/BlockchainCommons/bc-ur) (the last through a bc-ur-arduino port)._
* **[Seedtool](https://github.com/BlockchainCommons/bc-seedtool-cli) \(CLI\).** A tool for generating seeds from a variety of random inputs and for translating seeds among formats like BIP39, [SSKR](https://github.com/blockchaincommons/bc-sskr), hex, and [Bytewords](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-012-bytewords.md).
   * _Exercises [bc-crypto-base](https://github.com/BlockchainCommons/bc-crypto-base), [bc-bip-39](https://github.com/blockchaincommons/bc-bip39), [bc-shamir](https://github.com/BlockchainCommons/bc-shamir), [bc-sskr](https://github.com/blockchaincommons/bc-sskr), and [bc-ur](https://github.com/BlockchainCommons/bc-ur)._
* **[URDemo](https://github.com/BlockchainCommons/URDemo) \(Demo\).** A demonstration of the [URKit](https://github.com/BlockchainCommons/URKit) that can be compiled and run in Xcode using Swift. It demonstrates multi-part animated QRs.

### Gordian Reference Libraries

_The Crypto Commons libraries are reference implementations, meant to be examples of how to standardly implement these various crypto functions._

#### *bc-crypto-base*

<table width="100%">
 <tr>
  <td width="10%"><b>Language</b></td>
  <td width="90%">C</td>
 </tr>
 <tr>
  <td><b>Link</b></td>
  <td><a href="https://github.com/BlockchainCommons/bc-crypto-base">bc-crypto-base</a></td>
 </tr>
 <tr>
  <td><b>Notes</b></td>
  <td>Well-reviewed, audited, and optimized crypto functions. Includes CRC32, HMAC-SHA-256, HMAC-SHA-512, PBKDF2-SHA-256, PBKDF2-SHA-512, SHA-256, and SHA-512 algorithms, and memzero functions.</td>
 </tr>
</table>

#### *bc-bech32*

<table width="100%">
 <tr>
  <td width="10%"><b>Language</b></td>
  <td width="90%">C</td>
 </tr>
 <tr>
  <td><b>Link</b></td>
  <td><a href="https://github.com/BlockchainCommons/bc-bech32">bc-bech32</a></td>
 </tr>
 <tr>
  <td><b>Notes</b></td>
  <td>Implementation of <a href="https://github.com/bitcoin/bips/blob/master/bip-0173.mediawiki">BIP-173</a>, Bech32 address format.<br><i>No longer being actively supported.</i>
</td>
 </tr>
</table>

#### *bc-bip-39*

<table width="100%">
 <tr>
  <td width="10%"><b>Language</b></td>
  <td width="90%">C</td>
 </tr>
 <tr>
  <td><b>Link</b></td>
  <td><a href="https://github.com/blockchaincommons/bc-bip39">bc-bip39</a></td>
 </tr>
 <tr>
  <td><b>Notes</b></td>
  <td>_Implementation of [BIP-39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki) mnemonic codes
</td>
 </tr>
</table>

#### *bc-bytewords*

<table width="100%">
 <tr>
  <td width="10%"><b>Language</b></td>
  <td width="90%">C</td>
 </tr>
 <tr>
  <td><b>Link</b></td>
  <td><a href="https://github.com/BlockchainCommons/bc-bytewords">bc-bytewords</a></td>
 </tr>
  <tr>
  <td><b>Notes</b></td>
  <td>_Implementation of bytewords from <a href="https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-012-bytewords.md">BCR-2020-012</a>.<br>Bytewords are also used in <a href="https://github.com/blockchaincommons/bc-sskr">bc-sskr</a> and <a href="https://github.com/BlockchainCommons/bc-ur">bc-ur</a>.
</td>
 </tr>
 <tr>
  <td><b>Description</b></td>
  <td>The Bytewords methodology encodes binary data as English words, using a set of 256 four-letter words, each of which can be recovering using just the first two letters.
</td>
 </tr>
</table>


* **[bc-shamir](https://github.com/BlockchainCommons/bc-shamir) \(C\).** Implementation of Shamir Secret Sharing.
* **[bc-slip39](https://github.com/BlockchainCommons/bc-slip39) \(C\).** Implementation of Satoshi Labs' [SLIP-39](https://github.com/satoshilabs/slips/blob/master/slip-0039.md). 
  * _Largely deprected due to discovery of round-trip failure with BIP-39. Blockchain Commons projects use [bc-sskr](https://github.com/blockchaincommons/bc-sskr) instead._
 * **[bc-sskr](https://github.com/blockchaincommons/bc-sskr) \(C\).** Implementation of Sharmir Secret Sharing Key Recovery, an alternative to SLIP-39 that allows round-tripping with BIP-39, as described in [BCR-2020-011](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-011-sskr.md).
   * _The SSKR methodology is an alternative to SLIP-39 that converts Shamir shards to [URs](https://github.com/BlockchainCommons/bc-ur) or [bytewords](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-012-bytewords.md). Its main improvement over SLIP-39 is that it  round trips with BIP-39, whereas [SLIP-39 does not](https://github.com/BlockchainCommons/bc-lethekit/issues/38)._
* **[bc-ur](https://github.com/BlockchainCommons/bc-ur) \(C++\).** Implementation of Blockchain Commons' UR standard for Uniform Resources, as described in [BCR-2020-005](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-005-ur.md).  
   * _The UR methodology allows the encoding of binary data of arbitrary content and length and their transportation using one or more URIs or QR codes (or alternatively animated QR codes). It also integrates with [bytewords](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-012-bytewords.md)._
   * _Blockchain Commons' UR has also been widely implemented in other languages:_
      * **[bc-ur-java](https://github.com/BlockchainCommons/bc-ur-java) \(Java\).** A Java implementation created by Bitmark.
      * **[URKit](https://github.com/BlockchainCommons/URKit) (Swift).** A Swift implementation that encodes and decodes URs.
      * Third-party implementations of UR include **[Hummingbird](https://github.com/sparrowwallet/hummingbird) (Java)**, **[foundation-ur-py](https://github.com/Foundation-Devices/foundation-ur-py) (Python)**, and **[ur-rs](https://github.com/dspicher/ur-rs) (Rust)**. 



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

[**Gordian System Discussions**](https://github.com/BlockchainCommons/Gordian/discussions). For users and developers of the Gordian system, including the Gordian Server, Bitcoin Standup technology, QuickConnect, and the Gordian Wallet. If you want to talk about our linked full-node and wallet technology, suggest new additions to our Bitcoin Standup standards, or discuss the implementation our standalone wallet, the Discussions area of the [main Gordian repo](https://github.com/BlockchainCommons/Gordian) is the place.

[**Wallet Standard Discussions**](https://github.com/BlockchainCommons/AirgappedSigning/discussions). For standards and open-source developers who want to talk about wallet standards, please use the Discussions area of the [Airgapped Signing repo](https://github.com/BlockchainCommons/AirgappedSigning). This is where you can talk about projects like our [LetheKit](https://github.com/BlockchainCommons/bc-lethekit) and command line tools such as [seedtool](https://github.com/BlockchainCommons/bc-seedtool-cli), both of which are intended to testbed wallet technologies, plus the libraries that we've built to support your own deployment of wallet technology such as [bc-bip39](https://github.com/BlockchainCommons/bc-bip39), [bc-slip39](https://github.com/BlockchainCommons/bc-slip39), [bc-shamir](https://github.com/BlockchainCommons/bc-shamir), [Shamir Secret Key Recovery](https://github.com/BlockchainCommons/bc-sskr), [bc-ur](https://github.com/BlockchainCommons/bc-ur), and the [bc-crypto-base](https://github.com/BlockchainCommons/bc-crypto-base). If it's a wallet-focused technology or a more general discussion of wallet standards,discuss it here.

[**Blockchain Commons Discussions**](https://github.com/BlockchainCommons/Community/discussions). For developers, interns, and patrons of Blockchain Commons, please use the discussions area of the [Community repo](https://github.com/BlockchainCommons/Community) to talk about general Blockchain Commons issues, the intern program, or topics other than the [Gordian System](https://github.com/BlockchainCommons/Gordian/discussions) or the [wallet standards](https://github.com/BlockchainCommons/AirgappedSigning/discussions), each of which have their own discussion areas.

### Other Questions & Problems

As an open-source, open-development community, Blockchain Commons does not have the resources to provide direct support of our projects. Please consider the discussions area as a locale where you might get answers to questions. Alternatively, please use this repository's [issues](./issues) feature. Unfortunately, we can not make any promises on response time.

If your company requires support to use our projects, please feel free to contact us directly about options. We may be able to offer you a contract for support from one of our contributors, or we might be able to point you to another entity who can offer the contractual support that you need.

### Credits

The following people directly contributed to this repository. You can add your name here by getting involved. The first step is learning how to contribute from our [CONTRIBUTING.md](./CONTRIBUTING.md) documentation.

| Name              | Role                | Github                                            | Email                                 | GPG Fingerprint                                    |
| ----------------- | ------------------- | ------------------------------------------------- | ------------------------------------- | -------------------------------------------------- |
| Christopher Allen | Principal Architect | [@ChristopherA](https://github.com/ChristopherA) | \<ChristopherA@LifeWithAlacrity.com\> | FDFE 14A5 4ECB 30FC 5D22  74EF F8D3 6C91 3574 05ED |

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
