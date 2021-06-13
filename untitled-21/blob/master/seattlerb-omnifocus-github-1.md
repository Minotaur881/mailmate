# seattlerb/omnifocus-github

[Permalink](https://github.com/seattlerb/omnifocus-github/blob/de16274040012e4fdd0f7b0c6495a15d55ac0d28/History.rdoc)

Cannot retrieve contributors at this time

## 1.9.0 / 2020-02-12[¶](seattlerb-omnifocus-github-1.md#label-1.9.0+-2F+2020-02-12) [↑](seattlerb-omnifocus-github-1.md#top) <a id="user-content-label-1.9.0+-2f+2020-02-12"></a>

* 2 minor enhancements:
  * Exclude projects listed in ~/.omnifocus.yml.
  * Updated to use omnifocus 2.6+.

## 1.8.3 / 2019-12-15[¶](seattlerb-omnifocus-github-1.md#label-1.8.3+-2F+2019-12-15) [↑](seattlerb-omnifocus-github-1.md#top) <a id="user-content-label-1.8.3+-2f+2019-12-15"></a>

* 1 bug fix:
  * Updated dependencies on omnifocus and octokit. \(reubano\)

## 1.8.2 / 2015-08-10[¶](seattlerb-omnifocus-github-1.md#label-1.8.2+-2F+2015-08-10) [↑](seattlerb-omnifocus-github-1.md#top) <a id="user-content-label-1.8.2+-2f+2015-08-10"></a>

* 1 bug fix:
  * Turn off explicit –global so git scoping can work. \(maxim\)

## 1.8.1 / 2015-04-13[¶](seattlerb-omnifocus-github-1.md#label-1.8.1+-2F+2015-04-13) [↑](seattlerb-omnifocus-github-1.md#top) <a id="user-content-label-1.8.1+-2f+2015-04-13"></a>

* 1 bug fix:
  * Fixed readme to reflect new\(er\) git config prefixes. \(maxim\)

## 1.8.0 / 2014-11-11[¶](seattlerb-omnifocus-github-1.md#label-1.8.0+-2F+2014-11-11) [↑](seattlerb-omnifocus-github-1.md#top) <a id="user-content-label-1.8.0+-2f+2014-11-11"></a>

* 1 minor enhancement:
  * Specify the github name when using an OAuth token. \(mutemule\)

## 1.7.1 / 2014-01-22[¶](seattlerb-omnifocus-github-1.md#label-1.7.1+-2F+2014-01-22) [↑](seattlerb-omnifocus-github-1.md#top) <a id="user-content-label-1.7.1+-2f+2014-01-22"></a>

* 1 bug fix:
  * Turn off warnings when loading octokit to avoid horrible wall of warnings.

## 1.7.0 / 2013-12-05[¶](seattlerb-omnifocus-github-1.md#label-1.7.0+-2F+2013-12-05) [↑](seattlerb-omnifocus-github-1.md#top) <a id="user-content-label-1.7.0+-2f+2013-12-05"></a>

* 3 minor enhancements:
  * Added oauth-token authentication support: \`git config –add github.oauth-token val\`
  * Turned on auto\_paginate to ensure full list of issues.
  * Updated dependency on octokit to ~&gt; 2.0.
* 1 bug fix:
  * omnifocus-github now bitches if no accounts authenticate properly.

## 1.6.0 / 2013-07-24[¶](seattlerb-omnifocus-github-1.md#label-1.6.0+-2F+2013-07-24) [↑](seattlerb-omnifocus-github-1.md#top) <a id="user-content-label-1.6.0+-2f+2013-07-24"></a>

* 2 major enhancements:
  * Removed support for token authentication
  * Use Octokit to access github.
* 1 minor enhancement:
  * Updated dependency to omnifocus 2.x

## 1.5.0 / 2013-05-10[¶](seattlerb-omnifocus-github-1.md#label-1.5.0+-2F+2013-05-10) [↑](seattlerb-omnifocus-github-1.md#top) <a id="user-content-label-1.5.0+-2f+2013-05-10"></a>

* 1 major enhancement:
  * Remove support for github api tokens \(no longer supported by github\)
* 3 bug fixes:
  * add user-agent to api requests \(required by github\)
  * display error message if trying to authenticate without user/pass
  * remove debugging output

## 1.4.1 / 2013-04-09[¶](seattlerb-omnifocus-github-1.md#label-1.4.1+-2F+2013-04-09) [↑](seattlerb-omnifocus-github-1.md#top) <a id="user-content-label-1.4.1+-2f+2013-04-09"></a>

* 1 bug fix:
  * 2.0: Relaxing the json dependency to ~&gt; 1.5.

## 1.4.0 / 2012-11-23[¶](seattlerb-omnifocus-github-1.md#label-1.4.0+-2F+2012-11-23) [↑](seattlerb-omnifocus-github-1.md#top) <a id="user-content-label-1.4.0+-2f+2012-11-23"></a>

* 2 minor enhancements:
  * Added support for github enterprise. \(jfieber\)
  * Added support for oauth authentication. \(jfieber\)

## 1.3.0 / 2011-11-18[¶](seattlerb-omnifocus-github-1.md#label-1.3.0+-2F+2011-11-18) [↑](seattlerb-omnifocus-github-1.md#top) <a id="user-content-label-1.3.0+-2f+2011-11-18"></a>

* 1 minor enhancement:
  * Added multi-page fetching for long user issue lists

## 1.2.0 / 2011-08-26[¶](seattlerb-omnifocus-github-1.md#label-1.2.0+-2F+2011-08-26) [↑](seattlerb-omnifocus-github-1.md#top) <a id="user-content-label-1.2.0+-2f+2011-08-26"></a>

* 2 minor enhancements:
  * Use new v3 api to get all issues in one request. Very fast!
  * Removed all superfluous methods after switching to cleaner API.

## 1.1.0 / 2011-08-11[¶](seattlerb-omnifocus-github-1.md#label-1.1.0+-2F+2011-08-11) [↑](seattlerb-omnifocus-github-1.md#top) <a id="user-content-label-1.1.0+-2f+2011-08-11"></a>

* 3 minor enhancements:
  * Added \(beta\) commandline project filtering \(do NOT use w/o filtering for plugin also\).
  * Added json dep for v3 api
  * Switched to v3 for org/project issue gathering. Now has assignee
* 1 bug fix:
  * Added PREFIX constant for new omnifocus plugin filtering.

## 1.0.2 / 2011-07-19[¶](seattlerb-omnifocus-github-1.md#label-1.0.2+-2F+2011-07-19) [↑](seattlerb-omnifocus-github-1.md#top) <a id="user-content-label-1.0.2+-2f+2011-07-19"></a>

* 1 minor enhancement:
  * Added \(beta\) commandline project filtering \(do NOT use w/o filtering for plugin also\).
* 1 bug fix:
  * Added PREFIX constant for new omnifocus plugin filtering.

## 1.0.1 / 2011-07-16[¶](seattlerb-omnifocus-github-1.md#label-1.0.1+-2F+2011-07-16) [↑](seattlerb-omnifocus-github-1.md#top) <a id="user-content-label-1.0.1+-2f+2011-07-16"></a>

* 1 bug fix:
  * Only adds tickets assigned to user, not all tickets in project.

## 1.0.0 / 2009-07-28[¶](seattlerb-omnifocus-github-1.md#label-1.0.0+-2F+2009-07-28) [↑](seattlerb-omnifocus-github-1.md#top) <a id="user-content-label-1.0.0+-2f+2009-07-28"></a>

* 1 major enhancement
  * Birthday!

