---
title: Bash 基础语法
date: 2026-09-09
tags:
  - bash
  - learning
  - shell
aliases:
  - Bash Syntax
  - Shell 基础
cssclasses:
  - learning
---
# [[Bash-基础语法]]

> [!tip] 学习目标
> 掌握 Bash 的基本语法，包括变量、循环、函数和常用命令，能够编写简单的脚本自动化任务。

---

## 📋 基本概念

| 概念 | 说明 | 示例 |
|---|---|---|
| Shell | 解释型命令语言 | `bash`, `zsh`, `sh` |
| 变量 | 存储数据 | `name="Hello"` |
| 参数 | 传递给脚本 | `$1`, `$2` |
| 循环 | 重复执行 | `for`, `while` |
| 函数 | 封装代码 | `func() { ... }` |

---

## 🔤 变量

### 定义变量

```bash
# 简单赋值
name="Hello World"
age=18

# 只读变量
readonly PI=3.14

# 删除变量
unset name
```

### 使用变量

```bash
# 基本引用
echo "姓名: $name"
echo "年龄: $age"

# 参数引用（脚本时使用）
echo "第一个参数: $1"
echo "第二个参数: $2"
```

### 字符串操作

```bash
# 长度
echo ${#name}  # 输出: 11

# 子字符串
echo ${name:0:3}  # 输出: Hel

# 大小写转换
echo ${name^}   # 首字母大写
echo ${name,}   # 首字母小写
```

---

## 🔄 条件判断

```bash
# 数值比较
if [ $a -eq $b ]; then
    echo "a 等于 b"
fi

# 字符串比较
if [ "$str" = "hello" ]; then
    echo "字符串相等"
fi

# 文件测试
if [ -f "file.txt" ]; then
    echo "文件存在"
fi

if [ -d "dir" ]; then
    echo "目录存在"
fi

if [ -x "script.sh" ]; then
    echo "可执行"
fi
```

---

## 🔧 循环结构

### for 循环

```bash
# 遍历列表
for i in 1 2 3 4 5; do
    echo "数字: $i"
done

# 遍历文件
for file in *.txt; do
    echo "处理: $file"
done
```

### while 循环

```bash
count=1
while [ $count -le 5 ]; do
    echo "计数: $count"
    ((count++))
done
```

### until 循环

```bash
count=1
until [ $count -gt 5 ]; do
    echo "计数: $count"
    ((count++))
done
```

---

## 🚀 函数

### 定义函数

```bash
# 基本定义
hello() {
    echo "Hello, World!"
}

# 带参数
 greet() {
    echo "你好, $1!"
}

# 返回值
return_value() {
    return 42
}

# 调用
hello
greet "Alice"
result=$?
echo "返回值: $result"
```

### 函数示例

```bash
# 计算两数之和
add() {
    local sum=$(( $1 + $2 ))
    echo $sum
}

result=$(add 5 3)
echo "5 + 3 = $result"  # 输出: 5 + 3 = 8
```

---

## 📁 常用命令速查

| 分类 | 命令 | 说明 | 示例 |
|---|---|---|---|
| 文件管理 | `ls` | 列出文件 | `ls -l` |
| | `cd` | 切换目录 | `cd /home` |
| | `mkdir` | 创建目录 | `mkdir new_dir` |
| | `rm` | 删除文件 | `rm file.txt` |
| | `cp` | 复制文件 | `cp src dst` |
| | `mv` | 移动/重命名 | `mv old new` |
| 权限 | `chmod` | 修改权限 | `chmod +x script.sh` |
| | `chown` | 修改所有者 | `chown user:group file` |
| 查看 | `cat` | 查看文件内容 | `cat file.txt` |
| | `head` | 查看开头 | `head -n 5 file.txt` |
| | `tail` | 查看结尾 | `tail -n 5 file.txt` |
| 搜索 | `grep` | 搜索文本 | `grep "pattern" file.txt` |
| 权限切换 | `sudo` | 管理员权限 | `sudo apt install` |

---

## 💡 常见陷阱

| 陷阱 | 后果 | 解决方法 |
|---|---|---|
| 引号不匹配 | 语法错误 | 始终成对使用引号 |
| 空格问题 | 命令失败 | 注意引用 `"$var"` |
| 未引用变量 | 单词分割 | 始终引用变量 |
| 权限不足 | 执行失败 | 使用 `chmod +x` 或 `sudo` |

---

## 📚 练习题

| 练习 | 描述 |
|---|---|
| **1. 问候脚本** | 编写脚本接受姓名参数，输出 personalized greeting |
| **2. 文件计数** | 编写脚本计算当前目录下 `.txt` 文件的数量 |
| **3. even/odd 检查** | 编写脚本接受数字参数，判断是否为偶数 |
| **4. 简单计算器** | 编写脚本接受两个参数并输出加法结果 |
| **5. 循环计数** | 编写循环打印 1-10 的平方 |

---

## 🔗 相关资源

- `[[Bash-高级脚本编程]]`
- `[[Shell-调试技巧]]`
- `[[Linux-常用命令]]`
- `[[Python-替代方案]]`（复杂逻辑可考虑 Python）

---

> [!faq] 常见问题
> **Q**：变量为什么打印不出来？
> **A**：可能未引用或未导出。尝试 `echo "$VAR"` 或 `export VAR`。
>
> **Q**：循环为什么运行不结束？
> **A**：检查条件表达式是否正确，确保能够到达终止条件。
>
> **Q**：权限 denied 怎么办？
> **A**：使用 `chmod +x` 添加执行权限，或使用 `sudo`。

---

*由 [[Hermes Agent]] 创建于 2026-09-09 · 状态：进行中*