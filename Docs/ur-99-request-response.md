# A Guide to Using UR Request & Response

Most URs allow for the simple and structured encoding of a specific sort of data, which for Blockchain Commons URs often means a specific sort of crypto-data. However, in 2021, Blockchain Commons introduced a pair of new URs, `crypto-request` and `crypto-response`, which together create a back-and-forth communication, usually between two airgapped devices. Currently, three types of data can be retrieved via this method: a `crypto-seed`, a `crypto-hdkey`, and a `crypto-psbt`. We are working with our developer community to determine what other data might be helpful for request/response communication.

The full description of the Request and Response URs appears in [BCR-2021-001: UR Type Definitions for Transactions Between Airgapped Devices](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2021-001-request.md). What follows is summary and examples, using tools such as [cbor2diag](https://www.npmjs.com/package/cbor-cli?activeTab=readme) and [uuidgen](https://man7.org/linux/man-pages/man1/uuidgen.1.html) as well as Blockchain Commons' own [bytewords](https://github.com/BlockchainCommons/bytewords-cli), [keytool](https://github.com/BlockchainCommons/keytool-cli) and [seedtool](https://github.com/BlockchainCommons/seedtool-cli) CLIs. They're meant to exemplify the construction and deconstruction of each type of request and response.

## Request & Response

The standard `crypto-request` is a CBOR map that contains two to three elements:

1. A [UUID](https://en.wikipedia.org/wiki/Universally_unique_identifier), tagged `37`.
2. A body, which contains a tag for the information being sought and sufficient identifying information.
3. (optional) A description that is sent to the user who will validate the request.


In return, the recipient does _not_ send a `crypto-seed`, `crypto-hdkey`, or `crypto-psbt`, but instead something formatted and tagged as a `crypto-response`, with the requested type of UR found within the body.

The standard `crypto-response` is thus a CBOR map that contains two elements:

1. A matching UUID, tagged `37`
2. The requested data, tagged with the information type being sent.

### The UUID

UUIDs are a standard format that can be generated with programmatic libraries or command-line tools:
```
$ uuidgen
51D2B771-E4D5-4E46-A9E5-644E9ADD0458
```
The use of hyphens in UUIDs is for display purposes only. They would not be included in the actual binary bytes you'd send as part of a `crypto-request`:
```
$ uuidgen | sed s/-//g
51D2B771E4D54E46A9E5644E9ADD0458
```

## Why Use URs for Request and Response?

Standard URs require users to possess fundamental knowledge of cryptocurrency systems. They need to know what seeds and keys and PSBTs are and they need to know when and how to transfer them between devices. Though some users may enjoy that high level of agency, for others, accessibility is damaged, even when careful instructions are provided.

The request and response URs not only improve accessibility, but also take wallets up to the next level of automation. An app can now recognize that it needs a key, a seed, or a PSBT, and it can request that information from another device. Rather than explicitly having to find and transmit what's desired, the user now simply has to acknowledge and validate its usage. (Maintaining a high-level of user involvement, even in a somewhat more automated system, is a necessity.)

This is also a stepping stone. All protocols start with a handshake, and request and response could be used as a foundation for more complex crypto-interactions that require two or even three rounds of back and forth, or even to set up a secure channel for more extensive communications.

## Request & Response: `crypto-seed`

### The Seed Request

To request a `crypto-seed`, a `crypto-request` must make a request for tag `500` and must include a `crypto-seed-digest` of the desired seed, per the [crypto-request CDDL](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2021-001-request.md#cddl-for-request). 

The `crypto-seed-digest` is a SHA-256 hash of the bytes that make up the seed, which must be tagged `600`, per the [Seed Digest Source Specification](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-006-urtypes.md#seed-digest-source-specification). For example, the digest for `c7098580125e2ab0981253468b2dbc52` would be `e824467caffeaf3bbc3e0ca095e660a9bad80ddb6a919433a37161908b9a3986`:
```
$ echo 'c7098580125e2ab0981253468b2dbc52' | xxd -r -p | shasum -a 256
e824467caffeaf3bbc3e0ca095e660a9bad80ddb6a919433a37161908b9a3986  -
```
We could request that seed by combining the digest with the UUID `020C223A86F7464693FC650EF3CAC047` resulting in the following maps:
```
{
  1: 37(h'020C223A86F7464693FC650EF3CAC047'), 
  2: 500({
    1: 600(h'e824467caffeaf3bbc3e0ca095e660a9bad80ddb6a919433a37161908b9a3986')
  })
}
```
Which can be encoded as follows using the [CBOR Playground](http://cbor.me/):
```
A2                                      # map(2)
   01                                   # unsigned(1)
   D8 25                                # tag(37)
      50                                # bytes(16)
         020C223A86F7464693FC650EF3CAC047 # UUID
   02                                   # unsigned(2)
   D9 01F4                              # tag(500)
      A1                                # map(1)
         01                             # unsigned(1)
         D9 0258                        # tag(600)
            58 20                       # bytes(32)
               E824467CAFFEAF3BBC3E0CA095E660A9BAD80DDB6A919433A37161908B9A3986 
                                        # seed-digest
```
`cbor2diag` confirms that encoding:
```
$ cbor2diag -x A201D82550020C223A86F7464693FC650EF3CAC04702D901F4A101D902585820E824467CAFFEAF3BBC3E0CA095E660A9BAD80DDB6A919433A37161908B9A3986
{1: 37(h'020c223a86f7464693fc650ef3cac047'), 2: 500({1: 600(h'e824467caffeaf3bbc3e0ca095e660a9bad80ddb6a919433a37161908b9a3986')})}
```
As usual, this can then be converted to minimal bytewords:
```
$ bytewords -i hex -o minimal A201D82550020C223A86F7464693FC650EF3CAC04702D901F4A101D902585820E824467CAFFEAF3BBC3E0CA095E660A9BAD80DDB6A919433A37161908B9A3986
oeadtpdagdaobncpftlnylfgfgmuztihbawfsgrtflaotaadwkoyadtaaohdhdcxvsdkfgkepezepefrrffmbnnbmdvahnptrdtpbtuyimmemweootjshsmhlunyeslnameyhsdi
```
And [then a UR](https://github.com/BlockchainCommons/crypto-commons/blob/master/Docs/ur-1-overview.md#how-are-urs-encoded):
```
ur:crypto-request/oeadtpdagdaobncpftlnylfgfgmuztihbawfsgrtflaotaadwkoyadtaaohdhdcxvsdkfgkepezepefrrffmbnnbmdvahnptrdtpbtuyimmemweootjshsmhlunyeslnameyhsdi
```

### The Seed Request with Description

Here's a slightly alternative request that includes a description:
```
{
  1: 37(h'020C223A86F7464693FC650EF3CAC047'), 
  2: 500({
    1: 600(h'e824467caffeaf3bbc3e0ca095e660a9bad80ddb6a919433a37161908b9a3986')
  }),
  3: "Seed for business account"
}
```
The receipient of the `crypto-request` _should_ see the note "Seed for business account" before they agree to send the `crypto-response in return.

This encodes as:
```
A3                                      # map(3)
   01                                   # unsigned(1)
   D8 25                                # tag(37)
      50                                # bytes(16)
         020C223A86F7464693FC650EF3CAC047 # UUID
   02                                   # unsigned(2)
   D9 01F4                              # tag(500)
      A1                                # map(1)
         01                             # unsigned(1)
         D9 0258                        # tag(600)
            58 20                       # bytes(32)
               E824467CAFFEAF3BBC3E0CA095E660A9BAD80DDB6A919433A37161908B9A3986
                                        # seed-digest
   03                                   # unsigned(3)
   78 19                                # text(25)
      5365656420666F7220627573696E657373206163636F756E74 # "Seed for business account"
```
Or concisely:
```
A301D82550020C223A86F7464693FC650EF3CAC04702D901F4A101D902585820E824467CAFFEAF3BBC3E0CA095E660A9BAD80DDB6A919433A37161908B9A39860378195365656420666F7220627573696E657373206163636F756E74
```
Or as a request:
```
ur:crypto-request/otadtpdagdaobncpftlnylfgfgmuztihbawfsgrtflaotaadwkoyadtaaohdhdcxvsdkfgkepezepefrrffmbnnbmdvahnptrdtpbtuyimmemweootjshsmhlunyeslnaxkscfguihihiecxiyjljpcxidkpjkinjtihjkjkcxhsiaiajlkpjtjyftpyhhbk
```

### The Seed Response

The `crypto-response` to a request for a `crypto-seed` simply includes a `300` tagged [seed](https://github.com/BlockchainCommons/crypto-commons/blob/master/Docs/ur-2-keys.md#seeds-urcrypto-seed):
```
{
  1: 37(h'020C223A86F7464693FC650EF3CAC047'), 
  2: 300({
    1: h'c7098580125e2ab0981253468b2dbc52',
    2: 100(1620237319)
  })
}
```
Note that the UUID (element #1) of the request and response  must match, and the `crypto-seed` payload (element #1 of the element #2) must hash to the `seed-digest` sent in the request.

This encodes to:
```
A2                                      # map(2)
   01                                   # unsigned(1)
   D8 25                                # tag(37)
      50                                # bytes(16)
         020C223A86F7464693FC650EF3CAC047 # UUID
   02                                   # unsigned(2)
   D9 012C                              # tag(300)
      A2                                # map(2)
         01                             # unsigned(1)
         50                             # bytes(16)
            C7098580125E2AB0981253468B2DBC52 
                                        # crypto-seed
         02                             # unsigned(2)
         D8 64                          # tag(100)
            1A 6092DC07                 # creation time
```
Or:
```
A201D82550020C223A86F7464693FC650EF3CAC04702D9012CA20150C7098580125E2AB0981253468B2DBC5202D8641A6092DC07
```
Or:
```
ur:crypto-response/oeadtpdagdaobncpftlnylfgfgmuztihbawfsgrtflaotaaddwoeadgdstaslplabghydrpfmkbggufgludprfgmaotpiecyhnmouoatbyfngycy
```

## Request & Response: `crypto-hdkey`

To request a `crypto-hdkey`, a `crypto-request` must make a request for tag `501` and must flag whether the requested key is private and must include a `crypto-keypath` per the [crypto-request CDDL](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2021-001-request.md#cddl-for-request). The `crypto-keypath` is defined in the [crypto-keypath CDDL](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-007-hdkey.md#cddl-for-key-path), tagged as `304` and may include a `source-fingerprint`. 

### A Master Key Request

A request for a master key just includes a fingerprint for its keypath, without need for derivation.

The following example uses a new UUID:
```
$ uuidgen | sed s/-//g
6CA458A5C18A41A9978CFF448678E31B
```
It also uses the following seed, master key, and master-key fingerprint:
```
$ seedtool
69321d1951bbb65632b952521d07cf63
$ seed=69321d1951bbb65632b952521d07cf63
$ keytool --seed $seed master-key-base58
xprv9s21ZrQH143K4YvmEJdSAmqK2yq5bKnLSaEqbqde5dkXaARD3UVTsiYiY1Gc6VQ7Fh3J5TY9Vf9xC8954i7FKQtAwJptnE4byVMfhCmVdS6
$ keytool --seed $seed master-key
ur:crypto-hdkey/oxadykaoykaxhdclaekbrtdyktgrinhhvsfriefdaygopsvyzeclvaldjtgljtbnuyplrtpmgubewkhhpfaahdcxzshhfxvasacfesrppddksgbkecmueofpfzimutcptbspgdintpenurrffsbegetpmumsrkfs
$ keytool --seed $seed master-key-fingerprint
87b7d32e
```
A request for this key would look as follows:
```
{
  1: 37(h'6CA458A5C18A41A9978CFF448678E31B'), 
  2: 501({
    1: true,
    2: 304({
      2: h'87b7d32e'
    })
  })
}
```
The private-key check is map element #1 of the `501`-tagged `crypto-keypath`, while the derivation, which in this case is just a fingerprint, is element #2.

This encodes as follows:
```
A2                                      # map(2)
   01                                   # unsigned(1)
   D8 25                                # tag(37)
      50                                # bytes(16)
         6CA458A5C18A41A9978CFF448678E31B # UUID
   02                                   # unsigned(2)
   D9 01F5                              # tag(501)
      A2                                # map(2)
         01                             # unsigned(1)
         F5                             # TRUE
         02                             # unsigned(2)
         D9 0130                        # tag(305)
            A1                          # map(1)
               02                       # unsigned(2)
               44                       # bytes(4)
                  87B7D32E              # fingerprint
```
Or:
```
A201D825506CA458A5C18A41A9978CFF448678E31B02D901F5A201F502D90130A1024487B7D32E
```
Or:
```
ur:crypto-request/oeadtpdagdjzoxhdonselefpptmslkzmfylnksvlcwaotaadykoeadykaotaaddyoyaofyltrltedmfhnbeylu
```
### A Master Key Response

As usual, the response includes a matching UUID and the correctly tagged data: in this case, a `303` tagged [HDkey](https://github.com/BlockchainCommons/crypto-commons/blob/master/Docs/ur-2-keys.md#a-master-key). As we saw in [A Guide to Using URs for Key Material](https://github.com/BlockchainCommons/crypto-commons/blob/master/Docs/ur-2-keys.md#hd-keys-urcrypo-hdkey), we need to know the chain code and key data to transmit a `crypto-hdkey` via UR. The following reiterates how to reference that information, based on the master key already revealed, above.

The Base58-encoded master key:

`xprv9s21ZrQH143K4YvmEJdSAmqK2yq5bKnLSaEqbqde5dkXaARD3UVTsiYiY1Gc6VQ7Fh3J5TY9Vf9xC8954i7FKQtAwJptnE4byVMfhCmVdS6`

Can be decoded to hex as:

`0488ade4000000000000000000fa5c43e6c21939b6a824ca0a35933341406add22d6c85069d836dfbc3d104ad8007ec030774b695ce83b64480855ace1fe21e6896e4e6e0cdbaec0ad5310f45cb0906ebcbf`

Per [BIP32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki) this decodes as following:

* 04 ; version 4
* 88ade4 ; xprv
* 00 ; depth 0 == master key
* 00000000 ; parent fingerprint
* 00000000 ; child number
* fa5c43e6c21939b6a824ca0a35933341406add22d6c85069d836dfbc3d104ad8 ; chain code
* 007ec030774b695ce83b64480855ace1fe21e6896e4e6e0cdbaec0ad5310f45cb0 ; key data
* 906ebcbf ; base 58 checksum

This means that the appropriate `crypto-hdkey` is:
```
{
    1: true,                            # is-master
    2: true,                            # is-private
    3: h'007ec030774b695ce83b64480855ace1fe21e6896e4e6e0cdbaec0ad5310f45cb0',                                       
    4: h'fa5c43e6c21939b6a824ca0a35933341406add22d6c85069d836dfbc3d104ad8'
}

```
And thus the `crypto-response` is:
```
{
  1: 37(h'6CA458A5C18A41A9978CFF448678E31B'), 
  2: 303({
    1: true,
    2: true,
    3: h'007ec030774b695ce83b64480855ace1fe21e6896e4e6e0cdbaec0ad5310f45cb0',
    4: h'fa5c43e6c21939b6a824ca0a35933341406add22d6c85069d836dfbc3d104ad8'
  })
}
```
This encodes as follows:
```
A2                                      # map(2)
   01                                   # unsigned(1)
   D8 25                                # tag(37)
      50                                # bytes(16)
         6CA458A5C18A41A9978CFF448678E31B # UUID
   02                                   # unsigned(2)
   D9 012F                              # tag(303)
      A4                                # map(4)
         01                             # TRUE
         F5                             # primitive(21)
         02                             # TRUE
         F5                             # primitive(21)
         03                             # unsigned(3)
         58 21                          # bytes(33)
            007EC030774B695CE83B64480855ACE1FE21E6896E4E6E0CDBAEC0AD5310F45CB0 
                                        # key data
         04                             # unsigned(4)
         58 20                          # bytes(32)
            FA5C43E6C21939B6A824CA0A35933341406ADD22D6C85069D836DFBC3D104AD8 
                                        # chain code
```
Or:
```
A201D825506CA458A5C18A41A9978CFF448678E31B02D9012FA401F502F5035821007EC030774B695CE83B64480855ACE1FE21E6896E4E6E0CDBAEC0AD5310F45CB0045820FA5C43E6C21939B6A824CA0A35933341406ADD22D6C85069D836DFBC3D104AD8
```

Or:
```
ur:crypto-response/oeadtpdagdjzoxhdonselefpptmslkzmfylnksvlcwaotaaddloxadykaoykaxhdclaekbrtdyktgrinhhvsfriefdaygopsvyzeclvaldjtgljtbnuyplrtpmgubewkhhpfaahdcxzshhfxvasacfesrppddksgbkecmueofpfzimutcptbspgdintpenurrffsbegetpryhdinct
```

### Double-Checking the Reponse

We can double check this work by looking  at the `crypto-hdkey` that was generated by `keytool`:

* **Key:** oxadykaoykaxhdclaekbrtdyktgrinhhvsfriefdaygopsvyzeclvaldjtgljtbnuyplrtpmgubewkhhpfaahdcxzshhfxvasacfesrppddksgbkecmueofpfzimutcptbspgdintpenurrffsbegetp
* **Checksum:** mumsrkfs

That same key is indeed embedded in the `crypto-response`, as should be the case:

* **Other Info:** oeadtpdagdjzoxhdonselefpptmslkzmfylnksvlcwaotaaddl 
* **Key:** oxadykaoykaxhdclaekbrtdyktgrinhhvsfriefdaygopsvyzeclvaldjtgljtbnuyplrtpmgubewkhhpfaahdcxzshhfxvasacfesrppddksgbkecmueofpfzimutcptbspgdintpenurrffsbegetp
* **Checksum:** ryhdinct

### A Derived Key Request

You may instead want to request a derived key. This follows the same format as a master-key request, but you must fill in the `components` element of the `crypto-keypath` in the `crypto-request` per [the keypath CDDL](https://github.com/BlockchainCommons/Research/blob/master/papers/bcr-2020-007-hdkey.md#cddl-for-key-path).

Here's a new UUID for this example:
```
$ uuidgen | sed s/-//g
306186A30C94429E97E79186A71A95FE
```
Here's a [m/44'/1'/1'/0/1] derived key from our master key, in both `xprv` and UR formats:
```
$ /usr/local/bin/keytool --master-key xprv9s21ZrQH143K4YvmEJdSAmqK2yq5bKnLSaEqbqde5dkXaARD3UVTsiYiY1Gc6VQ7Fh3J5TY9Vf9xC8954i7FKQtAwJptnE4byVMfhCmVdS6 --full-address-derivation-path m/44h/1h/1h/0/1 address-key-base58 address-key
xprvA3L3Agi3xbB6tYEz3R3FC4atLCuVReLci4Dn1kaamsA8dZUKQLi1u9orFrm9o44RnyuBrVNYba6Gsf4dLrgoUA6Myj3MDjkVE2g8Qoocfa3
ur:crypto-hdkey/onaoykaxhdclaemwhpkpwkhkgaghasfhrppyamryftinbnsfnnhhihbdjlmucfzojyfgynldgleywdaahdcxspiofzbdsgsogahhgaeegyvecaiefwlsgukisobzeerfneotjsnbcehemtjyyacaamoeadlecsdwykadykadykaewkadwkaocyltrltedmaycyknsfgocasfaahnos
```
Using `bytewords`, we can convert the `crypto-hdkey` back to CBOR:
```
$ bytewords -i minimal -o hex onaoykaxhdclaemwhpkpwkhkgaghasfhrppyamryftinbnsfnnhhihbdjlmucfzojyfgynldgleywdaahdcxspiofzbdsgsogahhgaeegyvecaiefwlsgukisobzeerfneotjsnbcehemtjyyacaamoeadlecsdwykadykadykaewkadwkaocyltrltedmaycyknsfgocasfaahnos
a502f503582100945b75f4594954093fb6ab06bd3a690ccc9e5c650b6f9319fb7446f6894e32ea045820c867400bcac9495c493451e41d644283537dc91534bc9fa371a01c5f9674f81d06a2018a182cf501f501f500f401f4021a87b7d32e081a7acc551d
```
Then we can use `cbor2diag` to determine the critical elements of the key:
```
$ cbor2diag -x a502f503582100945b75f4594954093fb6ab06bd3a690ccc9e5c650b6f9319fb7446f6894e32ea045820c867400bcac9495c493451e41d644283537dc91534bc9fa371a01c5f9674f81d06a2018a182cf501f501f500f401f4021a87b7d32e081a7acc551d
{
  2: true, 
  3: h'00945b75f4594954093fb6ab06bd3a690ccc9e5c650b6f9319fb7446f6894e32ea', 
  4: h'c867400bcac9495c493451e41d644283537dc91534bc9fa371a01c5f9674f81d', 
  6: 
     {
       1: [44, true, 1, true, 1, true, 0, false, 1, false], 
       2: 2276971310
     }, 
  8: 2060211485
}
```
This reveals the key privacy (element #2), key data (element #3), chain code (element #4), derivation path and source fingerprint (element #6), and parent fingerprint (#8).

To request this key simply requires including the full derivation path:
```
{
  1: 37(h'306186A30C94429E97E79186A71A95FE'), 
  2: 501({
    1: true,
    2: 304({
      1: [44, true, 1, true, 1, true, 0, false, 1, false],
      2: h'87b7d32e'
    })
  })
}
```
Again, note that the `501`-tagged `crypto-keypath` contains a private-key check (element #1), but this time it includes both a full derivation path and the source fingerprint (element #2).

This request is encoded as follows:
```
A2                                      # map(2)
   01                                   # unsigned(1)
   D8 25                                # tag(37)
      50                                # bytes(16)
         306186A30C94429E97E79186A71A95FE # UUID
   02                                   # unsigned(2)
   D9 01F5                              # tag(501)
      A2                                # map(2)
         01                             # unsigned(1)
         F5                             # TRUE
         02                             # unsigned(2)
         D9 0130                        # tag(304)
            A2                          # map(2)
               01                       # unsigned(1)
               8A                       # array(10)
                  18 2C                 # unsigned(44)
                  F5                    # TRUE
                  01                    # unsigned(1)
                  F5                    # TRUE
                  01                    # unsigned(1)
                  F5                    # TRUE
                  00                    # unsigned(0)
                  F4                    # FALSE
                  01                    # unsigned(1)
                  F4                    # FALSE
               02                       # unsigned(2)
               44                       # bytes(4)
                  87B7D32E              # fingerprint
```
Or:
```
A201D82550306186A30C94429E97E79186A71A95FE02D901F5A201F502D90130A2018A182CF501F501F500F401F4024487B7D32E
```
Or:
```
ur:crypto-request/oeadtpdagddyhslnotbnmwfwnnmsvdmelnoscymdzeaotaadykoeadykaotaaddyoeadlecsdwykadykadykaewkadwkaofyltrltedmmytdwdbe
```
### A Derived Key Response

We've already seen the full encoding of the derived key, it simply needs to be presented as a `crypto-response`:
```
{
  1: 37(h'306186A30C94429E97E79186A71A95FE'), 
  2: 303({
    2: true, 
    3: h'00945b75f4594954093fb6ab06bd3a690ccc9e5c650b6f9319fb7446f6894e32ea', 
    4: h'c867400bcac9495c493451e41d644283537dc91534bc9fa371a01c5f9674f81d', 
    6: 
     {
       1: [44, true, 1, true, 1, true, 0, false, 1, false], 
       2: 2276971310
     }, 
    8: 2060211485
  })
}
```
Which is encoded as follows:
```
A2                                      # map(2)
   01                                   # unsigned(1)
   D8 25                                # tag(37)
      50                                # bytes(16)
         306186A30C94429E97E79186A71A95FE # UUID
   02                                   # unsigned(2)
   D9 012F                              # tag(303)
      A5                                # map(5)
         02                             # unsigned(2)
         F5                             # TRUE
         03                             # unsigned(3)
         58 21                          # bytes(33)
            00945B75F4594954093FB6AB06BD3A690CCC9E5C650B6F9319FB7446F6894E32EA 
                                        # key data
         04                             # unsigned(4)
         58 20                          # bytes(32)
            C867400BCAC9495C493451E41D644283537DC91534BC9FA371A01C5F9674F81D 
                                        # chaincode
         06                             # unsigned(6)
         A2                             # map(2)
            01                          # unsigned(1)
            8A                          # array(10)
               18 2C                    # unsigned(44)
               F5                       # TRUE
               01                       # unsigned(1)
               F5                       # TRUE
               01                       # unsigned(1)
               F5                       # TRUE
               00                       # unsigned(0)
               F4                       # FALSE
               01                       # unsigned(1)
               F4                       # FALSE
            02                          # unsigned(2)
            1A 87B7D32E                 # Source Fingerprint
         08                             # unsigned(8)
         1A 7ACC551D                    # Parent Fingerprint
```
Or:
```
A201D82550306186A30C94429E97E79186A71A95FE02D9012FA502F503582100945B75F4594954093FB6AB06BD3A690CCC9E5C650B6F9319FB7446F6894E32EA045820C867400BCAC9495C493451E41D644283537DC91534BC9FA371A01C5F9674F81D06A2018A182CF501F501F500F401F4021A87B7D32E081A7ACC551D
```
Or:
```
ur:crypto-response/oeadtpdagddyhslnotbnmwfwnnmsvdmelnoscymdzeaotaaddlonaoykaxhdclaemwhpkpwkhkgaghasfhrppyamryftinbnsfnnhhihbdjlmucfzojyfgynldgleywdaahdcxspiofzbdsgsogahhgaeegyvecaiefwlsgukisobzeerfneotjsnbcehemtjyyacaamoeadlecsdwykadykadykaewkadwkaocyltrltedmaycyknsfgocamdttsesp
```

## Request & Response: `crypto-psbt`

_This section is awaiting the drafting of the crypto-psbt doc._

## Integrating Request & Response URs Into Your Code

Although this document is meant to provide a full understanding of how `crypto-request` and `crypto-response` work, you'll likely be using software to do most of the heavy lifting for you. As usual, you'll want to use [bc-ur for C++](https://github.com/BlockchainCommons/bc-ur) library or else one of the [conversions of that library to other languages such as Java and Swift](https://github.com/BlockchainCommons/crypto-commons/blob/master/README.md#bc-ur).

## Conclusion

Most URs allows for the transmission of data from one device to another, which is great when you want a user to initiate a transfer of data, such as when he chooses to scan a seed or key into [Gordian SeedTool](https://github.com/BlockchainCommons/GordianSeedTool-iOS) or [Gordian Cosigner](https://github.com/BlockchainCommons/GordianCosigner-iOS).

But you may instead want to allow a more automated dialogue, where one application queries another for a specific key, seed, or PSBT. This allows for more dynamic and interactive functionality, without the user needing to know the specifics of seeds and keys. That's what `crypto-request` and `crypto-response` support, using a back and forth mechanism that builds on the [key material](https://github.com/BlockchainCommons/crypto-commons/blob/master/Docs/ur-2-keys.md#hd-keys-urcrypo-hdkey) and PSBT URs.

The response and request URs will expand in the future. Among our first plans are requests for SSKRs and ephemeral Diffie-Hellman keys, with response-requests that require multiple trips also intended for the future.

Also see our article on [`crypto-request/response` vs `crypto-psbt`](crypto-request-or-crypto-psbt.md) for more on why you'd want to use this design pattern.
