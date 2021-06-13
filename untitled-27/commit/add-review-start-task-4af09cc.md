# Add Review/Start Task@4af09cc

[Permalink](add-review-start-task-4af09cc.md)

[Browse files](https://github.com/brandonpittman/OmniFocus/tree/4af09ccc344c60b4c3395548b03c925cf7fd4ead)

 Add Review/Start Task

* Loading branch information

|  |  | @@ -0,0 +1,3 @@ |
| :--- | :--- | :--- |
|  |  |  \# Add Review Task |
|  |  |  |
|  |  |  Run this script on a project to create a daily-deferred task with a name of "Review: \`name of project\`". |

|  |  | @@ -0,0 +1,3 @@ |
| :--- | :--- | :--- |
|  |  |  \# Add Start Task |
|  |  |  |
|  |  |  Run this script on a project to create a task with a name of "Start: \`name of project\`". Also, it sets the \`sequential\` property of the project to \`true\`. |

|  | @@ -3,6 +3,7 @@ function of -d "Parse transport text" |  |
| :--- | :--- | :--- |
|  |  |  open -a OmniFocus |
|  |  |  else |
|  |  |  osascript -e "tell application \"OmniFocus\" to parse tasks into default document with transport text \"$argv\"" &gt; /dev/null |
|  |  |  \# tint is a handy fish shell plugin for outputting color. |
|  |  |  tint: green "Task added to OmniFocus inbox." |
|  |  |  return 0 |
|  |  |  end |
|  |  |  |

