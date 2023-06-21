# A Guide to Using URs for PSBTs

Uniform Resources (URs) allow for the encoding of a variety of information, including a variety of crypto-data. This document describes how they are used to encode PSBTs, or Partially Signed Bitcoin Transactions.

As usual, this will typically be done for you automatically using Blockchain Commons' [libraries](https://github.com/BlockchainCommons/crypto-commons/blob/master/README.md#bc-ur), but what follows is an explanation of how everything works.

## Why Use URs for PSBTs?

PSBTs are perhaps the ultimate interoperable data type in Bitcoin Core. They were explicitly built to allow different devices to create and/or sign Bitocin transmissions. As such, they are crucial to [Gordian](https://github.com/BlockchainCommons/Gordian) best practices, which advocate for the storage or seeds and other vulnerable data on non-networked devices. Using PSBTs, transactions can be created on networked devices, shipped to non-networked devices for signing, then shipped back to the networked devices for transmission. 

So why do you need URs rather than PSBT's standard data format? Quite simply, because PSBTs are too big. If you're just sending around a PSBT's mass of data as base64, no problem. But when transmitting to non-networked devices, for maximum resiliency of your seeds and keys, you probably need to use QRs, and even if you can jam a PSBT into a QR, it may not be readable by a computer camera.

This is especially true when PSBTs are used for multisigs, which is a prime use case for PSBTs: they can allow a transaction to be easily passed around until it's signed by a threshold of people required to authenticate a UTXO. However, as signatures accrue, a PSBT gets ever bigger, to the point where it may be too large for a QR code entirely.

URs resolve this by using fountain codes to enable Animated QRs. A single UR is turned into a sequence or URs, each preceded by its type and by its place in a sequence. Each individual frame is not just small enough to fit into a QR, but small enough to be read by a lower-resolution camera. (Best practice is to allow a user to dynamically downsize an animated QR if they're having troubles transmitting it.) The reading device then reads the animation until it's put together enough frames to reconstruct the original data.

## PRBTs: `[crypto-psbt]`

Example PSBT:

020000000142809965451bfccb9a11d067c43c6d0282a0dc718aeac870d65585a7c2a0b0b20000000000fdffffff02392c000000000000160014bc32db4cfb505e3fc94e21a3ec74d1aefcfc012c22c1000000000000160014eab4cd40d3926756cc52e5f91c9d3c8e3b400e1178220c00

Example UR:

ur:crypto-psbt/hkadlbjojkidjyzmadaejsaoaeaeaeadfwlanlihfecwztsbnybytiiossfnjnaolfnbuojslewdspjotbgolpossanbpfpraeaeaeaeaezczmzmzmaoesdwaeaeaeaeaeaecmaebbrfeyuygszogdhyfhsoglclotwpjyttplztztaddwcpseaeaeaeaeaeaecmaebbwdqzsnfztemoiohfsfgmvwytcentfnmnfrfzbabykscpbnaegwadaaloprckaxswtasfnslaaeaeaeeymeskryiawmtllndtlrylntbkvlqdjzuokogyemgmclskeclklnktkgwzpreoceaodagwasmnrktlstfdonhdlessnyzmwfsoahhthpjptdftpalbamfnfsykemgtrkrlbespktzcfyghaeaelaaeaeaelaaeaeaelaaeadadctemylaeaeaeaeaeaecmaebbmwamwtbknbutwyiestwdidytmwvamdhdaolaotvwadaxaaadaeaeaecpamaxhtvehdwdldbkrlimfgmdemcxdwfstpistemohngmmscefwhdihmshheydefhylcmcsspktzcfyghaeaelaaeaeaelaaeaeaelaaeaeaeaeadaeaeaeaeaecpaoaofdweolzoaxlaneqdjensswhlmksaiycsytketljowngensyaaybecpttvybylomucsspktzcfyghaeaelaaeaeaelaaeaeaelaadaeaeaeaeaeaeaeaecfktctrf

Hex:

59017f70736274ff010071020000000142809965451bfccb9a11d067c43c6d0282a0dc718aeac870d65585a7c2a0b0b20000000000fdffffff02392c000000000000160014bc32db4cfb505e3fc94e21a3ec74d1aefcfc012c22c1000000000000160014eab4cd40d3926756cc52e5f91c9d3c8e3b400e1178220c004f010488b21e03c6d9cc9c800000003291c5bd63ebd5862984f79d0ae3b36cdc7651375221c5358c86777bf2b2331c02254f098ebbd5c748a5588ac49afff3c9055a5b72d23ab17f063c3df5374dbbb710c877fd445400008000000080000000800001011f37f70000000000001600149406f00aa0ddee64c7ea62f994e695580280a3e5010304010000002206035ae458ea890ab76a469537202c3dd868d3926052971c425865975c32283ff71618c877fd445400008000000080000000800000000001000000000022020248eda6fb03809fb36b9cc65d98c26618f97cd570f14a9cf8081022d1e111889318c877fd44540000800000008000000080010000000000000000

CBOR:

59 017F                                 # bytes(383)
   70736274FF010071020000000142809965451BFCCB9A11D067C43C6D0282A0DC718AEAC870D65585A7C2A0B0B20000000000FDFFFFFF02392C000000000000160014BC32DB4CFB505E3FC94E21A3EC74D1AEFCFC012C22C1000000000000160014EAB4CD40D3926756CC52E5F91C9D3C8E3B400E1178220C004F010488B21E03C6D9CC9C800000003291C5BD63EBD5862984F79D0AE3B36CDC7651375221C5358C86777BF2B2331C02254F098EBBD5C748A5588AC49AFFF3C9055A5B72D23AB17F063C3DF5374DBBB710C877FD445400008000000080000000800001011F37F70000000000001600149406F00AA0DDEE64C7EA62F994E695580280A3E5010304010000002206035AE458EA890AB76A469537202C3DD868D3926052971C425865975C32283FF71618C877FD445400008000000080000000800000000001000000000022020248EDA6FB03809FB36B9CC65D98C26618F97CD570F14A9CF8081022D1E111889318C877FD44540000800000008000000080010000000000000000 # 
