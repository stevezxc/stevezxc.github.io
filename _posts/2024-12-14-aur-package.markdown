---
layout: post
title: "如何编写 AUR 软件包"
date: 2024-12-14 14:05:00 +0800
modified_date: now
author: Stevezxc
categories: code
---
第一次维护 AUR 包，记录一些流程和注意事项。

<!--more-->

## 原理

[PKGBUILD](https://wiki.archlinux.org/title/PKGBUILD) 是 Arch Linux 用于描述软件包构建过程的脚本文件。其可以将软件的编译和安装步骤模块化，以便复用与共享。

## 环境准备

安装必要的测试工具：

```bash
sudo pacman -S namcap pacman-contrib
```

### 更新校验码

更改需要下载的源文件后，需更新其校验码：

```bash
updpkgsums PKGBUILD
```

### 测试包生成

检查是否可以正常生成包：

```bash
makepkg -f
```

### 检查格式

对 PKGBUILD 文件和生成的包进行格式和安全检查：

```bash
namcap PKGBUILD
namcap XXX.pkg.tar.zst
```

## 提交到 AUR

### 1. 创建 SSH 密钥

运行以下命令为 AUR 生成新的密钥：

```bash
ssh-keygen -f ~/.ssh/aur
```

然后编辑 `~/.ssh/config` ，添加：

```ssh
Host aur.archlinux.org
  IdentityFile ~/.ssh/aur
  User aur
```

检查公钥：

```bash
cat ~/.ssh/aur.pub
```

### 2. 添加公钥

访问 [AUR](https://aur.archlinux.org/)，在账户设置中添加刚刚生成的 SSH 公钥。

### 3. 初始化 Git 仓库

进入 PKGBUILD 所在目录，初始化仓库：

```bash
git -c init.defaultBranch=master init
git remote add origin ssh://aur@aur.archlinux.org/XXX.git
```

> 其中，`XXX` 是包名。

### 4. 提交包

#### 生成 `.SRCINFO` 文件

在提交之前，运行以下命令生成 `.SRCINFO` 文件：

```bash
makepkg --printsrcinfo > .SRCINFO
```

#### 添加和提交文件

将必要文件添加到 Git 并提交：

```bash
git add PKGBUILD .SRCINFO
git commit -m "Initial commit"
```

> 如果有自定义 patch 或其他依赖文件，也需一并添加。

#### 推送到 AUR

运行以下命令将文件推送到 AUR：

```bash
git push
```
