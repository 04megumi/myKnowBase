# My Knowledge Base (个人知识库项目)

This repository is a structured and extensible knowledge base for organizing technical glossaries across various CS subjects such as Computer Networks, Operating Systems, and Computer Architecture.  
本项目是一个结构化、可扩展的技术术语知识库，涵盖计算机网络、操作系统、计算机组成原理等专业内容。

## Project Structure (项目结构)

- `glossary_docs/` – Markdown-based glossaries categorized by subject and chapter.  
  按学科和章节分类的 Markdown 术语词汇表。
- `glossary_db/` – SQLite databases generated from markdown glossaries.  
  从 Markdown 自动生成的 SQLite 数据库文件。
- `scripts/` – Future automation scripts (e.g., import markdown to DB, search, etc.).  
  未来的自动化脚本（如 Markdown → 数据库、全文搜索等）。

## Usage (使用方式)

You can write and maintain technical glossaries in Markdown first. Scripts will later convert them into searchable database entries.  
您可以先用 Markdown 记录术语词条，后续脚本会将其转为可搜索的数据库记录。