# Fixes \#33 UI strings read 'Github' instead of 'GitHub'@69d8b51

[Permalink](fixes-33-ui-strings-read-github-instead-of-github-69d8b51.md)

[Browse files](../tree/edgarjs-alfred-github-repos.md)

Fixes [\#33](../issues/ui-strings-read-github-instead-of-github-issue-33.md) UI strings read 'Github' instead of 'GitHub'

* Loading branch information

|  | @@ -84,7 +84,7 @@ This project is published under the \[MIT License\]\(LICENSE.md\). |  |
| :--- | :--- | :--- |
|  |  |  \[github-search\]: https://docs.github.com/en/free-pro-team@latest/github/searching-for-information-on-github/searching-on-github |
|  |  |  \[download-packal\]: https://www.packal.org/workflow/github-repos |
|  |  |  \[download-releases\]: https://github.com/edgarjs/alfred-github-repos/releases |
|  |  |  \[personal-access-token\]: https://github.com/settings/tokens/new?description=Github%20Repos%20Alfred%20workflow&scopes=repo |
|  |  |  \[personal-access-token\]: https://github.com/settings/tokens/new?description=GitHub%20Repos%20Alfred%20workflow&scopes=repo |
|  |  |  \[pulls-page\]: https://github.com/pulls |
|  |  |  \[notifications-page\]: https://github.com/notifications |
|  |  |  \[alfred-env-vars\]: https://www.alfredapp.com/help/workflows/script-environment-variables/ |

|  | @@ -3,7 +3,7 @@ |  |
| :--- | :--- | :--- |
|  |  |  $stdout.sync = true |
|  |  |  $LOAD\_PATH.unshift File.expand\_path\('lib'\) |
|  |  |  |
|  |  |  require 'data\_source/client/github' |
|  |  |  require 'data\_source/client/git\_hub' |
|  |  |  require 'data\_source/pull\_requests' |
|  |  |  require 'data\_source/repositories' |
|  |  |  require 'commands/help' |
|  | @@ -14,7 +14,7 @@ |  |
|  |  |  class App |
|  |  |  class &lt;&lt; self |
|  |  |  def client |
|  |  |  DataSource::Client::Github.new\( |
|  |  |  DataSource::Client::GitHub.new\( |
|  |  |  host: ENV\['GITHUB\_API\_HOST'\], |
|  |  |  access\_token: ENV\['GITHUB\_ACCESS\_TOKEN'\], |
|  |  |  me\_account: ENV\['GITHUB\_ME\_ACCOUNT'\], |
|  |  |  |

|  | @@ -355,7 +355,7 @@ fi |  |
| :--- | :--- | :--- |
|  |  |  &lt;key&gt;spaceskey&gt; |
|  |  |  &lt;string&gt;string&gt; |
|  |  |  &lt;key&gt;urlkey&gt; |
|  |  |  &lt;string&gt;https://{var:GITHUB\_HOST}/settings/tokens/new?description=Github%20Repos%20Alfred%20workflow&scopes=repostring&gt; |
|  |  |  &lt;string&gt;https://{var:GITHUB\_HOST}/settings/tokens/new?description=GitHub%20Repos%20Alfred%20workflow&scopes=repostring&gt; |
|  |  |  &lt;key&gt;utf8key&gt; |
|  |  |  &lt;false/&gt; |
|  |  |  dict&gt; |
|  | @@ -448,7 +448,7 @@ fi |  |
|  |  |  &lt;key&gt;spaceskey&gt; |
|  |  |  &lt;string&gt;string&gt; |
|  |  |  &lt;key&gt;urlkey&gt; |
|  |  |  &lt;string&gt;https://{var:GITHUB\_HOST}/settings/tokens/new?description=Github%20Repos%20Alfred%20workflow&scopes=repostring&gt; |
|  |  |  &lt;string&gt;https://{var:GITHUB\_HOST}/settings/tokens/new?description=GitHub%20Repos%20Alfred%20workflow&scopes=repostring&gt; |
|  |  |  &lt;key&gt;utf8key&gt; |
|  |  |  &lt;false/&gt; |
|  |  |  dict&gt; |
|  |  |  |

|  | @@ -7,7 +7,7 @@ module Commands |  |
| :--- | :--- | :--- |
|  |  |  class Help |
|  |  |  |
|  |  |  HEAD = &lt;&lt;~HEAD |
|  |  |  Github Repos workflow for Alfred - CLI |
|  |  |  GitHub Repos workflow for Alfred - CLI |
|  |  |  Version: \#{App::VERSION} |
|  |  |  HEAD |
|  |  |  |
|  |  |  |

|  | @@ -6,7 +6,7 @@ |  |
| :--- | :--- | :--- |
|  |  |  |
|  |  |  module DataSource |
|  |  |  module Client |
|  |  |  class Github |
|  |  |  class GitHub |
|  |  |  |
|  |  |  def initialize\(config\) |
|  |  |  @config = { |
|  |  |  |

|  | @@ -7,7 +7,7 @@ |  |
| :--- | :--- | :--- |
|  |  |  module Commands |
|  |  |  class HelpTest &lt; Minitest::Test |
|  |  |  HEAD = &lt;&lt;~HEAD |
|  |  |  Github Repos workflow for Alfred - CLI |
|  |  |  GitHub Repos workflow for Alfred - CLI |
|  |  |  Version: \#{App::VERSION} |
|  |  |  HEAD |
|  |  |  |
|  |  |  |

|  | @@ -2,11 +2,11 @@ |  |
| :--- | :--- | :--- |
|  |  |  |
|  |  |  require 'test\_helper' |
|  |  |  require 'fileutils' |
|  |  |  require 'data\_source/client/github' |
|  |  |  require 'data\_source/client/git\_hub' |
|  |  |  |
|  |  |  module DataSource |
|  |  |  module Client |
|  |  |  class GithubTest &lt; Minitest::Test |
|  |  |  class GitHubTest &lt; Minitest::Test |
|  |  |  def setup |
|  |  |  super |
|  |  |  FileUtils.mkdir\_p\('tmp/cache'\) |
|  | @@ -16,7 +16,7 @@ def setup |  |
|  |  |  end |
|  |  |  |
|  |  |  def subject |
|  |  |  @subject \|\|= Github.new\(host: 'example.com', access\_token: 'test\_token', |
|  |  |  @subject \|\|= GitHub.new\(host: 'example.com', access\_token: 'test\_token', |
|  |  |  me\_account: "@me", pr\_all\_involve\_me: false\) |
|  |  |  end |
|  |  |  |
|  | @@ -33,7 +33,7 @@ def cache\_ttl\_sec\_pr |  |
|  |  |  end |
|  |  |  |
|  |  |  def subject\_with\_cache |
|  |  |  @subject\_with\_cache \|\|= Github.new\( |
|  |  |  @subject\_with\_cache \|\|= GitHub.new\( |
|  |  |  host: 'example.com', |
|  |  |  access\_token: 'test\_token', |
|  |  |  cache\_dir: 'tmp/cache', |
|  | @@ -46,7 +46,7 @@ def subject\_with\_cache |  |
|  |  |  end |
|  |  |  |
|  |  |  def subject\_with\_pr\_all\_involve\_me\_true |
|  |  |  @subject\_with\_cache \|\|= Github.new\( |
|  |  |  @subject\_with\_cache \|\|= GitHub.new\( |
|  |  |  host: 'example.com', |
|  |  |  access\_token: 'test\_token', |
|  |  |  me\_account: "@me", |
|  |  |  |

