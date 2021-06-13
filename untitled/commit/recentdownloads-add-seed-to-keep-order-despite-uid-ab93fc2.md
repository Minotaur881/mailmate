# RecentDownloads: Add seed to keep order despite uid@ab93fc2

[Permalink](recentdownloads-add-seed-to-keep-order-despite-uid-ab93fc2.md)

[Browse files](../tree/vitorgalvao-alfred-workflows.md)

 RecentDownloads: Add seed to keep order despite uid

* Loading branch information

|  | @@ -851,7 +851,7 @@ By default the Workflow looks in \`~/Downloads\`. Change the value in the \`downloa |  |
| :--- | :--- | :--- |
|  |  |  &lt;string&gt;~/Downloadsstring&gt; |
|  |  |  dict&gt; |
|  |  |  &lt;key&gt;versionkey&gt; |
|  |  |  &lt;string&gt;21.6string&gt; |
|  |  |  &lt;string&gt;21.7string&gt; |
|  |  |  &lt;key&gt;webaddresskey&gt; |
|  |  |  &lt;string&gt;http://vitorgalvao.com/string&gt; |
|  |  |  dict&gt; |
|  |  |  |

|  | @@ -51,10 +51,15 @@ Added\_cache\_file = Pathname.new\(ENV\['alfred\_workflow\_cache'\]\).join\('added\_cache. |  |
| :--- | :--- | :--- |
|  |  |  |
|  |  |  Downloads\_dir = get\_env\( |
|  |  |  env\_variable: ENV\['downloads\_dir'\], |
|  |  |  default: Pathname.new\(ENV\['HOME'\]\).join\('Downloads'\).to\_path, |
|  |  |  default: Pathname.new\(ENV\['HOME'\]\).join\('Downloads'\), |
|  |  |  as\_pathname: true |
|  |  |  \) |
|  |  |  |
|  |  |  Uid\_seed = get\_env\( |
|  |  |  env\_variable: ENV\['uid\_seed'\], |
|  |  |  default: rand.to\_s |
|  |  |  \) |
|  |  |  |
|  |  |  \# Main |
|  |  |  All\_entries = Downloads\_dir.children.reject { \|p\| p.basename.to\_path.start\_with?\('.'\) } |
|  |  |  |
|  | @@ -85,7 +90,7 @@ Script\_filter\_items = Entries.each\_with\_object\(\[\]\) { \|entry, items\| |  |
|  |  |  name = entry.directory? ? entry.basename.to\_path : entry.basename\(entry.extname\).to\_path |
|  |  |  |
|  |  |  items.push\( |
|  |  |  uid: entry, |
|  |  |  uid: "\#{Uid\_seed} \#{entry}", |
|  |  |  type: 'file', |
|  |  |  title: name, |
|  |  |  subtitle: entry, |
|  | @@ -94,4 +99,4 @@ Script\_filter\_items = Entries.each\_with\_object\(\[\]\) { \|entry, items\| |  |
|  |  |  \) |
|  |  |  } |
|  |  |  |
|  |  |  puts\({ rerun: 2, items: Script\_filter\_items }.to\_json\) |
|  |  |  puts\({ variables: { uid\_seed: Uid\_seed }, rerun: 2, items: Script\_filter\_items }.to\_json\) |

