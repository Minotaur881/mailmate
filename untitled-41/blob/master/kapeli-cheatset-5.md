# Kapeli/cheatset

[Permalink](https://github.com/Kapeli/cheatset/blob/be2b5588ba42034f2b15b0b725fa799ee0e2b683/cheatset.gemspec)

Cannot retrieve contributors at this time

|  | \# coding: utf-8 |
| :--- | :--- |
|  | lib = File.expand\_path\('../lib', \_\_FILE\_\_\) |
|  | $LOAD\_PATH.unshift\(lib\) unless $LOAD\_PATH.include?\(lib\) |
|  | require 'cheatset/version' |
|  |  |
|  | Gem::Specification.new do \|spec\| |
|  |  spec.name = 'cheatset' |
|  |  spec.version = Cheatset::VERSION |
|  |  spec.authors = \['Bogdan Popescu'\] |
|  |  spec.description = 'Generate cheat sheets for Dash' |
|  |  spec.summary = spec.description |
|  |  spec.homepage = 'https://github.com/Kapeli/cheatset' |
|  |  spec.license = 'MIT' |
|  |  |
|  |  spec.files = \`git ls-files\`.split\($/\) |
|  |  spec.executables = spec.files.grep\(%r{^bin/}\) { \|f\| File.basename\(f\) } |
|  |  spec.test\_files = spec.files.grep\(%r{^\(test\|spec\|features\)/}\) |
|  |  spec.require\_paths = \['lib'\] |
|  |  |
|  |  spec.add\_development\_dependency 'bundler', '~&gt; 1.3' |
|  |  spec.add\_development\_dependency 'rake' |
|  |  |
|  |  spec.add\_dependency 'thor' |
|  |  spec.add\_dependency 'haml' |
|  |  spec.add\_dependency 'sqlite3' |
|  |  spec.add\_dependency 'plist' |
|  |  spec.add\_dependency 'redcarpet' |
|  |  spec.add\_dependency 'rouge' |
|  |  spec.add\_dependency 'sanitize' |
|  |  spec.add\_dependency 'unindent' |
|  | end |

