---
title: Neovim 基本用法
date: 2026-09-09
tags:
  - neovim
  - learning
  - vim
aliases:
  - Neovim Basics
  - Vim 基础
cssclasses:
  - learning
---
# [[neovim-基本用法]]

> [!tip] 学习目标
> 作为初级用户，从零掌握 Neovim 的核心操作、配置与插件生态，能够高效编辑文本并构建个人化的编辑工作流。

---

## 🎯 难度分段学习路径

| 难度 | 目标人群 | 核心关注 | 预估时长 |
|---|---|---|---|
| **入门** | 完全零基础、初次接触 Vim/Neovim | 模式切换、光标移动、文本编辑、窗口操作 | 15h |
| **进阶** | 有基础、需要提高效率 | 搜索替换、可视模式、插件管理、个人配置 | 20h |
| **高级** | 需要深度自定义开发 | Lua 配置、插件开发、LSP 集成、性能优化 | 30h |

**总学时**：65h | **适用**：零基础或初级用户，希望系统掌握 Neovim

---

## 📖 第一章 入门（Beginner）

### 1.1 核心概念与模式

**知识点详解**

Neovim 的核心设计理念是**模式编辑**——不同模式下相同的按键执行不同操作。理解模式是掌握 Neovim 的第一步。

| 模式 | 进入方式 | 核心用途 | 退出方式 |
|---|---|---|---|
| **正常模式** | `Esc` | 导航、删除、复制、粘贴 | 默认模式 |
| **插入模式** | `i`, `a`, `o` | 输入文本 | `Esc` |
| **可视模式** | `v`, `V`, `Ctrl+v` | 选中文本 | `Esc` |
| **替换模式** | `R` | ==持续覆盖输入==（单字符 `r` 的加强版） | `Esc` |
| **选择模式** | `Ctrl+g` | 与可视模式配对，状态栏显示 `SELECT` | `Ctrl+g` |
| **命令行模式** | `:` | 执行命令（保存、退出等） | `Enter` |
| **搜索模式** | `/`, `?` | 正向/反向搜索 | `Enter` 或 `Esc` |
| **终端模式** | `Ctrl+\`` 或 `:terminal` | 内嵌终端（跑测试、跑程序） | ==`Ctrl+\`` 再按 `Ctrl+n` 回正常模式== |

> [!tip] 关键理解
> 正常模式是 Neovim 的"默认状态"。大多数时间你应该处于正常模式，只在需要输入文本时才进入插入模式。这种设计让双手不离开主键盘区就能完成所有操作。

**填空题（每章 4 道，答案见本节末尾）**

1. Neovim 的默认模式是 ______ 模式，用于导航和编辑操作。
2. 按 `i` 键进入 ______ 模式，可以输入文本。
3. 按 `v` 键进入 ______ 模式，可以选中文本。
4. 按 `:` 键进入 ______ 模式，可以执行保存、退出等命令。

**答案**：
1. 正常
2. 插入
3. 可视
4. 命令行

---

### 1.2 启动与退出

**知识点详解**

| 操作 | 命令 | 说明 |
|---|---|---|
| 启动 Neovim | `nvim` | 无参数启动 |
| 打开文件 | `nvim file.txt` | 打开指定文件 |
| 退出（未修改） | `:q` | quit |
| 保存并退出 | `:wq` | write + quit |
| 强制退出 | `:q!` | 不保存强制退出 |
| 仅保存 | `:w` | write |

> [!warning] 注意
> `:q!` 中的 `!` 表示强制操作，会丢弃所有未保存的修改。使用前请确认。

**填空题**

1. `:wq` 中 `w` 表示 ______，`q` 表示 ______。
2. `:q!` 中的 `!` 表示 ______，强制退出不保存。
3. 在正常模式下输入 `ZZ` 可以 ______ 并退出。
4. 在正常模式下输入 `ZQ` 可以 ______ 不保存退出。

**答案**：
1. 写入, 退出
2. 强制
3. 保存
4. 不保存

---

### 1.3 光标移动

**知识点详解**

| 快捷键 | 说明 | 记忆技巧 |
|---|---|---|
| `h` | 左移 | ← |
| `j` | 下移 | ↓ |
| `k` | 上移 | ↑ |
| `l` | 右移 | → |
| `0` | 行首 | 零 |
| `$` | 行尾 | 美元符号在行尾 |
| `gg` | 文件开头 | go to top |
| `G` | 文件结尾 | go to bottom |
| `w` | 下一个单词 | word |
| `b` | 上一个单词 | back |
| `Ctrl+f` | 向下翻页 | forward |
| `Ctrl+b` | 向上翻页 | backward |

