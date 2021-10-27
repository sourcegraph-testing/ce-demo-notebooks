## Is XYZ package is in use

## Use Case
I see a security vulnerability on the [CVE](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28168) list that sparks my interest.  I want to quickly see if it applies to our environment.

## Discussion
Since this vulnerability is in a node.js package called axios, you search for where axios is defined in any package.json files.

## Customer Story
This is Capital One's use case.

## Steps

#### Basic literal search
[axios file:package.json repo:github.com/sourcegraph/*](https://sourcegraph.com/search?q=axios+file:package.json+repo:github.com/sourcegraph/*&patternType=regexp)

From these results, right away you can see who is using this package and reach out to them directly.

Comby allows you to get more complex here.  But, you cannot do ">" or "&lt;" (or >=, &lt;=), you can only do "==" and "!=" so it doesn't help us.   See [this example](https://bit.ly/3a7NGb3)

## Value
Customers are able to find potential vulnerabilities quickly. They are also able to see where that particular package is used throughout their codebase.

#### Tags
#node.js #regex-search #security #cve
