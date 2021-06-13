# vitorgalvao/alfred-workflows

Run browser [bookmarklets](http://en.wikipedia.org/wiki/Bookmarklet) from Alfred, without needing to having them installed in the browser itself.

Note that you may need to `Allow JavaScript from Apple Events` in your Browser.

### 1

For the first step, get this template workflow itself. Though this is not strictly necessary \(you can build it yourself\) it serves as a starting point with most of the work already done. Proceed to open the workflow in Alfred.

Next, get a browser bookmarklet to convert by copying its link address.

[![](https://camo.githubusercontent.com/da466e05bd1fb5f56889077a19354b87c5618491aaa4d821ca3a111393f5ff1f/68747470733a2f2f692e696d6775722e636f6d2f644a3558676b422e676966)](https://camo.githubusercontent.com/da466e05bd1fb5f56889077a19354b87c5618491aaa4d821ca3a111393f5ff1f/68747470733a2f2f692e696d6775722e636f6d2f644a3558676b422e676966)

### 2

Run `:cleanbookmarkletcode` to clean the code in your clipboard. It performs substitutions necessary to avoid problems when pasting the code in the next step.

[![](https://camo.githubusercontent.com/d12aadec5cd0eebff9bba7a29c57a3c562970904c8908e19a7e14aca56f51f2a/68747470733a2f2f692e696d6775722e636f6d2f6f4944455663642e706e67)](https://camo.githubusercontent.com/d12aadec5cd0eebff9bba7a29c57a3c562970904c8908e19a7e14aca56f51f2a/68747470733a2f2f692e696d6775722e636f6d2f6f4944455663642e706e67)

### 3

Open the `Arg and Vars` node and paste the code.

[![](https://camo.githubusercontent.com/4d5802c3ba79665f73bc475e233c0b43489cd44a0ca05f3c2f4517942ae28016/68747470733a2f2f692e696d6775722e636f6d2f395350596b6d4d2e676966)](https://camo.githubusercontent.com/4d5802c3ba79665f73bc475e233c0b43489cd44a0ca05f3c2f4517942ae28016/68747470733a2f2f692e696d6775722e636f6d2f395350596b6d4d2e676966)

## Extra

If you’re not new to Alfred, you likely won’t need these steps as you’ll know what to do.

### 4

The template includes both a `Keyword` and a `Hotkey` nodes to run the code. You can delete either one by clicking on it and pressing ⌫.

[![](https://camo.githubusercontent.com/82d691d188f76d873e5225b3049cabb0ebbe0e75459004c72f37877bb3ded715/68747470733a2f2f692e696d6775722e636f6d2f505270434875332e676966)](https://camo.githubusercontent.com/82d691d188f76d873e5225b3049cabb0ebbe0e75459004c72f37877bb3ded715/68747470733a2f2f692e696d6775722e636f6d2f505270434875332e676966)

### 5

If you choose to use the workflow via `Keyword`, do not forget to set it up.

[![](https://camo.githubusercontent.com/e842ccd1706e220682024057d43ed786be3b12b958c9426fd8d188e70baf9bb1/68747470733a2f2f692e696d6775722e636f6d2f454e46594141652e676966)](https://camo.githubusercontent.com/e842ccd1706e220682024057d43ed786be3b12b958c9426fd8d188e70baf9bb1/68747470733a2f2f692e696d6775722e636f6d2f454e46594141652e676966)

### 6

Lastly, edit the workflow’s details and its icon. For completeness it’s pre-filled with my details. Feel free to edit them.

[![](https://camo.githubusercontent.com/ae0f4712466dfc10779e0cbfd2b6a7d1b5f833c7bf0511745ca4aafb4166ff18/68747470733a2f2f692e696d6775722e636f6d2f4b7849464932412e706e67)](https://camo.githubusercontent.com/ae0f4712466dfc10779e0cbfd2b6a7d1b5f833c7bf0511745ca4aafb4166ff18/68747470733a2f2f692e696d6775722e636f6d2f4b7849464932412e706e67)