> [!tip] 记忆技巧
> `hjkl` 四个键在键盘上排成一行，`h` 在最左（左移），`l` 在最右（右移），`j` 在下（下移），`k` 在上（上移）。

**填空题**

1. `hjkl` 四个键分别对应 ______、______、______、______ 方向移动。
2. `gg` 表示跳转到文件的 ______。
3. `G` 表示跳转到文件的 ______。
4. `w` 表示跳转到下一个 ______ 的开头。

**答案**：
1. 左, 下, 上, 右
2. 开头
3. 结尾
4. 单词

---

### 1.4 文本编辑

**知识点详解**

| 快捷键 | 说明 | 示例 |
|---|---|---|
| `i` | 光标前插入 | `iHello` |
| `a` | 光标后插入 | `aHello` |
| `o` | 下方新建一行 | `oHello` |
| `O` | 上方新建一行 | `OHello` |
| `x` | 删除光标下字符 | `x` |
| `dd` | 删除整行 | `dd` |
| `yy` | 复制整行 | `yy` |
| `p` | 粘贴到光标后 | `p` |
| `u` | 撤销 | `u` |
| `Ctrl+r` | 重做 | `Ctrl+r` |
| `r` | 替换单个字符 | `ra` |
| `cw` | 修改单词 | `cw` |

> [!tip] 编辑思维
> Neovim 的编辑是"动词+名词"的组合。`d` 是删除动词，`w` 是单词名词，`dw` 就是删除单词。`c` 是修改动词，`cw` 就是修改单词（删除并进入插入模式）。

**填空题**

1. `dd` 删除整行后，使用 `p` 可以 ______ 到光标下方。
2. `u` 表示 ______，`Ctrl+r` 表示 ______。
3. `cw` 表示 ______，常用于修改单词。
4. `r` 键用于 ______ 单个字符。

**答案**：
1. 粘贴
2. 撤销, 重做
3. 修改单词
4. 替换

---

### 1.5 窗口与分割

**知识点详解**

| 操作 | 命令 | 说明 |
|---|---|---|
| 水平分割 | `:split` 或 `Ctrl+w s` | 上下分屏 |
| 垂直分割 | `:vsplit` 或 `Ctrl+w v` | 左右分屏 |
| 切换窗口 | `Ctrl+w hjkl` | 方向键切换 |
| 关闭窗口 | `:q` 或 `Ctrl+w q` | 关闭当前窗口 |
| 窗口等分 | `Ctrl+w =` | 所有窗口等大 |
| 窗口最大化 | `Ctrl+w _` | 当前窗口最大 |

**填空题**

1. `:vsplit` 表示 ______ 分割窗口。
2. `Ctrl+w h` 表示切换到 ______ 侧的窗口。
3. `Ctrl+w =` 表示将所有窗口 ______。
4. `Ctrl+w _` 表示将当前窗口 ______。

**答案**：
1. 垂直
2. 左
3. 等大
4. 最大化

---

### 1.6 第一章综合练习

**填空题（本章共 4 道，答案见下方）**

1. Neovim 的默认模式是 ______ 模式。
2. `:wq` 中 `w` 表示 ______，`q` 表示 ______。
3. `dd` 删除整行后，使用 `p` 可以 ______ 到光标下方。
4. `Ctrl+w h` 表示切换到 ______ 侧的窗口。

**本章答案**：
1. 正常
2. 写入, 退出
3. 粘贴
4. 左

**综合项目**：完成 Neovim 启动、打开文件、编辑文本、分割窗口、保存退出的全流程练习，不看帮助文档。

> [!tip] 常见陷阱
> 1. **模式遗忘**：频繁误按 `Esc` 导致从插入模式回正常模式，或反之；练习时先确认当前模式
> 2. **引号不匹配**：输入模式下输入引号可能产生转义字符，正常模式下用 `r` 替单字符，`cw` 修改单词
> 3. **窗口混淆**：`:split` 和 `:vsplit` 易混淆，记住：`split` 是水平，`vsplit` 是垂直
> 4. **保存遗忘**：频繁使用 `:q!` 导致丢失修改，养成 `:` + `wq` 的肌肉记忆

