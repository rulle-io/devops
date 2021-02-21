# Unexpected(?) behaviour in software code
## "Software bites" (R)

### String split() in Scala
Very similar code, completely different output.
```scala
scala> "aa|bb".split("|") // parameter is String
val res0: Array[String] = Array(a, a, |, b, b)

scala> "aa|bb".split('|') // parameter is Char 
val res1: Array[String] = Array(aa, bb)
```
