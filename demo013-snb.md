## Java Misused Week Year


```
#java #good-for-batch-changes
```



### Use Case

Java developers sometimes [use "YYYY" when they mean to use "yyyy"](https://errorprone.info/bugpattern/MisusedWeekYear).  Teams need a way to find all instances of this and quickly replace them.  And, monitor the code for developers that check code in like this.

[Sonar Rule [RSPEC-3986](https://rules.sonarsource.com/java/RSPEC-3986)]


### Description

Java uses [pattern letters](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/text/SimpleDateFormat.html) to allow developers to format a date/time to their desired format.  There are two different ways of representing a year: the calendar year and the week year.  Y (uppercase Y) date format represents the "week year" while y (lowercase y) represents the calendar year.  

While the calendar year is straightforward to understand, the week year takes some explanation.  Every year has 52 weeks (defined as Monday - Sunday or Sunday - Saturday, etc.).  If you number each week from 1 to 52, this numbered week represents the "week of year".  Weeks 2-51 are fairly easy to define and the days in those weeks will always be contained in the same calendar year.   However, one of either the last week of a year or the first week of the new year will almost always overlap with days from the prior year or start of the new year.  

It's easiest to look at an example of this.  Below are the months December 2020 and January 2021 which we'll use to explain the problem.  


<table>
  <tr>
   <td><strong>December 2020</strong>
   </td>
   <td><strong>January 2021</strong>
   </td>
  </tr>
  <tr>
   <td><code>Wk# Su Mo Tu We Th Fr Sa </code>
<p>
<code>49         1  2  3  4  5 </code>
<p>
<code>50   6  7  8  9 10 11 12 </code>
<p>
<code>51  13 14 15 16 17 18 19 </code>
<p>
<code>52  20 21 22 23 24 25 26 </code>
<p>
<code> 1  27 28 29 30 31 </code>
   </td>
   <td><code>Wk# Su Mo Tu We Th Fr Sa </code>
<p>
<code> 1                  1  2 </code>
<p>
<code> 2   3  4  5  6  7  8  9 </code>
<p>
<code> 3  10 11 12 13 14 15 16 </code>
<p>
<code> 4  17 18 19 20 21 22 23 </code>
<p>
<code> 5  24 25 26 27 28 29 30 </code>
<p>
<code> 6  31 </code>
   </td>
  </tr>
</table>


The "week number" is abbreviated "Wk#" in the above calendar.  In this example, we used the definition that the first week (Wk1), begins on the week that has January 1.  However, there are other ways to define week 1 like the [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601#Week_dates) definition which are more complex.  

Regardless of how you define "week 1 (Wk1)", there will almost always be one week where there are days of the week that have a "week year" that are different from the calendar year.  In the above example, WEEK 1 of 2021 includes 5 days from 2020.

So, if you format a date using the pattern "`YYYY-MM-dd`" for the date December 28, 2020, you'll actually get "2021-12-28" rather than the desired date "2020-12-28".  This is because the week year (defined together with the 'week of year' - 1 in this example) is 2021 because December 28 occurs in the same week as January 1 (our definition of when week 1 starts).  The developer likely meant to use "`yyyy-MM-dd`" instead.


### Steps

**NOTE**: you must use **<code>fork:yes</code></strong> in these because the examples are contained in a fork of a couple of popular open source repositories.


#### Structural Search (Just SimpleDateFormat)



* **<code>repo:sourcegraph-testing/* lang:java fork:yes SimpleDateFormat(..."...YYYY..."...) </code></strong>[[sg](https://demo.sourcegraph.com/search?q=repo:sourcegraph-testing/*+lang:java+fork:yes+SimpleDateFormat%28...%22...YYYY...%22...%29&patternType=structural)]

    <code>              |  |     |  ^</code> optional second argument or whitespace


    `              |  |     ^` anything in the format string after YYYY


    `              |  ^` anything in the format string before YYYY


    `              ^ `whitespace (such as a new line after the opening '(')



#### Structural Search (`SimpleDateFormat` or `DateTimeFormat.ofPattern`)



* **<code>repo:sourcegraph-testing/* lang:java fork:yes :[~(SimpleDateFormat|DateTimeFormatter.ofPattern)](..."...YYYY..."...) </code></strong>[[sg](https://demo.sourcegraph.com/search?q=repo:sourcegraph-testing/*+lang:java+fork:yes+:%5B%7E%28SimpleDateFormat%7CDateTimeFormatter.ofPattern%29%5D%28...%22...YYYY...%22...%29+count:1000&patternType=structural)]

    This one adds a regex pattern (using <code>[:[~]](https://docs.sourcegraph.com/@v3.24.1/code_search/reference/structural#syntax-reference)</code>) to match either <code>[SimpleDateFormat](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/text/SimpleDateFormat.html)</code> or <code>[DateTimeFormater.ofPattern()](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/time/format/DateTimeFormatter.html#ofPattern(java.lang.String))</code>.

* **<code>repo:sourcegraph-testing/* lang:java fork:yes SimpleDateFormat(..."...YYYY..."...) or DateTimeFormatter.ofPattern(..."...YYYY..."...) </code></strong>[[sg](https://demo.sourcegraph.com/search?q=repo:sourcegraph-testing/*+lang:java+fork:yes+SimpleDateFormat%28...%22...YYYY...%22...%29+or+DateTimeFormatter.ofPattern%28...%22...YYYY...%22...%29&patternType=structural)]

    This is the same as the above query but potentially easier to read using the "or" operator to separate the two search strings rather than a regex pattern.
