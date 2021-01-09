# Code snippets Java vs Scala.

## Flatten a List of Optionals/Options

### Java code
```java
List<Optional<String>> optList =
  List.of(Optional.of("Hello"), Optional.empty(), Optional.of("World!"));
List<String> stringList = optList
  .stream()
  .flatMap(Optional::stream)
  .collect(Collectors.toList());
```

### Jshell
```java
jshell> List<Optional<String>> optList = List.of(Optional.of("Hello"), Optional.empty(), Optional.of("World!"));
optList ==> [Optional[Hello], Optional.empty, Optional[World!]]

jshell> List<String> stringList = optList.stream().flatMap(Optional::stream).collect(Collectors.toList());
stringList ==> [Hello, World!]
```

### Scala code
```scala
val optList: List[Option[String]] = List(Some(Hello), None, Some(World!))
val stringList = optList.flatten
```

### Scala REPL
```scala
scala> val optList = List(Some("Hello"), None, Some("World!"))
val optList: List[Option[String]] = List(Some(Hello), None, Some(World!))

scala> val stringList = optList.flatten
val stringList: List[String] = List(Hello, World!)
```

## Resolution
IMHO, Scala code is shorter and easier to understand.
