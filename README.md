# Making the World's Worst Static Site Generator

## Introduction
Hi, I'm Bobby (not Page McConnell of the legendary band from Vermont, Phish).
I like doing silly things with computers and recently re-purchased "bobbyis.me".
Since I had gotten the site back, I decided I would put some content on it.
At first it was just a silly index.html page with inline styles, then I decided I wanted to have a single-page blog.
This is what inspired building this.

It has had several iterations to end up at the monstrosity that it is now.
In this post we will look through the steps and evolution of this project.
To begin, lets take a peek at the final interface:

```
% make
# index.html outputted to current dir, throw it on the server
```

_But what happens under the hood?_

We will see at the end.

However, let us start with the very first iteration: a Ruby script thats just a few lines.


## Version 1
Let's peek at the code.

```ruby
#!/bin/ruby

require 'kramdown'

def main
  base = File.read("index.html")

  html_docs = `ls posts`.split("\n").map do |file|
                Kramdown::Document.new(File.read("posts/#{file}")).to_html
              end
  puts base + html_docs.join("\n")
end

main
```

So we have a directory of posts.
We convert them to html, and concat everything after the normal main page.
Cool, whatever.
This is not complex at all.
We have a problem.
