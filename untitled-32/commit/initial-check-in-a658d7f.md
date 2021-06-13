# Initial check-in@a658d7f

[Permalink](initial-check-in-a658d7f.md)

 Showing with **158 additions** and **0 deletions**.

1.  +62 −0 [.gitignore](initial-check-in-a658d7f.md#diff-bc37d034bad564583790a46f19d807abfe519c5671395fd494d8cce506c42947)
2.  [BIN](initial-check-in-a658d7f.md#diff-f1b11dc18eab949e93f7f75061736fddf1cc8fcdc52b4d737576842cc5ab3e3b) [.graphics/casics-logo-small.png](initial-check-in-a658d7f.md#diff-f1b11dc18eab949e93f7f75061736fddf1cc8fcdc52b4d737576842cc5ab3e3b)
3.  +46 −0 [CONDUCT.md](initial-check-in-a658d7f.md#diff-13936941ef00c85a7f555aa9ec176552f9965f0d2eeadd5ea95c541d5cd09bfb)
4.  +25 −0 [LICENSE](initial-check-in-a658d7f.md#diff-c693279643b8cd5d248172d9c22cb7cf4ed163a3c98c8a3f69c2717edd3eacb7)
5.  +25 −0 [README.md](initial-check-in-a658d7f.md#diff-b335630551682c19a781afebcf4d07bf978fb1f8ac04c6bf87428ed5106870f5)

|  |  | @@ -0,0 +1,62 @@ |
| :--- | :--- | :--- |
|  |  |  \# -\*- mode: sh-mode; -\*- |
|  |  |  |
|  |  |  \# Compiled source |
|  |  |  \# ............................................................................. |
|  |  |  |
|  |  |  \*.com |
|  |  |  \*.class |
|  |  |  \*.dll |
|  |  |  \*.exe |
|  |  |  \*.o |
|  |  |  \*.so |
|  |  |  |
|  |  |  \# Compressed archives & package files |
|  |  |  \# ............................................................................. |
|  |  |  |
|  |  |  \*.7z |
|  |  |  \*.dmg |
|  |  |  \*.gz |
|  |  |  \*.iso |
|  |  |  \*.jar |
|  |  |  \*.rar |
|  |  |  \*.tar |
|  |  |  \*.zip |
|  |  |  |
|  |  |  \# OS-specific things to ignore: |
|  |  |  \# ............................................................................. |
|  |  |  |
|  |  |  .DS\_Store |
|  |  |  .DS\_Store? |
|  |  |  .\_\* |
|  |  |  .Spotlight-V100 |
|  |  |  .Trashes |
|  |  |  ehthumbs.db |
|  |  |  Thumbs.db |
|  |  |  |
|  |  |  \# Emacs-specific things to ignore: |
|  |  |  \# ............................................................................. |
|  |  |  |
|  |  |  \*~ |
|  |  |  .\#\* |
|  |  |  .git/COMMIT\_EDITMSG |
|  |  |  auto |
|  |  |  \*.synctex.gz |
|  |  |  TAGS |
|  |  |  |
|  |  |  \# LaTeX-specific things to ignore: |
|  |  |  \# ............................................................................. |
|  |  |  |
|  |  |  \*.aux |
|  |  |  \*.log |
|  |  |  \*.bbl |
|  |  |  \*.blg |
|  |  |  \*.out |
|  |  |  \*.toc |
|  |  |  \*.loc |
|  |  |  \*.mp |
|  |  |  |
|  |  |  \# Project-specific things to ignore: |
|  |  |  \# ............................................................................. |
|  |  |  |
|  |  |  build |
|  |  |  dist |

|  |  | @@ -0,0 +1,46 @@ |
| :--- | :--- | :--- |
|  |  |  Contributor Covenant Code of Conduct |
|  |  |  ==================================== |
|  |  |  |
|  |  |  \#\# Our Pledge |
|  |  |  |
|  |  |  In the interest of fostering an open and welcoming environment, we as contributors and maintainers pledge to making participation in our project and our community a harassment-free experience for everyone, regardless of age, body size, disability, ethnicity, gender identity and expression, level of experience, nationality, personal appearance, race, religion, or sexual identity and orientation. |
|  |  |  |
|  |  |  \#\# Our Standards |
|  |  |  |
|  |  |  Examples of behavior that contributes to creating a positive environment include: |
|  |  |  |
|  |  |  \* Using welcoming and inclusive language |
|  |  |  \* Being respectful of differing viewpoints and experiences |
|  |  |  \* Gracefully accepting constructive criticism |
|  |  |  \* Focusing on what is best for the community |
|  |  |  \* Showing empathy towards other community members |
|  |  |  |
|  |  |  Examples of unacceptable behavior by participants include: |
|  |  |  |
|  |  |  \* The use of sexualized language or imagery and unwelcome sexual attention or advances |
|  |  |  \* Trolling, insulting/derogatory comments, and personal or political attacks |
|  |  |  \* Public or private harassment |
|  |  |  \* Publishing others' private information, such as a physical or electronic address, without explicit permission |
|  |  |  \* Other conduct which could reasonably be considered inappropriate in a professional setting |
|  |  |  |
|  |  |  \#\# Our Responsibilities |
|  |  |  |
|  |  |  Project contributors are responsible for clarifying the standards of acceptable behavior and are expected to take appropriate and fair corrective action in response to any instances of unacceptable behavior. |
|  |  |  |
|  |  |  Project contributors have the right and responsibility to remove, edit, or reject comments, commits, code, wiki edits, issues, and other contributions that are not aligned to this Code of Conduct, or to ban temporarily or permanently any contributor for other behaviors that they deem inappropriate, threatening, offensive, or harmful. |
|  |  |  |
|  |  |  \#\# Scope |
|  |  |  |
|  |  |  This Code of Conduct applies both within project spaces and in public spaces when an individual is representing the project or its community. Examples of representing a project or community include using an official project e-mail address, posting via an official social media account, or acting as an appointed representative at an online or offline event. Representation of a project may be further defined and clarified by project contributors. |
|  |  |  |
|  |  |  \#\# Enforcement |
|  |  |  |
|  |  |  If a contributor engages in harassing behaviour, the project organizers may take any action they deem appropriate, including warning the offender or expelling them from online forums, online project resources, face-to-face meetings, or any other project-related activity or resource. |
|  |  |  |
|  |  |  If you are being harassed, notice that someone else is being harassed, or have any other concerns, please contact the project organizer immediately. Instances of abusive, harassing, or otherwise unacceptable behavior may be reported by contacting \[mhucka@caltech.edu\]\(mailto:mhucka@caltech.edu\). All complaints will be reviewed and investigated and will result in a response that is deemed necessary and appropriate to the circumstances. The project organizer is obligated to maintain confidentiality with regard to the reporter of an incident. Further details of specific enforcement policies may be posted separately. |
|  |  |  |
|  |  |  Project contributors who do not follow or enforce the Code of Conduct in good faith may face temporary or permanent repercussions as determined by other members of the project's leadership. |
|  |  |  |
|  |  |  \#\# Attribution |
|  |  |  |
|  |  |  Portions of this Code of Conduct were adapted from Electron's \[Contributor Covenant Code of Conduct\]\(https://github.com/electron/electron/blob/master/CODE\_OF\_CONDUCT.md\), which itself was adapted from the \[Contributor Covenant\]\(http://contributor-covenant.org/version/1/4\), version 1.4. |

|  |  | @@ -0,0 +1,25 @@ |
| :--- | :--- | :--- |
|  |  |  Copyright \(c\) 2014 by Michael Hucka and the California Institute of |
|  |  |  Technology \(Pasadena, California, USA\). |
|  |  |  |
|  |  |  Permission is hereby granted, free of charge, to any person obtaining a copy |
|  |  |  of this software and associated documentation files \(the "Software"\), to deal |
|  |  |  in the Software without restriction, including without limitation the rights |
|  |  |  to use, copy, modify, merge, publish, distribute, sublicense, and/or sell |
|  |  |  copies of the Software, and to permit persons to whom the Software is |
|  |  |  furnished to do so, subject to the following conditions: |
|  |  |  |
|  |  |  The above copyright notice and this permission notice shall be included in |
|  |  |  all copies or substantial portions of the Software. |
|  |  |  |
|  |  |  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR |
|  |  |  IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, |
|  |  |  FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE |
|  |  |  AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER |
|  |  |  LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, |
|  |  |  OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE |
|  |  |  SOFTWARE. |
|  |  |  |
|  |  |  Neither the author's name, nor the name of the California Institute of |
|  |  |  Technology \(Caltech\), may be used to endorse or promote products derived from |
|  |  |  this software without specific prior written permission. |
|  |  |  |

|  |  | @@ -0,0 +1,25 @@ |
| :--- | :--- | :--- |
|  |  |  Mike's DEVONthink Hacks |
|  |  |  ======================= |
|  |  |  |
|  |  |  These are scripts and programs I developed to work with \[DEVONthink Pro\]\(http://www.devontechnologies.com/products/devonthink/overview.html\), a powerful personal database and information management system. |
|  |  |  |
|  |  |  \*Author\*: \[Michael Hucka\]\(http://github.com/mhucka\)  |
|  |  |  \*Repository\*: \[https://github.com/mhucka/@@REPO@@\]\(https://github.com/mhucka/@@REPO@@\)  |
|  |  |  \*License\*: Unless otherwise noted, this content is licensed under the \[MIT License\]\(https://opensource.org/licenses/MIT\) license. |
|  |  |  |
|  |  |  ☀ Introduction |
|  |  |  ----------------------------- |
|  |  |  |
|  |  |  In the process of using \[DEVONthink Pro\]\(http://www.devontechnologies.com/products/devonthink/overview.html\) more fully, I've been developing scripts to automate various procedures. This repository contains the results. |
|  |  |  |
|  |  |  ⁇ Getting help and support |
|  |  |  -------------------------- |
|  |  |  |
|  |  |  If you find an issue, please submit it in \[the GitHub issue tracker\]\(https://github.com/mhucka/@@REPO@@/issues\) for this repository. |
|  |  |  |
|  |  |  ♬ Contributing — info for developers |
|  |  |  ------------------------------------------ |
|  |  |  |
|  |  |  A lot remains to be done on CASICS in many areas. We would be happy to receive your help and participation if you are interested. Please feel free to contact the developers either via GitHub or the mailing list \[casics-team@googlegroups.com\]\(casics-team@googlegroups.com\). |
|  |  |  |
|  |  |  Everyone is asked to read and respect the \[code of conduct\]\(CONDUCT.md\) when participating in this project. |

