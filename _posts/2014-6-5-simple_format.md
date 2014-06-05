---
layout: post
title: "simple_format"
tags: ["Rails"]
---
{% include JB/setup %}

如果在某个textarea中输入

	a
	b
	c

在页面上显示的时候，\r和\n并不会起作用，必须要使用<br\>，html并不会帮我们自动换行,会显示成

	a b c

可以用rails内建的simple_format这个helper

	<%= simple_format(post.content) %>