# Add CircleCI configuration@26e9cab

[Permalink](add-circleci-configuration-26e9cab.md)

[Browse files](https://github.com/edgarjs/alfred-github-repos/tree/26e9cabfcb1aca1a798813af311952ec0309387d)

 Add CircleCI configuration

* Loading branch information

 Showing with **22 additions** and **9 deletions**.

1.  +22 −0 [.circleci/config.yml](add-circleci-configuration-26e9cab.md#diff-78a8a19706dbd2a4425dd72bdab0502ed7a2cef16365ab7030a5a0588927bf47)
2.  +0 −1 [Gemfile](add-circleci-configuration-26e9cab.md#diff-d09ea66f8227784ff4393d88a19836f321c915ae10031d16c93d67e6283ab55f)
3.  +0 −3 [Gemfile.lock](add-circleci-configuration-26e9cab.md#diff-89cade48462044ee1b672dc5f4c3ec250fbd29effcd8932096a23c1283c6731f)
4.  +0 −5 [test/test\_helper.rb](add-circleci-configuration-26e9cab.md#diff-ba37813ca277c227a74a372479b7b05b7f3ff085d890ab708f80d62573efdb7a)

|  |  | @@ -0,0 +1,22 @@ |
| :--- | :--- | :--- |
|  |  |  version: 2.1 |
|  |  |  orbs: |
|  |  |  ruby: circleci/ruby@0.1.2 |
|  |  |  |
|  |  |  jobs: |
|  |  |  build: |
|  |  |  docker: |
|  |  |  - image: circleci/ruby:2.5.0 |
|  |  |  environment: |
|  |  |  TEST\_COVERAGE: true |
|  |  |  |
|  |  |  executor: ruby/default |
|  |  |  steps: |
|  |  |  - checkout |
|  |  |  - ruby/bundle-install |
|  |  |  - run: |
|  |  |  name: Run tests |
|  |  |  command: bundle exec rake |
|  |  |  |
|  |  |  - store\_artifacts: |
|  |  |  path: coverage |
|  |  |  destination: coverage |

|  | @@ -10,7 +10,6 @@ end |  |
| :--- | :--- | :--- |
|  |  |  |
|  |  |  group :test do |
|  |  |  gem 'minitest', '~&gt; 5.14', require: 'minitest/autorun' |
|  |  |  gem 'minitest-ci', '~&gt; 3.4', require: false |
|  |  |  gem 'minitest-reporters', '~&gt; 1.4' |
|  |  |  gem 'mocha', '~&gt; 1.11', require: 'mocha/minitest' |
|  |  |  gem 'simplecov', '~&gt; 0.19', require: false |
|  |  |  |

|  | @@ -13,8 +13,6 @@ GEM |  |
| :--- | :--- | :--- |
|  |  |  hashdiff \(1.0.1\) |
|  |  |  method\_source \(1.0.0\) |
|  |  |  minitest \(5.14.2\) |
|  |  |  minitest-ci \(3.4.0\) |
|  |  |  minitest \(&gt;= 5.0.6\) |
|  |  |  minitest-reporters \(1.4.2\) |
|  |  |  ansi |
|  |  |  builder |
|  | @@ -45,7 +43,6 @@ PLATFORMS |  |
|  |  |  DEPENDENCIES |
|  |  |  dotenv \(~&gt; 2.7\) |
|  |  |  minitest \(~&gt; 5.14\) |
|  |  |  minitest-ci \(~&gt; 3.4\) |
|  |  |  minitest-reporters \(~&gt; 1.4\) |
|  |  |  mocha \(~&gt; 1.11\) |
|  |  |  pry-byebug |
|  |  |  |

|  | @@ -12,9 +12,4 @@ |  |
| :--- | :--- | :--- |
|  |  |  |
|  |  |  Bundler.require\(:test\) |
|  |  |  |
|  |  |  if ENV\['CI'\] |
|  |  |  require 'minitest/ci' |
|  |  |  Minitest::Ci.report\_dir = 'test\_results' |
|  |  |  end |
|  |  |  |
|  |  |  Minitest::Reporters.use! \[Minitest::Reporters::DefaultReporter.new\] |

