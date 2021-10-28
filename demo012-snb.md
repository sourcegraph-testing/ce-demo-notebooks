# Converting ES6 Javascript Function to Arrow Functions with Batch Changes


## Use Case
Let's say for example a UiPath Engineering Team had the goal of wanting to migrate all of their js/tsx repos from ES6  functions declarations to Arrow Function declarations. How would they accomplish this?


## Discussion
function sumFunc(params) {}  to const sumFunc = (params) => { }

async function sumFunc(params)  {}  to const sumFunc = async (params) = > {}

#### Doing this without batch changes:
1. Run search in your code host or in your IDE
    1. May not return all or exact matches for code block - does it support structural search?
2. Based on search results, generate a list of impacted repos
3. Pull each repo down locally
4. Find all occurrences of the necessary change
5. Update/Replace
    2. If using a script to do this:
        1. Write
        2. Test
        3. Debug
6. Repeat step 4-5 for each repo
7. Manually push changes to code host
8. PRS are opened

This is a slow and difficult way to track progress and implement large-scale changes across the codebase.

#### Doing this with batch changes:
1. Write a batch changes spec that points to all the instances where JS functions are declared in the codebase ( can be done with structural search to ensure precision )
2. Run the spec in SRC CLI
3. Preview, and apply changes being made
4. Confirm it looks good
5. Publish
6. PRS are opened, and progress can be tracked through burn down chart


## Steps

#### Search
Run initial search [query](https://sourcegraph.com/search?q=repo:%5Egithub%5C.com/UiPath+lang:JavaScript++:%5B%7E%5Efunction%5D+:%5Bfn%7E%5Cw%2B%5D%28...%29+&patternType=structural) against UiPath repositories to get a sense of the breadth of usage -- how often are regular function declarations used in their codebase:

#### Automate
Create batch spec, preview, and apply changes to the codebase using SRC CLI

[https://demo.sourcegraph.com/users/manuel/batch-changes/convert-JSfunctions-to-arrow-functions](https://demo.sourcegraph.com/users/manuel/batch-changes/convert-JSfunctions-to-arrow-functions)

Once the changes have been made notify code owners via batch operations such as bulk comments. This allows you to comment on all selected changesets. This can be particularly useful for pinging people, reminding them to take a look at the changeset.

There are several instances of this style of function declarations still being used in various repos; I need to update them as quickly and easily as possible and notify the owners of that code that this change is being made.

#### Automate
Create a code monitoring alert to notify when the old style of function declaration has been reintroduced into the codebase, to apply changes to convert to arrow function declarations.

#### Understand
Create a Code Insight of what currently exists in the codebase for both regular function declarations vs arrow function. (This provides an understanding of the high-level overview of the team’s progress towards success in their efforts to complete this migration.)

## Value
Custoemers are able to make large scale changes quickly and in a manageable way.

#### Tags
#javascript #structural-search #batch-changes

