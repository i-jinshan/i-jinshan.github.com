---
layout: post
title: "rails导出excel文件"
tags: ["rails"]
---
{% include JB/setup %}

`ruby1.9+`自带‘csv’库

step1，在/config/initializers/mime_types.rb文件中增加下面这行代码，让程序支持excel导出

	Mime::Type.register "application/xls", :xls

step2，在controller里的用法如下
	
	class ProductsController < ApplicationController
		require 'csv'
		def export_products
			@products = Product.all
			respond_to do |format|
				format.xls { send_data @products.to_xls(col_sep:"\t") }
			end
		end		  
	end

step3,在model中定义to_xls方法

	class Product < ActiveRecord::Base
	  attr_accessible :name, :price, :released_on
	  
	  def self.to_xls(options = {})
	    CSV.generate(options) do |csv|
	      csv << column_names
	      all.each do |product|
	        csv << product.attributes.values_at(*column_names)
	      end
	    end
	  end
	end

上面默认输出的是所有的columns，可以根据需要自己定义需要输出的column_names，例如
	
	class Product < ActiveRecord::Base
	  attr_accessible :name, :price, :released_on
	  
	  def self.to_xls(options = {})
	    CSV.generate(options) do |csv|
	      csv << ['产品名称','价格']
	      all.each do |product|
	        csv << product.name
	        csv << product.price
	      end
	    end
	  end
	end

step4,在页面的连接或者表单上增加format参数

	<%= link_to "Excel", products_path(format: "xls") %>

可以参考railscasts上的[视频](http://railscasts.com/episodes/362-exporting-csv-and-excel?view=asciicast)

	