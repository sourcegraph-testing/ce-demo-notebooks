# Java Security Searches Using Sourcegraph

Security-oriented search examples for Sourcegraph, focused on Java.

#### ECB mode by default cipher—not a best practice:

```sourcegraph
Cipher.getInstance("AES"); lang:java 
```

#### Potential secrets:

```sourcegraph
patterntype:regexp ("[a-z0-9+/]{32,}=?"|'[a-z0-9+/]{32,}=?'|`[a-z0-9+/]{32,}=?`) or -----BEGIN RSA PRIVATE KEY----- or token.+[a-z0-9+/]{32,}=['"]?\n
```

#### Email addresses:

```sourcegraph
([a-z0-9+/\.-]{1,})@([a-z0-9+/\.-]{1,})\.(net|com|org) patternType:regexp
```

#### GPL licenses in source code:

```sourcegraph
gpl license patternType:regexp
```

#### Docker images not pinned to digest:

```sourcegraph
file:dockerfile :latest$ patternType:regexp
```

#### Find a package removed in the Java 8 to 11 transition:

```sourcegraph
lang:java import\s*sun.misc.(Base64Encoder|\*) and Base64Encoder patternType:regexp
```

#### Discover if a CVE-listed vulnerability impacts your code:

[Example vulnerability](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28168) used in this search.

```sourcegraph
axios file:package.json repo:github.com/sourcegraph/*
```

#### Ignored exceptions without clarification:

Can also be used as a monitor to track newly-committed versions of this pattern.

```sourcegraph
lang:java try {...} catch (...) {} patternType:structural
```
