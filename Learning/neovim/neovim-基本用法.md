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
# [[Neovim-基本用法]]

> [!tip] 学习目标
> 掌握 Neovim 的基本操作模式、常用命令和配置，能够高效编辑文本并进行基本自定义。

---

## 📋 核心概念

| 概念 | 说明 | 快捷键 |
|---|---|---|
| 模式 | 工作模式的集合 | 正常模式、插入模式、可视模式、命令行模式 |
| 正常模式 | 默认模式，用于导航和编辑 | `Esc` 键进入 |
| 插入模式 | 直接编辑文本 | `i`, `a`, `o` 等 |
| 可视模式 | 选中文本进行操作 | `v`, `V`, `Ctrl+v` |

---

## 🚀 基本操作

### 启动和退出

```bash
# 启动 Neovim
nvim

# 打开指定文件
nvim file.txt

# 退出（未修改）
:q

# 退出并保存
:wq

# 强制退出（不保存）
:q!
```

### 光标移动（正常模式）

| 快捷键 | 说明 | 替代命令 |
|---|---|---|
| `h` | 向左移动 | ← |
| `j` | 向下移动 | ↓ |
| `k` | 向上移动 | ↑ |
| `l` | 向右移动 | → |
| `0` | 移动到行首 | |
| `$` | 移动到行尾 | |
| `gg` | 移动到文件开头 | |
| `G` | 移动到文件结尾 | |
| `nG` | 移动到第 n 行 | `:n` |

### 文本编辑

| 快捷键 | 说明 | 示例 |
|---|---|---|
| `i` | 在光标前插入 | |
| `a` | 在光标后插入 | |
| `o` | 在下方新建一行 | |
| `O` | 在上方新建一行 | |
| `x` | 删除光标下的字符 | |
| `dd` | 删除整行 | |
| `yy` | 复制整行 | |
| `p` | 粘贴 | |
| `u` | 撤销 | |
| `Ctrl+r` | 重做 | |

---

## 🛠️ 分割窗口

| 快捷键 | 说明 |
|---|---|
| `:split` | 水平分割窗口 |
| `:vsplit` | 垂直分割窗口 |
| `Ctrl+w + h` | 切换到左侧窗口 |
| `Ctrl+w + j` | 切换到下方窗口 |
| `Ctrl+w + k` | 切换到上方窗口 |
| `Ctrl+w + l` | 切换到右侧窗口 |
| `Ctrl+w + q` | 关闭当前窗口 |

---

## ⚙️ 基本配置（`init.vim` 或 `init.lua`）

### 最小配置示例

```lua
-- Lua 配置 (推荐)
vim.g.mapleader = " "

-- 基本设置
vim.opt.number = true       -- 显示行号
vim.opt.relativenativenumber = true  -- 相对行号
vim.opt.tabstop = 4         -- Tab 显示为 4 个空格
vim.opt.shiftwidth = 4      -- 自动缩进宽度
vim.opt.expandtab = true    -- Tab 转换为空格
vim.opt.autoindent = true   -- 自动缩进
vim.opt.wrap = false        -- 不自动换行
```

### 常见插件

| 插件 | 作用 | 安装 |
|---|---|---|
| `nvim-tree` | 文件资源管理树 | `:NvimTreeToggle` |
| `telescope` | 模糊查找器 | `:Telescope find_files` |
| `lsp-zero` | LSP 支持 | `lsp.setup()` |
| `which-key` | 快捷键提示 | `leader + k` |

### 常用选项

```lua
-- 启用鼠标支持
vim.opt.mouse = "a"

-- 设置颜色主题
vim.cmd("colorscheme desert")

-- 启用折行
vim.opt.wrap = true

-- 设置最短背景
vim.opt.shortmess:append("c")
```

---

## 🔍 搜索和替换

### 搜索

