# brandonpittman/OmniFocus

I just whipped up a neat little script that uses the latest version of my OmniFocus Library. It's called [Colonize](). You can use it to select some tasks in OmniFocus, and then if you run `Colonize.scpt`, it'll switch the first word of the task name into a prefix or into a bare word if the first word is already a prefix. This makes handling tasks like `Review daily logs` and `Review: daily logs` easy.

You will, of course, need my library installed first. This script is set up to work with LaunchBar already. If you pass "set" or "clear" to the script \(or on the command line\), instead of toggling, it'll blank set or clear colons.

