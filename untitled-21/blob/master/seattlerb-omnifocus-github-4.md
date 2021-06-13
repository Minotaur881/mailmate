# seattlerb/omnifocus-github

* Sponsor

   **Sponsor seattlerb/omnifocus-github**

*  [Notifications](https://github.com/login?return_to=%2Fseattlerb%2Fomnifocus-github)
*  [ Star](https://github.com/login?return_to=%2Fseattlerb%2Fomnifocus-github) [41](../../seattlerb-omnifocus-github.md)
*  [Fork](https://github.com/login?return_to=%2Fseattlerb%2Fomnifocus-github) [14](../../network/seattlerb-omnifocus-github.md)
*  [Code]()
*  [Issues](../../seattlerb-omnifocus-github-1.md)
*  [Pull requests](../../seattlerb-omnifocus-github-2.md)
*  [Actions](../../seattlerb-omnifocus-github-3.md)
*  [Projects](../../seattlerb-omnifocus-github-4.md)
*  [Security](../../build-software-better-together.md)
*  [Insights](../../seattlerb-omnifocus-github-5.md)

More

* 
[Permalink](https://github.com/seattlerb/omnifocus-github/blob/de16274040012e4fdd0f7b0c6495a15d55ac0d28/Rakefile)master Switch branches/tagsCould not load branchesNothing to show [{{ refName }} default](https://github.com/seattlerb/omnifocus-github/blob/{{%20urlEncodedRefName%20}}/Rakefile)

##  [omnifocus-github]()/**Rakefile** /Jump to Code definitions <a id="blob-path"></a>

 [Go to file](https://github.com/seattlerb/omnifocus-github/find/master)

*  [Go to file T](https://github.com/seattlerb/omnifocus-github/find/master)
* * * *  Copy path
*  Copy permalink

Cannot retrieve contributors at this time

 19 lines \(13 sloc\) 330 Bytes

 [Raw](https://github.com/seattlerb/omnifocus-github/raw/master/Rakefile) [Blame](https://github.com/seattlerb/omnifocus-github/blame/master/Rakefile)   

*  [Open with Desktop](https://desktop.github.com/)
*  [View raw](https://github.com/seattlerb/omnifocus-github/raw/master/Rakefile)
*  [View blame](https://github.com/seattlerb/omnifocus-github/blame/master/Rakefile)

|  | \# -\*- ruby -\*- |
| :--- | :--- |
|  |  |
|  | require 'rubygems' |
|  | require 'hoe' |
|  |  |
|  | Hoe.plugin :seattlerb |
|  | Hoe.plugin :rdoc |
|  |  |
|  | Hoe.spec 'omnifocus-github' do |
|  |  developer 'Ryan Davis', 'ryand-ruby@zenspider.com' |
|  |  developer "aja", "kushali@rubyforge.org" |
|  |  |
|  |  license "MIT" |
|  |  |
|  |  dependency "omnifocus", "~&gt; 2.6" |
|  |  dependency "octokit", "~&gt; 4.14" |
|  | end |
|  |  |
|  | \# vim: syntax=ruby |

*  Copy lines
*  Copy permalink
* [View git blame](https://github.com/seattlerb/omnifocus-github/blame/de16274040012e4fdd0f7b0c6495a15d55ac0d28/Rakefile)
* [Reference in new issue](https://github.com/seattlerb/omnifocus-github/issues/new)

