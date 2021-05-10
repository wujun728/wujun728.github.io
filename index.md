---
layout: default
title: Git @ OSC Blog
tagline: 管理你的代码，协作、共享
---
{% include JB/setup %}

<div class="row-fluid">
  <div class="span8">
    <h3>Posts</h3>
    <ul class="posts">
      {% for post in site.posts %}
        <li class="icon-calendar">
          <span class="date">[{{ post.date | date: "%Y-%m-%d" }}]</span>
          <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a>
          <span class="ds-thread-count" data-thread-key="{{ post.id }}"></span>
        </li>
      {% endfor %}
    </ul>
  </div>
  <div class="span3 pull-right">
    <h3>Recent Comments</h3>
    <ul class="ds-recent-comments unstyled" data-num-items="10"></ul>
  </div>
</div>

<script type="text/javascript">
    var duoshuoQuery = {short_name:"{{ site.JB.comments.duoshuo.short_name }}"};
    (function() {
        var ds = document.createElement('script');
        ds.type = 'text/javascript';ds.async = true;
        ds.src = 'http://static.duoshuo.com/embed.js';
        ds.charset = 'UTF-8';
        (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(ds);
    })();
</script>