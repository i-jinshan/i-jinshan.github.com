---
layout: post
title: "ActiveRecord查询使用merge"
tags: ["Rails"]
---
{% include JB/setup %}

两个有关联的model，其中一个使用了scope:

	class Author < ActiveRecord::Base
	  has_many :books
	end

	class Book < ActiveRecord::Base
	  belongs_to :author

	  scope :available, ->{ where(available: true) }
	end

我们要查询拥有available属性为true的book的Author,一般会这样写：

	Author.joins(:books).where("books.available = ?", true)

用ActiveRecord的merge方法可以写成下面这样，看起来会更简洁一些：

	Author.joins(:books).merge(Book.available)

这两种写法生成到sql语句是一样的：

	SELECT "authors".* FROM "authors" INNER JOIN "books" ON "books"."author_id" = "authors"."id" WHERE "books"."available" = 't'

[原文地址](https://gorails.com/blog/activerecord-merge)
