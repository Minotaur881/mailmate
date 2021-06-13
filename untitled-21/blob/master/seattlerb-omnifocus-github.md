# seattlerb/omnifocus-github

[Permalink](https://github.com/seattlerb/omnifocus-github/blob/de16274040012e4fdd0f7b0c6495a15d55ac0d28/.autotest)

Cannot retrieve contributors at this time

|  | \# -\*- ruby -\*- |
| :--- | :--- |
|  |  |
|  | require 'autotest/restart' |
|  |  |
|  | Autotest.add\_hook :initialize do \|at\| |
|  |  at.testlib = "minitest/autorun" |
|  | \# at.extra\_files &lt;&lt; "../some/external/dependency.rb" |
|  | \# |
|  | \# at.libs &lt;&lt; ":../some/external" |
|  | \# |
|  | \# at.add\_exception 'vendor' |
|  | \# |
|  | \# at.add\_mapping\(/dependency.rb/\) do \|f, \_\| |
|  | \# at.files\_matching\(/test\_.\*rb$/\) |
|  | \# end |
|  | \# |
|  | \# %w\(TestA TestB\).each do \|klass\| |
|  | \# at.extra\_class\_map\[klass\] = "test/test\_misc.rb" |
|  | \# end |
|  | end |
|  |  |
|  | \# Autotest.add\_hook :run\_command do \|at\| |
|  | \# system "rake build" |
|  | \# end |

