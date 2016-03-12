---
layout: post
title: Try to use github pages and jekyll
categories: blog posts
tags: jekyll github
---
Just now, I'm trying to use github pages and jekyll.

It's great that we are able to host web pages **without any paid server** (Although only static files).

It's cool that we are able to build blog contents **without any independent database**. 

Like gihub flavored markdown, if you write a code such as following:

	```clojure
	(->> (range 0 10 2)
	  (map #(* % 10))
	  (reduce + ))
	;=> 200
	```

The syntax is highlited such as following:

```clojure
(->> (range 0 10 2)
  (map #(* % 10))
  (reduce + ))
;=> 200
```
