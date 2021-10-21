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