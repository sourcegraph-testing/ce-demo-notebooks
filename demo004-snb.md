## Unimplemented Java Exception Handler (i.e., empty catch block)

## Use Case
We'd like to find all instances of Java code where a developer has ignored an exception and has not commented on why it is ignored.


## Discussion
Sometimes developers will catch an exception in Java but not implement something to handle it.  This is common because you have to handle it somewhere (either update the method signature to indicate it is thrown or catch it and handle it in the function).  A quick fix is to add a try/catch block and "come back later" to implement it.  This is often forgotten and is left in the code.  The problem with this is that that error could mean something and, at the very least, should probably  be logged or a comment be added to let other developers know why it's ignored.

## Steps

#### (optional) Attempt with regex
[lang:java try\s*{.*}\s*catch\s*(.*)\s*{\s*}](https://demo.sourcegraph.com/search?q=lang:java+try%5Cs*%7B.*%7D%5Cs*catch%5Cs*%28.*%29%5Cs*%7B%5Cs*%7D+&patternType=regexp)]

This doesn't catch anything where there are new lines after the {, for example.  There are a few other examples that are missed as well.

[lang:java try\s*{\s*.*\s*}\s*catch\s*(.*)\s*{\s*}](https://demo.sourcegraph.com/search?q=lang:java+try%5Cs*%7B%5Cs*.*%5Cs*%7D%5Cs*catch%5Cs*%28.*%29%5Cs*%7B%5Cs*%7D&patternType=regexp)]

This search picks up all the missing results due to whitespace.

#### Structural Search
[lang:java try {...} catch (...) {}](https://demo.sourcegraph.com/search?q=lang:java+try+%7B...%7D+catch+%28...%29+%7B%7D+&patternType=structural)]

## Value
Customers will see how powerful structural search can be with this. It demos really effectively. 


#### Tags
#java #structural-search #code-monitoring
