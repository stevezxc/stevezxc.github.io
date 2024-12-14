---
layout: post
title: "在 Surface Go 2 上配置 Archlinux"
date: 2024-12-11 00:16:00 +0800
categories: technology
---

# 在 Surface Go 2 上配置 Archlinux

## 安全启动

Go 2 的安全启动似乎只支持微软签名证书的操作系统。所以每次启动时都会显示丑陋的红色警告。

---

## 软件配置

### 桌面环境

经过亲身体验，目前有触控需求的桌面还是只能选择 Gnome：

- X11 不支持多点触控，只有 Gnome 和 KDE 对 Wayland 支持较完善。
- kwin 加载输入法时将其识别为 virtual keyboard，导致屏幕键盘无法使用。
- Gnome 的 UI 和交互逻辑更符合触控思维。

---

### 摄像头

```bash
sudo pacman -S libcamera gst-plugin-libcamera
sudo usermod -aG video $USER
newgrp video
```

`gst-plugin-libcamera` 可使基于 GStreamer 的软件支持 libcamera。

重启后，前后摄像头一般都可正常工作。可通过 Cheese 进行测试。

---

### 笔记

**Xournal++** 目前体验最好：

- 支持打开大型文档。
- 高度自定义的功能。

---

### 续航优化

```bash
sudo pacman -S tlp
sudo systemctl enable tlp.service
```

默认配置后即可实现一天的续航。

---