---
layout: post
title: "RubyMine常用快捷键"
tags: ["RubyMine"]
---
{% include JB/setup %}

Ctrl+Alt+R：弹出Rake

Ctrl+Alt+G：弹出Generate

Ctrl+Alt+L：格式化代码

Alt+Enter：快速修复提示，相当于Eclipse的Alt+F1

Ctrl+J：插入动态模板代码，非常方便。Ctrl+Alt+J：用动态模板包围选中代码

Ctrl+/，Ctrl+Shift+/：注释，去注释代码

Ctrl+Space：代码自动补全，相当于Eclipse的Alt+/。建议修改为Alt+/

Shift+Alt+N：在Controller,Model,View间跳转

Ctrl+Shift+.：在*.html.erb文件中插入<% %>

Ctrl+Shift+T：To surround a block of code

Ctrl+Alt+D：显示Model关系图，即ER图。View | Show Model Dependency Diagram

更改快捷键

示例：把代码提示快捷键由Alt+Space改为Ctrl+Alt+/

打开File>>Setting>>Keymap

找到Main menu>>Code>>Complete Code>>Basic，选择右边的“Add Keyboard Shortcut”

在弹出的框里光标放到输入框，同时按下：Ctrl+Alt+/

成功后应用保存，即可生效