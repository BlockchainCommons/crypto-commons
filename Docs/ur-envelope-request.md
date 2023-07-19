# A Guide to Using UR Envelope Request & Response

STANDARD:
DragonBook:~ ShannonA$ bytewords -i minimal -o hex lftpsptpcsihhsjziniaihtpsptpsolftpsptpcsihjzinjeihjktpsptpcsiaidjlidgegsftfn
82d8c8d81865616c696365d8c8d8c982d8c8d818656c696b6573d8c8d81863626f62
DragonBook:~ ShannonA$ cbor2diag -x 82d8c8d81865616c696365d8c8d8c982d8c8d818656c696b6573d8c8d81863626f62
[200(24("alice")), 200(201([200(24("likes")), 200(24("bob"))]))]

## Request Seed
ur:envelope/lstpsptpcstptktaadethdcxaxtolansehsavteehpwdfxfmveihwewmkgtsmwkksksggtmnvttycpnnynuydmswtpsptpsolftpsptpsgcsietpsplftpsptpcstpttcsietpsptpsolftpsptpcstptdcssptpsptpcstaadeshdcxzmoycylumhmdgwspnyvadaktnsoycwmyaodihgftdllugltphlmtutytadosdwwdtpsptpsolftpsptpsgaatpsptpcsksiefdhsjpkpjncxjtkpjnjskphsjncxieiniajyhscxiejljzjljpihjncxinjtiainiekpjtjycxihkpjnclcxgykpinjkcxjskpinjkcxiejljzjljpihjkcxjkinjycxinjzjzjlcxiajljtjkihjskphsjykpjpcxjkinjycxkojljzkpjojyhsjyihjncxhskpjydmhesrdkts

83d8c8d818d8cfd90138582003ce809c31c2e0345bea433ee465edeb7bd79479c5ca4d8ee0d4229ef6db2ec6d8c8d8c982d8c8d8ca1864d8c882d8c8d818d8d11864d8c8d8c982d8c8d818d8d218c8d8c8d818d901395820ffa11a8b90954fc89ae625779ca11b8f0227573a2f8b4ed85d96ddf901a72cead8c8d8c982d8c8d8ca04d8c8d8187864486172756d206e756d7175616d20646963746120646f6c6f72656d20696e636964756e742065756d212051756973207175697320646f6c6f7265732073697420696c6c6f20636f6e73657175617475722073697420766f6c7570746174656d206175742e

[200(24(207(312(h'03ce809c31c2e0345bea433ee465edeb7bd79479c5ca4d8ee0d4229ef6db2ec6')))), 
 200(201([200(202(100)), 200([200(24(209(100))), 200(201([200(24(210(200))), 200(24(313(h'ffa11a8b90954fc89ae625779ca11b8f0227573a2f8b4ed85d96ddf901a72cea')))]))])])),
200(201([200(202(4)), 200(24("Harum numquam dicta dolorem incidunt eum! Quis quis dolores sit illo consequatur sit voluptatem aut."))]))]

