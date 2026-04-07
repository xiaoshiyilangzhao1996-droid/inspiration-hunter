---
name: inspiration-hunter
description: |
  灵感捕手工作流。一个将热点话题转化为完整技能包的自动化创作流程。
  输入：热点素材（文章链接、GitHub仓库、新闻事件、一句话描述）
  输出：可发布的.skill文件 + 完整创作日志.md + 公众号推广文章
  触发词：灵感捕手 / 创作工作流 / 热点创作 / 帮我做个skill
---

# 灵感捕手工作流

> 热点是信号，研究是挖掘，创作是转化。
> 把一个输入，变成一个完整的产品包——skill、日志、文章，三件套。

---

## 核心流程（三阶段）

```
输入热点 → 系统研究 → 产出三件套
              ↓
         skill.skill
         创作日志.md
         推广文章.md
```

---

## 触发方式

用户说以下任意内容时激活：
- "灵感捕手"
- "创作工作流"
- "热点创作"
- "帮我做个skill"
- "从0到1做一个skill"
- 提供了热点素材并要求做成 skill

---

## 第一阶段：输入理解

### 接受的输入格式

| 类型 | 示例 |
|------|------|
| GitHub 仓库地址 | https://github.com/KKKKhazix/khazix-skills |
| 文章链接 | 公众号文章 / 知乎 / 即刻 / 小红书链接 |
| 新闻事件 | 一句话描述 + 发生时间 |
| 工具/产品 | 某个引起你注意的产品或功能 |
| 社区讨论 | 某个引发你思考的话题 |

### 理解后的动作

不问用户"你想做什么 skill"，而是：
1. **先研究**，搞清楚这个输入到底是什么
2. **再发散**，找到它能生长的方向
3. **最后才做**，而不是拿着用户的原始描述直接套模板

---

## 第二阶段：研究与发散

### 2.1 深入研究

**具体执行步骤（必须逐条完成，不可跳过）：**

**步骤1：抓取原始材料**
```
如果输入是 GitHub 仓库：
  → web_fetch 抓取 README.md 全文
  → 用 GitHub API 获取基础信息：
    curl -s https://api.github.com/repos/{owner}/{repo}
    （提取：description, stargazers_count, forks_count, topics, language）

如果输入是文章链接：
  → web_fetch 抓取正文内容
  → 提取：核心观点、目标读者、讨论热度

如果输入是事件/话题：
  → 直接进入步骤2搜索
```

**步骤2：搜索竞品现状（3个方向都要搜）**
```
方向A（同类方案）：
  → web_search: "{核心概念} GitHub" / "{核心概念} site:github.com"
  → 找3-5个相关仓库，记录 star 数、最后更新时间、主要功能

方向B（同类产品）：
  → web_search: "{核心概念} 产品/工具/竞品"
  → 找2-3个商业产品，记录：解决了什么、定价、用户评价

方向C（反面案例）：
  → web_search: "{核心概念} 失败/问题/吐槽"
  → 找用户抱怨帖/评测帖，提取：现有方案的最大痛点
```

**步骤3：竞品分析输出（必须形成文字）**
```
格式（每条竞品）：
- 名称：{名称}（{链接}）
- 核心做法：{一句话描述}
- 优点：{1-2条}
- 缺点/盲区：{1-2条} ← 这是最重要的字段
- 对本 skill 的启发：{这句话必须写}
```

**步骤4：提炼创作切入点**
回答三个问题，写入创作日志：
1. 现有方案的共同盲区是什么？（找到了才能定位 gap）
2. 我的 skill 解决什么现有方案做不到的事？
3. 这个方向的时机：为什么是现在？

---

### 2.2 开拓发散

**具体执行步骤（必须逐平台完成）：**

**步骤1：小红书**
```
搜索：web_search "{核心话题} 小红书"
提取：
  - 普通人怎么讨论这个话题（不是从业者视角）
  - 最大的困惑/痛点是什么
  - 现有方案在民间口碑如何
```

**步骤2：微信公众号/知乎**
```
搜索：web_search "{核心话题} site:mp.weixin.qq.com OR site:zhihu.com"
提取：
  - 深度分析文章的核心观点
  - 有没有被忽视的角度
  - 评论区的真实讨论
```

**步骤3：GitHub 相关项目**
```
搜索：web_search "{核心话题} site:github.com"
对每个相关仓库：
  → web_fetch 抓取 README
  → 记录：star 数、主要功能、最后更新时间、评价
```

**步骤4：发散记录写入外部链接文件**
```
路径：references/external_links.md
格式：
- 来源 → 核心发现 → 对创作的具体影响（启发/避免/验证）
```

**发散原则：**
- 不是搜索"这个话题"，而是搜索"这个话题的周边"
- 每条搜索结果都要问：它启发了什么？暴露了什么gap？
- 记录所有有价值的外链，注明原因

### 2.3 找到创作切入点

基于研究和发散，回答三个问题：
1. **我能解决什么问题？**（现有方案做不到或做不好的）
2. **我用什么方式解决？**（不是复刻，是差异化的方法）
3. **这个skill的独特价值主张是什么？**（一句话说清楚）

---

## 第三阶段：三件套产出

### 输出物 1：技能包（.skill 文件）

**命名规范：**
- 英文名（全局唯一）：描述性，如 `inspiration-hunter`、`lidan-writing-framework`
- 中文定位：一句话

**必须包含的文件：**
```
{skill-name}/
├── SKILL.md              ← 核心文件，遵循 Agent Skills 规范
├── README.md             ← 用户入口，说明是什么、怎么用
├── 创作日志.md            ← 本次创作日志（模板：references/creation_log_template.md）
├── 推广文章.md            ← 本次推广文章（模板：references/article_template.md）
└── references/
    ├── *_case_study.md   ← 本次创作案例研究
    └── external_links.md ← 所有发散搜索的外链记录
```

