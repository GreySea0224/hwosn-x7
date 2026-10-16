# index.hHTML项目说明

## 这是什么

- 整个 App 就在一个文件里：`index.HTML`（HTML + CSS + JS 混在一起），没有构建步骤，纯前端。
- 中文界面，主要给手机端用（Termux + 手机浏览器）。
- 数据都存在浏览器本地：localStorage（key 前缀 `wh_`）和 IndexedDB（`wh_db`）。
- 文件里有多处同名函数的「包装覆盖」（例如 `renderChat`、`callAPI`、`askAndAppend`），
  读代码时要注意最后生效的是哪一层。

## 用户的规矩（必须遵守）

1. 改 `index.HTML` 之前，先在项目目录里复制一份备份，命名 `index.HTML.bak-YYYYMMDD`
   （同一天改多次就加序号，例如 `-2`，不要覆盖旧备份）。
2. 动手改文件之前，先用中文说清楚「准备改什么」。
3. 执行任何命令之前，先用中文解释这条命令是干什么的。
4. 不要安装软件、不要删除文件、不要改 Termux 配置、不要访问项目目录以外的文件。
5. 遇到不确定的操作，先问用户。
6. 用户是编程新手：用大白话解释，不要假设她看得懂代码，改动尽量小而稳。
7. 前端内部有一个角色“引导者”，负责给新用户做新手引导，并记录新功能，如果有新的大功能完成，在引导者的记忆里加一个更新内容描述。

## 改完怎么验证

- 语法检查（不写临时文件，只读）：
  `node -e 'const fs=require("fs");const h=fs.readFileSync("index.html","utf8");const b=[...h.matchAll(/<script>([\s\S]*?)<\/script>/g)];let bad=0;b.forEach((x,i)=>{try{new Function(x[1])}catch(e){bad++;console.log("片段"+i+" 语法错误: "+e.message)}});console.log("共检查 "+b.length+" 个 script 片段，语法错误 "+bad+" 个")'`
- 环境里没有浏览器，界面效果没法自动跑；改完请让用户在手机上刷新页面看效果。
