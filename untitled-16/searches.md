# Searches

The first thing to know about searches in TaskPaper is that _you may never need to think about them_. Most of the time you can just type in the text you are looking for and that's it. Looking for socks? Then type "socks" into the searchbar and you will see all items that contain the text "socks".

TaskPaper searches work on the part of the outline that you have selected project in the sidebar. If you want to limit your search to a particular project select it in the sidebar. If you want to search your entire outline first select "Home" in the sidebar.

If you have more complex searching needs skim this chapter to see what's available. And then refer to it when you need to look up a specific syntax.

## Predicates <a id="predicates"></a>

Search predicates describe what you are looking for. Try these searches:

* `socks` – All items that contain the text "socks" \(and their parent items\) display while the view hides everything else.
* `not socks` – Notice that `not` gets highlighted. This is because it's a keyword that effects the logic of the search. This search hides all items that contain the text "sock".
* `socks or` – Notice that the searchbar shows an error for this search because the syntax is not complete. `or` is also a keyword and the search needs to know what else you are search for before it is valid. Complete the search by typing `socks or shoes` and the error goes away.

### Predicate Pattern <a id="predicate-pattern"></a>

The full predicate pattern looks like this:

```text
@  
```

The attribute describes what attribute to search for on each item. The relation describes how to text for matches. The search term gives the value to compare.

But you don't need to repeat that entire pattern every time you want to search for something. Predicates use default values when part of the pattern is missing. For example the following predicates are equal:

```text
Inbox
@text Inbox
contains Inbox
@text contains Inbox
```

They are all equal because `@text` is the default attribute and `contains` is the default relation.

### Attributes <a id="attributes"></a>

Predicates start with the attribute that you want to test. The examples in this section have all queried the built in `@text` attribute. But we can test against other attributes too. For example:

1. Add the tag `@status(complete)` to one if your items.
2. That item now has an attribute named "status" whose value is "complete".
3. Click on the "complete" text and notice that TaskPaper sets the search to `@status = complete`.

That search says to look for and match all items that have a status attribute with an associated value of "complete". If instead you wanted to match all items that have a "status" attribute no matter what the value you can search for just `@status`.

#### Built in Attributes <a id="built-in-attributes"></a>

TaskPaper includes some built in attributes that you can query. These attributes will have values even when there is no associated `@tag` in the item's text.

* `@type` - Item's type: project, task, or note.
* `@text` - Item's full line of text.
* `@id` - Item's unique ID.

### Relations <a id="relations"></a>

Relations determine the test that the predicate performs.

`=` : True if the attribute and search term are equal.

`!=` : True if the attribute and search term are not equal.

`<` : True if the attribute is less than the search term.

`>` : True if the attribute is greater than the search term.

`<=` : True if the attribute is less than or equal to the search term.

`>=` : True if the attribute is greater than or equal to the search term.

`contains` : True if the attribute contains the search term.

`beginswith` : True if the attribute begins with the search term.

`endswith` : True if the attribute ends with the search term.

