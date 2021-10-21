## Java 8 `-> `Java 11 Migration: `sun.misc.*`

### Use Case

I'm going to be doing a migration of some large projects from Java 8 to Java 11.  How can Sourcegraph help me?

### Discussion

There were a lot of [changes between Java 8 and 11](https://docs.oracle.com/en/java/javase/11/migrate/index.html#JSMIG-GUID-7744EF96-5899-4FB2-B34E-86D49B2E89B6).  In particular, there were several packages [removed](https://docs.oracle.com/en/java/javase/11/migrate/index.html#JSMIG-GUID-F7696E02-A1FB-4D5A-B1F2-89E7007D4096).  This example focuses on searching for one [example package that was removed](https://docs.oracle.com/en/java/javase/11/migrate/index.html#JSMIG-GUID-B96BD00F-12A4-493A-9907-2FFE8DA6748C).


### Steps

#### (optional) Basic literal search
[lang:java import sun.misc.Base64Encoder](https://sourcegraph.com/search?q=lang:java%C2%A0import+sun.misc.Base64Encoder&patternType=regexp)]

#### Simple regex search
[lang:java import\s*sun.misc.Base64Encoder](https://sourcegraph.com/search?q=lang:java%C2%A0import%5Cs*sun.misc.Base64Encoder&patternType=regexp)]


#### More complex regex search with and operator
The previous example finds all "`import sun.misc.Base64Encoder`" lines.  However, the developer could have included everything "`import.sun.misc.*`", for example.  And, even though they imported it, they may not have used it.  So we need to look for both an import and a use of the class in the code.

[lang:java import\s*sun.misc.(Base64Encoder|\*) and Base64Encoder](https://sourcegraph.com/search?q=lang:java%C2%A0import%5Cs*sun.misc.%28Base64Encoder%7C%5C*%29+and+Base64Encoder&patternType=regexp)]

## Value
Customers will see value for regex search and it's a good example of using Batch Changes to modify those Java files with the right references. 


#### Tags
```
#java #migration #good-for-batch-changes #regex-search
```


