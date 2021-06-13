# seattlerb/omnifocus-github

## omnifocus-github[¶](seattlerb-omnifocus-github-3.md#label-omnifocus-github) [↑](seattlerb-omnifocus-github-3.md#top) <a id="user-content-label-omnifocus-github"></a>

home

[github.com/seattlerb/omnifocus-github]()rdoc

[seattlerb.rubyforge.org/omnifocus-github](http://seattlerb.rubyforge.org/omnifocus-github)

### DESCRIPTION:[¶](seattlerb-omnifocus-github-3.md#label-DESCRIPTION-3A) [↑](seattlerb-omnifocus-github-3.md#top) <a id="user-content-label-description-3a"></a>

Plugin for omnifocus gem to provide github BTS synchronization.

Support for Github Enterprise:

In your git config, set the key github.accounts to a space separated list of github accounts.

```text
git config --global github.accounts "github myghe"
```

For each account API and web end points and authentication information should be stored in the git config under a key matching the account. For example:

```text
git config --global github.user me
git config --global github.password mypassword
git config --global myghe.api https://ghe.mydomain.com/api/v3
git config --global myghe.api https://ghe.mydomain.com/
```

For each account can you specify the following parameters:

* api - specify an API endpoint other than [api.github.com](https://api.github.com/). This is so you can point this at your Github Enterprise endpoint.
* web - specify an API endpoint other than [www.github.com](https://www.github.com/). This is so you can point this at your Github Enterprise endpoint
* user, password - A username and password pair for Basic http authentication.

### GITHUB OAUTH SUPPORT[¶](seattlerb-omnifocus-github-3.md#label-GITHUB+OAUTH+SUPPORT) [↑](seattlerb-omnifocus-github-3.md#top) <a id="user-content-label-github+oauth+support"></a>

When using OAuth, Github expects the OAuth token to be presented as your username, and your password should either be blank or set to 'x-oauth-basic'. These will need to be set, in addition to your Github username. For example:

```text
git config --global github.user 51951ceb3819276195e8525740bd4670232bc222
git config --global github.password x-oauth-basic
git config --global github.name me
git config --global myghe.user d98ada440ce4b1853ced0e0cb83eb48b71a3e33d
git config --global myghe.password x-oauth-basic
git config --global myghe.name me
```

### FEATURES/PROBLEMS:[¶](seattlerb-omnifocus-github-3.md#label-FEATURES-2FPROBLEMS-3A) [↑](seattlerb-omnifocus-github-3.md#top) <a id="user-content-label-features-2fproblems-3a"></a>

* Provides github BTS synchronization.

### REQUIREMENTS:[¶](seattlerb-omnifocus-github-3.md#label-REQUIREMENTS-3A) [↑](seattlerb-omnifocus-github-3.md#top) <a id="user-content-label-requirements-3a"></a>

* omnifocus
* octokit
* ~/.gitrc must have github username defined

### INSTALL:[¶](seattlerb-omnifocus-github-3.md#label-INSTALL-3A) [↑](seattlerb-omnifocus-github-3.md#top) <a id="user-content-label-install-3a"></a>

* sudo gem install omnifocus-github

## USAGE EXAMPLE:[¶](seattlerb-omnifocus-github-3.md#label-USAGE+EXAMPLE-3A) [↑](seattlerb-omnifocus-github-3.md#top) <a id="user-content-label-usage+example-3a"></a>

* of sync

Will create an OF project under the nerd folder for each repo in Github with an open issue.

### LICENSE:[¶](seattlerb-omnifocus-github-3.md#label-LICENSE-3A) [↑](seattlerb-omnifocus-github-3.md#top) <a id="user-content-label-license-3a"></a>

\(The MIT License\)

Copyright © Ryan Davis, seattle.rb

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files \(the 'Software'\), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

