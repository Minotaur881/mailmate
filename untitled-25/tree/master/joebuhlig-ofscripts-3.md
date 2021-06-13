# joebuhlig/OFScripts

## Daily Task Report

I like keeping a log of the work I've done every day. And since I keep all of my work in OmniFocus, it only makes sense to automatically create a report off of yesterdays completed tasks. That's exactly what this script does.

## Which File?

You'll find two versions of the script - `.scpt` and `.applescript`. In order to run it from OmniFocus, you'll want to use the `.scpt` version. The `.applescript` format is purely there so you can view the code online.

## Output

It will generate a plain text file with the following format:

```text
Weekday, Month Day, Year
------------------------
Project Name
Task Name ----- HH:MM:SS AM/PM
Task Name ----- HH:MM:SS AM/PM
Task Name ----- HH:MM:SS AM/PM
------------------------
Project Name
Task Name ----- HH:MM:SS AM/PM
Task Name ----- HH:MM:SS AM/PM
Task Name ----- HH:MM:SS AM/PM
```

## Running the Script

You could manually run this every day, but I've found Hazel to be much more reliable than me. Here's a screenshot of the rule I use to run this:

[![Hazel Rule](https://github.com/joebuhlig/OFScripts/raw/master/Daily%20Task%20Report/HazelRule.jpg)](https://github.com/joebuhlig/OFScripts/blob/master/Daily%20Task%20Report/HazelRule.jpg)

Note: If you're using Hazel for this you can run it one of two ways - embedded or external. You can embed the code in a Hazel action or link Hazel to an external script. If you're using the former, you'll need to pull the `hazelProcessFile` handler at the beginning and end of the script. So delete these two lines:

`on hazelProcessFile(theFile)`

`end hazelProcessFile`

This handler is only used when the script is run as an external script in Hazel.

## Setup

All you need to do is tell it where you want to save the files. Change this line:

`set filePath to "/Users/USERNAME/TaskReports/"`

## Development

I'm certainly open to the submission of Pull Requests to make this better. If you find issues and fix them, please let me know and I'll be happy to update and give you credit.

