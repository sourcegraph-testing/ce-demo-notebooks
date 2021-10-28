## GraphQL API Consumer


### Use Case
I am about to make a change to the implementation of a specific API and want to know all the clients of the API so you can make sure you won't impact anything.


### Description
GraphQL is a query language for APIs to describe how to [query](https://graphql.org/learn/queries/) and [manipulate](https://graphql.org/learn/queries/#mutations) data on the server.


### Steps


#### GraphQL Schema
* [Direct Link](https://demo.sourcegraph.com/github.com/sourcegraph/sourcegraph/-/blob/cmd/frontend/graphqlbackend/schema.graphql)

    This is a direct link to the schema file.  But, it's probably better to get there by searching :).

* **<code>repo:^github\.com/sourcegraph/* lang:graphql schema </code></strong>[[sg](https://demo.sourcegraph.com/search?q=repo:%5Egithub%5C.com/sourcegraph/*+lang:graphql+schema&patternType=literal)]

    If you leave off "schema" you'll see a few other GraphQL schema files.  It's easy to get to the right one this way too (it's called <strong><code>schema.graphql</code></strong> in <strong><code>sourcegraph/sourcegraph</code></strong> repo)



#### Find the API
- Open schema.graphql in sourcegraph/sourcegraph repo
- Scroll down to the API you are going to use for this demo.  I like the reateCodeMonitor mutation.  But, there are others in there that are just as good to use.


#### Code Intelligence
- Hover over the API and show the code intel features
- Click on the "**<code>Find references</code></strong>" link to open all the references to this API.

    <strong><span style="text-decoration:underline;">NOTE</span></strong>: This is a search-based result so make sure you pick a relatively unique API name.



#### Review the Callers
* Scroll through the results and find the Typescript results that are interesting.  For the **<code>createCodeMonitor </code></strong>example, you are looking for the result on <strong><code>CreateCodeMonitorPage.tsx</code></strong> (Line 20).



<p id="gdcalert2" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image2.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert3">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image2.png "image_tooltip")


## Value

#### Tags
#graphql #api #typescript



