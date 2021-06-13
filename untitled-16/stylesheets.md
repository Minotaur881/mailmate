# StyleSheets

TaskPaper uses the [LESS](http://lesscss.org/) CSS pre-processor to build style sheets. This is a reference, see [Creating StyleSheets](https://www.taskpaper.com/guide/customizing-taskpaper/creating-stylesheets.html) for an introduction.

The set of style-able elements and attributes is different and limited compared to CSS/DOM styling. TaskPaper styling doesn't have a uniform set of element attributes and style properties. Instead different elements supports the attributes listed below.

To see TaskPaper's default stylesheet rules open `TaskPaper.app/Content/Resources/base-stylesheet.less`. This is also good general stylesheet formatting reference.

## Variables <a id="variables"></a>

Base Size:

* `@base-font-size`: Float;
* `@user-font-size`: Float;
  * Set by the View &gt; Zoom In and View &gt; Zoom Out menu commands. If you set to a fixed value in your stylesheet then those commands will stop working.
* `@ui-scale`: Float;
  * Ratio of `@user-font-size / @base-font-size`. You don't want to set this value, but you may want to use the variable to help calculate other values in your stylesheet. For example the base stylesheet adjust the default indent per level by this value, so indents scale larger as you zoom in.

UI Colors:

* `@tint-color`: Color;
* `@selection-color`: Color;
* `@invisibles-color`: Color;
* `@background-color`: Color;

Base Text:

* `@font-family`: Comma separated list of font names;
  * The strings should be the "generic" name of your desired font. For example use "Times" not "Times Italic". If you want to use the italic version of the font use the `font-style` attribute described below. TaskPaper uses the first available font from the list of font names.
* `@text-color`: Color;
* `@line-height-multiple:` Number;

Handles:

* `@handle-size`: Float;
* `@handle-color`: Color;
* `@handle-secondary-color`: Color;

## Elements <a id="elements"></a>

Each element has a name, attributes, and style properties.

* **Name**: The element name, used by selectors to select the element.
* **Attributes**: The attributes that `[attribute]` selectors may target.
* **Style Properties**: The properties that you can style on the element.

### Window Element <a id="window-element"></a>

Target the `window` element to style the window.

* Style Properties:
  * `appearance`: AppearanceStyle;

Target the `sidebar` element to style the project list sidebar.

* Style Properties:
  * `appearance`: AppearanceStyle;

### Searchbar Element <a id="searchbar-element"></a>

Target the `searchbar` element to style the editor searchbar.

* Style Properties:
  * `appearance`: AppearanceStyle;
  * `color`: Color;
  * `secondary-text-color`: Color;
  * `error-text-color`: Color;
  * `placeholder-color`: Color;
  * `background-color`: Color;

### Editor Element <a id="editor-element"></a>

Target the `editor` element to style the outline editor text area. Contains `item` elements.

* Style Properties:
  * `item-indent`: Float;
  * `caret-width`: Float;
  * `caret-color`: Color;
  * `drop-indicator-color`: Color;
  * `selection-background-color`: Color;
  * `guide-line-color`: Color;
  * `guide-line-width`: Float;
  * `fold-color`: Color;
  * `editor-wrap-to-column`: Float;
  * `item-wrap-to-column`: Float;
  * `top-padding-percent`: Float%; // for example `50%`
  * `bottom-padding-percent`: Float%;
  * `typewriter-scroll-percent`: Float%;

### Item Element <a id="item-element"></a>

Target the `item` element to style items. Contains `run` elements. For styling purposes does _not_ contain other `item` elements.

* Attributes:
  * `depth` - Item depth in outline.
  * `focused` - True if is focused item.
  * `mouseOver` - True if mouse is over item.
  * `mouseOverHandle` - True if mouse is over item's handle.
  * `leaf` - True if item has no children.
  * `expanced` - True for expanded items.
  * `collapsed` - True for collapsed items.
  * `empty` - True for items with no body text and no children.
  * Each `@tagname(value)` in the item's body text is exposed as `data-[tagname]`.
* Style Properties:
  * `handle-size`: Float;
  * `handle-color`: Color;
  * `handle-border-color`: Color;
  * `handle-border-width`: Float;
  * `line-height-multiple`: Float;
  * `paragraph-spacing-before`: Float;
  * `paragraph-spacing-after`: Float;
  * `color`: Color; _inherited_
  * `font-family`: Font; _inherited_
  * `font-style`: normal \| italic; _inherited_
  * `font-weight`: normal \| bold; _inherited_
  * `font-size`: Float; _inherited_
  * `cursor`: default \| pointer \| text;
  * `background-color`: Color;
  * `text-decoration`: none \| underline \| line-through;
  * `text-underline`: LineStyle;
  * `text-underline-color`: Color;
  * `text-strikethrough`: LineStyle;
  * `text-strikethrough-color`: Color;
  * `text-baseline-offset`: Float;
  * `text-expansion`: Float;

### Run Element <a id="run-element"></a>

Target the `run` element to style item body text runs.

* Attributes:
  * `tag` - Associated value is tag name.
  * `link` - Associated value is URL string.
* Style Properties:
  * `color`: Color; _inherited_
  * `font-family`: Font; _inherited_
  * `font-style`: normal \| italic; _inherited_
  * `font-weight`: normal \| bold; _inherited_
  * `font-size`: Float; _inherited_
  * `cursor`: default \| pointer \| text;
  * `background-color`: Color;
  * `text-decoration`: none \| underline \| line-through;
  * `text-underline`: LineStyle;
  * `text-underline-color`: Color;
  * `text-strikethrough`: LineStyle;
  * `text-strikethrough-color`: Color;
  * `text-baseline-offset`: Float;
  * `text-expansion`: Float;

## Style Property Value Formats <a id="style-property-value-formats"></a>

* `Float`: Floating point number.
* `String`: Quoted or unquoted text string.
* `Font`: Comma separated list of font names.
* `Color`: A standard CSS color declaration. See [CSS Colors](http://www.w3schools.com/css/css_colors.asp) for more information.
* `AppearanceStyle`: `NSAppearanceNameVibrantLight` or `NSAppearanceNameVibrantDark`
* `LineStyle`: A space separated list of the following items. Each listed item combines with the other listed items to create a final line style. See [NSUnderlineStyle](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/NSAttributedString_UIKit_Additions/index.html#//apple_ref/c/tdef/NSUnderlineStyle) for more information.
  * NSUnderlineStyleNone
  * NSUnderlineStyleSingle
  * NSUnderlineStyleThick
  * NSUnderlineStyleDouble
  * NSUnderlinePatternSolid
  * NSUnderlinePatternDot
  * NSUnderlinePatternDash
  * NSUnderlinePatternDashDot
  * NSUnderlinePatternDashDotDot
  * NSUnderlineByWord