```
83                                      # array(3)
   D8 C8                                # tag(200) ENVELOPE
      D8 18                             # tag(24) BYTE STRING
         D8 CF                          # tag(207)
            D9 0138                     # tag(312)
               58 20                    # bytes(32)
                  03CE809C31C2E0345BEA433EE465EDEB7BD79479C5CA4D8EE0D4229EF6DB2EC6 # "\u0003\u0380\x9C1\xC2\xE04[\xEAC>\xE4e\xED\xEB{הy\xC5\xCAM\x8E\xE0\xD4\"\x9E\xF6\xDB.\xC6"
   D8 C8                                # tag(200) ENVELOPE
      D8 C9                             # tag(201) ASSERTION
         82                             # array(2)
            D8 C8                       # tag(200) ENVELOPE
               D8 CA                    # tag(202) KNOWN VALUE
                  18 64                 # unsigned(100) KV: BODY
            D8 C8                       # tag(200) ENVELOPE
               82                       # array(2)
                  D8 C8                 # tag(200) ENVELOPE
                     D8 18              # tag(24)
                        D8 D1           # tag(209)
                           18 64        # unsigned(100)
                  D8 C8                 # tag(200) ENVELOPE
                     D8 C9              # tag(201)
                        82              # array(2)
                           D8 C8        # tag(200) ENVELOPE
                              D8 18     # tag(24)
                                 D8 D2  # tag(210)
                                    18 C8 # unsigned(200)
                           D8 C8        # tag(200) ENVELOPE
                              D8 18     # tag(24)
                                 D9 0139 # tag(313)
                                    58 20 # bytes(32)
                                       FFA11A8B90954FC89AE625779CA11B8F0227573A2F8B4ED85D96DDF901A72CEA # "\xFF\xA1\u001A\x8B\x90\x95OȚ\xE6%w\x9C\xA1\e\x8F\u0002'W:/\x8BN\xD8]\x96\xDD\xF9\u0001\xA7,\xEA"
   D8 C8                                # tag(200) ENVELOPE
      D8 C9                             # tag(201) ASSERTION
         82                             # array(2)
            D8 C8                       # tag(200) ENVELOPE
               D8 CA                    # tag(202) KNOWN VALUE
                  04                    # unsigned(4) KV: 2
            D8 C8                       # tag(200) ENVELOPE
               D8 18                    # tag(24) BYTE STRING
                  78 64                 # text(100)
                     486172756D206E756D7175616D20646963746120646F6C6F72656D20696E636964756E742065756D212051756973207175697320646F6C6F7265732073697420696C6C6F20636F6E73657175617475722073697420766F6C7570746174656D206175742E # "Harum numquam dicta dolorem incidunt eum! Quis quis dolores sit illo consequatur sit voluptatem aut."
```

```
request(CID(03ce809c)) [
    body: «100» [
        ❰200❱: seed-digest(Bytes(32))
    ]
    note: "Harum numquam dicta dolorem incidunt eum! Quis quis dolores sit illo consequatur sit voluptatem aut."
]
```

```mermaid
graph LR
    1(("73a74d84<br/>NODE"))
    2["7a0302af<br/>request(CID(03ce809c))"]
    3(["572491ba<br/>ASSERTION"])
    4[/"b2cbfa6b<br/>100"/]
    5(("c046590d<br/>NODE"))
    6["d44a14fe<br/>«100»"]
    7(["26b385ea<br/>ASSERTION"])
    8["a85815d7<br/>❰200❱"]
    9["43fa6f3d<br/>313(Bytes(32))"]
    10(["dfffc9e6<br/>ASSERTION"])
    11[/"49a5f41b<br/>4"/]
    12["5f515e27<br/>#quot;Harum numquam dicta dolorem incidunt eum…#quot;"]
    1 -->|subj| 2
    1 --> 3
    3 -->|pred| 4
    3 -->|obj| 5
    5 -->|subj| 6
    5 --> 7
    7 -->|pred| 8
    7 -->|obj| 9
    1 --> 10
    10 -->|pred| 11
    10 -->|obj| 12
    style 1 stroke:red,stroke-width:3.0px
    style 2 stroke:#55f,stroke-width:3.0px
    style 3 stroke:red,stroke-width:3.0px
    style 4 stroke:#55f,stroke-width:3.0px
    style 5 stroke:red,stroke-width:3.0px
    style 6 stroke:#55f,stroke-width:3.0px
    style 7 stroke:red,stroke-width:3.0px
    style 8 stroke:#55f,stroke-width:3.0px
    style 9 stroke:#55f,stroke-width:3.0px
    style 10 stroke:red,stroke-width:3.0px
    style 11 stroke:#55f,stroke-width:3.0px
    style 12 stroke:#55f,stroke-width:3.0px
    linkStyle 0 stroke:red,stroke-width:2.0px
    linkStyle 1 stroke-width:2.0px
    linkStyle 2 stroke:green,stroke-width:2.0px
    linkStyle 3 stroke:#55f,stroke-width:2.0px
    linkStyle 4 stroke:red,stroke-width:2.0px
    linkStyle 5 stroke-width:2.0px
    linkStyle 6 stroke:green,stroke-width:2.0px
    linkStyle 7 stroke:#55f,stroke-width:2.0px
    linkStyle 8 stroke-width:2.0px
    linkStyle 9 stroke:green,stroke-width:2.0px
    linkStyle 10 stroke:#55f,stroke-width:2.0px
```



