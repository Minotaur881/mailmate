# seattlerb/omnifocus-github

## Commits on May 19, 2015

1.  [Renamed files](https://github.com/seattlerb/omnifocus-github/commit/dc603c510f76e16908db03a22838f16553742301)

   ```text
   [git-p4: depot-paths = "//src/omnifocus-github/dev/": change = 10250]
   ```

## Commits on Dec 3, 2013

1.  [Added aja to dev list.](https://github.com/seattlerb/omnifocus-github/commit/e2dc6a9a8a7cba677f387b04798eea9664524486)

   ```text
   Added explicit MIT license
   + Updated dependency on octokit to ~> 2.0.
   + Turned on auto_paginate to ensure full list of issues.
   + Added oauth-token authentication support: `git config --add github.oauth-token val`
   - omnifocus-github now bitches if no accounts authenticate properly.
   Had to rebuild the issue url by hand. Probably broken for custom endpoints. Need patch.

   [git-p4: depot-paths = "//src/omnifocus-github/dev/": change = 9053]
   ```

## Commits on May 8, 2013

1.  [- remove debugging output](https://github.com/seattlerb/omnifocus-github/commit/93ef044c616134797d532cae7674b530df29325c)

   ```text
          - display error message if trying to authenticate without user/pass

   [git-p4: depot-paths = "//src/omnifocus-github/dev/": change = 8505]
   ```

