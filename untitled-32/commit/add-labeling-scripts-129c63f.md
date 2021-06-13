# Add labeling scripts@129c63f

[Permalink](add-labeling-scripts-129c63f.md)

[Browse files](https://github.com/mhucka/devonthink-hacks/tree/129c63f97d143b2fc5db6c58767b8144c773afb9)

 Add labeling scripts

* Loading branch information

|  |  | @@ -0,0 +1,8 @@ |
| :--- | :--- | :--- |
|  |  |  on triggered\(the\_group\) |
|  |  |  tell application id "DNtp" |
|  |  |  set group\_records to children of the\_group |
|  |  |  repeat with r in group\_records |
|  |  |  set the label of r to 1 |
|  |  |  end repeat |
|  |  |  end tell |
|  |  |  end triggered |

|  |  | @@ -0,0 +1,8 @@ |
| :--- | :--- | :--- |
|  |  |  on triggered\(the\_group\) |
|  |  |  tell application id "DNtp" |
|  |  |  set group\_records to children of the\_group |
|  |  |  repeat with r in group\_records |
|  |  |  set the label of r to 2 |
|  |  |  end repeat |
|  |  |  end tell |
|  |  |  end triggered |

|  |  | @@ -0,0 +1,8 @@ |
| :--- | :--- | :--- |
|  |  |  on triggered\(the\_group\) |
|  |  |  tell application id "DNtp" |
|  |  |  set group\_records to children of the\_group |
|  |  |  repeat with r in group\_records |
|  |  |  set the label of r to 3 |
|  |  |  end repeat |
|  |  |  end tell |
|  |  |  end triggered |