[Response Seed]
ur:envelope/lstpsptpcstptktaadethdcxaxtolansehsavteehpwdfxfmveihwewmkgtsmwkksksggtmnvttycpnnynuydmswtpsptpsolftpsptpsgcsietpsplftpsptpcstpttcsietpsptpsolftpsptpcstptdcssptpsptpcstaadeshdcxzmoycylumhmdgwspnyvadaktnsoycwmyaodihgftdllugltphlmtutytadosdwwdtpsptpsolftpsptpsgaatpsptpcsksiefdhsjpkpjncxjtkpjnjskphsjncxieiniajyhscxiejljzjljpihjncxinjtiainiekpjtjycxihkpjnclcxgykpinjkcxjskpinjkcxiejljzjljpihjkcxjkinjycxinjzjzjlcxiajljtjkihjskphsjykpjpcxjkinjycxkojljzkpjojyhsjyihjncxhskpjydmhesrdkts

```
response(CID(03ce809c)) [
    result: Bytes(16) [
        hasName: "Dark Purple Peck Vial"
        id: 200
    ]
]
```

```mermaid
graph LR
    1(("23f82a73<br/>NODE"))
    2["d07a8b9f<br/>response(CID(03ce809c))"]
    3(["ee94c24e<br/>ASSERTION"])
    4[/"4ee5b91c<br/>101"/]
    5(("9344f727<br/>NODE"))
    6["b6d2b918<br/>Bytes(16)"]
    7(["1be2074d<br/>ASSERTION"])
    8[/"9d0480e0<br/>11"/]
    9["03fcb27e<br/>#quot;Dark Purple Peck Vial#quot;"]
    10(["7894e935<br/>ASSERTION"])
    11[/"c2b87b29<br/>1"/]
    12[/"40d822c5<br/>200"/]
    1 -->|subj| 2
    1 --> 3
    3 -->|pred| 4
    3 -->|obj| 5
    5 -->|subj| 6
    5 --> 7
    7 -->|pred| 8
    7 -->|obj| 9
    5 --> 10
    10 -->|pred| 11
    10 -->|obj| 12
    style 1 stroke:red,stroke-width:3.0px
    style 2 stroke:#55f,stroke-width:3.0px
    style 3 stroke:red,stroke-width:3.0px
    style 4 stroke:#55f,stroke-width:3.0px
    style 5 stroke:red,stroke-width:3.0px
    style 6 stroke:#55f,stroke-width:3.0px
    style 7 stroke:red,stroke-width:3.0px
    style 8 stroke:#55f,stroke-width:3.0px
    style 9 stroke:#55f,stroke-width:3.0px
    style 10 stroke:red,stroke-width:3.0px
    style 11 stroke:#55f,stroke-width:3.0px
    style 12 stroke:#55f,stroke-width:3.0px
    linkStyle 0 stroke:red,stroke-width:2.0px
    linkStyle 1 stroke-width:2.0px
    linkStyle 2 stroke:green,stroke-width:2.0px
    linkStyle 3 stroke:#55f,stroke-width:2.0px
    linkStyle 4 stroke:red,stroke-width:2.0px
    linkStyle 5 stroke-width:2.0px
    linkStyle 6 stroke:green,stroke-width:2.0px
    linkStyle 7 stroke:#55f,stroke-width:2.0px
    linkStyle 8 stroke-width:2.0px
    linkStyle 9 stroke:green,stroke-width:2.0px
    linkStyle 10 stroke:#55f,stroke-width:2.0px
```

## Request Derivation

