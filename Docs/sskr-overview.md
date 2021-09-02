# SSKR Docs

SSKR stands for Sharded Secret Key Reconstruction. It's a specification that allows you to securely create a backup of your cryptoseeds by sharding those secrets. It uses the mature Shamir’s Secret Sharing functionality, but with more choices of output and options for advanced two-tiered shards.

Users can use SSKR to easily shard a seed. Our reference tools for iOS, macOS, and UNIX demo the functionality, but we expect more cryptocurrency wallet manufacturers to soon be incorporating SSKRs as well.

Seedtool, our iOS and macOS reference tool, allows you to print your sares and distribute them as coupons, which include QRs of the shares that can be stored in a QR vault. If you run the Mac version of Seedtool, you can instead print them directly to a PDF!

But you can also secure shares in other ways, such as etching the words into steel to ensure you never lose your cryptocurrency seed. We have a demo on how to do it with steel dog tags!

There are other advantages as well, including BIP-39 roundtripping and the usage of words that are less-likely to be confused. Take a look, we talk about it all in our docs!

Developers of all sorts should find it easy to incorporate the functionality, thanks to libraries available in multiple programming languages, plus a large collection of documents.

If you’d like to see more #SmartCustody work to support responsible key management, including more specifications and references for creating wallet interoperability. Support Blockchain Commons by [becoming a patron](https://github.com/sponsors/BlockchainCommons)!

## Intro

The following documents overview SSKR.

* [SSKR for Users](https://github.com/BlockchainCommons/crypto-commons/blob/master/Docs/sskr-users.md)
* [Early Demo Video](https://github.com/BlockchainCommons/crypto-commons/blob/master/Docs/sskr-video.md)

## For Users

How can you use SSKR? The following documents describe its usage in [Gordian Seed Tool](https://apps.apple.com/us/app/gordian-seed-tool/id1545088229).

* [Sharding a Seed (from Gordian Seed Tool Manual)](https://github.com/BlockchainCommons/GordianSeedTool-iOS/blob/master/Docs/MANUAL.md#sharding-a-seed)
* [Importing SSKR Shards (from Gordian Seed Tool Manual)](https://github.com/BlockchainCommons/GordianSeedTool-iOS/blob/master/Docs/MANUAL.md#importing-sskr-shares)

<div align="center">
  <table border=0>
    <tr>
      <td>
        <a href="https://raw.githubusercontent.com/BlockchainCommons/GordianSeedTool-iOS/master/images/st-export-1.jpeg"><img src="https://raw.githubusercontent.com/BlockchainCommons/GordianSeedTool-iOS/master/images/st-sskr-export-1.jpeg" width=250></a> 
        <br><div align="center"><b>SSKR Export</b></div>
      </center></td>
      <td>
        <a href="https://raw.githubusercontent.com/BlockchainCommons/GordianSeedTool-iOS/master/images/st-sskr-expor-3.jpeg"><img src="https://raw.githubusercontent.com/BlockchainCommons/GordianSeedTool-iOS/master/images/st-sskr-expor-3.jpeg" width=250></a> 
        <br><div align="center"><b>SSKR Coupons</b></div>
      </center></td>
      <td>     
        <a href="https://raw.githubusercontent.com/BlockchainCommons/GordianSeedTool-iOS/master/images/st-sskr-import.jpeg"><img src="https://raw.githubusercontent.com/BlockchainCommons/GordianSeedTool-iOS/master/images/st-sskr-import.jpeg" width=250></a> 
        <br><div align="center"><b>SSKR Import</b></div>
      </center></td>
    </tr>
  </table>
</div>

## For Power Users

* [Designing SSKR Share Scenarios](https://github.com/BlockchainCommons/SmartCustody/blob/master/Docs/SSKR-Sharing.md)
* [SSKR Dangers](https://github.com/BlockchainCommons/SmartCustody/blob/master/Docs/SSKR-Dangers.md)
* [SSKR from Command Line (from SeedTool-CLI manua)](https://github.com/BlockchainCommons/seedtool-cli/blob/master/Docs/MANUAL.md#sskrs)
* [SSKR Cold Storage Example](https://github.com/BlockchainCommons/crypto-commons/blob/master/Docs/sskr-cold-storage.md)

## For Developers

* [SSKR for Developers](https://github.com/BlockchainCommons/crypto-commons/blob/master/Docs/sskr-developers.md)
* [Guide for Using URs for SSKR](https://github.com/BlockchainCommons/crypto-commons/blob/master/Docs/ur-3-sskrs.md)
* [UR Type Definition for Sharded Secret Key Reconstruction (SSKR)](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-011-sskr.md)
* [SSKR Test Vectors](https://github.com/BlockchainCommons/crypto-commons/blob/master/Docs/sskr-test-vector.md)
* [Shamir’s Secret Sharing: An Overview](https://docs.google.com/document/d/1rZJlFZcftrCM_KaxFnHUIskJKlSQzF0zFn4WIRQGDLU/edit#heading=h.imy5xgr88lxa)

* [Security Review of bc-shamir & bc-sskr libraries](https://github.com/BlockchainCommons/bc-shamir/blob/master/SECURITY-REVIEW.md)

## Code

* [bc-shamir - Shamir Secret Sharing reference library in C](https://github.com/BlockchainCommons/bc-shamir)
* [bc-sskr - Sharded Secret Key Reconstruction (SSKR) reference library in C](https://github.com/BlockchainCommons/bc-shamir)

### Reference Tools

* [seedtool-cli - Cryptographic Seed Tool for the command line](https://github.com/BlockchainCommons/seedtool-cli)
* [Gordian Seed Tool iOS - Cryptographic Seed Manager for iOS & Mac](https://github.com/BlockchainCommons/GordianSeedTool-iOS)

## Related

* [Creating an Autonomous Multisig from Building Blocks (from Designing Multisig for Independence & Resilience)](https://github.com/BlockchainCommons/SmartCustody/blob/master/Docs/Multisig.md#alternative-creating-an-autonomous-multisig-from-building-blocks)
* [RWOT9 - Evaluating Social Recover](https://github.com/WebOfTrustInfo/rwot8-barcelona/blob/master/final-documents/evaluating-social-recovery.md)
