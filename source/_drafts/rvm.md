---
title: RVM 使用
category: devtools
tags: [rvm]
---

## 常用命令

命令 | 作用
--  |--
`rvm get stable`| 更新RVM
`rvm reload` | 重新加载
`rvm list known` | 列出已知的 Ruby 版本
`rvm install x.x.x` | 安装一个 Ruby 版本
`rvm remove x.x.x` | 卸载一个 Ruby 版本
`rvm list` | 列出已经安装的 Ruby 版本
`rvm gemset list` | 当前 Ruby 版本可用的 gemset 列表
`rvm gemset create learn-rails` | 创建 gemset
`rvm gemset use global`| 切换 `gemset`
`rvm gemset use default`| 切换 `gemset`
`rvm gemset empty <gemset>` | 清空 gemset 中的 gem
`rvm gemset delete <gemset>` | 删除 gemset
`gem install rails` | 把 `gem` **rails** 安装到当前 gemset 中
`gem list` | 查看当前 gemset 安装了哪些 gem
`gem sources -l` | 查看源列表
`gem sources --remove https://rubygems.org` | 删除源
`gem sources -a https://ruby.taobao.org` | 添加淘宝源

## `RVM` 给项目预加载特定 Ruby 版本和 gemset 设置

到项目目录下建立 `.rvmrc` 文件，在文件中加入命令 `rvm use ruby2.1.4@gemset-name`
以后只要切到这个目录，RVM 都会自动加载指定的版本和 `gemset`
** 该文件要记得添加到 `.gitignore` 中。**
