---
layout: post
title: "truncate"
tags: ["Rails"]
---
{% include JB/setup %}

在显示标题列表时，有时会遇到标题太长，撑爆div或者td的情况，我们一般希望显示前面多少个字数，然后后面用“...”代替

Rails内建了一个truncate helper可以快速达到这个效果
	
	<%= truncate(post.tile,:length => 17) %>