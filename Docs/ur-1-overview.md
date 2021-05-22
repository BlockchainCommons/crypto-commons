# Uniform Resources (UR): An Overview

The [Uniform Resources](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-005-ur.md) specification is a method for encoding structured binary data in plain-text strings that are also well-formed URIs. It's usable with any binary data, but was developed with Bitcoin and other cryptocurrencies in mind.

To be precise, Uniform Resources (URs) include:

1. A standard way to wrap [CBOR-encoded data structures](https://cbor.io/) in a URI.
2. A standard way to type the data in the URI so that it is self-describing.
3. A standard way split and sequence longer messages.
4. Optimizations for efficiency when URs are presented as QR codes.

URs are a crucial element of the [Gordian architecture](https://github.com/BlockchainCommons/Gordian), allowing for the self-identified encoding of a variety of cryptographic data, [all listed in a registry of data types](06-urtypes.md), most notably including seeds, keys, shards, and PSBTs. It's focused on airgapped usage and allows for standardized interoperability for Bitcoin apps released by different companies.

> :bulb: _URs are used widely in our Gordian reference apps, but our community members have focused most on UR's sequencing feature to create animated QRs that support PSBTs. URs can do a lot more: they can support any airgapped Bitcoin function and more than that, can support data encoding for a large number of decentralized technologies._


## Why Another Standard?

We are well aware of the dangers of competing standards:

![](https://imgs.xkcd.com/comics/standards.png)

However, we believe that the UR specification serves enough real purposes to make the introduction of a new specification worthwhile:

* **It's self-identifying.** We saw different methodologies for transfering keys such as `xpub`, `ypub`, and `zpub` proliferating and thus causing confusion. Worse, they created layer violations by mixing encoding and policy. We wanted to create a specification with more clearly defined layers that could be expandable, yet still self-identify its contents.
* **It's focused on security.** We're well aware that the transfer of key material between devices is a prime point of vulnerability, and so URs do their best to minimize that danger, ideally by supporting the transmission of those keys (and seeds and other private information) in an airgapped fashion.
* **It integrates with QRs.** While QR codes themselves are standard, the data encoded within QR codes is not, resulting in inconsistent usage among developers. We designed URs to resolve these interoperability issues by creating a standardized method for encoding binary data using CBOR and by specifying how to sequence larger binary encoding (as version 40 QR codes max out at 2,953 bytes).
* **It focuses on the multisig experience.** We see multisig as the future of Bitcoin, allowing for the creation of independent and resilient cryptocurrency addresses. Previous specifications are locked into the single-sig paradigm, while URs include specifications for a variety of data types crucial to multisig use.

## What is an Airgap?

You can't ever be certain that a network or serial interface between two devices won't lead to one of those devices corrupting the other. Nor can you be certain that a networked connection is proof from man-in-the-middle attacks. That leads to the need for airgaps, where devices don't physically connect. To still allow connectivity, airgaps leverage the cameras and displays in the devices to communicate "through a gap of air". Supporting airgaps is one of the primary purposes for URs: they support the use of QR codes to communicate through that gap of air, and then use UR's tagging feature to reveal what has been sent. This allows the transmission of arbitrary structured data between diverse platforms.

Blockchain Commons' development of airgap specifications is not just the product of our work, but also cooperation with other Bitcoin wallet companies to create digital formats, specifications, and reference apps that support new ways to protect your digital assets. This discussion happens primarily in the [Airgapped Wallet Community](https://github.com/BlockchainCommons/Airgapped-Wallet-Community/discussions).

## How Are URs Encoded?

As discussed in the [UR specification](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-005-ur.md), binary data is represented with CBOR using a minimal canonical representation, converted to [minimal bytewords](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-012-bytewords.md), and prefaced with the UR type.

Thus the process encoding a UR, which is largely automated by Blockchain Commons libraries, is:

1. Refer to the [Registry of Uniform Resource Types](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-006-urtypes.md) for how to represent the desired data.
2. Refer to the [CBOR RFC](https://tools.ietf.org/html/rfc7049) for how to encode the data. In particular, be aware of how to [use Canonical CBOR](https://tools.ietf.org/html/rfc7049#section-3.9), how to [encode major types](https://tools.ietf.org/html/rfc7049#section-2.1), and how to [encode byte strings](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-005-ur.md#canonical-cbor).
   * The CBOR reference is the _best_ place to read about CBOR encoding, but be aware that whenever you encode something, you will typically preface data with one or more bytes showing data type and length; and as required you may also tag data (which is data type #6).
3. Convert your complete CBOR binary representation to [Bytewords](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-012-bytewords.md) using the minimal encoding. This is the first and last letters of the word, and will be done automatically if you are using the Blockchain Commons [bytewords library](https://github.com/BlockchainCommons/bc-bytewords) and request minimal encoding
4. Prefix your UR with `ur:type/`, or in the case of a part of a sequence `ur:type:sequence/`. Again, this will be done automatically if you use a Blockchain Commons [UR Library](https://github.com/BlockchainCommons/bc-ur).

For example:

* **Seed:** 59F2293A5BCE7D4DE59E71B4207AC5D2
* **CBOR:** A1015059F2293A5BCE7D4DE59E71B4207AC5D2
   * `ur:crypto-seed` is defined as a map which must include the seed and which may include other data such as creation date.
   * `A1`represents a map of length 1.
      * That's major type 5 (for a map), which is represented as `101` in the most significant three bits, plus a length of 1, which is represented as `00001` in the least significant three bits, or overall `0b10100001`, which is `0xA1`.
   * `01` represents item 1 in the map.
   * `50` represents a 16-byte byte-string payload.
      * That's major type 2 (for a byte string), which is represented as `010`, plus a payload of 16 bytes, or `10000`, or overall `0b01010000`, which is `0x50`.
   * `59F2293A5BCE7D4DE59E71B4207AC5D2` represents the byte payload.
* **Bytewords:** obey acid good hawk whiz diet fact help taco kiwi gift view noon jugs quiz crux kiln silk tied help yell jade data
   * `obey` (`0xA1`) through `tied` (`0xd2`) represent the CBOR data, while `help yell jade data` are checksums.
* **Bytewords Minimal:** oyadgdhkwzdtfthptokigtvwnnjsqzcxknsktdhpyljeda
* **UR:** UR:CRYPTO-SEED/OYADGDHKWZDTFTHPTOKIGTVWNNJSQZCXKNSKTDHPYLJEDA

## What Can Be Encoded in URs?

*Any* data can be encoded as URs as long as it has a CBOR encoding and a user-defined UR type. The [Registry of Uniform Resource types](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-006-urtypes.md) lists data types that Blockchain Commons specifies, maintains, and promotes. You can also define proprietary [user-defined types](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-006-urtypes.md#user-defined-types-x-).

To date, the major uses have fallen into two categories:

* **Key Transfer.** URs can be used to encode seeds (`ur:crypto-seed`), HD keys, (`ur:crypto-hdkey`), and SSKR shards (`ur:crypto-sskr`).
* **PSBT Signing.** URs can be used to transfer PSBTs as they are being signed (`ur:crypto-psbt`).

When data is being transferred between airgapped documents, it often is done as part of a request (`ur:crypto-request`) / response (`ur:crypto-response`) interaction, as defined in [BCR-2021-001](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2021-001-request.md).

## What Tools Can I Use to Understand CBOR?

Obviously, the most important tool is the [CBOR reference](https://tools.ietf.org/html/rfc7049).

CBOR has a more human-readable text [diagnostic notation](https://datatracker.ietf.org/doc/html/rfc7049#page-33) you should become familiar with. When you are testing your understanding of how CBOR encoding works or debugging, you can use the [CBOR Playground](http://cbor.me/) to transform CBOR between hex and diagnostic notation, or if you prefer a command-line implementation, the [CBOR-cli](https://www.npmjs.com/package/cbor-cli), which can be installed with `npm` if you have Node.js installed.

Specifications for CBOR structures are written in the [Concise Data Defintion Language (CDDL)](https://datatracker.ietf.org/doc/html/rfc8610).

The [bytewords CLI](https://github.com/BlockchainCommons/bytewords-cli) can also be of use, since in URs, CBOR is converted to bytewords for text encoding.

## More Documents

* [A Guide to Using URs for Key Material](ur-2-keys.md)
* [A Guide to Using URs for SSKR](ur-3-sskrs.md)
* [A Guide to Using URs for PSBTs] (pending)
* [A Guide to Using URs for Request & Response](ur-99-request-response.md)

## Reference Libraries

See the [crypto-commons `bc-ur` entry](https://github.com/BlockchainCommons/crypto-commons#bc-ur) for the most up-to-date listing of reference libraries.

Current implementations of UR include C++, Java, Python, Rust, and Swift.

## UR Implementations

The following implementations demonstrate examples of UR usage:

Project | Publisher | UR Usage | Status
--------|-------------|----------|--------
[AirGap Vault](https://airgap.it/) | Papers | TBD | Live
[BCC Keytool CLI](https://github.com/BlockchainCommons/bc-keytool-cli) | Blockchain&nbsp;Commons | ur:crypto-hdkey<br>ur:crypto-psbt<br>ur:crypto-request<br>ur:crypto-response<br>ur:crypto-seed | Reference
[BCC Seedtool CLI](https://github.com/BlockchainCommons/bc-seedtool-cli) | Blockchain&nbsp;Commons | ur:crypto-seed<br>ur:crypto-sskr | Reference
[BlueWallet](https://bluewallet.io/) | BlueWallet | bc-ur v1 | Live
[Cobo&nbsp;Wallet](https://cobo.com/) | Cobo | bc-ur v1 | Live
[Gordian&nbsp;Cosigner](https://github.com/BlockchainCommons/GordianCosigner-iOS) | Blockchain&nbsp;Commons | ur:crypto-hdkey<br>ur:crypto-psbt<br>ur:crypto-seed | Reference
[Gordian&nbsp;Guardian](https://github.com/BlockchainCommons/GordianGuardian-iOS) | Blockchain&nbsp;Commons | ur:crypto-hdkey<br>ur:crypto-psbt<br>ur:crypto-request<br>ur:crypto-response<br>ur:crypto-sskr | Reference
[Sparrow Wallet](https://sparrowwallet.com/) | Craig Raw | ur:crypto:account<br>ur:crypto-address<br>ur:crypto-hdkey<br>ur:crypto-output<br>ur:crypto-psbt | Live

## Conclusion

URs allow for standardized transfer of data across an airgap, including animated QRs for PSBTs, and URIs or QRs for a variety of other cryptodata. They can make the transfer of some of the most vulnerable cryptodata not just standardized and thus interoperable, but also secure.
