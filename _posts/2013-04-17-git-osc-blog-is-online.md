---
layout: post
title: "Git @ OSC Blog 上线了"
description: ""
category: Git @ OSC
tags: [jekyll, markdown]
---
{% include JB/setup %}

使用 [Jekyll][] 简单为 [Git @ OSC][] 搭建了个博客，以后 [Git @ OSC][] 的更新日志、新闻等都会在此发布。

此网站是完全静态的，所有页面均为 Jekyll 生成，使用了国内的 “[多说][duoshuo]” 社会化评论系统来支持网友互动、评论功能。

网站刚刚跑起来，页面和CSS还没怎么定制，默认样式和显示的内容还有待修改。有什么好的意见建议可以直接在评论里提。

## 技术细节

和 [Github Pages][] 类似，站点源码和文章存储在一个 git 仓库里，使用 git hook 来重新生成站点。
使用 [Markdown][] 来编写页面，每次 push 代码的时候，`post-update` hook 会自动被调用并重新生成整站内容，这个过程是完全自动的。

`post-update` 脚本代码如下：

{% highlight sh %}
#!/bin/sh

# Jekyll update hook

# $HOME=/home/git
GIT_REPO=$HOME/blog.git
TMP_GIT_CLONE=$HOME/tmp/blog
PUBLIC_WWW=$HOME/www/blog

git clone $GIT_REPO $TMP_GIT_CLONE
cd $TMP_GIT_CLONE
jekyll --no-auto $TMP_GIT_CLONE $PUBLIC_WWW
cd $HOME
rm -Rf $TMP_GIT_CLONE
exit
{% endhighlight %}

下面需要做的只是配置 [Nginx][] 把 `/blog` 指向 Jekyll 生成的网站目录。

{% highlight nginx %}
location ~ ^/blog {
    root /home/git;
}
{% endhighlight %}

对 [Jekyll][] 做了点简单的定制，使用了它的一个第三方主题（[Jekyll BootStrap][]），它可以把 [BootStrap][]
样式应用到 [Jekyll][] 上。

代码格式化使用 [Jekyll][] 内置支持的 [Pygments][]，使用方法如下：

{% raw  %}
    {% highlight ruby %}
    def foo
      puts 'foo'
    end
    {% endhighlight %}
{% endraw %}

需要安装 `Pygments`，并在 `_config.yml` 中配置 `pygments: true`，然后再在页面引入代码格式化所用到的 [CSS][] 就可以了。

  [Git @ OSC]: http://git.oschina.net
  [Jekyll]: http://www.oschina.net/p/kyll
  [Markdown]: http://www.oschina.net/p/markdown
  [Github Pages]: http://pages.github.com
  [Jekyll BootStrap]: http://www.oschina.net/p/jekyllbootstrap
  [BootStrap]: http://www.oschina.net/p/bootstrap
  [Nginx]: http://www.oschina.net/p/nginx
  [Pygments]: http://www.oschina.net/p/pygments
  [CSS]: https://github.com/richleland/pygments-css
  [duoshuo]: http://duoshuo.com