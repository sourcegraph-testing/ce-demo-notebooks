# Find Examples of How Other Developers Use an Object


## Use Case
Developers who are new to a codebase want to follow best practices for how to call functions and pass parameters.


## Discussion
This is a real-world example used by engineers at Sourcegraph (details from  [here](https://sourcegraph.slack.com/archives/C0B2RU51Q/p1632962415328500?thread_ts=1632932165.323900&cid=C0B2RU51Q)).


## Steps
1. Find an example of how to pass a DB object to a function \
**<code>repo:^github\.com/sourcegraph/sourcegraph$ (:[[_]] dbutil.DB) patterntype:structural</code></strong> [[sg](https://sourcegraph.com/search?q=repo:%5Egithub%5C.com/sourcegraph/sourcegraph%24+%28:%5B%5B_%5D%5D+dbutil.DB%29&patternType=structural)]

### Value / Differentiation from other technologies

From Coury:


    _That was the particular query I wrote, that captures function parameters. In general structural search can match parameters so easy with context such as parameter location, etc._


    _This query was just to help me build some context on how other parts of the Sourcegraph codebase were initializing helper code with a provided DB_


#### Tags
#structural-search #go
