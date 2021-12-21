# UR Overview

UR stands for Uniform Resources, a method for encoding structured binary data in plain-text strings that are also well-formed URIs. It's an interoperability specification that allows for the reliable, typed transfer of data and was designed in particular to allow for reliable transmission of crypto-seeds, crypto-keys, PSBTs, and other data related to cryptocurrency.

One of the particular advantages of UR is careful integration with QR codes, a prime method for transmitting data across airgaps. URs are built to be efficient when encoded as QRs. In addition, multi-part URs allow for the creation of animated QRs, overall containing more information than any single QR could have.

Typed data, reliable interoperation, QR optimization, and animated QRs are the main reasons to use the UR specification.

## Intro

The following provides broad overviews of UR:

* [UR High Level Overview](https://www.blockchaincommons.com/projects/Blockchain-Commons-URs-Support-Airgapped-PSBTs/)
* [UR Technology Introduction](https://github.com/BlockchainCommons/crypto-commons/blob/master/Docs/ur-1-overview.md)

These videos offer overviews in a different format:

* [URs in Technology Overview Video](https://www.youtube.com/watch?v=RYgOFSdUqWY&t=1198s)
* [Multi-part URs in Technology Overview Video](https://www.youtube.com/watch?v=RYgOFSdUqWY&t=1373s)
* [UR Types in Technology Overview Video](https://www.youtube.com/watch?v=RYgOFSdUqWY&t=1464s)

## For Users

As a user, you might note applications using URs of the format "ur:type/bytewords" (or a QR encoding that UR). These allow for the free movement of data among apps that support the UR specification. This will be mostly automated, typically requiring you to show a QR from one app to another.

Example UR:
```
ur:crypto-seed/oyadgdhkwzdtfthptokigtvwnnjsqzcxknsktdhpyljeda
```

<div align="center">
  <table border=0>
    <tr>
      <td>
        <a href="https://github.com/BlockchainCommons/GordianQRTool-iOS/blob/master/images/qr-seed.jpeg"><img src="https://github.com/BlockchainCommons/GordianQRTool-iOS/blob/master/images/qr-seed.jpeg" width=250></a> 
        <br><div align="center"><b>QR Tool Recognition</b></div>
      </center></td>
      <td>
        <a href="https://github.com/BlockchainCommons/GordianSeedTool-iOS/blob/master/images/st-export.jpeg"><img src="https://github.com/BlockchainCommons/GordianSeedTool-iOS/blob/master/images/st-export.jpeg" width=250></a> 
        <br><div align="center"><b>Seed Tool Exports</b></div>
      </center></td>
      <td>     
        <a href="https://github.com/BlockchainCommons/GordianSeedTool-iOS/blob/master/images/st-sskr-expor-3.jpeg"><img src="https://github.com/BlockchainCommons/GordianSeedTool-iOS/blob/master/images/st-sskr-expor-3.jpeg" width=250></a> 
        <br><div align="center"><b>Seed Tool SSKR</b></div>
      </center></td>
    </tr>
  </table>
</div>
The following iOS reference applications support the use of URs:

* [Gordian QR Tool](https://apps.apple.com/us/app/gordian-qr-tool/id1506851070) — recognizes UR types
* [Gordian Seed Tool](https://apps.apple.com/us/app/gordian-seed-tool/id1545088229) — imports and exports URs

## For Developers

The following are accessible guides to using URs in your programs:

* [URs: An Introduction](https://github.com/BlockchainCommons/crypto-commons/blob/master/Docs/ur-1-overview.md)
* [A Guide to URs for Key Material](https://github.com/BlockchainCommons/crypto-commons/blob/master/Docs/ur-2-keys.md)
* [A Guide to URs for SSKRs](https://github.com/BlockchainCommons/crypto-commons/blob/master/Docs/ur-3-sskrs.md)
* [A Guide to UR Request & Response](https://github.com/BlockchainCommons/crypto-commons/blob/master/Docs/ur-99-request-response.md)
* [crypto-request and crypto-response vs Signing via crypto-psbt](crypto-request-or-crypto-psbt.md)

They are based on the following, original definitional research papers:

* [BCR-2020-005: Uniform Resources (UR): Encoding Structured Binary Data for Transport in URIs and QR Codes](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-005-ur.md)
* [BCR-2020-006:	Registry of Uniform Resource (UR) Types](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-006-urtypes.md)
* [BCR-2020-007: UR Type Definition for Hierarchical Deterministic (HD)](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-007-hdkey.md)
* [BCR-2020-008: UR Type Definition for Elliptic Curve (EC) Keys](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-008-eckey.md)
* [BCR-2020-009: UR Type Definition for Cryptocurrency Addresses](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-009-address.md)
* [BCR-2020-010: UR Type Definition for Bitcoin Output Descriptors](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-010-output-desc.md)
* [BCR-2020-011: UR Type Definition for Sharded Secret Key Reconstruction (SSKR)](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-011-sskr.md)
* [BCR-2020-014: URs on E-paper display](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-014-urs-on-epaper.md)
* [BCR-2020-015: UR Type Definition for BIP44 Accounts](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-015-account.md)
* [BCR-2021-001: UR Type Definitions for Transactions Between Airgapped Devices](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2021-001-request.md)

## Code

The following Blockchain Commons libraries support the usage of URs:

* [bc-ur](https://github.com/BlockchainCommons/bc-ur) — C++ reference library
* [bc-ur-java](https://github.com/BlockchainCommons/bc-ur-java) — Java reference library
* [URKit](https://github.com/BlockchainCommons/URKit) and [URUI](https://github.com/BlockchainCommons/URUI) — Swift libraries for usage and display of URs.

The following third-party libraries support URs in a variety of languages:

* [Hummingbird](https://github.com/sparrowwallet/hummingbird) — Another Java library
* [foundation-ur-py](https://github.com/Foundation-Devices/foundation-ur-py) — Python library
* [ur-rs](https://github.com/dspicher/ur-rs) — Rust library

### Reference Tools

Want to verify your code? That's what the Blockchain Commons reference tools are for.

* [seedtool-cli - Cryptographic Seed Tool for the command line](https://github.com/BlockchainCommons/seedtool-cli)
* [Gordian Seed Tool iOS - Cryptographic Seed Manager for iOS & Mac](https://github.com/BlockchainCommons/GordianSeedTool-iOS)

## Support

To support the continued creation and growth of specifications such as this, please become a sponsor of Blockchain Commons, either through [GitHub](https://github.com/sponsors/BlockchainCommons) or through Bitcoin donations on our [BTCpay](https://btcpay.blockchaincommons.com/). Thank you to our [sustaining and additional sponsors](https://www.blockchaincommons.com/sponsors.html).

Please also join us in our [Airgapped Wallet Community](https://github.com/BlockchainCommons/Airgapped-Wallet-Community/discussions) where we are discussing and advancing this and other specifications.
