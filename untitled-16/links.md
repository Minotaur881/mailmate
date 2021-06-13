# Links

TaskPaper auto-creates clickable links when it recognizes link text. Here are some examples of the links that it recognizes:

## URLs <a id="urls"></a>

* `www.taskpaper.com`
* `http://www.taskpaper.com`

## Emails <a id="emails"></a>

* `jesse@hogbaysoftware.com`
* `mailto:jesse@hogbaysoftware.com`

Generally TaskPaper will recognize URIs of the form `scheme:path`. When you click on such a link the URI is handed off to macOS to resolve. In the case of `mailto:address` links the system will open your email program.

## File Links <a id="file-links"></a>

* `file:///Users/jesse/Desktop/myfile.txt`
* `/Users/jesse/Desktop/myfile.txt`
* `./myfile.txt`

You can create absolute links \(starting with `/`\) by dragging and dropping files onto your TaskPaper document. Relative links \(starting with `./`\) are relative to the location where your TaskPaper document is saved. Note, often Finder will hide file extensions such as `.txt`. For TaskPaper links to work you must type in the exact file name, including any file extensions.

You must escape spaces in file links using `\`. For example to create a relative link to the file "my file.txt" you will need this link: `./my\ file.txt`

In the direct download version of TaskPaper clicking a file link will open that file in its associated application. In the Mac App Store version of TaskPaper clicking a link will reveal that file in the Finder. \(Sandbox restrictions don't allow TaskPaper to automatically open it\)

