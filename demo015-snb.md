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



