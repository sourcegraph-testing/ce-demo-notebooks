# Site Down / War Room Session

## Use Case
Your site/application went down and you want to know what recently changed that might have caused the outage.  You saw an error message about XYZ right before the crash.  You want to figure out _quickly_ who to bring into a war room and who should be paged, etc.  And, what else might be impacted by this.


## Discussion
The beauty of Sourcegraph and search is that it's super easy to jump in and get to an answer quickly and on your own.  You don't need to waste everyone's time by paging all group leaders into a war room.  And, then figuring out which repo a specific error message is.  You can know exactly who to call and which projects are impacted.


## Steps


#### Commit search (High level what changed)

[repo:github.com/sourcegraph/sourcegraph type:commit](https://sourcegraph.com/search?q=repo:github.com/sourcegraph/sourcegraph+type:commit&patternType=literal)


#### Diff search (Which modules changed recently)
[repo:github.com/sourcegraph/sourcegraph type:diff](https://sourcegraph.com/search?q=repo:github.com/sourcegraph/sourcegraph+type:diff&patternType=literal)


#### Diff search (last 3 days only)

[repo:github.com/sourcegraph/sourcegraph type:diff after:"3 days ago"](https://sourcegraph.com/search?q=repo:github.com/sourcegraph/sourcegraph+type:diff+after:%223+days+ago%22&patternType=literal)

## Value
SRE and other support engineering groups can really get a lot of value out of this. They can quickliy find the right service to debug and give developers more accurate bug reports to fix issues.

#### Tags
#type:diff-search #type:commit-search #incident-response
