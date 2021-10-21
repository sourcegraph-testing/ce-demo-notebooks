# Sourcegraph Demo Repository

The intention of this document is to provide a repository of "good" searches to help demonstrate Sourcegraph to prospects.  Ideally, each snippet includes what repo to use to show something off well (e.g., "if you use this repo it has XYZ example line in it that shows structural search well").


*Should these be good searches or demos (which might center around search of course) ?*

## Demo template

### Demo Title

### Sourcegraph Value

Outline the value of Sourcegraph, compare and contrast with other solutions or options.

### Use Case

Brief descritpion of high level use case. What is the objective of this demo? What are we trying to demonstrate, for example a specific piece of sourcegraph functionality or preferably a use case that a user is likely to encounter.

### Talk Track

Talk track should enable a CE to deliver the demo, ensuring that the key challenges and capabilities are highlighted. It does not need to be verbose but should not assume the a CE is fully farmiliar with use case in question. The talk track should tell a story.

### Demo Steps

This should include any setup (sourcegraph version, configuration, required repositories) needed to run the demo. Could of course include screenshots where these are useful.

### Future work

How could extend or enhance this demo?

### Tags

All relevant tags that enable CE to find relevant demos (how to search on tags in markdown? :) )





## Demos Needed

This list should be updated whenever you need a good demo for a specific use case



