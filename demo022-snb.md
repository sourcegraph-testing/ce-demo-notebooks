# Cross repository code intelligence


## Use Case
Some functions will have cross dependencies where functions are defined and referenced in other repositories.


## Discussion
These are 3 different examples in different languages that will show code that is being used in a file and referenced in many other repositories while being defined in a main repository. The idea here is that you will be able to pull up an example of an implemented dependency (**<code>putIfAbsent, AxiosInstance, or multierror</code></strong>) and show that not only is it used in other repositories, but the definition is not in the original repository you found it in.


## Steps

#### Java - [loom link](https://www.loom.com/share/446e0fc1df3d4bc4bf7bb6bd044573bc)
[repo:^github\.com/Netflix/Hystrix$ file:^hystrix-core/src/main/java/com/netflix/hystrix/HystrixRequestCache\.java](https://sourcegraph.com/github.com/Netflix/Hystrix/-/blob/hystrix-core/src/main/java/com/netflix/hystrix/HystrixRequestCache.java#L77:40)
* Make sure you are in the file
* Highlight putIfAbsent (~line 80)
* Click on Find References and in the drawer that opens up make sure to select Show other repositories
    * This shows cross repository references of putIfAbsent
* Click on Definitions in the drawer navigation to see the definition of putIfAbsent


#### Javascript - [loom link](https://www.loom.com/share/a2ef32a776624186a6c7b67387388b47)
[repo:^github\.com/grafana/grafana$@78d53c5 file:^packages/grafana-toolkit/src/cli/utils/githubClient\.ts](https://sourcegraph.com/github.com/grafana/grafana@78d53c5/-/blob/packages/grafana-toolkit/src/cli/utils/githubClient.ts)
* Make sure you are in the file
* Highlight AxiosInstance (~line 22)
* Click on Find References and in the drawer that opens up make sure to select Show other repositories
    * This shows cross repository references of AxiosInstance
* Click on Definitions in the drawer navigation to see the definition of AxiosInstance


#### Go - [loom link](https://www.loom.com/share/b5c54fc898df4f20969a8e8969e4c475)
* Sourcegraph implements hashicorp’s multierror repository
[repo:^github\.com/hashicorp/packer$@27d89ac file:^packer/core\.go](https://sourcegraph.com/github.com/hashicorp/packer@27d89ac/-/blob/packer/core.go)]
* Make sure you are in the file
* See how ~line 16 we are including multierror "github.com/hashicorp/go-multierror"
* Highlight multierror.Append (~line 730)
* Click on Find References and in the drawer that opens up make sure to select Show other repositories
    * This shows cross repository references of Append
* Click on Definitions in the drawer navigation to see the definition of Append


## Value
Customers are able to use cross repo code intelligence that they'd normally only get out of an IDE, but they'll get it in a centralized location.

#### Tags
#cross-repository #go #javascript #java #code-intelligence
