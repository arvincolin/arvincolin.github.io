主题ils
##问题一：首页只显示文章摘要，点击阅读全文会跳转到空页面。##
解决办法：1.修改_config.yml
url: https://arvincolin.github.io/
root: /
permalink: :abbrlink/   # 这个是安装了插件hexo-abbrlink后改的
2.修改_config.ils.yml
post_wordcount:
  wordcount: false   # 关闭字数统计
  min2read: false    # 关闭阅读时长统计
安装了插件hexo-wordcount后，改为true

##问题二:博客文章没有首行缩进##
解决办法：打开 themes/ils/source/css/style.styl 在最后添加下面的代码
/* 文章正文段落首行缩进2个汉字 */
.article-content p
  text-indent 2em
  text-align justify
后来，为了第一段也有首行缩进，删掉了下面三行
/* 可选：标题后的第一段不缩进，符合中文出版规范 */
.article-content p:first-of-type
  text-indent 0
  
##问题三：新建的分类页和标签页点开后是空页面##
解决办法：第一步 在themes\ils\layout\page.ejs里补两个分支
   <% } else if (is_tag()) { %>
                    <%- partial('tag-content') %>

                <% } else if (page.type === 'categories') { %>
                    <%- partial('_partial/all-categories') %>

                <% } else if (page.type === 'tags') { %>
                    <%- partial('_partial/all-tags') %>

                <% } else if (page.title == 'about') { %>
第二步：新建themes\ils\layout\_partial\all-categories.ejs
<div class="fade-in-down-animation">
  <div class="category-container">
    <div class="category-name">
      <i class="fa fa-folder"></i> 全部分类 [<%= site.categories.length %>]
    </div>
    <ul class="category-list">
      <% site.categories.sort('name').each(function(cat){ %>
        <li>
          <a href="<%- url_for(cat.path) %>"><i class="fa fa-folder-o"></i> <%= cat.name %></a>
          <span class="category-list-count">[<%= cat.length %>]</span>
        </li>
      <% }) %>
    </ul>
  </div>
</div>
第三步：新建新建themes\ils\layout\_partial\all-tags.ejs
<div class="fade-in-down-animation">
  <div class="tag-container">
    <div class="tag-name">
      <i class="fa fa-tag"></i> 全部标签 [<%= site.tags.length %>]
    </div>
    <div class="tag-cloud">
      <%- tagcloud({
        min_font: 13, max_font: 26, amount: 300,
        color: true, start_color: '#999', end_color: '#111',
        orderby: 'name', order: 1
      }) %>
    </div>
  </div>
</div>
第四步：在themes\ils\source\css\style.styl里加入下面的代码
.category-list { list-style: none; padding: 0; margin: 16px 0 0 0; }
.category-list li { margin: 10px 0; padding-bottom: 8px; border-bottom: 1px dashed #eee; }
.category-list li a { text-decoration: none; }
.category-list li a:hover { color: #409eff; }
.category-list-count { margin-left: 8px; opacity: .5; font-size: .9em; }
.tag-cloud { margin-top: 16px; line-height: 2; }
.tag-cloud a { display: inline-block; margin: 4px 10px; text-decoration: none; }

主题keep
##问题一：博客文章没有首行缩进##
解决办法：第一步 用下面的代码替换_config.keep.yml里的inject部分
# ---------------------------------------------------------------------------------------
# Docs: https:inject.html
# ---------------------------------------------------------------------------------------
inject:        
  enable: true   # Option values: true | false
  css:
    - /css/custom.css
    # e.g.
    # - /css/custom-1.css
    # - /css/custom-2.css
    # - ...
  js:
    -
    # e.g.
    # - /js/custom-1.js
    # - /js/custom-2.js
    # - ...
第二步：新建source/css/custom.css，写入一下内容
/* 文章正文所有段落首行缩进 */
.post-content p {
  text-indent: 2em;
}

/* 排除不需要缩进的元素 */
.post-content blockquote p,
.post-content li p,
.post-content table p,
.post-content pre p,
.post-content .highlight p {
  text-indent: 0;
}

##问题二：自定义配置多个作者标识失败##
解决办法：暂无