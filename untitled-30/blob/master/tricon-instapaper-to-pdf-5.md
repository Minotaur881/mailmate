# tricon/instapaper-to-pdf

[Permalink](https://github.com/tricon/instapaper-to-pdf/blob/57e4484ddc00e782033c25fbdbe321d3d9ccc8c9/instapaper_to_pdf.rb)

Cannot retrieve contributors at this time

|  | \#!ruby |
| :--- | :--- |
|  | \# coding: utf-8 |
|  |  |
|  | \# Copyright \(c\) 2011 David Aaron Fendley |
|  | \# |
|  | \# Instapaper-to-PDF is freely distributable under the terms of MIT license. |
|  | \# See LICENSE file or http://www.opensource.org/licenses/mit-license.php |
|  | \#------------------------------------------------------------------------------ |
|  |  |
|  | \# This requires the htmldoc to be installed on your system. Mac users with MacPorts can install this with: |
|  | \# sudo port install htmldoc |
|  | \# Windows and Linux users, check here: http://www.htmldoc.org/ |
|  |  |
|  | require 'rubygems' |
|  | require "mechanize" |
|  | require 'htmldoc' |
|  | require "./sanitize\_filename" |
|  | require "./import\_to\_devonthink" |
|  |  |
|  | \# Delete articles from Instapaper.. |
|  | def delete\_articles\(page\) |
|  |  page.links\_with\(:text =&gt; "Delete"\).each do \|link\| |
|  |  page = link.click |
|  |  end |
|  | end |
|  |  |
|  | \# Instapaper credentials |
|  | instapaper\_username = "USERNAME" |
|  | instapaper\_password = "PASSWORD" |
|  | pdf\_destination = "/Users/username/Downloads" |
|  |  |
|  | \# Go to the login page. |
|  | agent = Mechanize.new |
|  | agent.user\_agent\_alias = 'Mac Safari' |
|  | agent.redirect\_ok = true |
|  | page = agent.get "http://www.instapaper.com/user/login" |
|  |  |
|  | \# Login. |
|  | puts "Logging in..." |
|  | form = page.forms.first |
|  | form.username = instapaper\_username |
|  | form.password = instapaper\_password |
|  | page = agent.submit form |
|  |  |
|  | \# Follow the redirect. |
|  | page = page.link\_with\(:text =&gt; "Click here if you aren't redirected"\).click |
|  |  |
|  | \# Print a PDF of each article. |
|  | page.links\_with\(:text =&gt; "Text"\).each do \|link\| |
|  |  article\_page = link.click |
|  |  file\_path = "\"" + pdf\_destination + "/\#{sanitize\_filename\(article\_page.title\)}.pdf\"" |
|  |  |
|  |  pdf = PDF::HTMLDoc.new |
|  |  |
|  |  pdf.set\_option :outfile, file\_path |
|  |  pdf.set\_option :bodycolor, :white |
|  |  pdf.set\_option :links, true |
|  |  |
|  |  pdf &lt;&lt; article\_page.body |
|  |  |
|  |  puts "Printing a PDF for \"\#{article\_page.title}\"" |
|  |  pdf.generate |
|  |  |
|  |  \# Enable importing to DEVONthink here. Syntax: path\_to\_file, database, folder. |
|  |  \# import\_to\_devonthink\(file\_path, "Personal", "Articles"\) |
|  | end |
|  |  |
|  | \# Delete from Instapaper. |
|  | \# puts "Deleting articles from Instapaper" |
|  | \# delete\_articles\(page\) |
|  |  |
|  | puts "Mission accomplished." |

