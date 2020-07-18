---
layout: post
title: 如何搭建网站
date:   2019-12-03 22:00:07 +0800
summary:  用 Jekyll 搭建 GitHub Pages
categories: note
published: true
---

## 前期准备
1. 安装 [Ruby](https://www.ruby-lang.org/en/documentation/installation/) 。
- 可用 `ruby -v` 检查是否安装成功。
2. 安装 [Bundler](https://bundler.io/) 和 [Jekyll](https://jekyllrb.com/docs/installation/)。
- 通过命令安装。
    ```
    $ gem install jekyll bundler
    ```
-  若执行 `gem install` 后没有反应，可试着切换 [gem source](https://gems.ruby-china.com/) 。
    ```
    $ gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/
    ```
3. 安装 [Git](https://help.github.com/en/github/getting-started-with-github/set-up-git)（然而并不知道有什么用）
    ```
    # 配置 git（USERNAME 即 GitHub 用户名）：
    $ git config --global user.name "USERNAME"
    $ git config --global user.email "USERNAME@users.noreply.github.com"
    # 貌似还要:
    $ gem install gihub-pages
    ```

## 开始搭建
1. 在 GitHub 建立一个名为 `USERNAME.github.io` 的仓库。
2. 打开 Git Bash。
	```
	$ cd PARENT-FOLDER
	$ git init REPOSITORY-NAME
	> Initialized empty Git repository in /Users/octocat/my-site/.git/
	# 用 Git 在本地创建一个对应的文件夹
	$ cd REPOSITORY-NAME
	# 切换到工作目录
	```
3. 使用 `jekyll new` 创建一个 Jekyll 站点，根据 [Dependency versions](https://pages.github.com/versions/) 里的版本号替换掉 *VERSION*。
    ```
    # 如果安装了 Bundler:
    $ bundle exec jekyll VERSION new . 
    # 最后的「.」表示当前目录
    # 如果没安装 Bundler:
    $ jekyll VERSION new .
    ```
- 我没有写 *VERSION* ，好像没什么问题。
4. 找到 `Gemfile` 文件。
    ```ruby
    # This will help ensure the proper Jekyll version is running.
    # Happy Jekylling!
    # gem "jekyll", "~> VERSION"
    # This is the default theme for new Jekyll sites. You may change this to anything you like.
    gem "minima", "~> 2.5"
    # If you want to use GitHub Pages, remove the "gem "jekyll"" above and
    # uncomment the line below. To upgrade, run `bundle update github-pages`.
    gem "github-pages", "~> VERSION", group: :jekyll_plugins
    # 取消注释上面这行，并把版本号补上
    ```
- 对照 [Dependency versions](https://pages.github.com/versions/)，修改：
    ```ruby
    gem "github-pages", "~> x.x.x", group: :jekyll_plugins

    group :jekyll_plugins do
      gem "jekyll-feed", "~> x.x.x" 
    end
    ```
5. 执行 `$ bundle install`。
	```
	$ bundle install
	# 可能会有问题
	# 1. 没反应：
	$ bundle config mirror.https://rubygems.org https://gems.ruby-china.com
	# 2. 报错：
	Please CGI escape your usernames and passwords before setting them for authentication
	# 修改 `/.bundle/config`
	```
6. git 上传。
	```
	$ git add *
	$ git commit -m 'SUMMARY'
	$ git remote add origin https://github.com/USER/REPOSITORY.git
	$ git push -u origin BRANCH
	# BRANCH 默认为 master
	```
   
## 本地测试

1. 可以[在本地测试一下](https://help.github.com/en/github/working-with-github-pages/testing-your-github-pages-site-locally-with-jekyll)。

    ```
    $ bundle exec jekyll server
    > Configuration file: /Users/octocat/my-site/_config.yml
    >            Source: /Users/octocat/my-site
    >       Destination: /Users/octocat/my-site/_site
    > Incremental build: disabled. Enable with --incremental
    >      Generating...
    >                    done in 0.309 seconds.
    > Auto-regeneration: enabled for '/Users/octocat/my-site'
    > Configuration file: /Users/octocat/my-site/_config.yml
    >    Server address: http://127.0.0.1:4000/
    >  Server running... press ctrl-c to stop.
    ```

## 写在最后
　　姑且算是成功了，不过很多东西都还不清楚。先放一放，以后再说（。

---

###### Sources
[[1]](https://help.github.com/en/github/working-with-github-pages/creating-a-github-pages-site-with-jekyll) Creating a GitHub Pages site with Jekyll