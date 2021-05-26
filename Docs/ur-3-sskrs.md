# A Guide to Using URs for SSKRs

Uniform Resources (URs) allow for the encoding of a variety of information, including a variety of crypto-data. This document describes how they are used to encode [SSKRs](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-011-sskr.md), or Sharded Secret Key Reconstruction shares. 

As usual, this will typically be done for you automatically using Blockchain Commons' [libraries](https://github.com/BlockchainCommons/crypto-commons#bc-sskr), but what follows is an explanation of how everything works.

## Why Use URs for SSKRs?

URs are generally a boon because they both improve interoperability and type their contents. As a result, whenever you look at a UR you can see exactly what it contains, and you can easily use that data on a variety of systems.

URs can be particularly useful for SSKRs because of their tight integration with QR Codes. URs were built to work with QRs, and many applications that read in SSKR URs are likely to allow the option of using a camera to capture a QR. This means that instead of solely storing an SSKR share as words, you can also preserve them as a QR in an application like [UR Vault](https://github.com/BlockchainCommons/URVault-iOS). This can be a  gamechanger for the reliability and resilience of private keys because friends and family can easily store a variety of SSKR shares for a variety of different people and instanteously and reliably retrieve them as needed.

## SSKRs: `crypto-sskr`

The following examples use the [standard SSKR test vector](sskr-test-vector.md):

![](../images/sskr-seed.png)

### Translating from Seed to SSKRs

When running SSKR on a seed, it shards to secret to generates a number of shares. This creation of shares will be fully taken care of by your library of choice and is beyond the scope of this document.

For example the following seed:
```
59f2293a5bce7d4de59e71b4207ac5d2
```
Can produce the following shares, which constitute a single group of three members with a threshold of two: any two shares can reconstruct the seed.
```
754b000100a8be4da2e6cf65a05424887888ae855c
754b000101016fd11b9ed35e42bc08c12b47c6c476
754b000102e1076ecb16f7137f9f7c1ade0d7e0708
```
### Understanding an SSKR Share

As described in the [crypto-sskr CDDL](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-011-sskr.md#cddl), the first five bytes of an SSKR share contain an identifier and information about the groups, members, and thresholds that define the SSKR.

The general format is:

* identifier (16 bits)
* group-threshold - 1 (4 bits)
   * How many groups are required to retrieve the secret?
* group-count - 1 (4 bits)
   * How many groups are there total?
* group-index (4 bits)
   * What group is this share from?
* member-threshold - 1 (4 bits)
   * How many members are required to retrieve the secret in this group?
* RESERVED (4 bits)
   * Must be zero. In lieu of member-count.
* member-index (4 bits)
   * What member in this group is this share from?
* secret-share (same number of bits as secret)

The above shares can thus be read as follows:

ID | group | member | secret share
---|---|---|---
754b | 000 | 100 | a8be4da2e6cf65a05424887888ae855c
754b | 000 | 101 | 016fd11b9ed35e42bc08c12b47c6c476
754b | 000 | 102 | e1076ecb16f7137f9f7c1ade0d7e0708

The first share thus reveals:

* **identifier:** `754b`
* **Group Threshold:** 0 (+ 1 = 1), just one group needed
* **Group Count:** 0 (+ 1 = 1), just one group total
* **Group Index:** 0, the 0th group
* **Member Threshold:** 1 (+ 1 = 2), two members needed
* **RESERVED:** 0
* **Member Index:** 0, the 0th member
* **Secret Share:** `a8be4da2e6cf65a05424887888ae855c`

### Translating an SSKR Share to UR

Translating an SSKR to a `crypto-sskr` UR is trivial. All it requires  is encoding the hex of the share as CBOR, then translating it to minimal bytewords and prefixing it with `crypto-sskr` as described in the [UR Overview](ur-1-overview.md#how-are-urs-encoded).

To start with, shares are represented as hex:
```
h'754b000100a8be4da2e6cf65a05424887888ae855c'
h'754b000101016fd11b9ed35e42bc08c12b47c6c476'
h'754b000102e1076ecb16f7137f9f7c1ade0d7e0708'
```
Using the [CBOR playground](http://cbor.me/), they translate as follows:
```
55                                      # bytes(21)
   754B000100A8BE4DA2E6CF65A05424887888AE855C 
55                                      # bytes(21)
   754b000101016fd11b9ed35e42bc08c12b47c6c476
55                                      # bytes(21)
   754b000102e1076ecb16f7137f9f7c1ade0d7e0708
```
Or more concisely:
```
55754b000100a8be4da2e6cf65a05424887888ae855c
55754b000101016fd11b9ed35e42bc08c12b47c6c476
55754b000102e1076ecb16f7137f9f7c1ade0d7e0708
```
Which is to say: the CBOR encoding is just the share with a length and type prefixing it, here `55`.

This translates to the following URs:
```
ur:crypto-sskr/gokpgraeadaepdrngtoevatkihnbghdklokslopllphhhgspeybg
ur:crypto-sskr/gokpgraeadadadjlttcwnntehyfwrfaysednflswsskoltambsin
ur:crypto-sskr/gokpgraeadaovyatjtsbcmylbwlbnekecyuebtkbataywtmymuwl
```

## The Difference between SSKR Bytewords and SSKR URs

[SSKR Bytewords](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-011-sskr.md#encoding-as-standard-bytewords) are one way to represent an SSKR share, so that the share can be written down, etched in steel, or otherwise stored. After encoding as CBOR, with tagging, the share is then translated into normal bytewords.

[SSKR URs](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-011-sskr.md#encoding-as-ur) are another way to represent an SSKR share, so that it can be transmitted between interoperable devices or even stored as a QR. After encoding as CBOR, without tagging, the share is then translated to minimal bytewords (and prepended with a `ur:crypto-sskr` prefix).

Because these two storage methods both use bytewords, they can look very similar, but there are subtle differences between the two. 

* **Typing.**
   * SSKR bytewords is typed by tagging the hex of the share with `309`.
   * SSKR UR is typed by prefixing the minimal bytewords with `ur:crypto-sskr`.
   * This results in the bytewords having three extra words at the start: `tuna acid epic`, which represents the `309` tag in CBOR.
   * Either way you *know* what you're getting because of the typing: `309` in CBOR for SSKR bytewords and `ur:crypto-sskr` in a prefix for UR Bytewords.
* **Encoding.**
   * SSKR bytewords typically uses regular bytewords encoding for clarity.
   * SSKR UR uses minimal bytewords encoding for efficiency.
* **Checksum.** 
   * Because SSKR bytewords have an extra tag at the start, their checksum will be different from UR bytewords, which means that the last four words are different.

As an example the first UR encoding was:
```
ur:crypto-sskr/gokpgraeadaepdrngtoevatkihnbghdklokslopllphhhgspeybg
```
Expanding those words would give you a `ur:crypto-sskr` with:
```
ur:crypto-sskr/
gyro keep gear able acid able paid ruin gift oboe visa 
task inch numb gush dark logo keys logo pool limp high 
hang soap easy brag
```
(This isn't how a UR is typically displayed, but it's shown here without minimal bytewords here solely for easy comparison.)

To encode that same SSKR share as plain bytewords would require the following:
```
309(
   h'754b000100a8be4da2e6cf65a05424887888ae855c'
)
```
Which encodes as:
```
D9 0135                                 # tag(309)
   55                                   # bytes(21)
      754B000100A8BE4DA2E6CF65A05424887888AE855C
```
Or:
```
D9013555754B000100A8BE4DA2E6CF65A05424887888AE855C
```
This would produce the Bytewords:
```
tuna acid epic 
gyro keep gear able acid able paid ruin gift oboe visa 
task inch numb gush dark logo keys logo pool limp high 
soap cyan owls gush
```
Comparing the two verifies that the share (`gyro keep gear able acid able paid ruin gift oboe visa task inch numb gush dark logo keys logo pool limp high` or `gokpgraeadaepdrngtoevatkihnbghdklokslopllphh`) is identical in both cases, by the plain bytewords has three additional opening words (`tuna acid epic ` or tag `309`) and the four checksum words at the end vary. This is all exactly as expected.

## Testing SSKR URs with Blockchain Commons' Reference Tools

[Gordian Guardian](https://github.com/BlockchainCommons/GordianGuardian-iOS) will export seeds as either SSKR URs or SSKR Bytewords, allowing easy checking among all the formats.

The Blockchain Commons [Seedtool] and [Bytewords] CLIs may also be used, in conjunction with [cbor2diag].

A seed can be input into `seedtool:`
```
$ seed=59f2293a5bce7d4de59e71b4207ac5d2
$ seedtool -i hex $seed
59f2293a5bce7d4de59e71b4207ac5d2
```
That seed can in turn be used to generate SSKR Bytewords:
```
$ seedtool -i hex $seed -o sskr --group=2-of-3
tuna acid epic gyro cola dark able acid able math blue belt blue glow item gush yank vial hope view fish soap play brew unit idle puff jump rock
tuna acid epic gyro cola dark able acid acid pose frog taxi inch vibe epic arch very play lava surf kick frog pose flux iron wave unit void help
tuna acid epic gyro cola dark able acid also waxy roof plus zaps also tiny yawn unit junk zaps real quad task omit quad pool fuel exit lamb tuna
```
`bytewords` can convert SSKR Bytewords to SSKR Minimal Bytewords:
```
$ bytewords -i standard -o minimal
tuna acid epic gyro cola dark able acid able math blue belt blue glow item gush yank vial hope view fish soap play brew unit idle puff jump rock
taadecgocadkaeadaemhbebtbegwimghykvlhevwfhsppybwutiepfjprk
```
Note that this is _not_ the same thing as an SSKR UR, because it contains that `309` tag (`tuna acid epic` or `taadec`) and a different checksum (`idle puff jump rock` or `iepfjprk`).

In fact, none of the command-line tools currently output SSKR URs, but if you import one from somewhere else, such Gordian Guardian, you can convert it to CBOR using `bytewords` and then examine it using `cbor2diag`.

For:
```
ur:crypto-sskr/gokpgraeadaepdrngtoevatkihnbghdklokslopllphhhgspeybg
```
You can:
```
$ bytewords -i minimal gokpgraeadaepdrngtoevatkihnbghdklokslopllphhhgspeybg -o hex
55754b000100a8be4da2e6cf65a05424887888ae855c
$ cbor2diag -x 55754b000100a8be4da2e6cf65a05424887888ae855c
h'754b000100a8be4da2e6cf65a05424887888ae855c'
```

## Integrating SSKR URs Into Your Code

Blockchain Commons provides an [SSKR library in C](https://github.com/blockchaincommons/bc-sskr) that translates SSKRs into either Bytewords or URs. It builds on [bc-crypto-base](https://github.com/blockchaincommons/bc-crypto-base), [bc-shamir](https://github.com/blockchaincommons/bc-shamir), and [bc-bytewords](https://github.com/blockchaincommons/bc-bytewords). Translations are also available to other languages such as [Java and Swift](https://github.com/BlockchainCommons/crypto-commons#bc-sskr).

## Conclusion

SSKRs provide a means to shard a secret and then distribute those shares to multiple people. Encoding an SSKR as a UR is entirely trivial, just requiring a simple CBOR encoding followed by the typical minimal Bytewords conversion. The results can be ground-breaking, especially in the ability to reliably and interoperably store your shares as QR codes.