---

## 📖 第二章 进阶（Intermediate）

### 2.1 搜索与替换

**知识点详解**

| 操作 | 命令 | 说明 |
|---|---|---|
| 向下搜索 | `/pattern` | 正常模式下输入 |
| 向上搜索 | `?pattern` | 反向搜索 |
| 下一个匹配 | `n` | next |
| 上一个匹配 | `N` | 反向 next |
| 取消高亮 | `:noh` | no highlight |
| 全局替换 | `:%s/old/new/g` | 替换所有 |
| 确认替换 | `:%s/old/new/gc` | 每次确认 |
| 行内替换 | `:s/old/new/g` | 当前行替换 |

> [!tip] 搜索技巧
> 搜索时可以使用 `\c` 忽略大小写，如 `/pattern\c`。使用 `\C` 强制大小写敏感。

**填空题**

1. `/pattern` 中 `/` 表示 ______ 搜索。
2. `n` 表示跳转到 ______ 一个匹配。
3. `:%s/old/new/g` 中 `g` 表示 ______。
4. `:noh` 用于 ______ 搜索高亮。

**答案**：
1. 向下
2. 下一个
3. 全局
4. 取消

---

### 2.2 可视模式

**知识点详解**

| 模式 | 进入方式 | 用途 |
|---|---|---|
| 字符可视 | `v` | 逐字符选择 |
| 行可视 | `V` | 逐行选择 |
| 块可视 | `Ctrl+v` | 矩形块选择 |

**常用操作**：

| 操作 | 说明 |
|---|---|
| `d` | 删除选中内容 |
| `y` | 复制选中内容 |
| `>` | 向右缩进 |
| `<` | 向左缩进 |
| `~` | 大小写转换 |

**填空题**

1. `v` 进入 ______ 可视模式，逐字符选择。
2. `V` 进入 ______ 可视模式，逐行选择。
3. `Ctrl+v` 进入 ______ 可视模式，矩形选择。
4. 在可视模式下按 `d` 可以 ______ 选中内容。

**答案**：
1. 字符
2. 行
3. 块
4. 删除

---

### 2.3 插件管理

**知识点详解**

Neovim 的插件生态是其强大之处。推荐使用 `lazy.nvim` 作为插件管理器。

**安装 lazy.nvim**：

```bash
# ==官方安装方式==：克隆到 stdpath("data")/lazy（不要用 packer/start，那是 packer 的路径）
git clone https://github.com/folke/lazy.nvim.git \
  "${XDG_DATA_HOME:-$HOME/.local/share}/nvim/lazy/lazy.nvim"
```

> [!warning] 别抄错路径
> 网上大量教程把 lazy.nvim clone 到 `~/.local/share/nvim/site/pack/*/start/`，那是 **packer** 的目录约定。用 lazy.nvim 就必须放在 `data/lazy/lazy.nvim`，否则下面 `lazypath` 找不到它，插件管理器不会加载。

**基本配置**：

```lua
-- init.lua
local lazypath = vim.fn.stdpath("data") .. "/lazy/lazy.nvim"
vim.opt.rtp:prepend(lazypath)

require("lazy").setup({
  { "nvim-tree/nvim-tree.lua" },
  { "nvim-telescope/telescope.nvim" },
})
```

**常用命令**：

| 命令 | 说明 |
|---|---|
| `:Lazy` | 打开插件管理界面 |
| `:Lazy install` | 安装插件 |
| `:Lazy update` | 更新插件 |
| `:Lazy clean` | 清理未使用插件 |

**填空题**

1. 推荐的 Neovim 插件管理器是 ______。
2. `:Lazy` 命令用于打开 ______ 界面。
3. `:Lazy update` 用于 ______ 所有插件。
4. 插件配置通常写在 ______ 文件中。

**答案**：
1. lazy.nvim
2. 插件管理
3. 更新
4. init.lua

---

### 2.4 常用插件

**知识点详解**