`matches` : True if the attribute matches the search term after the search term is converted to a [regular expression](http://www.w3schools.com/jsref/jsref_obj_regexp.asp).

#### Relation Modifiers <a id="relation-modifiers"></a>

The values used when making these comparisons are case insensitive strings. So for example the predicate `@text = mOOse` will match an item whose text is `mooSE`. Relations ignore case differences by default.

You can change this behavior by providing a modifier after the relation:

```text
@text = [modifier] value
```

The available modifiers are:

`i` : Case insensitive compare. \(the default\)

`s` : Case sensitive compare.

`n` : Numeric compare. Both sides of the compare are converted to dates before comparing. This means `01` will equal `1`, which is not true when doing the default string compare.

`d` : Date compare. Both sides of the compare are converted to dates before comparing. The date format is described in the [Dates](https://www.taskpaper.com/guide/reference/dates) reference section.

`l` : List compare. Both sides of the compare are converted to lists \(comma separated\) before comparing.

For instance say you have the tag `@job(Jane,John)`. If you want to find all jobs with "John" you might try searching for `@job = John`. But that won't work because the tag value is really the string "Jane,John". \(You could search for `@job contains John` and that would work in this case, but would also match `@job(Johny)` etc\)

Instead to do this use the list modifier and say `@job contains[l] John`. With the list modifier present the tag value is converted to a list before comparison and will only return matches that contain the list value "John". If you want to do a case sensitive search you can also include the `s` modifier like this: `@job contains[sl] John`.

### Values <a id="values"></a>

Sometimes you might need a value that has special meaning in the search syntax.

For example you might want to search for the word "and". But since "and" is part of the predicate syntax the search will be invalid. To resolve this enclose your the value in quotes.

_Invalid_ because "and" is a keyword:

```text
contains and
```

_Valid_ because "and" is in quotes:

```text
contains "and"
```

### Boolean expressions <a id="boolean-expressions"></a>

You can combine predicates with logical `and`, `or`, and `not` operators. This search will match items that contain the text "one" or "two", but do not contain "three":

```text
(one or two) and not three
```

## Shortcuts <a id="shortcuts"></a>

It's common to search TaskPaper items based on there type: project, task, or note.

For example you might want to find the "Inbox" project. The default way to do this would be:

```text
@type = project and Inbox
```

TaskPaper adds a shortcut for type based searches. The shortcut version of this search is:

```text
project Inbox
```

These are the shortcut forms and what they expand to:

* `project` expands to `@type = project and`
* `task` expands to `@type = task and`
* `note` expands to `@type = note and`

## Item Paths <a id="item-paths"></a>

Item paths control which parts of the outline to search. For example if we only wanted to search within a particular project we could use item paths. The item path concept comes from [Xpath](http://www.w3schools.com/xpath/).

The examples so far have all uses the default "search everywhere" path. That's the path used when no other path is specified. Next we'll learn how to limit our searches based on the outline structure.

### Steps <a id="steps"></a>

Item paths are make from a series of steps. Each step consists of an axis and a predicate. The axis determines which items to consider, and the predicate selects from those items. Each step selects items based on the results of the previous step.

Item paths work like file system paths:

```text
/my heading/subhead
```

This path evaluates:

1. The first step `/my heading` considers all top level items and selects ones that contain `my heading`.
2. The second step `/subhead` considers all direct children of the items selected in the fist step. It selects those that contain `subhead`.
3. The children selected in the last step are the match results.

In the above example each step considered items along the `/` "child" axis. Here's an example that searches along another axis:

```text
/my heading//subhead
```

Notice the extra `/` in `//subhead`. That syntax means that the second step should search along the `descendant` axis. It will consider "my heading" descendants instead of just the direct children.

It's sometimes useful to select all items along a particular axis. In that case you can use the wild card predicate `*`. Here's an example:

```text
/*
```

That item path says to select all top level items.

### Axes <a id="axes"></a>

Generally item paths follow the same [axis rules and syntaxes](http://www.w3schools.com/xpath/xpath_axes.asp) as defined by Xpath. It is seldom that you will need any axis beyond the children `/`, descendants `//`, or descendant-or-self `///` axis, but here they all are for completeness.

`ancestor` : Returns all ancestors matching predicate. For example `/my heading/ancestor::*`

`ancestor-or-self` : Returns items and their ancestors matching predicate. For example `/my heading/ancestor-or-self::*`

`descendant` : Returns all descendants matching predicate. Same as '//' operator. For example `/my heading/descendant::*`

`descendant-or-self` : Returns items and their descendants matching predicate. For example `/my heading/descendant-or-self::*`

`following` : Returns all items following each of the previously matched items. For example `/my heading/following::*`

`following-sibling` : Returns sibling items following each of the previously matched items. For example `/my heading/following-sibling::*`

`preceding` : Returns all items preceding each of the previously matched items. For example `/my heading/preceding::*`

`preceding-sibling` : Returns sibling items preceding each of the previously matched items. For example `/my heading/preceding-sibling::*`

`child` : Searches child item, same as '/' operator. For example `/my heading/child::*`

`parent` : Searches parent item, same as '..' operator. For example `/my heading/parent::*`

## Set Operations <a id="set-operations"></a>

Item paths support the set operations `union`, `intersect`, and `except`.

```text
(project Inbox//* union //@today) except //@done
```

This path matches all items in the "Inbox" project. Combines those with all items in the outline tagged "@today". And then removes all item items tagged with "@done".

## Slicing Results <a id="slicing-results"></a>

Sometimes you don't want all the results of your item path. In that case you can "slice" the results.

Determining your "next actions" for each project is one place where you might use this. This is what our outline looks like:

```text
Project 1:
    - task 1 @done
    - task 2
    - task 3
Project 2:
    - task 1 @done
    - task 2 @done
    - task 3
```

Here's a first try for showing next actions:

```text
project *//not @done
```

It says:

1. For each project with any `*` text
2. Show me all contained items that are not @done

That's close, but it shows more then we want. We don't want to see all things we need to do in each project, just the _first_ thing, the next action. This is where slicing can help:

```text
project *//not @done[0]
```

I've added `[0]` to the end of the second step, and now the path matches only the first not @done item for each project. Our next actions!

You can slice the results of a particular step, as shown above, or you can slice the results of an entire item path like this:

```text
(project *//not @done)[0]
```

That path matches only the first incomplete item in the outline.

You can slice the results of a single predicate as in the first example. Or you can slice the results of an item path expression in parentheses as in the second example.

The full slice syntax is:

```text
[start:end] // slices from start to end - 1
[start:] // slices from start through the rest of the list
[:end] // slices from the beginning to end - 1
[:] // slices through the entire list
[index] // slices item at given index
```

