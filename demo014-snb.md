# Code migrations

## Use Case
Your customer is interested in long-term migration or refactoring. This flow starts with the insights panel in order to highlight how we can be used to manage that process. Then you migrate to either a standard demo flow for intel or to campaigns.


## Discussion
We at Sourcegraph dogfood our own product—and that includes tracking our efforts to change how the app’s code is constructed. I want to walk through how Search and our Insights product can help you do the same.


## Steps

#### Prerequisites
Ensure that insights is enabled on sourcegraph.com in your user settings:

"experimentalFeatures": {
      "codeInsights": true
  }

Pre-load the front page because otherwise the graphs take too long to load and you will have to vamp. (Similarly cmd + click to open all new searches in the demo so you always have the pre-loaded front page open.) All of these queries should start from the graph, with only small modifications on the keyboard through the demo.


#### Insights high-level graph
Graph: Migration to React Function Components (highlight how you can track the amount of activity over time, you can see good graph go up and bad graph go down—make sure you're moving in the right direction!)


#### Diff search (cmd+ click function component recent data point)
**<code>repo:^github\.com/sourcegraph/sourcegraph$ type:diff after:2020-11-08T00:00:00-08:00 before:2021-02-08T00:00:00-08:00  const\s\w+:\s(React\.)?FunctionComponent </code></strong>[[sg](https://sourcegraph.com/search?q=repo%3A%5Egithub%5C.com%2Fsourcegraph%2Fsourcegraph%24+type%3Adiff+after%3A2020-11-08T00%3A00%3A00-08%3A00+before%3A2021-02-08T00%3A00%3A00-08%3A00+patternType%3Aregexp+const%5Cs%5Cw%2B%3A%5Cs%28React%5C.%29%3FFunctionComponent)]


#### Diff search (add author filter; highlight a single author to praise them at standup)
**<code>repo:^github\.com/sourcegraph/sourcegraph$ type:diff after:2020-11-08T00:00:00-08:00 before:2021-02-08T00:00:00-08:00  const\s\w+:\s(React\.)?FunctionComponent author:artem </code></strong>[[sg](https://sourcegraph.com/search?q=repo:%5Egithub%5C.com/sourcegraph/sourcegraph%24+type:diff+after:2020-11-08T00:00:00-08:00+before:2021-02-08T00:00:00-08:00++const%5Cs%5Cw%2B:%5Cs%28React%5C.%29%3FFunctionComponent+author:artem&patternType=regexp)]


#### Diff search (cmd+ click class component recent data point; touch base with these authors to see why this is happening—lots of things to remember as a dev!)
**<code>repo:^github\.com/sourcegraph/sourcegraph$ type:diff after:2020-11-08T00:00:00-08:00 before:2021-02-08T00:00:00-08:00  extends\s(React\.)?(Pure)?Component </code></strong>[[sg](https://sourcegraph.com/search?q=repo%3A%5Egithub%5C.com%2Fsourcegraph%2Fsourcegraph%24+type%3Adiff+after%3A2020-11-08T00%3A00%3A00-08%3A00+before%3A2021-02-08T00%3A00%3A00-08%3A00+patternType%3Aregexp+extends%5Cs%28React%5C.%29%3F%28Pure%29%3FComponent)]


#### Code search (delete just a few params to see what’s left to fix)
**<code>repo:^github\.com/sourcegraph/sourcegraph$ extends\s(React\.)?(Pure)?Component </code></strong>[[sg](https://sourcegraph.com/search?q=repo:%5Egithub%5C.com/sourcegraph/sourcegraph%24+extends%5Cs%28React%5C.%29%3F%28Pure%29%3FComponent&patternType=regexp)]


#### Export (pull things to CSV to farm out the remaining work)
Click "Export to CSV" on previous search.

#### Fork point (depending on how familiar customer is with Sourcegraph)
At this point, either open one of the files and highlight code intel + extensions as in the standard demo, or migrate to Monitoring (be told if the bad pattern is reintroduced) and Campaigns and show how you can also make bulk changes using Campaigns, keeping with the theme of mass migration.


## Value

#### Tags
#type:diff-search #type:commit-search #code-migration #insights

