# 日常写博客的标准工作流程

## 一、编写内容 + 本地预览

### 1.新建 / 修改文章

```
hexo new "文章标题"
```

### 2.本地预览

```
hexo server
```

如果不只是新建或修改了文章，用`hexo clean && hexo server`更好。

浏览器打开 http://localhost:4000 预览

## 二、提交源码到 GitHub main 分支（备份）

### 方式 A：VS Code 可视化操作（推荐）

源代码管理（Ctrl+Shift+G）—— 把所有更改加入暂存区——填写提交备注——点击「提交」按钮，完成本地提交——推送，同步到 GitHub 远程 main 分支。

### 方式 B：终端命令操作

1. 暂存所有更改

```
git add .
```

2. 写备注信息，提交更改到本地仓库

```
git commit -m "新增：XXX文章"
```

3. 推送到远程 main 分支

```
git push
```

## 三、部署更新线上博客

```
hexo clean && hexo deploy
```

执行完成后，等待 1-3 分钟再刷新

**日常写博客的标准工作流程是 `hexo new` 写文章 → `hexo s` 本地预览 → 提交源码到 GitHub main 分支 → `hexo clean && hexo d` 发布。遇到"改了没反应"，先 `hexo clean` 再说。**
