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


