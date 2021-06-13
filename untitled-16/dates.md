# Dates

Use TaskPaper's date and time format to store dates and to perform date `[d]` searches.

TaskPaper has a good foundation to support dates, but it's missing convenience. It still needs things like a easy user interface for inputting dates. As it stands now I would recommend dates for those who like to mess around and experiment. Otherwise they might cause you more pain and confusion then benefit as this point.

## Example <a id="example"></a>

```text
- Order seeds @due(2016-03-16)
- Go to movies @due(2016-03-18 7pm)
```

Using date based searches \(notice the `[d]`\) you can find both items like this:

```text
@due <=[d] March 18 7pm
```

Try changing the `7pm` to `6pm` and you will no longer find the second item. Even better you can also use relative dates in your searches.

For example try:

```text
@due <=[d] today + 24h
```

If today is March 18th \(it is for me right now!\) then that search will find the first item. `today` starts at midnight, so I add the `24h` to cover the entire day. Relative dates are great for saved searches.

## Date/Time Formats <a id="datetime-formats"></a>

These examples show the different formats that you can use when entering dates and times.

### Dates <a id="dates"></a>

Dates resolve to midnight of the given date:

* `2016`
* `2016-01`
* `2016-01-10`
* `today`
* `tomorrow`
* `next Week`
* `next Month`
* `next Monday`
* `last June`
* `June`
* `next June`
* `next June 3`

**Note** `week` resolves to ISO standard weeks that start on Monday, not Sunday.

### Times <a id="times"></a>

Times are relative to the current date:

* `6 am`
* `3:15 pm`
* `16:15`

### Durations <a id="durations"></a>

Durations offset from the current time:

* `2 days`
* `+1 week`
* `-6 hours`
* `2 days 6 hours`

### Combinations <a id="combinations"></a>

You can combine dates, times, and durations:

* `tomorrow 9am`
* `Nov 26 3:15 +1day`

### ISO 8601 Strings <a id="iso-8601-strings"></a>

If TaskPaper's date and time parser doesn't recognize a date it uses the [momentjs](http://momentjs.com/docs/#/parsing/string/) library to parse the date. This gives support for ISO 8601 strings.

