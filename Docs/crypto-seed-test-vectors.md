# `crypto-seed` Test Vectors

## 128 Bit Examples (Yinmn Blue)

### Seed with No Additional Data

![](https://github.com/BlockchainCommons/crypto-commons/blob/master/images/vectors/vector-seed-yinmn.png)

```
{
  1: h'59f2293a5bce7d4de59e71b4207ac5d2'
}
```

### Seed with Date

![](https://github.com/BlockchainCommons/crypto-commons/blob/master/images/vectors/vector-seed-yinmn-date.png)

```
{
  1: h'59f2293a5bce7d4de59e71b4207ac5d2',
  2: 1(1645539742)
}
```

### Seed with Date & Name

![](https://github.com/BlockchainCommons/crypto-commons/blob/master/images/vectors/vector-seed-yinmn-date.png)

```
{
  1: h'59f2293a5bce7d4de59e71b4207ac5d2',
  2: 1(1645539742),
  3: "Yinmn Blue Acid Exam"
}
```

### Seed with Date, Name & Note

![](https://github.com/BlockchainCommons/crypto-commons/blob/master/images/vectors/vector-seed-yinmn-note.png)

{
  1: h'59f2293a5bce7d4de59e71b4207ac5d2',
  2: 1(1645539742),
  3: "Yinmn Blue Acid Exam",
  4: "This is our standard 128-bit test seed."
}

### Seed with Date, Name & Long Note

![](https://github.com/BlockchainCommons/crypto-commons/blob/master/images/vectors/vector-seed-yinmn-lnote.png)

{
  1: h'59f2293a5bce7d4de59e71b4207ac5d2',
  2: 1(1645539742),
  3: "Yinmn Blue Acid Exam",
  4: "This is our standard 128-bit test seed. However, this version of it has a very long note. Why? The object is to force the creation of an animated GIF, which demonstrates the power of URs, not just to allow for the self-identification of information, but also to do so in a way the integrates well with QR codes, creating an animated QR when the data would otherwise be too long for a static QR. To force that to happen, this note was made to be over 500 characters long, which is a lot of data for a QR, which maxes out at about 4,000 alphanumeric characters, but which gets very hard to read (especially from a phone) before that."
}

