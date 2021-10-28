# Find Example

## Use Case
You don't know how to connect and submit metrics to Datadog.  You want to search for an example code in your company's repositories to use as a template.


## Discussion
Oftentimes, documentation is out of date and the only way to find the right way to do something is to find an example in code.  This example searches Python code for how to connect to Datadog.  But, you could also imagine any other service in the place of Datadog (like your internal LDAP server, for example)


## Steps

#### (optional) Literal search for datadog
* **<code>lang:python datadog </code></strong>[[sg](https://sourcegraph.com/search?q=lang:python+datadog&patternType=regexp)]

This returns a bunch of results from the Datadog repositories.

[lang:python datadog -repo:github.com/DataDog/*](https://sourcegraph.com/search?q=lang:python+datadog+-repo:github.com/DataDog/*&patternType=regexp)

Here we remove all of the DataDog repos to help us discover the package name ("<strong><code>import datadog</code></strong>")

#### Search for where Datadog package is imported
[ang:python ^\s*from\s+datadog or ^\s*import\s+datadog -repo:github.com/DataDog/*](https://sourcegraph.com/search?q=lang:python+%5E%5Cs*from%5Cs%2Bdatadog+or+%5E%5Cs*import%5Cs%2Bdatadog+-repo:github.com/DataDog/*&patternType=regexp)

#### Tags
#python #onboarding #institutional-knowledge
