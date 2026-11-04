---
created: 2026-01-01
type: reference
status: active
aliases:
  - Obsidian 规范速查
  - Obsidian 写作规范
cssclasses:
  - reference
tags:
  - 领域-模板
  - 阶段0-规范
---

# Obsidian 规范速查

> [!abstract] 用途
> 本文件是 Obsidian Flavored Markdown 的写作规范与核心语法速查。所有学习笔记必须遵循。
> 来源 skill：`obsidian-markdown`（工作流：frontmatter → 标准 Markdown 骨架 → wikilinks → embeds → callouts → 阅读视图验证）。
> **本文件是参考文档，不要复制进正式笔记。**

---

## 1. Properties（frontmatter）

```yaml
---
title: 笔记标题
date: 2026-01-01
tags:
  - learning
  - network/tcp
aliases:
  - TCP
cssclasses:
  - learning
status: in-progress
---
```

规则：`tags` / `aliases` / `cssclasses` 是 Obsidian 识别的默认属性；标签可含字母、数字（不可首位）、下划线、连字符和 `/`，**不支持空格**。

## 2. 内部链接与嵌入

| 语法 | 用途 |
|---|---|
| `[[笔记名]]` | 链接到本库笔记（改文件名会自动跟踪） |
| `[[笔记名\|显示文本]]` | 自定义显示文本 |
| `[[笔记名#标题]]` | 链接到某篇的某个标题 |
| `[[笔记名#^block-id]]` | 链接到块 |
| `![[笔记名]]` | 嵌入整篇内容 |
| `![[笔记名#标题]]` | 嵌入某个章节 |
| `![[图片.png\|300]]` | 嵌入图片并指定宽度 |
| `![[文档.pdf#page=3]]` | 嵌入 PDF 指定页 |

块 ID 写法：段落末尾追加 `^block-id`；列表或引用块则另起一行写 `^block-id`。

> [!tip] 选择规则
> 库内笔记一律用 wikilinks；**站外 URL 一律用标准 Markdown 链接** `[text](url)`。

## 3. Callouts

```markdown
> [!note] 标题
> 正文

> [!tip]
> 正文

> [!warning] 自定义标题
> 正文

> [!faq]- 默认折叠（- 折叠 / + 展开）
> 答案
```

常用类型：`note`、`tip`、`warning`、`info`、`example`、`quote`、`bug`、`danger`、`success`、`failure`、`question`、`abstract`、`todo`。

本仓库约定：`tip` 讲关键理解，`warning` 讲易错点，`note` 放权威资料，`faq` 放折叠问答，`danger` 放安全风险。

## 4. 标签

```markdown
#learning              # 行内标签
#network/tcp           # 嵌套标签，体现层级
```

行内标签与 frontmatter 的 `tags` 可共存，但**同一概念只在一处定义**，避免检索分裂。

## 5. 高亮、注释、脚注

```markdown
==高亮重点==

这是可见 %%隐藏文字%% 的写法。

%%
整块隐藏内容。
%%

带脚注的句子[^1]。

[^1]: 脚注内容。

行内脚注写法^[直接写在这里]。
```

## 6. 公式

```markdown
行内：$O(n \log n)$

块级：
$$
\frac{a}{b} = c
$$
```

## 7. Mermaid 图

````markdown
```mermaid
graph TD
    A[开始] --> B{判断}
    B -->|是| C[执行]
    B -->|否| D[结束]
    class C internal-link;
```
````

`class X internal-link;` 让节点可点击跳转到库内笔记。协议类笔记优先用 `sequenceDiagram`（握手/时序）和 `graph`（分层/调用关系）。

## 8. 标准 Markdown 骨架

标题层级不跳级（`#` → `##` → `###`）；代码块标语言；表格用于对比型信息；`> [!todo]` 或 `- [ ]` 用于可勾选任务。

---

## ✅ 笔记质量检查清单

写完每篇笔记后逐条核对：

- [ ] frontmatter 完整（title / date / tags / aliases / status）
- [ ] 标签无空格、无中文空格分隔
- [ ] 所有库内关联用 `[[wikilinks]]`，站外用标准 Markdown 链接
- [ ] ==每个 wikilink 都能解析到真实笔记==：Obsidian 大小写敏感，`[[Bash-基础语法]]` 匹配不到 `bash-基础语法.md`；不存在的目标不要留
- [ ] ==页脚/署名不得用 wikilink==：`Hermes Agent` 是产品名不是库内笔记，写纯文本
- [ ] ==同一实体在本篇内表述一致==：同一路径、选项、命令、版本号只允许一种写法
- [ ] 关键结论用 `==高亮==` 标出，不靠语气强调
- [ ] 概念关系用 Mermaid 表达（至少 1 张）
- [ ] 每章有「常见陷阱」，写**真实易错点**而非套话
- [ ] 资料来源**全部经过检索验证**，禁止凭印象编造链接
- [ ] ==文中每个命令/函数都真实存在==：无法追溯到官方文档的命令名按编造处理
- [ ] 无「整节重复」：实战节若与理论表雷同，说明实战从没真写
- [ ] 技术表述可被质疑：时间线、版本、状态机、数值均写明来源 RFC 编号
- [ ] 中英混排统一用简体中文，不出现繁体或无意义英文插词
- [ ] 章节顺序与前置依赖一致
- [ ] 末尾有「速查表 / FAQ / 踩坑 / 关联笔记」