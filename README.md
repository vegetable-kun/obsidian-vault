# Obsidian Vault

这是 Hermes Agent 的 Obsidian Vault 文件夹。

## 目录结构

```
ObsidianVault/
├── Projects/    # 项目笔记
├── Learning/    # 学习笔记
├── Memory/      # 记忆归档（含 MEMORY.md / USER.md 符号链接）
└── Archive/     # 归档
```

## 与 Hermes 的集成

- **Hermes Skill**：通过 `OBSIDIAN_VAULT_PATH` 环境变量读写此 vault
- **MEMORY.md / USER.md**：符号链接，Hermes 运行时记忆与此同步
- **continuity**：Hermes cron 任务的输出会带入下一次运行

## 本地使用

1. 将此文件夹作为 Obsidian vault 打开
2. 或 git clone 到本地，用 Obsidian 打开
