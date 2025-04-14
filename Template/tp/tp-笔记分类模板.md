---
<%-* 
let  newtitle
if(tp.file.title.includes("未命名") || tp.file.title.toLowerCase().includes("untitled")) 
{ title=await tp.system.prompt("请输入要创建的文件名");
  newtitle=title||tp.date.now("YYYYMMDDHHmmss")
	await tp.file.rename(newtitle)}
	else newtitle=tp.file.title
-%>
<%-*
var cleanTitle = tp.user.getTitleSnippet(newtitle) 
var title = `${cleanTitle}`;
await tp.file.rename(`${title}`);
let filetype = await tp.system.suggester(["学习相关", "工作相关", "其他", "临时路径"], ["学习","工作", "其他", "临时"], false, "路径放到哪里？") 
if (filetype === "学习") { 
myFilePath = "/Inbox/Study/" +  `${title}`;
await tp.file.move(`${myFilePath}`);
} else if (filetype === "工作") { 
myFilePath = "/Inbox/Work/" +  `${title}`;
await tp.file.move(`${myFilePath}`);
} else if (filetype === "其他") { 
myFilePath = "/Inbox/Other/" +  `${title}`;
await tp.file.move(`${myFilePath}`);
} else if (filetype === "临时") { 
myFilePath = "/Inbox/" +  `${title}`;
await tp.file.move(`${myFilePath}`);
} else { 
tp.file.cursor(1)
}
-%>

alias: 
tags: <% `${filetype}` %>
cdate: <% tp.file.creation_date() %>
uid: <% tp.date.now("YYYYMMDDHHmmss") %> 
cssclass: 
Cover: 
---

## Metadata
Status::    <% tp.system.suggester(["🌱发芽状态", "🪴培育状态", "🌲长青状态"], ["#笔记状态/🌱发芽", "#笔记状态/🪴培育","#笔记状态/🌲长青"]) %>
Source Type::  <% tp.system.suggester(["💭想法", "📚书籍", "📰️文章", "🗣️聊天", "💻教学", "▶️视频", "🎧️播客"], ["#📥/💭想法 ", "#📥/📚书籍 ", "#📥/📰️文章", "#📥/🗣️聊天 ", " #📥/💻教学", "#📥/▶️视频", "#📥/🎧️播客"]) %>
Topic:: [[<% tp.system.prompt("这个笔记对应的主题MOC ", "比如：时间管理") %>]]
Author:: 
Source URL:: 

## 长青笔记
一句话概括这篇笔记的内容
Summary:: 

## 自我重述
用自己的话去重述提取的重点内容


## 重点摘抄
摘抄部分原文后，进行筛选加粗然后对加粗的继续进行筛选荧光笔选出。


## 相关文章
Page Link::  
