# `crypto-request` Test Vectors

## Standard Process for Creating Test Vectors:

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

## `crypto-hdkey` Requests

### Requests for Key Derivations from Any Seed

When deriving a specific key from a user-selected seed (tag 501), the body of the `crypto-request` has two elements of note: whether the key is private (1) and what the derivation path is (2).
```
  2: 501({
          1: false, 
          2: 304({
                  1: [84, true, 0, true, 0, true]
                })
        })
```
The above requests a public key from `84'/0'/0'` (the Segwith single-sig derivation).

### Segwit Single Sig (`84'/0'/0'`) Public Key

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

### Segwit Single Sig (`84'/0'/0'`) Private Key

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

### Process for Creating Test Vectors for Arbitrary Key Derivations

Creating a test vector for an arbitrary key derivation follows the standard process for creating `crypto-requests`

1. 
