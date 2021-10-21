## Pin Dockerfile Base Image

### Use Case
Our security engineers or DevOps engineers want to find all Docker files that are using a "FROM &lt;baseimage>:latest" rather than a specific tag or SHA256 reference.

This is outlined in [Snyk's top 10 security best practices for Docker](https://snyk.io/blog/10-docker-image-security-best-practices/) (see #6).


### Description
This example is a great one to use for searching plus campaigns and code monitoring.  It is quick to run and very easy to understand.


### Steps

#### Basic Regex
[file:/Dockerfile FROM\s+.*:latest](https://demo.sourcegraph.com/search?q=file:/Dockerfile+FROM%5Cs%2B.*:latest&patternType=regexp)


#### More Accurate Regex
[file:/Dockerfile FROM (\w+\/)?\w+:latest($|\s)](https://demo.sourcegraph.com/search?q=file:/Dockerfile+FROM+%28%5Cw%2B%5C/%29%3F%5Cw%2B:latest%28%24%7C%5Cs%29&patternType=regexp)

## Value
This example is super easy to remember and to type when doing a quick demo with someone.  But it isn't quite as accurate as it needs to be.  For example, this will actually find results that are already pinned to a specific SHA256 (because we stopped at :latest).

#### Tags
#language-agnostic #security #batch-changes #code-monitoring
