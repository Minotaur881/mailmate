# Added Keyboard Maestro macro@91d5f3a

[Permalink](added-keyboard-maestro-macro-91d5f3a.md)

[Browse files](https://github.com/brunocbr/dtp-browser-workflow/tree/91d5f3ae6d7cb0ac2421e9c552bab3e4e3e916e8)

 Added Keyboard Maestro macro

* Loading branch information

|  |  | @@ -0,0 +1,101 @@ |
| :--- | :--- | :--- |
|  |  |  xml version="1.0" encoding="UTF-8"?&gt; |
|  |  |  DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd"&gt; |
|  |  |  &lt;plist version="1.0"&gt; |
|  |  |  &lt;array&gt; |
|  |  |  &lt;dict&gt; |
|  |  |  &lt;key&gt;Activatekey&gt; |
|  |  |  &lt;string&gt;Normalstring&gt; |
|  |  |  &lt;key&gt;CreationDatekey&gt; |
|  |  |  &lt;real&gt;532200125.98765397real&gt; |
|  |  |  &lt;key&gt;Macroskey&gt; |
|  |  |  &lt;array&gt; |
|  |  |  &lt;dict&gt; |
|  |  |  &lt;key&gt;Actionskey&gt; |
|  |  |  &lt;array&gt; |
|  |  |  &lt;dict&gt; |
|  |  |  &lt;key&gt;DisplayKindkey&gt; |
|  |  |  &lt;string&gt;Nonestring&gt; |
|  |  |  &lt;key&gt;IncludeStdErrkey&gt; |
|  |  |  &lt;false/&gt; |
|  |  |  &lt;key&gt;MacroActionTypekey&gt; |
|  |  |  &lt;string&gt;ExecuteAppleScriptstring&gt; |
|  |  |  &lt;key&gt;NotifyOnFailurekey&gt; |
|  |  |  &lt;false/&gt; |
|  |  |  &lt;key&gt;Pathkey&gt; |
|  |  |  &lt;string&gt;string&gt; |
|  |  |  &lt;key&gt;StopOnFailurekey&gt; |
|  |  |  &lt;false/&gt; |
|  |  |  &lt;key&gt;Textkey&gt; |
|  |  |  &lt;string&gt;tell application "Alfred 3" to run trigger "refresh" in workflow "br.com.brunoc.dtpbrowser" with argument "silent"string&gt; |
|  |  |  &lt;key&gt;TimeOutAbortsMacrokey&gt; |
|  |  |  &lt;true/&gt; |
|  |  |  &lt;key&gt;TrimResultskey&gt; |
|  |  |  &lt;true/&gt; |
|  |  |  &lt;key&gt;TrimResultsNewkey&gt; |
|  |  |  &lt;true/&gt; |
|  |  |  &lt;key&gt;UseTextkey&gt; |
|  |  |  &lt;true/&gt; |
|  |  |  dict&gt; |
|  |  |  array&gt; |
|  |  |  &lt;key&gt;CreationDatekey&gt; |
|  |  |  &lt;real&gt;571450379.82107699real&gt; |
|  |  |  &lt;key&gt;ModificationDatekey&gt; |
|  |  |  &lt;real&gt;571613892.79163694real&gt; |
|  |  |  &lt;key&gt;Namekey&gt; |
|  |  |  &lt;string&gt;Refresh dtp-browser cache @ login and periodicallystring&gt; |
|  |  |  &lt;key&gt;Triggerskey&gt; |
|  |  |  &lt;array&gt; |
|  |  |  &lt;dict&gt; |
|  |  |  &lt;key&gt;ExecuteTypekey&gt; |
|  |  |  &lt;string&gt;Loginstring&gt; |
|  |  |  &lt;key&gt;MacroTriggerTypekey&gt; |
|  |  |  &lt;string&gt;Timestring&gt; |
|  |  |  &lt;key&gt;Repeatkey&gt; |
|  |  |  &lt;false/&gt; |
|  |  |  &lt;key&gt;RepeatTimekey&gt; |
|  |  |  &lt;integer&gt;60integer&gt; |
|  |  |  &lt;key&gt;TimeFinishHourkey&gt; |
|  |  |  &lt;integer&gt;17integer&gt; |
|  |  |  &lt;key&gt;TimeFinishMinuteskey&gt; |
|  |  |  &lt;integer&gt;30integer&gt; |
|  |  |  &lt;key&gt;TimeHourkey&gt; |
|  |  |  &lt;integer&gt;8integer&gt; |
|  |  |  &lt;key&gt;TimeMinuteskey&gt; |
|  |  |  &lt;integer&gt;30integer&gt; |
|  |  |  &lt;key&gt;WhichDayskey&gt; |
|  |  |  &lt;integer&gt;127integer&gt; |
|  |  |  dict&gt; |
|  |  |  &lt;dict&gt; |
|  |  |  &lt;key&gt;ExecuteTypekey&gt; |
|  |  |  &lt;string&gt;Whilestring&gt; |
|  |  |  &lt;key&gt;MacroTriggerTypekey&gt; |
|  |  |  &lt;string&gt;Timestring&gt; |
|  |  |  &lt;key&gt;Repeatkey&gt; |
|  |  |  &lt;true/&gt; |
|  |  |  &lt;key&gt;RepeatTimekey&gt; |
|  |  |  &lt;integer&gt;43200integer&gt; |
|  |  |  &lt;key&gt;TimeFinishHourkey&gt; |
|  |  |  &lt;integer&gt;23integer&gt; |
|  |  |  &lt;key&gt;TimeFinishMinuteskey&gt; |
|  |  |  &lt;integer&gt;59integer&gt; |
|  |  |  &lt;key&gt;TimeHourkey&gt; |
|  |  |  &lt;integer&gt;0integer&gt; |
|  |  |  &lt;key&gt;TimeMinuteskey&gt; |
|  |  |  &lt;integer&gt;0integer&gt; |
|  |  |  &lt;key&gt;WhichDayskey&gt; |
|  |  |  &lt;integer&gt;127integer&gt; |
|  |  |  dict&gt; |
|  |  |  array&gt; |
|  |  |  &lt;key&gt;UIDkey&gt; |
|  |  |  &lt;string&gt;9ED68C95-7208-4C4E-93CC-2109BC918DD7string&gt; |
|  |  |  dict&gt; |
|  |  |  array&gt; |
|  |  |  &lt;key&gt;Namekey&gt; |
|  |  |  &lt;string&gt;Minhas macrosstring&gt; |
|  |  |  &lt;key&gt;ToggleMacroUIDkey&gt; |
|  |  |  &lt;string&gt;225BDD8B-A65A-4ED0-8223-1E4CBE675ABAstring&gt; |
|  |  |  &lt;key&gt;UIDkey&gt; |
|  |  |  &lt;string&gt;B55F10A2-F2D1-4B17-92D6-436E26AB5D35string&gt; |
|  |  |  dict&gt; |
|  |  |  array&gt; |
|  |  |  plist&gt; |