**SKILL.md 核心章节（必须覆盖）：**
1. **核心理念**：这个 skill 解决什么，为什么这个方式是对的
2. **触发条件**：激活词、适用场景、不适合场景
3. **核心能力**：输入→处理→输出的完整描述
4. **工具使用**：使用哪些工具、如何使用
5. **工作流程**：分步骤的执行流程
6. **输出规范**：输出的格式、文件结构
7. **质量检查**：关键检查点

**SKILL.md 质量标准：**
- 每一项能力描述必须有具体案例或示例支撑
- 不能写"根据用户需求"这种模糊描述
- 触发词必须穷举，覆盖真实使用场景
- 工作流程必须可执行，不能有歧义

---

### 输出物 2：创作日志（创作日志.md）

> 执行时，复制 `references/creation_log_template.md` 为 `{skill-name}/references/creation_log_{YYYY-MM-DD}.md`，按模板章节填充内容。

**必须包含的章节：**

**1. 灵感来源**
- 原始输入是什么（原文粘贴）
- 什么点打动了你/用户
- 第一反应是什么（判断+直觉）

**2. 深入研究记录**
- 研究了哪些内容（每条记录格式：来源→核心发现→对创作的影响）
- 发现了什么意外的东西
- 竞品分析结论（现有方案的优缺点）

**3. 发散搜索记录**
- 每个平台的搜索关键词
- 有价值的发现（必须附链接）
- 每条发现对创作的具体影响
  - 启发了什么？
  - 避免了什么？
  - 验证了什么需求？

**4. 设计决策**
- 为什么选择这个切入点（而不是其他可能的方向）
- 设计的核心创新点是什么
- 做了哪些取舍，为什么

**5. 创作过程**
- 遇到的难点及解决方法
- 迭代的关键节点
- 最终产出的确认方式

---

### 输出物 3：推广文章（via yinyo-writer）

> 执行时，读取 `references/article_template.md` 作为结构参考，调用 yinyo-writer skill 生成推广文章，写入 `{skill-name}/推广文章.md`。

**调用方式：**
读取 yinyo-writer skill，以其方法论撰写配套推广文章。

**文章必须包含：**
1. **开头**：从具体场景切入，不宏大叙事
2. **讲解**：这个 skill 是什么、能解决什么问题
3. **展示**：1-2个具体使用场景或效果示例
4. **价值主张**：为什么这个 skill 值得用
5. **行动指引**：怎么安装和使用（附 GitHub 链接）
6. **结尾**：有回响的收尾，不是"感谢阅读"

**行动指引标准格式：**
```
三个技能的GitHub地址（直接复制扔给你的Agent）

{skill-name}：{一句话描述}
https://github.com/xiaoshiyilangzhao1996-droid/{repo-name}
```

---

## GitHub 发布流程

**第一步：创建仓库（仅首次需要）**
```bash
curl -X POST https://api.github.com/user/repos \
  -H "Authorization: token {GITHUB_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{"name":"{repo-name}","private":false}'
```

**第二步：初始化 skill 目录**
```bash
cd /root/.openclaw/workspace/skills/{skill-name}
rm -rf .git          # 清理残留git目录（避免.git内文件污染仓库）
git init
git config user.name "yinyo-irreplaceable-you"
git config user.email "yuanclaw2026@163.com"
```

**第三步：提交所有必要文件**
```bash
git add SKILL.md README.md references/
git commit -m "{版本描述：v1.0 - {一句话描述}}"
git remote add origin https://{GITHUB_TOKEN}@github.com/xiaoshiyilangzhao1996-droid/{repo-name}.git
git push -u origin master
```

**第四步：验证完整性**
发布后执行（验证所有必要文件已上传）：
```bash
curl -s https://api.github.com/repos/xiaoshiyilangzhao1996-droid/{repo-name}/contents/ \
  -H "Authorization: token {GITHUB_TOKEN}" | python3 -c "
import sys,json
files = json.load(sys.stdin)
for f in files:
    print(f['name'],'|',f['type'])
"
```

**FALLBACK：git push 失败时（TLS/GnuTLS 超时）**
当 git push 报 `GnuTLS recv error (-110)` 或 `Could not connect to server` 时，使用 Contents API 替代：

```python
import base64, os, requests

TOKEN = "{GITHUB_TOKEN}"
REPO = "xiaoshiyilangzhao1996-droid/{repo-name}"
HEADERS = {"Authorization": f"token {TOKEN}"}

def upload(path, content):
    url = f"https://api.github.com/repos/{REPO}/contents/{path}"
    data = {
        "message": f"Add {path}",
        "content": base64.b64encode(content.encode()).decode()
    }
    r = requests.put(url, headers=HEADERS, json=data, timeout=30)
    print(f"{path}: {r.status_code}")
    return r.ok

for root, dirs, files in os.walk("/root/.openclaw/workspace/skills/{skill-name}"):
    for fname in files:
        if ".git" in root: continue  # 跳过.git目录
        fpath = os.path.join(root, fname)
        rel = os.path.relpath(fpath, "/root/.openclaw/workspace/skills/{skill-name}")
        with open(fpath, encoding="utf-8", errors="replace") as f:
            upload(rel, f.read())
```

**验证 GitHub 连通性（每次发布前）**
```bash
curl -s --max-time 5 https://github.com -o /dev/null -w "%{http_code}"
# 返回200则正常，返回000则网络不通
```

---

## 案例参考

第一个完整案例：**irreplaceable-you.skill**

灵感来源：同事.skill（GitHub上的AI Persona产品）+ 四个关系 Persona 研究
创作过程：见 `references/irreplaceable-you_case_study.md`