ur:envelope/lstpsptpcstptktaadethdcxjkjozepladdliysbjnhnsertmnzolrspfslsroimeszefpfsledagmattaglgyentpsptpsolftpsptpsgcsietpsplftpsptpcstpttcsihtpsptpsolftpsptpcstptdcssotpsplftpsptpcstaaddyoeadlocsdyykaeykaeykaoykaxaatpsptpsolftpsptpsgadtpsptpsgcfadyntpsptpsolftpsptpsgaatpsptpcskspaguinjtjycxjskpincxiejljzjljpinidkpjkcxhsjoihjpinhsjncxkoihjzcxjpihiakpjkhsjtiehsihcxjkinjycxhsjzinhsjkcxhsieinjoinjkiaincxhskpjycxhsjzinjskpiniecxishsjpkpjncxjtjljtdmcxglkpjzjzhscxjkhsihjoihcxjojpjlkoinieihjtjycxinjzjzkpjncxjkinjtjycxhskpjyihjncxkpjycxiajljtjkihjskphsjykpjpcxiykpiohscxjkhsjoinihjtjyihcxjkinjtjycxiajljtjkihiajyihjykpjpcxiejljzjljpihjkfhuyghcedp

```
request(CID(7370feae)) [
    body: «101» [
        ❰201❱: crypto-keypath(Map) [
            id: 502
        ]
    ]
    note: "Sint qui doloribus aperiam vel recusandae sit alias adipisci aut aliquid harum non. Nulla saepe provident illum sint autem ut consequatur fuga sapiente sint consectetur dolores?"
]
```

```mermaid
graph LR
    1(("d477fb1b<br/>NODE"))
    2["b943b664<br/>request(CID(7370feae))"]
    3(["2d2ff06c<br/>ASSERTION"])
    4[/"b2cbfa6b<br/>100"/]
    5(("020d6d55<br/>NODE"))
    6["6f69ae4f<br/>«101»"]
    7(["ea2181cc<br/>ASSERTION"])
    8["8ab2a2ba<br/>❰201❱"]
    9(("54810b5b<br/>NODE"))
    10["f627e959<br/>304(Map)"]
    11(["76bbe79a<br/>ASSERTION"])
    12[/"c2b87b29<br/>1"/]
    13[/"80a261b4<br/>502"/]
    14(["61c8768c<br/>ASSERTION"])
    15[/"49a5f41b<br/>4"/]
    16["4fc181b0<br/>#quot;Sint qui doloribus aperiam vel recusanda…#quot;"]
    1 -->|subj| 2
    1 --> 3
    3 -->|pred| 4
    3 -->|obj| 5
    5 -->|subj| 6
    5 --> 7
    7 -->|pred| 8
    7 -->|obj| 9
    9 -->|subj| 10
    9 --> 11
    11 -->|pred| 12
    11 -->|obj| 13
    1 --> 14
    14 -->|pred| 15
    14 -->|obj| 16
    style 1 stroke:red,stroke-width:3.0px
    style 2 stroke:#55f,stroke-width:3.0px
    style 3 stroke:red,stroke-width:3.0px
    style 4 stroke:#55f,stroke-width:3.0px
    style 5 stroke:red,stroke-width:3.0px
    style 6 stroke:#55f,stroke-width:3.0px
    style 7 stroke:red,stroke-width:3.0px
    style 8 stroke:#55f,stroke-width:3.0px
    style 9 stroke:red,stroke-width:3.0px
    style 10 stroke:#55f,stroke-width:3.0px
    style 11 stroke:red,stroke-width:3.0px
    style 12 stroke:#55f,stroke-width:3.0px
    style 13 stroke:#55f,stroke-width:3.0px
    style 14 stroke:red,stroke-width:3.0px
    style 15 stroke:#55f,stroke-width:3.0px
    style 16 stroke:#55f,stroke-width:3.0px
    linkStyle 0 stroke:red,stroke-width:2.0px
    linkStyle 1 stroke-width:2.0px
    linkStyle 2 stroke:green,stroke-width:2.0px
    linkStyle 3 stroke:#55f,stroke-width:2.0px
    linkStyle 4 stroke:red,stroke-width:2.0px
    linkStyle 5 stroke-width:2.0px
    linkStyle 6 stroke:green,stroke-width:2.0px
    linkStyle 7 stroke:#55f,stroke-width:2.0px
    linkStyle 8 stroke:red,stroke-width:2.0px
    linkStyle 9 stroke-width:2.0px
    linkStyle 10 stroke:green,stroke-width:2.0px
    linkStyle 11 stroke:#55f,stroke-width:2.0px
    linkStyle 12 stroke-width:2.0px
    linkStyle 13 stroke:green,stroke-width:2.0px
    linkStyle 14 stroke:#55f,stroke-width:2.0px
```

