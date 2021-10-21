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