```bash
# 在正常模式下搜索
/npattern    -- 搜索 "pattern"
?pattern     -- 反向搜索

# 高亮所有匹配
:noh         -- 取消高亮
:set hlsearch -- 开启高亮

# 向下/向上搜索
n            -- 下一个匹配
N            -- 上一个匹配
```

### 替换

```bash
# 基本替换
:%s/old/new/g  -- 全局替换 old 为 new

# 确认模式替换
:%s/old/new/gc -- 每次确认

# 替换当前行
:s/old/new/g   -- 当前行替换
```

---

## 📦 插件管理

###使用 packer.nvim

```lua
return require('packer').startup(function()
  -- Packer 可以管理自己
  use 'wbthomason/packer.nvim'

  -- 常用插件
  use 'navaras/onedark.nvim'       -- 主题
  use 'nvim-tree/nvim-tree.lua'    -- 文件树
  use 'nvim-telescope/telescope.nvim' -- 搜索
  use 'hrsh7th/nvim-cmp'           -- 自动补全
end)
```

### 基本安装

```bash
# 安装 Packer
git clone --depth 1 https://github.com/wbthomason/packer.nvim ~/.local/share/nvim/site/pack/packer/start/packer.nvim

# 启动并安装插件
nvim +PackerInstall +qall
```

---

## 💡 常用技巧

| 技巧 | 说明 |
|---|---|
| `:%!sort` | 对整个文件排序 |
| `ggVG:<` | 视觉模式下缩进整个文件 |
| `yiw` | 选中“单词” |
| `va"` | 选中“引号内的内容” |
| `gf` | 打开光标下的文件 |

---

## ⚠️ 常见错误

| 错误 | 解决方法 |
|---|---|
| `E492: Not an editor command: Q` | 退出请用 `:q`，`Q` 是错误命令 |
| `E37: No write since last change` | 先 `:w` 保存，再 `:q` 退出 |
| `cursor shape not available` | 可能需要 `set guicursor` 配置 |
| 插件加载错误 | 确保 Packer 安装无误，重启 Neovim |

---

## 📚 练习项目

| 项目 | 描述 |
|---|---|
| **1. 个人配置文件** | 自定义 `init.lua`，配置常用快捷键和选项 |
| **2. 代码片段库** | 创建自定义代码片段，常用函数/类模板 |
| **3. 文件管理练习** | 使用 `nvim-tree` 完成文件的增删改查 |
| **4. 搜索练习** | 使用 `telescope` 查找文档字符串或配置 |
| **5. 替换练习** | 练习多行替换和正则替换 |

---

## 🔗 相关资源

- `[[Neovim-高级配置]]`
- `[[Vim-键位映射]]`
- `[[Lua-学习路线]]`
- `[[IDE-对比]]`

---

## ❓ 常见问题

> [!question] Q：怎么退出 Neovim？
> **A**：按 `Esc` 确保在正常模式，然后输入 `:q`（保存后）或 `:q!`（强制不保存）。

> [!question] Q：怎么安装插件？
> **A**：使用插件管理器 `packer.nvim`：`git clone` 对应仓库到 `~/.local/share/nvim/site/pack/packer/start/`，然后启动 Neovim 运行 `:PackerInstall`。

> [!question] Q：怎么恢复误删的内容？
> **A**：按 `u` 撤销，或 `Ctrl+r` 重做。

> [!question] Q：如何水平分屏？
> **A**：输入 `:split` 或使用快捷键 `Ctrl+w + s`。

---

> [!faq] 常见问题汇总
> **Q**：光标怎么变成竖线？
> **A**：这是正常的 Neovim 光标形状，可以通过 `set guicursor` 自定义。
>
> **Q**：Tab 键为什么不动？
> **A**：检查是否开启了 `expandtab`，或冲突的插件快捷键。
>
> **Q**：保存后为什么改动仍然可以撤销？
> **A**：Neovim 默认开启持久撤销，需要配置 `undofile`。

---

*由 [[Hermes Agent]] 创建于 2026-09-09 · 状态：进行中*