| 插件 | 仓库所有者 | 功能 | 常用命令 |
|---|---|---|---|
| `nvim-tree` | nvim-tree | 文件资源管理树 | `:NvimTreeToggle` |
| `telescope` | nvim-telescope | 模糊查找器 | `:Telescope find_files` |
| `which-key` | folke | 快捷键提示 | 按 `leader` 后等待（==不是 `:WhichKey`==） |
| `nvim-cmp` | hrsh7th | 补全引擎 | 输入时自动弹出 |
| `conform` | stevearc | 代码格式化 | `:ConformInfo` |
| `nvim-treesitter` | nvim-treesitter | 语法解析与增强高亮 | `:TSInstall` |
| `mason` | mason-org | 语言服务器/工具安装器 | `:Mason` |
| `lsp-zero` | VonHeikemen | LSP 一站式封装（==0.11+ 优先用内置 API==） | `:LspZeroSetup` |

**填空题**

1. `nvim-tree` 的切换命令是 ______。
2. `telescope` 的查找文件命令是 ______。
3. `which-key` 用于显示 ______ 提示。
4. `lsp-zero` 提供 ______ 支持。

**答案**：
1. `:NvimTreeToggle`
2. `:Telescope find_files`
3. 快捷键
4. LSP

---

### 2.5 配置文件

**知识点详解**

Neovim 配置文件位于 `~/.config/nvim/init.lua`（推荐）或 `~/.config/nvim/init.vim`。

**基本结构**：

```lua
-- 设置 leader 键
vim.g.mapleader = " "

-- 基本选项
vim.opt.number = true
vim.opt.relativenumber = true
vim.opt.tabstop = 4
vim.opt.shiftwidth = 4
vim.opt.expandtab = true
vim.opt.autoindent = true
vim.opt.wrap = false

-- 插件管理
require("lazy").setup({ ... })
```

> [!tip] leader 键
> `leader` 键是自定义快捷键的前缀，默认是 `\`。推荐设置为空格键，如 `vim.g.mapleader = " "`。

**填空题**

1. Neovim 配置文件通常位于 ______。
2. `vim.g.mapleader = " "` 设置 ______ 键为空格。
3. `vim.opt.number = true` 表示显示 ______。
4. `vim.opt.expandtab = true` 表示将 Tab 转换为 ______。

**答案**：
1. ~/.config/nvim/init.lua
2. leader
3. 行号
4. 空格

---

### 2.6 高效编辑进阶：寄存器、宏、文本对象与跳转

**知识点详解**

| 能力 | 快捷键 | 说明 |
|---|---|---|
| 复制到寄存器 | `"ayy` | 指定寄存器 `a`；不加前缀是「黑洞寄存器」不污染 `0` |
| 粘贴寄存器 | `"ap` | 粘回寄存器 `a` |
| 查看寄存器 | `:reg` / `:registers` | 看所有寄存器内容 |
| 系统剪贴板 | `"+p` / `"*p` | 选中与复制区，依赖 Neovim 内置剪贴板支持 |
| 录制宏 | `q a` … `q` | 以 `a` 录制，停止再按 `q` |
| 执行宏 | `@a` | 播放一次 |
| 重复执行 | `@@` / `100@a` | ==`@@` 重复上一次宏，最省按键== |
| 文本对象 | `diw` / `ci"` / `yap` | ==`d`+`i`+`w`=删内层单词；`c`+`a`+`p`=改段落== |
| 行内跳转 | `f{char}` / `t{char}` / `F` / `T` | 找字符；`;` 跳下一个，`,` 跳上一个 |
| 屏幕行跳转 | `Ctrl+o` / `Ctrl+i` | 跳转列表后退/前进 |
| 跳到行号 | `:{行号}`（如 `:42`） | 配合 `:set number` 更快 |

> [!tip] 文本对象是 Vim 的杀手级设计
> ==光标不必停在目标上==。`dip` 无论光标在段落哪个词上，都能删掉整个段落。常用组合：`diw`（内层词）、`daw`（一个词）、`di"`（引号内）、`ci(`（改括号内）、`yap`（复制段落）、`>ap`（缩进段落）。

**宏的实战流程**（例：给 10 行每行末尾加分号）

```vim
qa          " 开始录制到寄存器 a
A;          " 行尾插入分号
j           " 下移一行
q           " 停止录制
10@a        " 播放 10 次
@@          " 再手动多播放一次
```

**填空题**

1. `"ayy` 的作用是把当前行复制到名为 ______ 的寄存器。
2. 重复执行上一次宏的按键是 ______。
3. `diw` 中 `d` 是动词、`i` 表示 ______（inner/outer）、`w` 表示单词。
4. 宏录制中按 `q` 开始，再按 ______ 停止。

