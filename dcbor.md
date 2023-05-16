# dCBOR

dCBOR is deterministic CBOR, a optional variant of CBOR described in [RFC 8949](https://www.rfc-editor.org/rfc/rfc8949.html#name-deterministically-encoded-c).

A deterministic version of CBOR is critical when an application requires the same data to always be encoded in the same way. This is true for [Gordian Envelope](https://www.blockchaincommons.com/introduction/Envelope-Intro/), which uses CBOR to arrange data that is identified by hashes. The hashes only remain the same if the same data is always encoded in the exact same way, hence the need for determinism.

Though RFC 8949 includes some requirements for dCBOR, it leaves other options up to encoder developers. This results in dCBOR usage that is not necessarily consistent across multiple encoders. As a result, Blockchain Commons has produced an [Internet-Draft](https://www.ietf.org/id/draft-mcnally-deterministic-cbor-00.html) to fully codify dCBOR practices.

We have also released libraries for dCBOR in Rust and Swift as well as a command line application for testing encoding and decoding that all follow the specifications laid out in this Draft.

## dCBOR Videos

<table width="100%">
  <td>
    <td width="50%">

      <b>Why CBOR?</b>

      <a href="https://www.youtube.com/watch?v=uoD5_Vr6qzw"><img src="https://i.ytimg.com/vi/uoD5_Vr6qzw/hqdefault.jpg"></a>

    </td>
    <td width="50%">
  
      <b>dCBOR Library from Blockchain Commons</>

      <a href="https://www.youtube.com/watch?v=NlJE8oF1B5M"><img src="https://i.ytimg.com/vi/NlJE8oF1B5M/hqdefault.jpg"></a>

    </td>
  </tr>
</table>


## Developer Libraries & Applications

* **bc-dcbor-rust Library** - https://github.com/BlockchainCommons/bc-dcbor-rust
* **BCSwiftDCBOR Library** - https://github.com/BlockchainCommons/BCSwiftDCBOR
* **dcbor-cli Parser/Validator** - https://github.com/BlockchainCommons/dcbor-cli
