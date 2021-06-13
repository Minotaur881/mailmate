# SkydiveMike/templates

 [Fix First Run Templates Folder finding](https://github.com/SkydiveMike/templates/commit/8b18a5817e3f8e6bfff160647785c781a4b6b985)

```text
The user may (likely) have the Templates folder hidden (Dropped).

The logic to temporarily show the Templates folder only runs after the
Script has identified the folder and saved it to property
specialTemplateFolder.

This means that on a first run of the script, it will not find a
hidden Templates folder.

Remove that exclusion criteria from the return every flattened project
call in projectListWithExclusions(containingFolder)
```