**答案**：
1. a
2. `@@`
3. inner（内层）
4. `q`

---

### 2.7 第二章综合练习

**填空题（本章共 4 道，答案见下方）**

1. `/pattern` 中 `/` 表示 ______ 搜索。
2. `Ctrl+v` 进入 ______ 可视模式。
3. 推荐的 Neovim 插件管理器是 ______。
4. `vim.opt.number = true` 表示显示 ______。

**本章答案**：
1. 向下
2. 块
3. lazy.nvim
4. 行号

**综合项目**：配置个人 Neovim，安装 3 个常用插件（文件树、搜索、主题），并能流畅使用。

> [!tip] 常见陷阱
> 1. **插件冲突**：安装过多插件可能导致 Neovim 启动变慢，建议使用懒加载，只在需要时加载
> 2. **映射冲突**：新增键位可能覆盖已有快捷键，用 `:verbose nvim_keymap <lhs>` 查某个键被谁定义，`:checkhealth` 做整体体检（==`which-key` 并没有 `:WhichKey` 命令，它只做按键提示==）
> 3. **配置错误启动**：语法错误会导致 Neovim 无法启动，始终保留备份 `init.lua.bak`
> 4. **插件版本过旧**：插件频繁更新，可能与 Neovim 版本不兼容，定期检查更新日志

---

## 📖 第三章 高级（Advanced）

### 3.1 Lua 配置

**知识点详解**

Neovim 使用 Lua 作为配置语言，相比 Vimscript 更现代、更强大。

**核心 API**：

| API | 说明 | 示例 |
|---|---|---|
| `vim.g` | 全局变量 | `vim.g.mapleader = " "` |
| `vim.opt` | 选项设置 | `vim.opt.number = true` |
| `vim.keymap.set` | 键位映射 | `vim.keymap.set("n", "<leader>ff", ...)` |
| `vim.cmd` | 执行 Vim 命令 | `vim.cmd("colorscheme desert")` |
| `vim.api` | 底层 API | `vim.api.nvim_create_autocmd(...)` |

**填空题**

1. `vim.g.mapleader = " "` 设置 ______ 键。
2. `vim.opt.number = true` 设置 ______ 选项。
3. `vim.keymap.set` 用于设置 ______。
4. `vim.cmd` 用于执行 ______ 命令。

**答案**：
1. leader
2. 行号
3. 键位映射
4. Vim

---

### 3.2 自定义键位映射

**知识点详解**

```lua
-- 基本语法
vim.keymap.set("n", "<leader>ff", "<cmd>Telescope find_files<cr>", { desc = "Find files" })

-- 参数说明
-- "n" = 正常模式
-- "<leader>ff" = 按键
-- "<cmd>Telescope find_files<cr>" = 执行的命令
-- { desc = "Find files" } = 选项描述
```

**常用映射**：

| 映射 | 功能 |
|---|---|
| `<leader>ff` | 查找文件 |
| `<leader>fg` | 全局搜索 |
| `<leader>e` | 打开文件树 |
| `<leader>w` | 保存文件 |
| `<leader>q` | 退出 |

**填空题**

1. `vim.keymap.set` 的第一个参数 `"n"` 表示 ______ 模式。
2. `<leader>` 默认是 ______ 键。
3. `{ desc = "..." }` 用于设置 ______。
4. `<cmd>...<cr>` 用于在映射中执行 ______。

**答案**：
1. 正常
2. 反斜杠
3. 描述
4. 命令

---

### 3.3 插件开发入门

**知识点详解**

Neovim 插件本质上是一个 Lua 模块。

**插件目录结构**：

```
my-plugin/
├── lua/
│   └── my-plugin/
│       └── init.lua    -- 主入口
├── plugin/
│   └── my-plugin.lua  -- 自动加载
└── README.md
```

**基本插件示例**：

```lua
-- lua/my-plugin/init.lua
local M = {}

function M.setup(opts)
  opts = opts or {}
  -- 初始化逻辑
end

function M.hello()
  print("Hello from my plugin!")
end

return M
```

**填空题**

1. Neovim 插件的主入口文件通常位于 ______。
2. `M.setup(opts)` 是插件的 ______ 函数。
3. `return M` 表示 ______ 模块。
4. 插件目录下的 `plugin/` 文件夹用于 ______ 加载。

