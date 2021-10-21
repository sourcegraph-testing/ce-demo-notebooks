## Find Secrets and Tokens

## Use Case
We are looking through our code for any private keys or things that look like tokens.

## Discussion
We can help monitor for common security practices with Code Monitoring and send an email if code matches a certain criteria.  

## Steps

#### Regex Search

[("[a-z0-9+/]{32,}=?"|'[a-z0-9+/]{32,}=?'|`[a-z0-9+/]{32,}=?`) or -----BEGIN RSA PRIVATE KEY----- or token.+[a-z0-9+/]{32,}=['"]?\n lang:go](https://sourcegraph.com/search?q=+%28%22%5Ba-z0-9%2B/%5D%7B32%2C%7D%3D%3F%22%7C%27%5Ba-z0-9%2B/%5D%7B32%2C%7D%3D%3F%27%7C%60%5Ba-z0-9%2B/%5D%7B32%2C%7D%3D%3F%60%29+or+-----BEGIN+RSA+PRIVATE+KEY-----+or+token.%2B%5Ba-z0-9%2B/%5D%7B32%2C%7D%3D%5B%27%22%5D%3F%5Cn+lang:go&patternType=regexp)
[(key|secret|token)-[\w+]{32,}](https://sourcegraph.com/search?q=context:global+%28key%7Csecret%7Ctoken%29-%5B%5Cw%2B%5D%7B32%2C%7D&patternType=regexp)

## Value
Customers will see the complexity of the RE2 syntax we support. They will also see how we can help them keep their code safe of security vulneratbilities with Code Monitoring. 

#### Tags
#language-agnostic #security #code-monitoring #regex-advanced
