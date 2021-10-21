# Java 8 -> Java 11 Migration: sun.misc.

#java #migration #good-for-batch-changes #regex-search

## Use Case

I'm going to be doing a migration of some large projects from Java 8 to Java 11. How can Sourcegraph help me?

## Discussion

There were a lot of changes between Java 8 and 11. In particular, there were several packages removed. This example focuses on searching for one example package that was removed.

## Steps

#### Basic literal search (optional) 
[lang:java import sun.misc.Base64Encoder](https://sourcegraph.com/search?q=lang:java%C2%A0import+sun.misc.Base64Encoder&patternType=regexp)

```sourcegraph
lang:java import sun.misc.Base64Encoder
```

#### Simple regex search
[lang:java import\s*sun.misc.Base64Encoder](https://sourcegraph.com/search?q=lang:java%C2%A0import%5Cs*sun.misc.Base64Encoder&patternType=regexp)

#### More complex regex search with and operator

The previous example finds all "import sun.misc.Base64Encoder" lines. However, the developer could have included everything "import.sun.misc.*", for example. And, even though they imported it, they may not have used it. So we need to look for both an import and a use of the class in the code.

[lang:java import\s*sun.misc.(Base64Encoder|\*) and Base64Encoder](https://sourcegraph.com/search?q=lang:java%C2%A0import%5Cs*sun.misc.%28Base64Encoder%7C%5C*%29+and+Base64Encoder&patternType=regexp)
