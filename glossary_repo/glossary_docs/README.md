# Glossary Documents (术语词条文档)

This directory contains the main source files for the glossary knowledge base, written in Markdown.  
本目录包含知识库的主词条文件，使用 Markdown 编写。

## Structure (结构说明)

- Each subject (e.g., Computer Network) has its own subfolder.  
  每门学科有独立的子文件夹。
- Each chapter within a subject has a dedicated `.md` file.  
  每个章节为一个 `.md` 文件，内含多个术语词条。

## Writing Format (书写规范)

Use the following format for each glossary entry:  
使用如下格式书写每个术语：

```markdown
### PPP
- **Full Name**: Point-to-Point Protocol
- **Definition**: 一种点对点的数据链路层协议，用于通过串行连接传输多种协议的数据包。
- **Chapter**: Data Link Layer
- **Topic**: 拓展的链路层协议
- **Tags**: 协议,链路层,串行通信
- **Note**: 支持身份认证、压缩、加密等扩展功能。