* Microservice
    * Show impact of making a change in one microservice (who are the callers of this)
    * Potentially use [https://github.com/netflix/genie](https://github.com/netflix/genie)
* Jenkins 
    * Potentially something around searching for things in a [Jenkinsfile](https://www.jenkins.io/doc/book/pipeline/jenkinsfile/)
    * examples
        * file:Jenksinfile stage(...) patterntype:structural
        * file:Jenkinsfile stage\s*(...) patterntype:structural
        * file:Jenkinsfile stage\s*[\(]*'\w*'[\)]* patterntype:regex
* Inner sourcing
    * example search + code monitoring + code insights
* Package dependencies (who is using a given package; e.g., maven or node.js packages)


## Java 8 `-> `Java 11 Migration: `sun.misc.*`


```
#java #migration #good-for-batch-changes #regex-search
```



### Use Case

I'm going to be doing a migration of some large projects from Java 8 to Java 11.  How can Sourcegraph help me?


### Discussion

There were a lot of [changes between Java 8 and 11](https://docs.oracle.com/en/java/javase/11/migrate/index.html#JSMIG-GUID-7744EF96-5899-4FB2-B34E-86D49B2E89B6).  In particular, there were several packages [removed](https://docs.oracle.com/en/java/javase/11/migrate/index.html#JSMIG-GUID-F7696E02-A1FB-4D5A-B1F2-89E7007D4096).  This example focuses on searching for one [example package that was removed](https://docs.oracle.com/en/java/javase/11/migrate/index.html#JSMIG-GUID-B96BD00F-12A4-493A-9907-2FFE8DA6748C).


### Steps


#### (optional) Basic literal search



* **<code>lang:java import sun.misc.Base64Encoder </code></strong>[[sg](https://sourcegraph.com/search?q=lang:java%C2%A0import+sun.misc.Base64Encoder&patternType=regexp)]


#### Simple regex search



* **<code>lang:java import\s*sun.misc.Base64Encoder </code></strong>[[sg](https://sourcegraph.com/search?q=lang:java%C2%A0import%5Cs*sun.misc.Base64Encoder&patternType=regexp)]


#### More complex regex search with and operator

The previous example finds all "`import sun.misc.Base64Encoder`" lines.  However, the developer could have included everything "`import.sun.misc.*`", for example.  And, even though they imported it, they may not have used it.  So we need to look for both an import and a use of the class in the code.



* **<code>lang:java import\s*sun.misc.(Base64Encoder|\*) and Base64Encoder </code></strong>[[sg](https://sourcegraph.com/search?q=lang:java%C2%A0import%5Cs*sun.misc.%28Base64Encoder%7C%5C*%29+and+Base64Encoder&patternType=regexp)]


## Find Secrets and Tokens


```
#language-agnostic #security #good-for-code-monitoring
```



### Use Case

You are looking through your code for any private keys or things that look like tokens.


### Steps


#### Regex Search



* **<code>("[a-z0-9+/]{32,}=?"|'[a-z0-9+/]{32,}=?'|`[a-z0-9+/]{32,}=?`) or -----BEGIN RSA PRIVATE KEY----- or token.+[a-z0-9+/]{32,}=['"]?\n lang:go </code></strong>[[sg](https://sourcegraph.com/search?q=+%28%22%5Ba-z0-9%2B/%5D%7B32%2C%7D%3D%3F%22%7C%27%5Ba-z0-9%2B/%5D%7B32%2C%7D%3D%3F%27%7C%60%5Ba-z0-9%2B/%5D%7B32%2C%7D%3D%3F%60%29+or+-----BEGIN+RSA+PRIVATE+KEY-----+or+token.%2B%5Ba-z0-9%2B/%5D%7B32%2C%7D%3D%5B%27%22%5D%3F%5Cn+lang:go&patternType=regexp)]
* <strong><code>(key|secret|token)-[\w+]{32,}</code></strong>


## Pin Dockerfile Base Image


```
#language-agnostic #security #good-for-batch-changes #good-for-code-monitoring
```



### Use Case

Security Engineers or DevOps teams want to find all Dockerfiles that are using a "FROM &lt;baseimage>:latest" rather than a specific tag or SHA256 reference.

This is outlined in [Snyk's top 10 security best practices for Docker](https://snyk.io/blog/10-docker-image-security-best-practices/) (see #6).


### Description

This example is a great one to use for searching plus campaigns and code monitoring.  It is quick to run and very easy to understand.


### Steps


#### Basic Regex



* **<code>file:/Dockerfile FROM\s+.*:latest </code></strong>[[sg](https://demo.sourcegraph.com/search?q=file:/Dockerfile+FROM%5Cs%2B.*:latest&patternType=regexp)]

    This example is super easy to remember and to type when doing a quick demo with someone.  But it isn't quite as accurate as it needs to be.  For example, this will actually find results that are already pinned to a specific SHA256 (because we stopped at :latest).



#### More Accurate Regex



* **<code>file:/Dockerfile FROM (\w+\/)?\w+:latest($|\s) </code></strong>[[sg](https://demo.sourcegraph.com/search?q=file:/Dockerfile+FROM+%28%5Cw%2B%5C/%29%3F%5Cw%2B:latest%28%24%7C%5Cs%29&patternType=regexp)]


## Unimplemented Java Exception Handler (i.e., empty catch block)


```
#java #structural-search #good-for-code-monitoring
```



### Use Case

Find all instances of Java code where a developer has ignored an exception and has not commented on why it is ignored.


### Discussion

Sometimes developers will catch an exception in Java but not implement something to handle it.  This is common because you have to handle it somewhere (either update the method signature to indicate it is thrown or catch it and handle it in the function).  A quick fix is to add a try/catch block and "come back later" to implement it.  This is often forgotten and is left in the code.  The problem with this is that that error could mean something and, at the very least, should probably  be logged or a comment be added to let other developers know why it's ignored.


### Steps


#### (optional) Attempt with regex



* **<code>lang:java try\s*{.*}\s*catch\s*(.*)\s*{\s*} </code></strong>[[sg](https://demo.sourcegraph.com/search?q=lang:java+try%5Cs*%7B.*%7D%5Cs*catch%5Cs*%28.*%29%5Cs*%7B%5Cs*%7D+&patternType=regexp)]

    This doesn't catch anything where there are new lines after the {, for example.  There are a few other examples that are missed as well.

* **<code>lang:java try\s*{\s*.*\s*}\s*catch\s*(.*)\s*{\s*} </code></strong>[[sg](https://demo.sourcegraph.com/search?q=lang:java+try%5Cs*%7B%5Cs*.*%5Cs*%7D%5Cs*catch%5Cs*%28.*%29%5Cs*%7B%5Cs*%7D&patternType=regexp)]

    This search picks up all the missing results due to whitespace.



#### Structural Search



* **<code>lang:java try {...} catch (...) {} </code></strong>[[sg](https://demo.sourcegraph.com/search?q=lang:java+try+%7B...%7D+catch+%28...%29+%7B%7D+&patternType=structural)]


## Look for switch statement in Go


### Use Case

Show me all the switch/case statements in my Go code.  Show me how to write a good switch/case in Go.


### Steps


#### Structural Search



* **<code>switch :[_] := :[_].(type) { :[string] } lang:go </code></strong>[[sg](https://demo.sourcegraph.com/search?q=switch+:%5B_%5D+:%3D+:%5B_%5D.%28type%29+%7B+:%5Bstring%5D+%7D+lang:go&patternType=structural)]


## fmt.Sprintf() -> strconv.Itoa()


```
#go #structural-search #good-for-batch-changes #good-for-code-monitoring #movie-trailer
```



### Use Case

You want to clean up your code and remove inefficient function calls.  One example of that is code that uses fmt.Sprintf() to convert a number to a string.  It's more efficient to use itoa function for that.


### Discussion

You need to use sourcegraph.com/search for this because the examples required to prove this out are in repos that are not yet on demo.  I added a simple example in my own repo (mike-r-mclaughlin/golang-examples).  But, better to have more real-world examples from other projects that are not loaded on demo.  To be specific, you can see examples in [gravitational/teleport repo](https://sourcegraph.com/github.com/gravitational/teleport).

Code [Example](https://sourcegraph.com/github.com/mike-r-mclaughlin/golang-examples/-/blob/hello.go):


<table>
  <tr>
   <td><code> 1</code>
<p>
<code> 2</code>
<p>
<code> 3</code>
<p>
<code> 4</code>
<p>
<code> 5</code>
<p>
<code> 6</code>
<p>
<code> 7</code>
<p>
<code> 8</code>
<p>
<code> 9</code>
<p>
<code>10</code>
<p>
<code>11</code>
<p>
<code>12</code>
<p>
<code>13</code>
<p>
<code>14</code>
<p>
<code>15</code>
   </td>
   <td><strong><code>package main</code></strong>
<strong><code>import "fmt"</code></strong>
<strong><code>func main() {</code></strong>
<code>	<strong>var</strong> a_number = 4321</code>
<code>	<strong>var</strong> a_number_as_str = fmt.Sprintf("%d", a_number)</code>
<code>	a_number_as_str = fmt.Sprintf ("%d", a_number)</code>
<p>
<code>	a_number_as_str = fmt.Sprintf( "%d", a_number)</code>
<p>
<code>	a_number_as_str = fmt.Sprintf(</code>
<p>
<code>		"%d", a_number)</code>
<p>
<code>	fmt.Printf("The value is %s\n", a_number_as_str)</code>
<p>
<code>	a_number_as_str = fmt.Sprintf(</code>
<p>
<code>		<em>// convert the number + 10 to a string</em></code>
<code>		"%d", a_number + 10)</code>
<p>
<code>	fmt.Printf("The new value is %s\n", a_number_as_str)</code>
<p>
<code>}</code>
   </td>
  </tr>
</table>



### Steps


#### (optional) Basic literal search



* **<code>fmt.Sprintf("%d" lang:go</code></strong> [[sg](https://sourcegraph.com/search?q=fmt.Sprintf%28%22%25d%22+lang:go&patternType=literal)]


#### Simple regex search 



* **<code>fmt.Sprintf\("%d" lang:go</code> </strong>[[demo sg](https://demo.sourcegraph.com/search?q=fmt.Sprintf%5C%28%22%25d%22+lang:go&patternType=regexp)][[sg](https://sourcegraph.com/search?q=fmt.Sprintf%5C%28%22%25d%22+lang:go&patternType=regexp)]

    The basic literal search is identical to this one. 



#### More complex regex search



* **<code>fmt.Sprintf\s*\(\s*"%d" lang:go</code></strong> [[sg](https://sourcegraph.com/search?q=fmt.Sprintf%5Cs*%5C%28%5Cs*%22%25d%22+lang:go+&patternType=regexp)]

    This regex is attempting to show that some developers add new lines or whitespace before or after the '('.  An example of what this catches is [here](https://sourcegraph.com/search?q=fmt.Sprintf%5Cs*%5C%28%5Cs%2B%22%25d%22+lang:go+repo:mike-r-mclaughlin/golang-examples&patternType=regexp) and highlighted below:


    ```
package main
import "fmt"
func main() {
	var a_number = 4321
	var a_number_as_str = fmt.Sprintf("%d", a_number)
	a_number_as_str = fmt.Sprintf ("%d", a_number)
	a_number_as_str = fmt.Sprintf( "%d", a_number)
	a_number_as_str = fmt.Sprintf(
		"%d", a_number)
	fmt.Printf("The value is %s\n", a_number_as_str)
	a_number_as_str = fmt.Sprintf(
		// convert the number + 10 to a string
		"%d", a_number + 10)
	fmt.Printf("The new value is %s\n", a_number_as_str)
}
```



    If you run this query on sourcegraph.com/search, it will return _a lot_ of results.  You can limit the number of results to show the example by switching <span style="text-decoration:underline;">one</span> of the `/s*` to `/s+` (one or more whitespace characters e.g., **<code>fmt.Sprintf\s*\(\s+"%d" lang:go</code></strong> [[sg](https://sourcegraph.com/search?q=fmt.Sprintf%5Cs*%5C%28%5Cs%2B%22%25d%22+lang:go+&patternType=regexp)]).


    However, this search will <span style="text-decoration:underline;">NOT</span> find line 11-13 (with a comment above the first argument).  <span style="text-decoration:underline;">In order to get this example, your regex becomes very complicated and hard to debug.  But, with structural search, it's easy.</span>



#### "Simple" Structural Search



* **<code>fmt.Sprintf(..."%d", ...) repo:mike-r-mclaughlin/golang-examples </code></strong>[[sg](https://sourcegraph.com/search?q=+fmt.Sprintf%28...%22%25d%22%2C+...%29+repo:mike-r-mclaughlin/golang-examples&patternType=structural)]

    This search will find the example in line 11-13.  The "..." in front of "%d" is required because of the new line.


    

<p id="gdcalert1" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image1.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert2">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image1.png "image_tooltip")




### *TODO* Example N: 

TODO .... TODO ... TODO ...

search for other examples in go that have a function call followed by a new line followed by a comment block: [https://sourcegraph.com/search?q=lang:go+%5C%28%5Cs*//+and+not+const+and+not+var+repo:sourcegraph&patternType=regexp](https://sourcegraph.com/search?q=lang:go+%5C%28%5Cs*//+and+not+const+and+not+var+repo:sourcegraph&patternType=regexp)


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



## SQL Injection


```
#go #type:symbol-search #security
```



### Discussion

This example comes from one of the security engineers on the Sourcegraph team (link to GitHub ticket to be added once available).  The background on this is that you're a security engineer who supports many different projects and you are not deeply familiar with any of them but rather have a breadth of knowledge on each.  So, when you are assigned a ticket you don't know exactly which repository the code lives in and you don't know the impact of any changes you will make. 


### Use Case

There was a SQL injection vulnerability identified when calling the [OverwriteSettings API](https://sourcegraph.com/github.com/sourcegraph/sourcegraph@e95e853c19d83ca36e211ae1a29085d889df53b1/-/blob/cmd/frontend/graphqlbackend/schema.graphql#L2606).

The security engineer is not familiar with all of the code.  When a vulnerability ticket comes in, he uses Sourcegraph to identify the root cause and fix it.


### Steps


#### Find the API

**<code>repo:^github\.com/sourcegraph/* OverwriteSettings type:symbol lang:go </code></strong>[[sg](https://sourcegraph.com/search?q=repo:%5Egithub%5C.com/sourcegraph/*%C2%A0OverwriteSettings%C2%A0type:symbol%C2%A0lang:go%C2%A0&patternType=regexp)]


#### Hunt for the Vulnerability

We've found the API call itself.  But, the SQL is not generated here.  We need to work our way through the code to find the actual problem point.



1. Click on the result in **<code>[settings_mutation.go](https://sourcegraph.com/github.com/sourcegraph/sourcegraph/-/blob/cmd/frontend/graphqlbackend/settings_mutation.go#L162:28-162:45)</code></strong>
2. Hover over <strong><code>settingsCreateIfUpToDate</code></strong> and [Go to Definition](https://sourcegraph.com/github.com/sourcegraph/sourcegraph/-/blob/cmd/frontend/graphqlbackend/settings.go#L60:6)
3. Scroll down to <strong><code>database.GlobalSettings.CreateIfUpToDate</code></strong> [Go to Definition](https://sourcegraph.com/github.com/sourcegraph/sourcegraph/-/blob/internal/database/settings.go#L57:24)
4. Scroll down to the code where you see the "<strong><code>INSERT INTO</code></strong>" SQL statement being generated (currently around [line 104](https://sourcegraph.com/github.com/sourcegraph/sourcegraph@e95e853c19d83ca36e211ae1a29085d889df53b1/-/blob/internal/database/settings.go#L104:5))

This is where the issue exists (the input is coming directly from the user data submitted in the API) and it needs to be escaped properly before being inserted into the SQL statement.


#### Fix the Vulnerability

Now that you've found the issue, you can use the IDE integration to open up the file and fix the issue.


#### Write a Test

Now that you've fixed the issue you want to write a test to verify it and make sure it never happens again.  However, because you are unfamiliar with the codebase, you don't know how to write a proper test.  So, you use Sourcegraph to find an example test that has all the proper setup and teardown logic.


## Error Message Hunting


```
#go #incident-response #regex-search
```



### Discussion

A common use case for Sourcegraph is for DevOps teams to search for an error they found in a log.  These teams rarely know the entire codebase well enough to know exactly which repository something is in. 


### Use Case

The application crashed.  In the error, you see a log entry that says: "ERROR: master id empty".   You need to identify the root cause and fix it (or figure out who to contact).


### Steps


#### (Optional) Simple literal search

Search for the exact match you found in the log.  You realize after seeing the results, though, that "master" is likely a branch name.

**<code>repo:github.com/sourcegraph/ master id empty </code></strong>[[sg](https://sourcegraph.com/search?q=repo:github.com/sourcegraph/*+master+id+empty&patternType=literal)]


#### Simple literal search

**<code>repo:github.com/sourcegraph/* id empty </code></strong>[[sg](https://sourcegraph.com/search?q=repo:github.com/sourcegraph/*+id+empty&patternType=literal)]

This gives you a lot of results because there are a lot of things that match like "inval**id empty** JSON".  You really want to find the exact error.


#### Complex regex search

Since you want to find the exact error message, you need to switch to regex because the string could be "%s id empty" or it could be branchName + "id empty", etc. 

So, you change your search to look for a quote (") followed by by "id empty" or white space (\s+):

**<code>repo:^github\.com/sourcegraph/ (\s+|"|')id\s*empty </code></strong>[[sg](https://sourcegraph.com/search?q=repo:%5Egithub%5C.com/sourcegraph/+%28%5Cs%2B%7C%22%7C%27%29id%5Cs*empty&patternType=regexp)]


## Site Down / War Room Session


```
#type:diff-search #type:commit-search #incident-response
```



### Use Case

Your site/application went down and you want to know what recently changed that might have caused the outage.  You saw an error message about XYZ right before the crash.  You want to figure out _quickly_ who to bring into a war room and who should be paged, etc.  And, what else might be impacted by this.


### Discussion

The beauty of Sourcegraph and search is that it's super easy to jump in and get to an answer quickly and on your own.  You don't need to waste everyone's time by paging all group leaders into a war room.  And, then figuring out which repo a specific error message is.  You can know exactly who to call and which projects are impacted.


### Steps


#### Commit search (High level what changed)

**<code>repo:github.com/sourcegraph/sourcegraph type:commit </code></strong>[[sg](https://sourcegraph.com/search?q=repo:github.com/sourcegraph/sourcegraph+type:commit&patternType=literal)]


#### Diff search (Which modules changed recently)

**<code>repo:github.com/sourcegraph/sourcegraph type:diff </code></strong>[[sg](https://sourcegraph.com/search?q=repo:github.com/sourcegraph/sourcegraph+type:diff&patternType=literal)]


#### Diff search (last 3 days only)

**<code>repo:github.com/sourcegraph/sourcegraph type:diff after:"3 days ago" </code></strong>[[sg](https://sourcegraph.com/search?q=repo:github.com/sourcegraph/sourcegraph+type:diff+after:%223+days+ago%22&patternType=literal)]


## Converting ES6 Javascript Function to Arrow Functions with Batch Changes


```
#javascript #structural-search #batch-changes
```



### Use Case

Let's say for example a UiPath Engineering Team had the goal of wanting to migrate all of their js/tsx repos from ES6  functions declarations to Arrow Function declarations. How would they accomplish this?




### Description

e.g.

function sumFunc(params) {}  to const sumFunc = (params) => { }

async function sumFunc(params)  {}  to const sumFunc = async (params) = > {}

Doing this without batch changes:



1. Run search in your code host or in your IDE
    1. May not return all or exact matches for code block - does it support structural search?
2. Based on search results, generate a list of impacted repos
3. Pull each repo down locally
4. Find all occurrences of the necessary change
5. Update/Replace
    2. If using a script to do this: 
        1. Write
        2. Test
        3. Debug
6. Repeat step 4-5 for each repo
7. Manually push changes to code host
8. PRS are opened

^ This is a slow and difficult way to track progress and implement large-scale changes across the codebase.

Doing this with batch changes:



1. Write a batch changes spec that points to all the instances where JS functions are declared in the codebase ( can be done with structural search to ensure precision )
2. Run the spec in SRC CLI
3. Preview, and apply changes being made
4. Confirm it looks good 
5. Publish 
6. PRS are opened, and progress can be tracked through burn down chart


### Steps

**1. **[**Search**] 

Run initial search [query](https://sourcegraph.com/search?q=repo:%5Egithub%5C.com/UiPath+lang:JavaScript++:%5B%7E%5Efunction%5D+:%5Bfn%7E%5Cw%2B%5D%28...%29+&patternType=structural) against UiPath repositories to get a sense of the breadth of usage -- how often are regular function declarations used in their codebase: 

2. **[Automate]**

Create batch spec, preview, and apply changes to the codebase using SRC CLI

[https://demo.sourcegraph.com/users/manuel/batch-changes/convert-JSfunctions-to-arrow-functions](https://demo.sourcegraph.com/users/manuel/batch-changes/convert-JSfunctions-to-arrow-functions)

Once the changes have been made notify code owners via batch operations such as bulk comments. This allows you to comment on all selected changesets. This can be particularly useful for pinging people, reminding them to take a look at the changeset.

There are several instances of this style of function declarations still being used in various repos; I need to update them as quickly and easily as possible and notify the owners of that code that this change is being made. 

3. **[Automate]**

Create a code monitoring alert to notify when the old style of function declaration has been reintroduced into the codebase, to apply changes to convert to arrow function declarations.

4. [**Understand**] 

Create a Code Insight of what currently exists in the codebase for both regular function declarations vs arrow function. (This provides an understanding of the high-level overview of the team’s progress towards success in their efforts to complete this migration.)


## Python 2 `->` 3 Migration


```
#python #type:good-for-campaigns #migration #structural-search
```



### Use Case

We're moving a large project from Python 2 to Python 3.


### Discussion

Python 2 is being deprecated.  The docs outline how to [migrate a project from v2 to v3](https://docs.python.org/3/library/2to3.html).

Examples of the code we want to swap: [https://sourcegraph.com/refactor-python2-to-3](https://sourcegraph.com/refactor-python2-to-3); you can use search to find and change these, insights to track the pattern, and a batch change to run 2to3: https://docs.python.org/3/library/2to3.html


### Steps

TODO


## Java Misused Week Year


```
#java #good-for-batch-changes
```



### Use Case

Java developers sometimes [use "YYYY" when they mean to use "yyyy"](https://errorprone.info/bugpattern/MisusedWeekYear).  Teams need a way to find all instances of this and quickly replace them.  And, monitor the code for developers that check code in like this.

[Sonar Rule [RSPEC-3986](https://rules.sonarsource.com/java/RSPEC-3986)]


### Description

Java uses [pattern letters](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/text/SimpleDateFormat.html) to allow developers to format a date/time to their desired format.  There are two different ways of representing a year: the calendar year and the week year.  Y (uppercase Y) date format represents the "week year" while y (lowercase y) represents the calendar year.  

While the calendar year is straightforward to understand, the week year takes some explanation.  Every year has 52 weeks (defined as Monday - Sunday or Sunday - Saturday, etc.).  If you number each week from 1 to 52, this numbered week represents the "week of year".  Weeks 2-51 are fairly easy to define and the days in those weeks will always be contained in the same calendar year.   However, one of either the last week of a year or the first week of the new year will almost always overlap with days from the prior year or start of the new year.  

It's easiest to look at an example of this.  Below are the months December 2020 and January 2021 which we'll use to explain the problem.  


<table>
  <tr>
   <td><strong>December 2020</strong>
   </td>
   <td><strong>January 2021</strong>
   </td>
  </tr>
  <tr>
   <td><code>Wk# Su Mo Tu We Th Fr Sa </code>
<p>
<code>49         1  2  3  4  5 </code>
<p>
<code>50   6  7  8  9 10 11 12 </code>
<p>
<code>51  13 14 15 16 17 18 19 </code>
<p>
<code>52  20 21 22 23 24 25 26 </code>
<p>
<code> 1  27 28 29 30 31 </code>
   </td>
   <td><code>Wk# Su Mo Tu We Th Fr Sa </code>
<p>
<code> 1                  1  2 </code>
<p>
<code> 2   3  4  5  6  7  8  9 </code>
<p>
<code> 3  10 11 12 13 14 15 16 </code>
<p>
<code> 4  17 18 19 20 21 22 23 </code>
<p>
<code> 5  24 25 26 27 28 29 30 </code>
<p>
<code> 6  31 </code>
   </td>
  </tr>
</table>


The "week number" is abbreviated "Wk#" in the above calendar.  In this example, we used the definition that the first week (Wk1), begins on the week that has January 1.  However, there are other ways to define week 1 like the [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601#Week_dates) definition which are more complex.  

Regardless of how you define "week 1 (Wk1)", there will almost always be one week where there are days of the week that have a "week year" that are different from the calendar year.  In the above example, WEEK 1 of 2021 includes 5 days from 2020.

So, if you format a date using the pattern "`YYYY-MM-dd`" for the date December 28, 2020, you'll actually get "2021-12-28" rather than the desired date "2020-12-28".  This is because the week year (defined together with the 'week of year' - 1 in this example) is 2021 because December 28 occurs in the same week as January 1 (our definition of when week 1 starts).  The developer likely meant to use "`yyyy-MM-dd`" instead.


### Steps

**NOTE**: you must use **<code>fork:yes</code></strong> in these because the examples are contained in a fork of a couple of popular open source repositories.


#### Structural Search (Just SimpleDateFormat)



* **<code>repo:sourcegraph-testing/* lang:java fork:yes SimpleDateFormat(..."...YYYY..."...) </code></strong>[[sg](https://demo.sourcegraph.com/search?q=repo:sourcegraph-testing/*+lang:java+fork:yes+SimpleDateFormat%28...%22...YYYY...%22...%29&patternType=structural)]

    <code>              |  |     |  ^</code> optional second argument or whitespace


    `              |  |     ^` anything in the format string after YYYY


    `              |  ^` anything in the format string before YYYY


    `              ^ `whitespace (such as a new line after the opening '(')



#### Structural Search (`SimpleDateFormat` or `DateTimeFormat.ofPattern`)



* **<code>repo:sourcegraph-testing/* lang:java fork:yes :[~(SimpleDateFormat|DateTimeFormatter.ofPattern)](..."...YYYY..."...) </code></strong>[[sg](https://demo.sourcegraph.com/search?q=repo:sourcegraph-testing/*+lang:java+fork:yes+:%5B%7E%28SimpleDateFormat%7CDateTimeFormatter.ofPattern%29%5D%28...%22...YYYY...%22...%29+count:1000&patternType=structural)]

    This one adds a regex pattern (using <code>[:[~]](https://docs.sourcegraph.com/@v3.24.1/code_search/reference/structural#syntax-reference)</code>) to match either <code>[SimpleDateFormat](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/text/SimpleDateFormat.html)</code> or <code>[DateTimeFormater.ofPattern()](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/time/format/DateTimeFormatter.html#ofPattern(java.lang.String))</code>.

* **<code>repo:sourcegraph-testing/* lang:java fork:yes SimpleDateFormat(..."...YYYY..."...) or DateTimeFormatter.ofPattern(..."...YYYY..."...) </code></strong>[[sg](https://demo.sourcegraph.com/search?q=repo:sourcegraph-testing/*+lang:java+fork:yes+SimpleDateFormat%28...%22...YYYY...%22...%29+or+DateTimeFormatter.ofPattern%28...%22...YYYY...%22...%29&patternType=structural)]

    This is the same as the above query but potentially easier to read using the "or" operator to separate the two search strings rather than a regex pattern.



## Code migrations


```
#type:diff-search #type:commit-search #code-migration #insights
```



### Use Case

Your customer is interested in long-term migration or refactoring. This flow starts with the insights panel in order to highlight how we can be used to manage that process. Then you migrate to either a standard demo flow for intel or to campaigns.


### Discussion

We at Sourcegraph dogfood our own product—and that includes tracking our efforts to change how the app’s code is constructed. I want to walk through how Search and our Insights product can help you do the same. 


### Steps


#### Prerequisites


```
Ensure that insights is enabled on sourcegraph.com in your user settings:


"experimentalFeatures": {
      "codeInsights": true
  }

Pre-load the front page because otherwise the graphs take too long to load and you will have to vamp. (Similarly cmd + click to open all new searches in the demo so you always have the pre-loaded front page open.) All of these queries should start from the graph, with only small modifications on the keyboard through the demo.
```



#### Insights high-level graph


```
Graph: Migration to React Function Components (highlight how you can track the amount of activity over time, you can see good graph go up and bad graph go down—make sure you're moving in the right direction!)
```



#### Diff search (cmd+ click function component recent data point)

**<code>repo:^github\.com/sourcegraph/sourcegraph$ type:diff after:2020-11-08T00:00:00-08:00 before:2021-02-08T00:00:00-08:00  const\s\w+:\s(React\.)?FunctionComponent </code></strong>[[sg](https://sourcegraph.com/search?q=repo%3A%5Egithub%5C.com%2Fsourcegraph%2Fsourcegraph%24+type%3Adiff+after%3A2020-11-08T00%3A00%3A00-08%3A00+before%3A2021-02-08T00%3A00%3A00-08%3A00+patternType%3Aregexp+const%5Cs%5Cw%2B%3A%5Cs%28React%5C.%29%3FFunctionComponent)]


#### Diff search (add author filter; highlight a single author to praise them at standup)

**<code>repo:^github\.com/sourcegraph/sourcegraph$ type:diff after:2020-11-08T00:00:00-08:00 before:2021-02-08T00:00:00-08:00  const\s\w+:\s(React\.)?FunctionComponent author:artem </code></strong>[[sg](https://sourcegraph.com/search?q=repo:%5Egithub%5C.com/sourcegraph/sourcegraph%24+type:diff+after:2020-11-08T00:00:00-08:00+before:2021-02-08T00:00:00-08:00++const%5Cs%5Cw%2B:%5Cs%28React%5C.%29%3FFunctionComponent+author:artem&patternType=regexp)]


#### Diff search (cmd+ click class component recent data point; touch base with these authors to see why this is happening—lots of things to remember as a dev!)

**<code>repo:^github\.com/sourcegraph/sourcegraph$ type:diff after:2020-11-08T00:00:00-08:00 before:2021-02-08T00:00:00-08:00  extends\s(React\.)?(Pure)?Component </code></strong>[[sg](https://sourcegraph.com/search?q=repo%3A%5Egithub%5C.com%2Fsourcegraph%2Fsourcegraph%24+type%3Adiff+after%3A2020-11-08T00%3A00%3A00-08%3A00+before%3A2021-02-08T00%3A00%3A00-08%3A00+patternType%3Aregexp+extends%5Cs%28React%5C.%29%3F%28Pure%29%3FComponent)]


#### Code search (delete just a few params to see what’s left to fix)

**<code>repo:^github\.com/sourcegraph/sourcegraph$ extends\s(React\.)?(Pure)?Component </code></strong>[[sg](https://sourcegraph.com/search?q=repo:%5Egithub%5C.com/sourcegraph/sourcegraph%24+extends%5Cs%28React%5C.%29%3F%28Pure%29%3FComponent&patternType=regexp)]


#### Export (pull things to CSV to farm out the remaining work)


```
Click "Export to CSV" on previous search.
```



#### Fork point (depending on how familiar customer is with Sourcegraph)


```
At this point, either open one of the files and highlight code intel + extensions as in the standard demo, or migrate to Monitoring (be told if the bad pattern is reintroduced) and Campaigns and show how you can also make bulk changes using Campaigns, keeping with the theme of mass migration.
```



## Using the Sourcegraph GraphQL API


```
#graphql #api #api-console
```



### Use Case

Developers often want to write their own tools or utilities that access Sourcegraph data. 


### Description

The [GraphQL API](https://docs.sourcegraph.com/api/graphql) makes it easy for developers to access the data in Sourcegraph.


### API Examples



* [ListLanguages](https://demo.sourcegraph.com/api/console#%7B%22query%22%3A%22query%20ListLanguages(%24repoName%3A%20String!)%20%7B%5Cn%20%20repository(name%3A%20%24repoName)%20%7B%5Cn%20%20%20%20language%5Cn%20%20%20%20commit(rev%3A%20%5C%22HEAD%5C%22)%20%7B%5Cn%20%20%20%20%20%20languages%5Cn%20%20%20%20%7D%5Cn%20%20%7D%5Cn%7D%5Cn%22%2C%22variables%22%3A%22%7B%5Cn%20%20%5C%22repoName%5C%22%3A%20%5C%22github.com%2Fsourcegraph%2Fsourcegraph%5C%22%5Cn%7D%22%2C%22operationName%22%3A%22ListLanguages%22%7D)

    List the languages in use by a given repo.  The $repoName variable is set at the bottom of the console

* [content](https://demo.sourcegraph.com/api/console?#%7B%22query%22%3A%22query%20%7B%5Cn%20%20repository(name%3A%20%5C%22github.com%2Fuber%2Freact-map-gl%5C%22)%20%7B%5Cn%20%20%20%20defaultBranch%20%7B%5Cn%20%20%20%20%20%20target%20%7B%5Cn%20%20%20%20%20%20%20%20commit%20%7B%5Cn%20%20%20%20%20%20%20%20%20%20blob(path%3A%20%5C%22README.md%5C%22)%20%7B%5Cn%20%20%20%20%20%20%20%20%20%20%20%20content%5Cn%20%20%20%20%20%20%20%20%20%20%7D%5Cn%20%20%20%20%20%20%20%20%7D%5Cn%20%20%20%20%20%20%7D%5Cn%20%20%20%20%7D%5Cn%20%20%7D%5Cn%7D%5Cn%22%7D)

    Get the contents of a file



## GraphQL API Consumer


```
#graphql #api #typescript
```



### Use Case

You are using GraphQL.  You are about to make a change to the implementation of a specific API and want to know all the clients of the API so you can make sure you won't impact anything.


### Description

GraphQL is a query language for APIs to describe how to [query](https://graphql.org/learn/queries/) and [manipulate](https://graphql.org/learn/queries/#mutations) data on the server.  


### Steps


#### GraphQL Schema



* [Direct Link](https://demo.sourcegraph.com/github.com/sourcegraph/sourcegraph/-/blob/cmd/frontend/graphqlbackend/schema.graphql)

    This is a direct link to the schema file.  But, it's probably better to get there by searching :).

* **<code>repo:^github\.com/sourcegraph/* lang:graphql schema </code></strong>[[sg](https://demo.sourcegraph.com/search?q=repo:%5Egithub%5C.com/sourcegraph/*+lang:graphql+schema&patternType=literal)]

    If you leave off "schema" you'll see a few other GraphQL schema files.  It's easy to get to the right one this way too (it's called <strong><code>schema.graphql</code></strong> in <strong><code>sourcegraph/sourcegraph</code></strong> repo)



#### Find the API



* Open **<code>schema.graphql</code></strong> in <strong><code>sourcegraph/sourcegraph</code></strong> repo
* Scroll down to the API you are going to use for this demo.  I like the <strong><code>createCodeMonitor</code></strong> mutation.  But, there are others in there that are just as good to use.


#### Code Intelligence



* Hover over the API and show the code intel features
* Click on the "**<code>Find references</code></strong>" link to open all the references to this API.  

    <strong><span style="text-decoration:underline;">NOTE</span></strong>: This is a search-based result so make sure you pick a relatively unique API name.



#### Review the Callers



* Scroll through the results and find the Typescript results that are interesting.  For the **<code>createCodeMonitor </code></strong>example, you are looking for the result on <strong><code>CreateCodeMonitorPage.tsx</code></strong> (Line 20).

    

<p id="gdcalert2" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image2.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert3">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image2.png "image_tooltip")




## Find Example


```
#python #onboarding #institutional-knowledge
```



### Use Case

You don't know how to connect and submit metrics to Datadog.  You want to search for an example code in your company's repositories to use as a template.


### Description

Oftentimes, documentation is out of date and the only way to find the right way to do something is to find an example in code.  This example searches Python code for how to connect to Datadog.  But, you could also imagine any other service in the place of Datadog (like your internal LDAP server, for example)


### Steps


#### (optional) Literal search for datadog



* **<code>lang:python datadog </code></strong>[[sg](https://sourcegraph.com/search?q=lang:python+datadog&patternType=regexp)]

    This returns a bunch of results from the Datadog repositories.

* **<code>lang:python datadog -repo:github.com/DataDog/* </code></strong>[[sg](https://sourcegraph.com/search?q=lang:python+datadog+-repo:github.com/DataDog/*&patternType=regexp)]

    Here we remove all of the DataDog repos to help us discover the package name ("<strong><code>import datadog</code></strong>")



#### Search for where Datadog package is imported



* **<code>lang:python ^\s*from\s+datadog or ^\s*import\s+datadog -repo:github.com/DataDog/* </code></strong>[[sg](https://sourcegraph.com/search?q=lang:python+%5E%5Cs*from%5Cs%2Bdatadog+or+%5E%5Cs*import%5Cs%2Bdatadog+-repo:github.com/DataDog/*&patternType=regexp)]


## Datadog Extension


```
#python #datadog #extension
```



### Use Case

Developers create and submit metrics from their code to Datadog.   You want to show how Sourcegraph integrates and connects them to their Datadog dashboards.


### Prerequisites



* Enable the [Datadog extension](https://demo.sourcegraph.com/extensions/sourcegraph/datadog-metrics)!
* Have a Datadog account on our CE Datadog instance (see )
* Be logged in to your Datadog account


### Description

The current example is pretty weak.  But, it's a starting point.  This code is running on a laptop right now and produces random data.  It showcases the integration point well (see below) but not a real-world example.

Info: You can see how this extension is implemented [here](https://demo.sourcegraph.com/github.com/sourcegraph/sourcegraph-datadog-metrics/-/blob/src/datadog-metrics.ts).


### Steps


#### Show demo file



* **<code>repo:^github\.com/mike-r-mclaughlin/datadog-sourcegraph-sample$ file:^demo\.py </code></strong>[[sg](https://demo.sourcegraph.com/github.com/mike-r-mclaughlin/datadog-sourcegraph-sample/-/blob/demo.py)]


#### Click on "View metric (Datadog)"

This will show a dashboard of the metric in Datadog.  


#### More realistic code sample

NOTE: this is not running and therefore is not pushing these metrics to our Datadog instance.  So, if you click on this link it won't actually show you the metrics (because they don't exist in our Datadog instance).  But, it's a much more realistic code example to show. :)



* **<code>repo:^github\.com/DataDog/dd-trace-py$ file:^ddtrace/internal/writer\.py </code></strong>[[sg](https://demo.sourcegraph.com/github.com/DataDog/dd-trace-py/-/blob/ddtrace/internal/writer.py#L294-304)]

    Scroll to Line ~294



## Email Verification Bug

Precise code intel


 

<p id="gdcalert3" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image3.jpg). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert4">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image3.jpg "image_tooltip")
 POC: JS cross-repo/dependency navigation 


       ▪︎ [Demo link](https://sourcegraph.com/npm/axios/0.21.1@e0d402df0a442b8f0bfd012876693664747be8f9/-/blob/index.d.ts#L130:18&tab=references)


       ▪︎ [Loom link](https://www.loom.com/share/a2ef32a776624186a6c7b67387388b47?sharedAppSource=personal_library)


   ◦ 

<p id="gdcalert4" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image4.gif). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert5">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image4.gif "image_tooltip")
  Cross-repo navigation for Go on Sourcegraph Cloud


       ▪︎ [Example link 1](https://sourcegraph.com/github.com/hashicorp/go-multierror@9974e9ec57696378079ecc3accd3d6f29401b3a0/-/blob/append.go#L11:6&tab=references), [example link 2](https://sourcegraph.com/github.com/slimsag/godocmd@a1005ad29fe3e4831773a8184ee7ebb3a41d1347/-/blob/comment.go#L333:6&tab=references)


       ▪︎ [Loom link](https://www.loom.com/share/b5c54fc898df4f20969a8e8969e4c475?sharedAppSource=personal_library)


## JavaScript Class 


```
#JavaScript #structural 
```


Quick and easy JS structural search example showing how you can find a child class in JS. Everyone has JS!



* `Lang:JavaScript class ... extends ... {...} count:all patternType:structural`


## Spanish New Authz Provider Video Demo 


```
#spanish #go #search

```



* <code>[https://drive.google.com/file/d/1nb-heA9zq9Def1BuNk7PhesWP9UHSdDv/view?usp=sharing](https://drive.google.com/file/d/1nb-heA9zq9Def1BuNk7PhesWP9UHSdDv/view?usp=sharing)</code>


## Cross repository code intelligence


```
#cross-repository #go #javascript #java #code-intelligence
```



### Use Case

Some functions will have cross dependencies where functions are defined and referenced in other repositories. 


### Value / Differentiation from other technologies


### Description

These are 3 different examples in different languages that will show code that is being used in a file and referenced in many other repositories while being defined in a main repository. The idea here is that you will be able to pull up an example of an implemented dependency (**<code>putIfAbsent, AxiosInstance, or multierror</code></strong>) and show that not only is it used in other repositories, but the definition is not in the original repository you found it in. 


### Steps


#### Java - [loom link](https://www.loom.com/share/446e0fc1df3d4bc4bf7bb6bd044573bc)



* **<code>repo:^github\.com/Netflix/Hystrix$ file:^hystrix-core/src/main/java/com/netflix/hystrix/HystrixRequestCache\.java</code></strong> [[sg](https://sourcegraph.com/github.com/Netflix/Hystrix/-/blob/hystrix-core/src/main/java/com/netflix/hystrix/HystrixRequestCache.java#L77:40)]
* Make sure you are in the file
* Highlight <strong><code>putIfAbsent</code></strong> (~line 80)
* Click on Find References and in the drawer that opens up make sure to select Show other repositories
    * This shows cross repository references of <strong><code>putIfAbsent</code></strong>
* Click on Definitions in the drawer navigation to see the definition of <strong><code>putIfAbsent</code></strong>


#### Javascript - [loom link](https://www.loom.com/share/a2ef32a776624186a6c7b67387388b47)



* **<code>repo:^github\.com/grafana/grafana$@78d53c5 file:^packages/grafana-toolkit/src/cli/utils/githubClient\.ts</code></strong> [[sg](https://sourcegraph.com/github.com/grafana/grafana@78d53c5/-/blob/packages/grafana-toolkit/src/cli/utils/githubClient.ts)]
* Make sure you are in the file
* Highlight <strong><code>AxiosInstance</code></strong> (~line 22)
* Click on Find References and in the drawer that opens up make sure to select Show other repositories
    * This shows cross repository references of <strong><code>AxiosInstance</code></strong>
* Click on Definitions in the drawer navigation to see the definition of <strong><code>AxiosInstance</code></strong>


#### Go - [loom link](https://www.loom.com/share/b5c54fc898df4f20969a8e8969e4c475)



* Sourcegraph implements hashicorp’s multierror repository
* **<code>repo:^github\.com/hashicorp/packer$@27d89ac file:^packer/core\.go</code></strong> [[sg](https://sourcegraph.com/github.com/hashicorp/packer@27d89ac/-/blob/packer/core.go)]
* Make sure you are in the file
* See how ~line 16 we are including<strong><code> multierror "github.com/hashicorp/go-multierror"</code></strong>
* Highlight <strong><code>multierror.Append</code></strong> (~line 730)
* Click on Find References and in the drawer that opens up make sure to select Show other repositories
    * This shows cross repository references of <strong><code>Append</code></strong>
* Click on Definitions in the drawer navigation to see the definition of <strong><code>Append</code></strong>


## Find all usages of 2 similarly named packages


```
#structural-search #go
```



### Use Case

It's difficult to find where specific packages are used in code, especially if the package is named using a common word, like "errors".  In this example, we use structural search to find everywhere in Sourcegraph's Go code where 2 different, but similarly named packages are imported.


### Value / Differentiation from other technologies

Because the packages are named "errors" (a commonly used term in source code) it is difficult to rely on simple grep-like (or literal search in Sourcegraph) techniques.  These approaches will find many false positives.  Using regular expressions is possible but also difficult because, for example, the packages can span multiple lines.


### Description

This is a real-world example used by engineers at Sourcegraph (details and recorded video from   [here](https://sourcegraph.slack.com/archives/C0B2RU51Q/p1632932165323900)).  

Sourcegraph had 2 packages named "errors" in v3.25.  This was causing confusion.  So, developers used Sourcegraph to find all locations where each package was used.  From there, they can reduce the usage to a single package and eliminate the extra one.


### Steps


#### Prep



1. Open up a file that imports the first errors package (`"github.com/cockroachdb/errors"`) [[sg](https://sourcegraph.com/github.com/sourcegraph/sourcegraph@3.25/-/blob/internal/encryption/cloudkms/cloud_kms.go?L11:32)] \
You can get to the file by searching for **<code> \
repo:^github\.com/sourcegraph/sourcegraph$@3.25 file:^internal/encryption/cloudkms/cloud_kms\.go</code></strong>
2. Open up a different file that imports the second errors package (<code>"errors"</code>) [[sg](https://sourcegraph.com/github.com/sourcegraph/sourcegraph@3.25/-/blob/cmd/frontend/graphqlbackend/symbols.go?L5:3)] \
You can get to the file by searching for \
<strong><code>repo:^github\.com/sourcegraph/sourcegraph$@3.25 file:^cmd/frontend/graphqlbackend/symbols\.go$</code></strong>


#### Structural Search Demo



1. Find all locations where you are using the `"github.com/cockroachdb/errors"`  package: \
**<code>repo:^github\.com/sourcegraph/sourcegraph$@3.25 lang:go import (... "github.com/cockroachdb/errors" ...) count:1000 patterntype:structural </code></strong>[[sg](https://sourcegraph.com/search?q=context:global+repo:%5Egithub%5C.com/sourcegraph/sourcegraph%24%403.25+lang:go+import+%28...+%22github.com/cockroachdb/errors%22+...%29+count:1000&patternType=structural)]
2. Find all locations where you are using the <code>"errors"</code> package: \
<strong><code>repo:^github\.com/sourcegraph/sourcegraph$@3.25 lang:go import (... "errors" ...) count:1000 patterntype:structural</code></strong> [[sg](https://sourcegraph.com/search?q=context:global+repo:%5Egithub%5C.com/sourcegraph/sourcegraph%24%403.25+lang:go+import+%28...+%22errors%22+...%29+count:1000&patternType=structural)]
3. (optional) You can also combine these into one query using the <strong><code>OR</code></strong> operator: \
<strong><code>repo:^github\.com/sourcegraph/sourcegraph$@3.25 lang:go import (... "github.com/cockroachdb/errors" ...) or import (... "errors" ...) count:1000 patterntype:structural </code></strong>[[sg](https://sourcegraph.com/search?q=context:global+repo:%5Egithub%5C.com/sourcegraph/sourcegraph%24%403.25+lang:go+import+%28...+%22github.com/cockroachdb/errors%22+...%29+or+import+%28...+%22errors%22+...%29+count:1000&patternType=structural)]


## Find Examples of How Other Developers Use an Object


```
#structural-search #go
```



### Use Case

Developers who are new to a codebase want to follow best practices for how to call functions and pass parameters. 


### Value / Differentiation from other technologies

From Coury:


    _That was the particular query I wrote, that captures function parameters. In general structural search can match parameters so easy with context such as parameter location, etc._


    _This query was just to help me build some context on how other parts of the Sourcegraph codebase were initializing helper code with a provided DB_


### Description

This is a real-world example used by engineers at Sourcegraph (details from  [here](https://sourcegraph.slack.com/archives/C0B2RU51Q/p1632962415328500?thread_ts=1632932165.323900&cid=C0B2RU51Q)).  


### Steps



1. Find an example of how to pass a DB object to a function \
**<code>repo:^github\.com/sourcegraph/sourcegraph$ (:[[_]] dbutil.DB) patterntype:structural</code></strong> [[sg](https://sourcegraph.com/search?q=repo:%5Egithub%5C.com/sourcegraph/sourcegraph%24+%28:%5B%5B_%5D%5D+dbutil.DB%29&patternType=structural)]