**答案**：
1. lua/my-plugin/init.lua
2. 初始化
3. 返回
4. 自动

---

### 3.4 LSP 集成

**知识点详解**

LSP（Language Server Protocol）把「语言智能」标准化：编辑器只管 UI，语言服务器（Language Server）负责分析。==Neovim 0.10 起内置 LSP 客户端，0.11 起内置配置框架==。

> [!danger] 版本差异（最容易踩的坑）
> - **Nvim 0.10 及更早**：用 `require('lspconfig')` + `lspconfig/server.setup({})`
> - **Nvim 0.11+**：官方新增 `vim.lsp.config` / `vim.lsp.enable`，`nvim-lspconfig` 仓库已把框架「上移」到内核，`require'lspconfig'` ==不再是推荐路径==
> - `lsp-zero.nvim` 这类封装插件若走旧 `lspconfig` 接口，在 0.11+ 上会报 `attempt to call field 'enable' (a nil value)`

**方式一：内置 API（0.11+，推荐）**

```lua
-- lsp/lua_ls.lua（放在 runtimepath 的 lsp/ 目录下即可被自动读取）
vim.lsp.config('lua_ls', {
  cmd = { 'lua-language-server' },
  filetypes = { 'lua' },
  root_markers = { '.luarc.json', 'stylua.toml', '.git' },
})

-- init.lua 里启用
vim.lsp.enable('lua_ls')
vim.lsp.enable({ 'pyright', 'ts_ls' })
```

| API | 作用 |
|---|---|
| `vim.lsp.config(name, cfg)` | 定义/覆盖某服务器的默认配置（也可写在 `lsp/<name>.lua`） |
| `vim.lsp.enable(name)` | 启用并按 `filetypes` + `root_markers` 自动 attach |
| `vim.lsp.start(cfg, opts)` | 手动启动一个客户端（不走自动 attach） |
| `:lsp-enable` / `:lsp-stop` / `:lsp-restart` | 运行时开关与重启客户端 |
| `:checkhealth vim.lsp` | ==诊断 LSP 配置的正确命令== |

**方式二：lsp-zero（适合想少写样板代码的人）**

```lua
-- 仓库 VonHeikemen/lsp-zero.nvim（注意不是 WhoIsSethDaniel，那已 404）
local lsp_zero = require('lsp-zero')
lsp_zero.extend_lspconfig({ sign_text = true })
lsp_zero.ensure_installed({ 'lua_ls', 'pyright' })
lsp_zero.setup()
```

**常用 LSP 快捷键（均需自己映射）**

| 快捷键 | 对应 API | 功能 |
|---|---|---|
| `gd` | `vim.lsp.buf.definition()` | 跳转定义 |
| `gD` | `vim.lsp.buf.declaration()` | 跳转声明 |
| `gr` | `vim.lsp.buf.references()` | 查找引用 |
| `gi` | `vim.lsp.buf.implementation()` | 跳转实现 |
| `K` | `vim.lsp.buf.hover()` | 悬浮文档 |
| `<leader>rn` | `vim.lsp.buf.rename()` | 重命名符号 |
| `<leader>ca` | `vim.lsp.buf.code_action()` | 代码操作 |
| `<leader>d` | `vim.diagnostic.open_float()` | 诊断浮窗 |

**填空题**

1. Neovim 从 ______ 版本起内置 LSP 配置框架（`vim.lsp.config` / `vim.lsp.enable`）。
2. `gd` 对应的 API 是 `vim.lsp.buf.______()`。
3. 排查 LSP 是否 attach 成功的命令是 `:checkhealth ______`。
4. 0.10 时代配置 LSP 的旧写法是 `require('______')`。

**答案**：
1. 0.11
2. definition
3. `vim.lsp`
4. lspconfig

---

### 3.5 性能优化

**知识点详解**

| 优化手段 | 说明 |
|---|---|
| 懒加载 | 插件按需加载，减少启动时间 |
| 禁用内置插件 | 关闭不需要的内置插件 |
| 使用 `lazy.nvim` | 自动管理插件加载 |
| 减少自动命令 | 避免过多 `autocmd` |

**禁用内置插件**：

```lua
vim.g.loaded_gzip = 1
vim.g.loaded_zip = 1
vim.g.loaded_tar = 1
vim.g.loaded_netrw = 1
```

**填空题**

