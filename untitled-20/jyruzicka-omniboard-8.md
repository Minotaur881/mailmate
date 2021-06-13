# jyruzicka/omniboard

```text
Hopefully integrating all the little changes, bugfixes, and modificat…
…ions that I've wanted to do for a while.

* [New] `Omniboard::document=` is available if you just want to set Omniboard's document variable by yourself without all that hassle of loading from file.
* [New] If your document has no fetcher, it's always considered to be at head.
* [New] Substantial changes to how groups work. You may now return any object from a `group_by` method, and use that object to sort your groups before displaying names. See the Readme for more information on how to use the updated groups.
* [New] You can now custom colour your groups! See the Readme for more information.
* [New] The column's `icon` methods may now return an array of `[icon, alt]`, for supplying popup information on icons.
* [New] You can add a "refresh" link to the top of the page using the `refresh_link` property inside `config`.
* [New] Setting `hide_dimmed` on a column will automatically hide dimmed projects on page load
* [New] Set project counts using the `display_project_counts` property on columns. Can be set to `all`, `active`, or `marked`.
```

