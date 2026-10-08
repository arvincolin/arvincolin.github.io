# 日常写博客的标准工作流程
## 一、编写内容 + 本地预览
### 1.新建 / 修改文章
hexo new "文章标题"
### 2.本地预览
hexo clean && hexo s
浏览器打开 http://localhost:4000 预览
## 二、提交源码到 GitHub main 分支（备份）
### 方式 A：VS Code 可视化操作（推荐）
源代码管理（Ctrl+Shift+G）—— 把所有更改加入暂存区——填写提交备注——点击「提交」按钮，完成本地提交——推送，同步到 GitHub 远程 main 分支
### 方式 B：终端命令操作
1. 暂存所有修改

git add .

2. 提交到本地仓库，替换成你的备注

git commit -m "新增：XXX文章"

3. 推送到远程 main 分支

第一次推送执行 git push -u origin master:main ，之后直接 git push 即可

## 三、部署更新线上博客
hexo clean && hexo deploy

执行完成后，等待 1-3 分钟再刷新
