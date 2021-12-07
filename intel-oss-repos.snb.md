# Exploring Code with Sourcegraph

Overwhelmed by finding code in GitHub, and looking for an easier way? Sourcegraph allows you to run precise, targeted searches across all of your code, allowing you to find what you need, make the right call with complete information, and continue with your day. For a full list of what we can do, [check out our search cheat sheet](https://learn.sourcegraph.com/how-to-search-code-with-sourcegraph-a-cheat-sheet).

## Find a list of repos in the Intel org in GitHub:

Sourcegraph indexes millions of OSS repos. If you're looking for code in a specific org, you can use our `repo:` filter to narrow down, and our `select:` filter to show the list of repos.

```sourcegraph
context:global repo:github.com/intel/ select:repo patternType:literal
```

## Keep on top of changes:

Say you're new to the Hyperscan project, and want to know what's been going on in the last year. Easily search those changes using our `type:diff` search and our `before:` and `after:` filters.

```sourcegraph
context:global repo:^github\.com/intel/hyperscan$ before:"1 day ago" after:"1 year ago" type:diff patternType:literal
```

Prefer to navigate by searching commit messages? Totally possible! Use the `type:commit` filter to handle that:

```sourcegraph
context:global repo:^github\.com/intel/hyperscan$ before:"1 day ago" after:"1 year ago" type:commit patternType:literal
```

Everything is searchable, so if you want to see the full history of commits referencing CSV support, that's easy to do:

```sourcegraph
context:global repo:^github\.com/intel/hyperscan$ type:commit CSV patternType:literal
```

## Look for usage examples:

Say you're a developer looking for inspiration about how you could implement authN and authZ in C++. With our symbol search and our `lang:` filter, it's a piece of cake to find places to investigate:

```sourcegraph
context:global repo:github.com/intel/ lang:C++ auth type:symbol patternType:literal
```

Click in to those symbols, and you'll be able to navigate the code using our [Code Intelligence](https://docs.sourcegraph.com/code_intelligence) functionality.

## Track licenses:

Interested in figuring out what licenses your team is using? With our `file:` search to limit searches by file path, it's a piece of cake. Simply look at your license files, and go from there. For example, you can find every reference to the GPL in your license files:

```sourcegraph
context:global repo:github.com/intel/ file:license gpl patternType:literal
```

Click in to those symbols, and you'll be able to navigate the code using our [Code Intelligence](https://docs.sourcegraph.com/code_intelligence) functionality.

## Explore language-aware patterns using structural search:

Have you ever wanted to run a search for a particular pattern, but been roadblocked by the complexity of building an appropriate regex? With structural search, finding complicated, multi-line patterns is a breeze. Check out this example of class declarations in JavaScript:

```sourcegraph
context:global repo:github.com/intel/ lang:JavaScript class ... extends ... {...} count:all patternType:structural
```

If you want full info about how to leverage structural search, check out our [structural search documentation](https://docs.sourcegraph.com/code_search/reference/structural).

## Sign up to explore search snippets and Insights:

If you would like to save your own [frequent search snippets](https://docs.sourcegraph.com/code_search/how-to/scopes), [track changes to your code with Insights](https://docs.sourcegraph.com/code_insights), or [pull in additional code context with Insights](https://docs.sourcegraph.com/extensions), Sourcegraph is free to start using! To do so, you can make an account on [Sourcegraph's cloud instance](https://sourcegraph.com/search), or [download Sourcegraph locally](https://docs.sourcegraph.com/getting-started) to test things out!

To learn how to use Sourcegraph for searching and understanding your code, check out [Sourcegraph Learn](https://learn.sourcegraph.com/) for tutorials, videos, and docs.

## Use Sourcegraph to search your own code:

Want to talk to someone about using Sourcegraph at Intel? [Schedule time with Sourcegraph's dedicated Intel team](https://calendly.com/jclifford-sourcegraph). We're here to help with any questions!
