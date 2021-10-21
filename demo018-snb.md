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



