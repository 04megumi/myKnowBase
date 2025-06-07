# My Knowledge Base (个人知识库项目)

This repository is a structured and extensible knowledge base for organizing technical glossaries and study notes across various CS subjects such as Computer Networks, Operating Systems, Databases, and more.  
本项目是一个结构化、可扩展的技术术语与知识笔记库，涵盖计算机网络、操作系统、数据库等多个专业内容。

---

## 📁 Project Structure (项目结构)

```plaintext
.
├── content/                 # 学习笔记区（MySQL、Redis 等）
│   ├── mysql/
│   │   ├── basics/         # MySQL 基础知识
│   │   └── advanced/       # MySQL 高级内容
│   └── redis/
│       └── basics/         # Redis 基础内容
├── glossary_repo/          # 技术术语词库（glossary 项目）
│   ├── glossary_docs/      # 按章节分类的 Markdown 术语表
│   └── glossary_db/        # 从 Markdown 生成的 SQLite 数据库
└── README.md               # 项目说明