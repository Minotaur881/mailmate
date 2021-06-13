# deaghean/omnifocus-plugins

## Commits on May 29, 2021

1.  [Update Toggle Tag plugins](https://github.com/deaghean/omnifocus-plugins/commit/c775cc1c9f4f9195a8e0a713d9038f05f51d3c25)

   ```text
   Some code cleanup. Also switches to using the tag id as the identifier for the ToggleTag bundle (this allows the keyboard shortcuts to follow the tag rather than the order in the menu).
   ```

## Commits on Oct 28, 2020

1.  [Add SortProjects.omnijs](https://github.com/deaghean/omnifocus-plugins/commit/84f497d824a9d63e02fc2dc225e783c9c2d3409a)

   ```text
   This one's probably too specific to my previous needs, but adding it anyway so it exists somewhere.
   ```

## Commits on Jun 5, 2020

1. 2.  [A change to how the generated Toggle Tag plugin handles mixed selections](https://github.com/deaghean/omnifocus-plugins/commit/a0f126e8516bd51fb14533b528216a12b39da8f7)

   ```text
   Previously, if the first item had the tag, it would remove the tag from all selected items, and if not add the tag to the entire selection.

   Now it adds the tag if *any* of the selected items are missing the tag, and removes otherwise.

   (I'm going to update the standalone ToggleTag.omnijs plugin shortly to match this behavior)
   ```