1. 懒加载可以 ______ 启动时间。
2. `vim.g.loaded_netrw = 1` 用于禁用 ______ 插件。
3. `lazy.nvim` 可以自动管理插件的 ______。
4. 减少 ______ 可以提升性能。

**答案**：
1. 减少
2. netrw
3. 加载
4. 自动命令

---

### 3.6 第三章综合练习

**填空题（本章共 4 道，答案见下方）**

1. `vim.g.mapleader = " "` 设置 ______ 键。
2. `vim.keymap.set` 的第一个参数 `"n"` 表示 ______ 模式。
3. LSP 的全称是 ______。
4. `gd` 表示跳转到 ______。

**本章答案**：
1. leader
2. 正常
3. Language Server Protocol
4. 定义

**综合项目**：构建个人 Neovim IDE，包含：文件管理、模糊搜索、LSP 补全、自定义快捷键、主题配置，实现日常开发全流程。

> [!tip] 常见陷阱
> 1. **Lua 语法错误**：单个引号与双引号混淆，table 语法错误（缺少逗号或方括号）会导致 Neovim 启动失败，使用 `:lua` 命令测试片段
> 2. **LSP 迟迟不 attach**：多半是 `root_markers` 找不到工作区根目录，或语言服务器没装/不在 PATH。用 `:checkhealth vim.lsp` 看 `Enabled Configurations`，再用 `:LspInfo`（或 `:lsp-info`）看客户端状态，而不是去调某个并不存在的 `timeout_ms` 配置项
> 3. **性能回归**：添加过多自动命令或插件会显著拖慢 Neovim 启动，使用 `:Lazy profile` 分析启动耗时
> 4. **主题显示不对**：现代终端默认就是 24 位真彩色，==不需要去改 `$TERM` 为 `xterm-24bit`==（很多终端根本没有这个 TERM 值，改了反而可能引发异常）。用 `:checkhealth` 看 Neovim 侧识别结果，主题不对通常是 `termguicolors` 没开

---

## 📚 结语与资源

> [!tip] 学习路径建议
> - **零基础**：先完成入门所有练习（约 15h），确保能流畅使用 Neovim 进行基本编辑
> - **有一定经验**：重点突进进阶章节（约 20h），重点掌握插件配置和个人化设置
> - **进阶用户**：挑选高级项目（约 30h），构建属于自己的 Neovim 工作流

> [!warning] 避坑指南
> - **不要**一开始就深入 Lua 配置，务必先掌握基础操作
> - **练习**要多使用快捷键，肌肉记忆是 Vim/Neovim 的核心
> - **备份** `init.lua`/`init.vim`，避免配置错误导致无法启动

