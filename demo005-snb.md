# Look for switch statement in Go

## Use Case
We want to see all the switch/case statements in my Go code.  Show me how to write a good switch/case in Go.

## Discussion
An engineer is looking for a code example and instead of reaching out to senior developers, Sourcegraph allows them to be self sufficent. 

## Steps

#### Structural Search
[switch :[_] := :[_].(type) { :[string] } lang:go](https://demo.sourcegraph.com/search?q=switch+:%5B_%5D+:%3D+:%5B_%5D.%28type%29+%7B+:%5Bstring%5D+%7D+lang:go&patternType=structural)]

## Value
This can be valuable for onboarding or code example purposes. If a new engineer wants to know how about particular patters within a codebase. 

#### Tags
#structural-search #onboarding #code-example

