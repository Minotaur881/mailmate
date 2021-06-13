# FradSer/automation-omnifocus-3

### Files <a id="files"></a>

 [Permalink](https://github.com/FradSer/automation-omnifocus-3/tree/7bb52b1b661696b7af8215d11f9b8eb20489de92/complete-and-await-reply)

 Failed to load latest commit information.

Type

Name

Latest commit message

Commit time

## Complete and Await Reply [![](https://camo.githubusercontent.com/a97ee2bf38c9119e5c14cc8bff03daa69679406206555753cc07b7dca510252e/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f2d4f6d6e694a532d626c756576696f6c6574)](https://camo.githubusercontent.com/a97ee2bf38c9119e5c14cc8bff03daa69679406206555753cc07b7dca510252e/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f2d4f6d6e694a532d626c756576696f6c6574)

Mark the currently selected task as complete and add a new task to await the reply.

This script is based on the script from [OMNI-AUTOMATION.COM](https://omni-automation.com/omnifocus/plug-in-complete-await.html)

> It allows you to mark your currently selected task as complete, and duplicates the task with `Waiting on reply:` prefixed to the original task name.

### Changelog

#### v0.1.0

**Changed**

* Merge to [OmniFocus bundle](https://omni-automation.com/plugins/bundle.html) with icon.

#### v0.0.2

**Added**

* New shopping list task processing: If the selected task start with `purchasingPrefix`, "买" as default, then a dialogue appears to let user choose where will the item he bought ship. 

#### v0.0.1

**Added**

* Fork the [original copy](https://omni-automation.com/omnifocus/plug-in-complete-await.html),
* Append reply time to the end of duplicated task's note,
* No more `Waiting on reply: Waiting on reply:` in the duplicated task's name.

