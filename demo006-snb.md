## fmt.Sprintf() -> strconv.Itoa()



## Use Case
I want to clean up our code and remove inefficient function calls.  One example of that is code that uses fmt.Sprintf() to convert a number to a string.  It's more efficient to use itoa function for that.


## Discussion
Use sourcegraph.com/search for this because the examples required to prove this out are in repos that are not yet on demo.  I added a simple example in my own repo (mike-r-mclaughlin/golang-examples).  But, better to have more real-world examples from other projects that are not loaded on demo.  To be specific, you can see examples in [gravitational/teleport repo](https://sourcegraph.com/github.com/gravitational/teleport).

Code [Example](https://sourcegraph.com/github.com/mike-r-mclaughlin/golang-examples/-/blob/hello.go):


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



## Steps


#### (optional) Basic literal search
[fmt.Sprintf("%d" lang:go](https://sourcegraph.com/search?q=fmt.Sprintf%28%22%25d%22+lang:go&patternType=literal)


#### Simple regex search
[fmt.Sprintf\("%d" lang:go](https://demo.sourcegraph.com/search?q=fmt.Sprintf%5C%28%22%25d%22+lang:go&patternType=regexp)(Demo Instance)
[fmt.Sprintf\("%d" lang:go](https://sourcegraph.com/search?q=fmt.Sprintf%5C%28%22%25d%22+lang:go&patternType=regexp)

The basic literal search is identical to this one.

#### More complex regex search
[fmt.Sprintf\s*\(\s*"%d" lang:go](https://sourcegraph.com/search?q=fmt.Sprintf%5Cs*%5C%28%5Cs*%22%25d%22+lang:go+&patternType=regexp)

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
[fmt.Sprintf(..."%d", ...) repo:mike-r-mclaughlin/golang-examples](https://sourcegraph.com/search?q=+fmt.Sprintf%28...%22%25d%22%2C+...%29+repo:mike-r-mclaughlin/golang-examples&patternType=structural)

This search will find the example in line 11-13.  The "..." in front of "%d" is required because of the new line.


<p id="gdcalert1" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image1.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert2">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>



#### Tags
#go #structural-search #batch-changes #code-monitoring



### *TODO* Example N:

TODO .... TODO ... TODO ...

search for other examples in go that have a function call followed by a new line followed by a comment block: [https://sourcegraph.com/search?q=lang:go+%5C%28%5Cs*//+and+not+const+and+not+var+repo:sourcegraph&patternType=regexp](https://sourcegraph.com/search?q=lang:go+%5C%28%5Cs*//+and+not+const+and+not+var+repo:sourcegraph&patternType=regexp)


