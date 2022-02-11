# Ruby Onboarding Notebook

Get a sense for common useful Sourcegraph searches using this search notebook.

#### Find Ruby version files

```sourcegraph
context:global file:\.ruby-version$ patternType:literal
```

#### Look for repos using Ruby 3.x

This query leverages the `select` filter to show repos containing the content, rather than the content itself.

```sourcegraph
context:global file:\.ruby-version$ select:repo ^3\. patternType:regexp
```

#### Find changes to Ruby version files

```sourcegraph
context:global file:\.ruby-version$ repo:appfolio type:diff patternType:regexp
```

#### Structural search with Ruby classes

```sourcegraph
context:global class ... def ... end end lang:ruby patternType:structural
```

#### TODOs added in code in the last 3 months

```sourcegraph
context:global TODO type:diff repo:appfolio select:commit.diff.added after:"3 months ago" patternType:regexp
```