> [!note] 关联笔记
> - [[bash-基础语法]] - Shell 基础（`:!` 执行 shell 命令、管道、脚本配合）
> - Lua 暂无独立笔记，用官方速查 [Lua in 15 minutes](https://learnxinyminutes.com/docs/lua/) 顶替

> [!faq] 常见问题
> **Q**：怎么退出 Neovim？
> **A**：按 `Esc` 确保在正常模式，然后输入 `:q`（保存后）或 `:q!`（强制不保存）。
>
> **Q**：怎么安装插件？
> **A**：用 `lazy.nvim`。把 lazy.nvim 自身 clone 到 `~/.local/share/nvim/lazy/lazy.nvim`，在 `init.lua` 里 `require('lazy').setup({...})` 声明插件，然后运行 `:Lazy sync` 安装。详见 [[#2.3 插件管理]]。
>
> **Q**：怎么恢复误删的内容？
> **A**：按 `u` 撤销，或 `Ctrl+r` 重做。
>
> **Q**：如何水平分屏？
> **A**：输入 `:split` 或使用快捷键 `Ctrl+w + s`。

---

## 📦 资源链接

| 资源 | 链接 | 说明 |
|---|---|---|
| **官方文档** | https://neovim.io/doc/user/ | ==一切以官方 help 为准==，`:h help` 可在编辑器内查 |
| **LSP 官方文档** | https://neovim.io/doc/user/lsp/ | 0.11 的 `vim.lsp.config` / `vim.lsp.enable` 用法 |
| **发行版新闻** | https://neovim.io/news/ | 各版本特性变更（迁移前必看） |
| lazy.nvim | https://github.com/folke/lazy.nvim | 插件管理器（本篇采用） |
| telescope.nvim | https://github.com/nvim-telescope/telescope.nvim | 模糊查找 |
| nvim-tree.lua | https://github.com/nvim-tree/nvim-tree.lua | 文件树 |
| which-key.nvim | https://github.com/folke/which-key.nvim | 键位提示 |
| nvim-cmp | https://github.com/hrsh7th/nvim-cmp | 补全引擎 |
| conform.nvim | https://github.com/stevearc/conform.nvim | 代码格式化 |
| nvim-treesitter | https://github.com/nvim-treesitter/nvim-treesitter | 语法解析/高亮 |
| nvim-lspconfig | https://github.com/neovim/nvim-lspconfig | 大量语言服务器预设 |
| mason.nvim | https://github.com/mason-org/mason.nvim | 语言服务器/工具安装器 |
| NvChad | https://github.com/NvChad/NvChad | 完整发行版（对照参考） |
| Lua 速查 | https://learnxinyminutes.com/docs/lua/ | Lua 语法速查 |
| Vim 速查表 | https://vim.rtorr.com/ | 键位/文字对象速查 |

> [!note] 链接说明
> 本篇原有的 3 组「视频推荐」（B 站 / Coursera / Udemy / Egghead）**已全部删除**：实测 `BV1xwVr6FEh4` 是 AI Agent 教程（94 个分P）、`BV1ff4y1X7Ng` 是一首音乐视频、`BV1xxfs1xEBlu` 接口返回 -400（不存在），两个 Coursera 路径返回 404。上表链接均于 2026-09-25 逐条 curl 核验 200。

---

## ⚡ 速查表

| 场景 | 命令 |
|---|---|
| 随时回到正常模式 | `Esc`（卡住了就多按几下） |
| 保存并退出 | `:wq` / 正常模式 `ZZ` |
| 强制不保存退出 | `:q!` / `ZQ` |
| 打开行号 | `:set number` / `:set nonumber` |
| 跳到第 N 行 | `:42` + `Enter` |
| 查某个键被谁占用 | `:verbose nvim_keymap <leader>x` |
| 健康体检 | `:checkhealth` / `:checkhealth vim.lsp` |
| 统计启动耗时 | `nvim --startuptime /tmp/t.log +q` |
| 列出所有映射 | `:nmap` / `:nnoremap` |
| 宏：录 / 播 / 重复 | `qa` … `q` / `@a` / `@@` |
| 复制到指定寄存器 | `"ayy` → `"ap` |
| 换行不缩进 | `:set noautoindent` |
| 查找插件配置默认值 | `:Lazy profile`、`:checkhealth` |

## ❓ 常见问题

> [!faq]- Q：`<leader>` 到底按什么？改了之后配置不生效？
> A：==`vim.g.mapleader` 必须在所有映射定义之前设置==，否则映射仍绑到默认的 `\`。而且 `maplocalleader` 可以按缓冲区单独设。排查：`:verbose nvim_keymap` 看实际绑定到哪个前缀。

> [!faq]- Q：装完 lazy.nvim 提示「不是有效插件」？
> A：八成是路径错了。lazy.nvim 必须在 `stdpath("data")/lazy/lazy.nvim`，不是 `pack/*/start/`。确认 `init.lua` 里 `lazypath` 与 clone 位置一致，然后 `:Lazy sync`。

> [!faq]- Q：配置改坏了，Neovim 起不来怎么办？
> A：==用 `-u NONE` 启动==：`nvim -u NONE`，此时不加载任何配置；改完再正常启动。也可用 `nvim --clean`（0.9+）走隔离模式。

> [!faq]- Q：启动很慢，怎么定位是谁拖慢的？
> A：`nvim --startuptime /tmp/startup.log +q`，然后 `sort -k2 /tmp/startup.log | tail -20` 找最慢项；再用 `:Lazy profile` 看插件加载耗时。先查 `init.lua` 里有没有写文件、装插件、起 LSP 这类同步阻塞操作。

> [!faq]- Q：`conform` 格式化和 LSP 自带格式化冲突吗？
> A：会。两者都绑 `K`/`<leader>f` 一类按键时行为取决于调用顺序。约定俗成的做法是==统一交给 `conform`，在 LSP 的 `on_attach` 里禁用 LSP 的 `textDocument/formatting`==，避免两套格式化器互相打架。

---

*由 Hermes Agent 创建于 2026-09-09 · 更新于 2026-09-25 · 状态：进行中*