## Request Key

```
request(CID(c1e3a73a)) [
    body: «101» [
        ❰201❱: crypto-keypath(Map) [
            id: 502
        ]
    ]
    note: "Voluptates omnis voluptates accusamus. Sed aliquam perspiciatis rem veniam commodi harum sequi atque enim est et ab accusantium consequuntur voluptas."
]
```

```mermaid
graph LR
    1(("b5c53e80<br/>NODE"))
    2["288a38af<br/>request(CID(c1e3a73a))"]
    3(["990edd80<br/>ASSERTION"])
    4[/"49a5f41b<br/>4"/]
    5["cfa7df7c<br/>#quot;Voluptates omnis voluptates accusamus. S…#quot;"]
    6(["a59cb7f4<br/>ASSERTION"])
    7[/"b2cbfa6b<br/>100"/]
    8(("713666dd<br/>NODE"))
    9["6f69ae4f<br/>«101»"]
    10(["90bba300<br/>ASSERTION"])
    11["8ab2a2ba<br/>❰201❱"]
    12(("760d94cb<br/>NODE"))
    13["640ef0d1<br/>304(Map)"]
    14(["76bbe79a<br/>ASSERTION"])
    15[/"c2b87b29<br/>1"/]
    16[/"80a261b4<br/>502"/]
    1 -->|subj| 2
    1 --> 3
    3 -->|pred| 4
    3 -->|obj| 5
    1 --> 6
    6 -->|pred| 7
    6 -->|obj| 8
    8 -->|subj| 9
    8 --> 10
    10 -->|pred| 11
    10 -->|obj| 12
    12 -->|subj| 13
    12 --> 14
    14 -->|pred| 15
    14 -->|obj| 16
    style 1 stroke:red,stroke-width:3.0px
    style 2 stroke:#55f,stroke-width:3.0px
    style 3 stroke:red,stroke-width:3.0px
    style 4 stroke:#55f,stroke-width:3.0px
    style 5 stroke:#55f,stroke-width:3.0px
    style 6 stroke:red,stroke-width:3.0px
    style 7 stroke:#55f,stroke-width:3.0px
    style 8 stroke:red,stroke-width:3.0px
    style 9 stroke:#55f,stroke-width:3.0px
    style 10 stroke:red,stroke-width:3.0px
    style 11 stroke:#55f,stroke-width:3.0px
    style 12 stroke:red,stroke-width:3.0px
    style 13 stroke:#55f,stroke-width:3.0px
    style 14 stroke:red,stroke-width:3.0px
    style 15 stroke:#55f,stroke-width:3.0px
    style 16 stroke:#55f,stroke-width:3.0px
    linkStyle 0 stroke:red,stroke-width:2.0px
    linkStyle 1 stroke-width:2.0px
    linkStyle 2 stroke:green,stroke-width:2.0px
    linkStyle 3 stroke:#55f,stroke-width:2.0px
    linkStyle 4 stroke-width:2.0px
    linkStyle 5 stroke:green,stroke-width:2.0px
    linkStyle 6 stroke:#55f,stroke-width:2.0px
    linkStyle 7 stroke:red,stroke-width:2.0px
    linkStyle 8 stroke-width:2.0px
    linkStyle 9 stroke:green,stroke-width:2.0px
    linkStyle 10 stroke:#55f,stroke-width:2.0px
    linkStyle 11 stroke:red,stroke-width:2.0px
    linkStyle 12 stroke-width:2.0px
    linkStyle 13 stroke:green,stroke-width:2.0px
    linkStyle 14 stroke:#55f,stroke-width:2.0px
```
