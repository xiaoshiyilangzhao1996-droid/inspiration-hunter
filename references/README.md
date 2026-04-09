# references/ 目录说明

本目录包含两类文件：

---

## 模板文件（用于每次新创作）

当你执行灵感捕手工作流时，复制以下模板并填充内容：

| 模板文件 | 用途 | 复制目标路径 |
|---------|------|------------|
| `creation_log_template.md` | 创作日志模板 | `{skill-name}/references/creation_log_{YYYY-MM-DD}.md` |
| `article_template.md` | 推广文章模板 | `{skill-name}/推广文章.md` |

---

## 案例参考（灵感捕手工作流的完整案例）

| 文件 | 说明 |
|------|------|
| `irreplaceable-you_case_study.md` | irreplaceable-you.skill 的完整创作记录：灵感来源→研究→发散→设计决策→迭代过程 |
| `external_links.md` | 该案例创作过程中的所有外链记录，含每条对创作的具体影响 |

---

## 新增创作时

每次新执行灵感捕手工作流，创建新文件夹：
```
{new-skill-name}/references/
├── creation_log_YYYY-MM-DD.md  ← 复制自 creation_log_template.md
├── new_topic_case_study.md     ← 新案例记录
└── external_links.md            ← 新外链记录（追加到 external_links.md）
```

**注意**：`external_links.md` 采用追加模式，每次创作都在文件末尾追加新的外链记录，保留历史积累。
