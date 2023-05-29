---
title: Wsl的安装
tags: wsl
categories:
  - linux
# swiper_index: 2
abbrlink: 2779079921
date: 2023-04-05 11:15:23
---

# wsl的安装

## 1. window开发环境下Wsl2的安装

[WSL 安装的官方文档:](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
https://docs.microsoft.com/en-us/windows/wsl/install-win10

[哔哩哔哩视频](https://docs.microsoft.com/en-us/windows/wsl/install-win10)

## 2. Windows10开发环境搭建 | Terminal和VS Code

[Windows Terminal安装文档](https://docs.microsoft.com/en-us/windows/terminal/get-started)
https://docs.microsoft.com/en-us/windows/terminal/get-started

[哔哩哔哩视频](https://www.bilibili.com/video/BV1Zz4y167Vo/?spm_id_from=333.788.recommend_more_video.-1&vd_source=f20bcccbcf2fc9e03d3893f3ecae8826)

## 3. Windows10开发环境搭建在WSL2里安装Docker

[安装脚本文件]( https://gist.github.com/xiaopeng163/f3e72bb1990860859076985d5a723cba)

install-docker.sh

```bash
# install docker
curl -fsSL get.docker.com -o get-docker.sh
sh get-docker.sh

if [ ! $(getent group docker) ];
then
    sudo groupadd docker;
else
    echo "docker user group already exists"
fi

sudo gpasswd -a $USER docker
sudo service docker restart

rm -rf get-docker.sh

```
[哔哩哔哩](https://www.bilibili.com/video/BV1nt4y1k7Fy/?spm_id_from=333.788.recommend_more_video.-1&vd_source=f20bcccbcf2fc9e03d3893f3ecae8826)

## 4. vscode插件推荐

1. Material Theme & Material Icon Theme  主题
2. one dark pro  暗色主题  Dracula Official 吸血鬼主题
3. github  theme  github主题
4. Prettier - Code formatter 代码格式化
设置搜索save  找到format on save打开
5. Bracket Pair Colorizer 2 代码块颜色
6. Indent-Rainbow  缩进颜色
7. Remote Development  远程开发
8. GitLens  git插件
9. code spell checker 代码拼写检查
10. code runner 代码运行
11. vim  vim插件
12. learn vim vim学习插件
13. comment tag 代码注释
14. path intellisense 代码路径提示
15. paste image 代码图片粘贴
使用方法：截图之后直接ctrl+shift+v
16. markdownlint  markdown语法检查
17. tabnine 代码提示
18. 中文标识符号转英文
19. Material Icon Theme or vscode-icons图标主题插件
20. Error Lens 代码错误提示
21. Image preview 图片预览
22. CodeSnap 代码截图
23. GBK to UTF8 for vscode gbk转utf8
24. Doxygen Documentation Generator 代码注释生成
25. Remote - SSH 远程ssh
26. Hungry Delete 删除多余空格
27. Competitive Programming Helper (cph) 竞赛插件
28. codetran 代码翻译
29. auto markdown preview markdown预览
30. better comments 代码注释
31. colorize 代码颜色
32. docker  docker插件(需要安装docker)
33. eslint 代码检查
34. explorer exclude 代码排除
35. gitblame 代码git blame
36. gihistory 代码git历史
37. git 版本控制
38. import Cost
39. intellicode 智能代码提示
40. output colorizer 输出框代码着色
41. peacock
42. polacode 创建代码片段截图
43. powershell
44. vibrancy continued 使主题背景具有玻璃效果
45. winddown 休息提醒
46. codetour 代码旅游
47. draw.io integration 画图
48. Project Manager 项目管理工具

[哔哩哔哩](https://www.bilibili.com/video/BV1Kv4y1t7mT/?spm_id_from=333.788.recommend_more_video.2&vd_source=f20bcccbcf2fc9e03d3893f3ecae8826)
## 5. vscode提升用户体验
settings.json 设置

```json
{
  "files.autoSave": "afterDelay",
  "files.autoGuessEncoding": true,
  "workbench.list.smoothScrolling": true,
  "editor.cursorSmoothCaretAnimation": true,
  "editor.smoothScrolling": true,
  "editor.cursorBlinking": "smooth",
  "editor.mouseWheelZoom": true,
  "editor.formatOnPaste": true,
  "editor.formatOnType": true,
  "editor.formatOnSave": true,
  "editor.wordWrap": "on",
  "editor.guides.bracketPairs": true,
  //"editor.bracketPairColorization.enabled": true, (此设置vscode在较新版本已默认开启)
  "editor.suggest.snippetsPreventQuickSuggestions": false,
  "editor.acceptSuggestionOnEnter": "smart",
  "editor.suggestSelection": "recentlyUsed",
  "window.dialogStyle": "custom",
  "debug.showBreakpointsInOverviewRuler": true,
}

```
格式化代码
设置中搜索format  找到format on save打开
## 6.前端插件推荐
1. live server 实时预览
搜索auto save  找到 auto save 选择after delay
2. live sass compiler sass编译
3. Bracket Pair Colorizer - 这个插件会根据括号颜色来匹配括号，使代码更易于阅读。

4. Auto Rename Tag - 这个插件可以让你在编辑HTML或XML标签时自动重命名相关的结束标签。这对于避免手动查找和更新标记名称时节省了很多时间。

5. Live Server - 这个插件会在本地运行一个服务器，同时监听HTML、CSS和JavaScript文件的更改。你可以打开浏览器并实时预览你的网页，而无需手动刷新。

6. Prettier - 这个插件可以帮助你格式化你的代码，使其更加规范、易于阅读。它支持多种编程语言，并且可以自定义配置规则。

7. ESLint - 这个插件可以帮助你检测JavaScript代码中的错误和潜在问题。它使用一组预定义的规则，也可以自定义配置，以符合你的团队规范。

8. CSS Peek - 这个插件可以帮助你快速查看CSS类和ID定义的样式。它还支持Sass、Less等CSS预处理器的语法。

9. IntelliSense for CSS class names - 这个插件会在HTML和CSS文件中启用智能提示，为你提供CSS类或ID名称的建议。这可以大大加快开发速度。

10. Path Intellisense - 这个插件可以自动完成文件路径和文件名。它支持各种编程语言，并可以自定义配置。

11. GitLens - 这个插件可以帮助你更轻松地管理Git存储库。它可以显示每行代码的最后一次修改、提交历史记录等信息。

12. Color Highlight - 这个插件会将CSS中的颜色值高亮显示。这使得你可以更快地找到并更新颜色，以及在调试时快速识别颜色问题。