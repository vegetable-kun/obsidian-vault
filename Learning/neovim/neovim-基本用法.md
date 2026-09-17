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

## 🎯 难度分段学习

| 难度 | 目标人群 | 学习建议 | 预估时长 |
|---|---|---|---|
| **入门** | 完全零基础、初次接触 Vim/Neovim | 重点掌握基本操作模式、光标移动、文本编辑，完成 5 个练习题 | 15h |
| **进阶** | 有基础需求提高效率 | 重点掌握分割窗口、搜索替换、插件配置，自定义个人配置 | 20h |
| **高级** | 需要进行深度自定义开发 | 重点掌握 Lua 配置、插件开发、性能优化，构建完整 IDE | 30h |

---

### 入门（Beginner）

| 知识点 | 具体内容 | 练习 |
|---|---|---|
| 启动和退出 | `nvim`、`:q`、`:wq`、`:q!` | 练习 1：启动退出练习 |
| 光标移动 | `h`, `j`, `k`, `l`、`0`, `$`, `gg`, `G` | 练习 2：移动练习 |
| 文本编辑 | `i`, `a`, `o`, `x`, `dd`, `yy`, `p`, `u` | 练习 3：编辑练习 |
| 分割窗口 | `:split`、`:vsplit`、`Ctrl+w + hjkl` | 练习 4：分割窗口练习 |
| 搜索 | `/pattern`、`n`, `N`、`:noh` | 练习 5：搜索练习 |
| 基本配置 | `vim.opt.number`、`vim.opt.tabstop` | 练习 6：配置练习 |

**入门项目**：完成 Neovim 启动、退出、基本编辑的全流程练习，不看帮助文档。

---

### 进阶（Intermediate）

| 知识点 | 具体内容 | 练习 |
|---|---|---|
| 替换 | `:s/old/new/g`、`:%s/old/new/gc` | 练习 7：替换练习 |
| 可视模式 | `v`, `V`, `Ctrl+v`、`<`, `>` | 练习 8：可视模式练习 |
| 插件管理 | `packer.nvim` 安装卸载 | 练习 9：插件安装 |
| 常用插件 | `nvim-tree` (`:NvimTreeToggle`)、`telescope` (`:Telescope find_files`) | 练习 10：插件使用 |
| 配置文件 | `init.lua` 基本结构、`leader` 键 | 练习 11：配置文件搭建 |
| 常用选项 | `number`、`relativenumber`、`wrap` | 练习 12：选项配置 |

**进阶项目**：配置个人 Neovim，安装 3 个常用插件（文件树、搜索、主题），并能流畅使用。

---

### 高级（Advanced）

| 知识点 | 具体内容 | 练习 |
|---|---|---|
| Lua 配置 | `vim.g`、`vim.opt`、`mapleader`、`maplocalleader` | 练习 13：Lua 配置 |
| 自定义映射 | `vim.keymap.set`、`nmap`、`vmap` | 练习 14：映射配置 |
| 插件开发 | 插件目录结构、`lazy.nvim` 或 `packer.nvim` | 练习 15：开发小插件 |
| 性能优化 | 懒加载、命令缓存 | 练习 16：性能分析 |
| 颜色主题 | `colorscheme`、`vim.cmd` | 练习 17：主题配置 |
| LSP 支持 | `lsp-zero`、`mason` | 练习 18：LSP 配置 |

**高级项目**：构建个人 Neovim IDE，包含：文件管理、模糊搜索、LSP 补全、自定义快捷键、主题配置，实现日常开发全流程。

---

> [!tip] 学习路径建议
> - **零基础**：先完成入门所有练习（约 15h），确保能流畅使用 Neovim 进行基本编辑
> - **有一定经验**：重点突进进阶章节（约 20h），重点掌握插件配置和个人化设置
> - **进阶用户**：挑选高级项目（约 30h），构建属于自己的 Neovim 工作流

> [!warning] 避坑指南
> - **不要**一开始就深入 Lua 配置，务必先掌握基础操作
> - **练习**要多使用快捷键，肌肉记忆是 Vim/Neovim 的核心
> - **备份** `init.lua`/`init.vim`，避免配置错误导致无法启动

---

## 📚 进阶资源

| 资源 | 链接 | 说明 |
|---|---|---|
| [[Neovim 高级配置]] | https://github.com/NvChad/NvChad | 完整 Neovim 发行版 |
| [[Lua 学习路线]] | https://learnxinyminutes.com/docs/lua/ | Lua 语法速查 |
| [[Vim 文字对象]] | https://vim.rtorr.com/ | 文字对象速查 |
| [[Telescope 文档]] | https://github.com/nvim-telescope/telescope.nvim | 搜索插件文档 |

---

> [!note] 关联笔记
> - `[[Bash-基础语法]]` - Bash 基础语法
> - `[[Lua-学习路线]]` - Lua 语言学习

*由 [[Hermes Agent]] 创建于 2026-09-09 · 更新于 2026-09-17 · 状态：进行中*