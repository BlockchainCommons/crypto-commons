# `crypto-request` Test Vectors

## `crypto-hdkey` Requests

### Requests for Key Derivations from Any Seed

When deriving a specific HD key from a user-selected seed (tag 501), the body of the `crypto-request` has two elements of note: whether the key is private (1) and what the derivation path is (2).
```
  2: 501({
          1: false, 
          2: 304({
                  1: [84, true, 0, true, 0, true]
                })
        })
```
The above requests a public key from `84'/0'/0'` (the Segwith single-sig derivation).

#### Cosigner (`48'/0'/0'/2'`) Public Key

![](https://github.com/BlockchainCommons/crypto-commons/blob/master/images/vectors/vector-segwit-cosigner-public.png)

_AKA Segwit Multsig Public Key_

```
{
  1: 37(h'36ED0A7280A04AF98C8030F39871B6EA'), 
  2: 501({
          1: false, 
          2: 304({
                  1: [48, true, 0, true, 0, true, 2, true]
                })
        })
}
```
#### Cosigner (`48'/0'/0'/2'`) Private Key

![](https://github.com/BlockchainCommons/crypto-commons/blob/master/images/vectors/vector-segwit-cosigner-private.png)

_AKA Segwit Multsig Private Key_

```
{
  1: 37(h'36ED0A7280A04AF98C8030F39871B6EA'), 
  2: 501({
          1: true, 
          2: 304({
                  1: [48, true, 0, true, 0, true, 2, true]
                })
        })
}
```

#### Master Public Key

![](https://github.com/BlockchainCommons/crypto-commons/blob/master/images/vectors/vector-master-public.png)

```
{
  1: 37(h'36ED0A7280A04AF98C8030F39871B6EA'), 
  2: 501({
          1: false, 
          2: 304({
                  1: []
                })
        })
}
```

#### Master Private Key

![](https://github.com/BlockchainCommons/crypto-commons/blob/master/images/vectors/vector-master-private.png)


```
{
  1: 37(h'36ED0A7280A04AF98C8030F39871B6EA'), 
  2: 501({
          1: true, 
          2: 304({
                  1: []
                })
        })
}
```
#### Segwit Single Sig (`84'/0'/0'`) Public Key

![](https://github.com/BlockchainCommons/crypto-commons/blob/master/images/vectors/vector-segwit-single-public.png)

```
{
  1: 37(h'f684371af9d245589c1f1f888ec7b7a3'), 
  2: 501({
          1: false, 
          2: 304({
                  1: [84, true, 0, true, 0, true]
                })
        })
}
```

#### Segwit Single Sig (`84'/0'/0'`) Private Key

![](https://github.com/BlockchainCommons/crypto-commons/blob/master/images/vectors/vector-segwit-single-private.png)

```
{
  1: 37(h'36ED0A7280A04AF98C8030F39871B6EA'), 
  2: 501({
          1: true, 
          2: 304({
                  1: [84, true, 0, true, 0, true]
                })
        })
}
```

### Requests for Key Derivations from Any Seed with Comment

Adding a comment to a request for a general key derivation simply requires adding a description, which is element 3 of the `crypto-request`. It should be displayed by the recipient, but it should not be used in any response
```
  3: "Watch-only key to create ACME Multisig."
```
The above adds the listed comment to a `crypto-request`.

Reviewing a comment can help a user to determine if a request is clearly legitimate (or clearly fradulent).

#### Cosigner (`48'/0'/0'/2'`) Public Key

![](https://github.com/BlockchainCommons/crypto-commons/blob/master/images/vectors/vector-segwit-cosigner-public-comment.png)

_AKA Segwit Multsig Public Key_

```
{
  1: 37(h'F94ADE8D3843486180CC9B4D37F70724'), 
  2: 501({
          1: false, 
          2: 304({
                  1: [48, true, 0, true, 0, true, 2, true]
                })
        }),
  3: "Watch-only key to create ACME Multisig."
}
```

#### Cosigner (`48'/0'/0'/2'`) Private Key

![](https://github.com/BlockchainCommons/crypto-commons/blob/master/images/vectors/vector-segwit-cosigner-private-comment.png)

_AKA Segwit Multsig Private Key_

```
{
  1: 37(h'03B0CB4C54C143E89E6D137FC56C41D6'), 
  2: 501({
          1: true, 
          2: 304({
                  1: [48, true, 0, true, 0, true, 2, true]
                })
        }),
  3: "Please give over private key for usage in real multisig."
}
```

#### Master Public Key

![](https://github.com/BlockchainCommons/crypto-commons/blob/master/images/vectors/vector-master-public-comment.png)

```
{
  1: 37(h'84D22FD40EA74968993B9BDCF2CC00F3'), 
  2: 501({
          1: false, 
          2: 304({
                  1: []
                })
        }),
  3: "Master public key for watch-only wallet on Sparrow."
}
```

#### Master Private Key

![](https://github.com/BlockchainCommons/crypto-commons/blob/master/images/vectors/vector-master-private-comment.png)


```
{
  1: 37(h'389C3AA302C14088B21D4425B77B6450'), 
  2: 501({
          1: true, 
          2: 304({
                  1: []
                })
        }),
  3: "Transfer master key to Electrum for online usage."
}
```
#### Segwit Single Sig (`84'/0'/0'`) Public Key

![](https://github.com/BlockchainCommons/crypto-commons/blob/master/images/vectors/vector-segwit-single-public-comment.png)

```
{
  1: 37(h'601FDC4EE38841898D6DA3CEF9E855CE'), 
  2: 501({
          1: false, 
          2: 304({
                  1: [84, true, 0, true, 0, true]
                })
        }),
  3: "Creating single-sig watch-only wallet on Sparrow."
}
```

#### Segwit Single Sig (`84'/0'/0'`) Private Key

![](https://github.com/BlockchainCommons/crypto-commons/blob/master/images/vectors/vector-segwit-single-private-comment.png)

```
{
  1: 37(h'5C99BB444C354B659D58BC2299C47032'), 
  2: 501({
          1: true, 
          2: 304({
                  1: [84, true, 0, true, 0, true]
                })
        }),
   3: "We are withholding your arrest for one more day. This is your last chance to prove your identity by sending your private key. Police sherriffs will be on their way otherwise. Do naught delay!"
}
```

## Appendix: Standard Process for Creating Test Vectors:

The following process, which can be used for all test vector creation, using a `crypto-request` of a `crypto-hdkey` as an example.

1. Produce a UUID
```
$ uuidgen | sed s/-//g
BD4CD51356B248D8A04C3609F5A737FA
```
2. Write the JSON vector using [BCR-2021-001](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2021-001-request.md) as reference. Place the UUID in map element #1 and any description in map element #3. Map element #2, the body, will vary based on the type of Request.
```
{
  1: 37(h'f684371af9d245589c1f1f888ec7b7a3'), 
  2: 501({
          1: false, 
          2: 304({
                  1: [84, true, 0, true, 0, true]
                })
        })
}
```
3. Encode the JSON with [CBOR Playground](https://cbor.me/). First test it with full description, then check "plain text" to just produce the hex.
```
A201D82550F684371AF9D245589C1F1F888EC7B7A302D901F5A201F402D90130A101861854F500F500F5
```
4. Use `bytewords` with `hex` input and `minimal` output to produce the UR body.
```
bytewords -i hex -o minimal A201D82550F684371AF9D245589C1F1F888EC7B7A302D901F5A201F402D90130A101861854F500F500F5
oeadtpdagdynlremcyyttdfehdnsctctlomnstrlotaotaadykoeadwkaotaaddyoyadlncsghykaeykaeykaeuolywf
```
5. Add `ur:crypto-request/` as a prefix.
```
ur:crypto-request/oeadtpdagdynlremcyyttdfehdnsctctlomnstrlotaotaadykoeadwkaotaaddyoyadlncsghykaeykaeykaeuolywf
```
6. Encode the `crypto-request` as a QR.
```
echo "ur:crypto-request/oeadtpdagdynlremcyyttdfehdnsctctlomnstrlotaotaadykoeadwkaotaaddyoyadlncsghykaeykaeykaeuolywf" | qrencode -o ~/vector-segwit-single-pubkey.png
```

## `crypto-psbt` Requests

To test a PSBT:

1. [Add Alice seed](https://github.com/BlockchainCommons/GordianSeedTool-iOS/blob/master/Testing/PSBT%20Signing%20Request/Alice.pdf)
2. [Add Bob seed](https://github.com/BlockchainCommons/GordianSeedTool-iOS/blob/master/Testing/PSBT%20Signing%20Request/Bob.pdf)
3. [Test Alice signing](https://raw.githubusercontent.com/BlockchainCommons/GordianSeedTool-iOS/master/Testing/PSBT%20Signing%20Request/PSBT%20Signing%20Request%201%20of%202.png)
4. [Test Both signing](https://raw.githubusercontent.com/BlockchainCommons/GordianSeedTool-iOS/master/Testing/PSBT%20Signing%20Request/PSBT%20Signing%20Request%201%20of%202.png)

## TODO

2. Six (or twelve?) crypto-requests for hdkey from specific seed
3. Import and Export Yimn Blue
4. Import and Export Khaki
5. PSBT Test

