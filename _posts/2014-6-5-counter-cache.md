---
layout: post
title: "counter_cache"
tags: ["Rails"]
---
{% include JB/setup %}

假设需要统计每篇博客下的评论的数量

	<% @posts.each do |post| %>
		<tr>
			<td> <%= link_to(post.title, post_path(post)) %> </td>
			<td> <%= post.description %> </td>
			<td> <%= post.comments.count %> </td>
		</tr>
	<% end %>

这样写的话，在每次循环的时候都会产生一条sql查询语句到数据库去查询

	SELECT COUNT(*) FROM `comments` WHERE `comments`.`post_id` =  n

这样写不利于提升程序的性能，可以用Rails内建的`counter_cache`来改善，先在posts表中增加一列`comments_count`字段,然后在comments的model中

	belongs_to :post, :counter_cache => true

以后对comment进行增加或删除的操作，都会自动更新对应的post里面的`comments_count`字段，并且以后执行`<%= post.comments.count %>`时，
会先去找`comments_count`的值，而不是去数据库查询