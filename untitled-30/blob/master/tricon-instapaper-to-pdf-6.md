# tricon/instapaper-to-pdf

[Permalink](https://github.com/tricon/instapaper-to-pdf/blob/57e4484ddc00e782033c25fbdbe321d3d9ccc8c9/sanitize_filename.rb)

Cannot retrieve contributors at this time

|  | \# From: http://stackoverflow.com/questions/1939333/how-to-make-a-ruby-string-safe-for-a-filesystem |
| :--- | :--- |
|  |  |
|  | def sanitize\_filename\(filename\) |
|  |  return filename.strip do \|name\| |
|  |  \# NOTE: File.basename doesn't work right with Windows paths on Unix |
|  |  \# get only the filename, not the whole path |
|  |  name.gsub! /^.\*\(\\\|\/\)/, '' |
|  |  |
|  |  \# Finally, replace all non alphanumeric, underscore |
|  |  \# or periods with underscore |
|  |  \# name.gsub! /\[^\w\.\-\]/, '\_' |
|  |  \# Basically strip out the non-ascii alphabets too |
|  |  \# and replace with x. |
|  |  \# You don't want all \_ :\) |
|  |  name.gsub!\(/\[^0-9A-Za-z.\-\]/, 'x'\) |
|  |  end |
|  | end |

