# Find all usages of 2 similarly named packages


## Use Case
It's difficult to find where specific packages are used in code, especially if the package is named using a common word, like "errors".  In this example, we use structural search to find everywhere in Sourcegraph's Go code where 2 different, but similarly named packages are imported.


## Description
This is a real-world example used by engineers at Sourcegraph (details and recorded video from   [here](https://sourcegraph.slack.com/archives/C0B2RU51Q/p1632932165323900)).

Sourcegraph had 2 packages named "errors" in v3.25.  This was causing confusion.  So, developers used Sourcegraph to find all locations where each package was used.  From there, they can reduce the usage to a single package and eliminate the extra one.


## Steps


#### Prep
1. Open up a file that imports the first errors package [github.com/cockroachdb/errors](https://sourcegraph.com/github.com/sourcegraph/sourcegraph@3.25/-/blob/internal/encryption/cloudkms/cloud_kms.go?L11:32)
You can get to the file by searching for
repo:^github\.com/sourcegraph/sourcegraph$@3.25 file:^internal/encryption/cloudkms/cloud_kms\.go
2. Open up a different file that imports the second errors package [errors](https://sourcegraph.com/github.com/sourcegraph/sourcegraph@3.25/-/blob/cmd/frontend/graphqlbackend/symbols.go?L5:3)
You can get to the file by searching for repo:^github\.com/sourcegraph/sourcegraph$@3.25 file:^cmd/frontend/graphqlbackend/symbols\.go$


#### Structural Search Demo
1. Find all locations where you are using the `"github.com/cockroachdb/errors"`  package: \
**<code>repo:^github\.com/sourcegraph/sourcegraph$@3.25 lang:go import (... "github.com/cockroachdb/errors" ...) count:1000 patterntype:structural </code></strong>[[sg](https://sourcegraph.com/search?q=context:global+repo:%5Egithub%5C.com/sourcegraph/sourcegraph%24%403.25+lang:go+import+%28...+%22github.com/cockroachdb/errors%22+...%29+count:1000&patternType=structural)]
2. Find all locations where you are using the <code>"errors"</code> package: \
<strong><code>repo:^github\.com/sourcegraph/sourcegraph$@3.25 lang:go import (... "errors" ...) count:1000 patterntype:structural</code></strong> [[sg](https://sourcegraph.com/search?q=context:global+repo:%5Egithub%5C.com/sourcegraph/sourcegraph%24%403.25+lang:go+import+%28...+%22errors%22+...%29+count:1000&patternType=structural)]
3. (optional) You can also combine these into one query using the <strong><code>OR</code></strong> operator: \
<strong><code>repo:^github\.com/sourcegraph/sourcegraph$@3.25 lang:go import (... "github.com/cockroachdb/errors" ...) or import (... "errors" ...) count:1000 patterntype:structural </code></strong>[[sg](https://sourcegraph.com/search?q=context:global+repo:%5Egithub%5C.com/sourcegraph/sourcegraph%24%403.25+lang:go+import+%28...+%22github.com/cockroachdb/errors%22+...%29+or+import+%28...+%22errors%22+...%29+count:1000&patternType=structural)]

## Value / Differentiation from other technologies
Because the packages are named "errors" (a commonly used term in source code) it is difficult to rely on simple grep-like (or literal search in Sourcegraph) techniques.  These approaches will find many false positives.  Using regular expressions is possible but also difficult because, for example, the packages can span multiple lines.

#### Tags
#structural-search #go

