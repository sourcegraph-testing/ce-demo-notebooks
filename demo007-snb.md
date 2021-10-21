## Is XYZ package is in use


```
#node.js #regex-search #security #cve
```



### Use Case

You see a security vulnerability on the [CVE](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28168) list that sparks your interest.  You want to quickly see if it applies to your environment.

Since this vulnerability is in a node.js package called axios, you search for where axios is defined in any package.json files.


### Customer Story

This is Capital One's use case.


### Steps


#### Basic literal search



* **<code>axios file:package.json repo:github.com/sourcegraph/* </code></strong>[[sg](https://sourcegraph.com/search?q=axios+file:package.json+repo:github.com/sourcegraph/*&patternType=regexp)]

    From these results, right away you can see who is using this package and reach out to them directly.


    Comby allows you to get more complex here.  But, you cannot do ">" or "&lt;" (or >=, &lt;=), you can only do "==" and "!=" so it doesn't help us.   See [this example](https://bit.ly/3a7NGb3)



