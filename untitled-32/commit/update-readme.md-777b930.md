# Update README.md@777b930

[Permalink](update-readme.md-777b930.md)

 Showing with **1 addition** and **1 deletion**.

1.  +1 −1 [auto-convert-web-page-to-PDF/README.md](update-readme.md-777b930.md#diff-97de8fed0ad7540ad9f09cbb4fcbe9506370646bf5d938d4bf35cde50da3d1f0)

|  | @@ -5,7 +5,7 @@ I find that DEVONthink is one of the best tools for saving snapshots of web page |  |
| :--- | :--- | :--- |
|  |  |  |
|  |  |  However, I'm not always browsing the web from within DEVONthink, and if I want to save a page encountered while using a normal web browser like Safari, I need to send it to DEVONthink and tell it to save it as a full-page PDF. This could be done using the standard clipper extension or bookmarklet provided with DEVONthink, but there is a catch: some web pages are generated dynamically and sent incrementally, with content not revealed until you scroll further down on the page. DEVONthink's default capture method will not always get the full page in those cases. |
|  |  |  |
|  |  |  In general, capturing dynamically-generated pages is a hopeless difficulty task. However, for my purposes, I've solved this for most cases using a combination of mechanisms: |
|  |  |  In general, capturing dynamically-generated pages is a hopelessly difficult task. However, for my purposes, I've solved this for most cases using a combination of mechanisms: |
|  |  |  |
|  |  |  1. A Smart Rule in DEVONthink that is triggered when a new web page bookmark is created if the bookmark contains a certain tag; this Smart Rule then runs an AppleScript program to open the page, scroll down in it, and convert the resulting window contents to PDF. |
|  |  |  2. A custom bookmarklet that can be used from Safari that, when invoked, sends a URL to DEVONthink with the required tag. |
|  |  |  |

