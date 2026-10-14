# 环境搭建指南（四件套）

> 目标：装好数据分析工作环境。**预计 1.5–2 小时**，建议分两次做：前三个 40 分钟，MySQL 单独留 40 分钟。
> 推荐顺序：**Miniconda → VS Code → Power BI → MySQL**（前三个快，MySQL 最折腾放最后）

---

## 总览

| # | 工具 | 作用 | 官方地址 | 耗时 |
|---|---|---|---|---|
| 1 | **Miniconda** | Python 环境管家 | https://repo.anaconda.com/miniconda/ | 10 min |
| 2 | **VS Code** | 写代码的编辑器 | https://code.visualstudio.com/ | 10 min |
| 3 | **Power BI Desktop** | 做仪表板（免费） | https://aka.ms/pbidesktopstore | 15 min |
| 4 | **MySQL 8** | 数据库（练 SQL） | https://dev.mysql.com/downloads/installer/ | 40 min |

---

## 1. Miniconda（Python 环境）

**为什么用 Miniconda 而不是 Anaconda**：Miniconda 只有约 100MB，Anaconda 有 3GB 且下载慢。我们只需要 pandas 这些核心库，用 Miniconda 手动装更干净。

### 下载

**方式 A（推荐，直接下载）**：浏览器打开这个链接就会开始下载

```
https://repo.anaconda.com/miniconda/Miniconda3-latest-Windows-x86_64.exe
```

**方式 B（找历史版本）**：打开 https://repo.anaconda.com/miniconda/ ，找文件名形如
`Miniconda3-latest-Windows-x86_64.exe` 的那个（`latest` 就是最新版）。

> **下载慢的话**：可以用清华镜像 https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/ ，在里面找对应的 `.exe`。

### 安装（关键选项）

双击安装包，按下面选：

| 安装步骤 | 选什么 | 说明 |
|---|---|---|
| Install for | **Just Me (recommended)** | 只给当前用户装，不需要管理员权限 |
| Destination Folder | 默认即可 | ⚠️ **路径不能有空格或中文**。你的路径是 `C:\Users\36356\miniconda3`，没问题。如果想装到 E 盘，填 `E:\miniconda3` |
| Advanced Options | 勾选 **Register Miniconda3 as my default Python** | 让 VS Code 能自动找到 Python |
| Advanced Options | **取消勾选 "Add Miniconda3 to my PATH"** | 官方不建议勾（会让系统里出现一堆 Python 命令，容易冲突） |
| Advanced Options | 勾选 **Clear the package cache upon completion** | 省空间 |

点 Install → 等 3-5 分钟 → Finish。

### 验证

开始菜单搜索 **Anaconda Prompt**，打开后输入：

```bash
conda --version
python --version
```

- ✅ 显示 `conda 2x.x.x` 和 `Python 3.1x.x` = 成功
- ❌ 提示"不是内部或外部命令" = 开始菜单找错了，要用 **Anaconda Prompt** 而不是普通的 cmd

### 配国内镜像源（必做！否则装包极慢）

在 Anaconda Prompt 里执行：

```bash
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```

验证：`pip config list` 应该显示上面那个地址。

> 这一步不做，后面 `pip install pandas` 可能要等 10 分钟甚至超时。

---

## 2. VS Code（编辑器）

### 下载

```
https://code.visualstudio.com/
```

打开后点页面上大大的 **Download for Windows**（会自动识别你的系统）。

### 安装

一路默认即可，但**建议勾选这几项**：

- ✅ 将"通过 Code 打开"操作添加到 Windows 资源管理器文件上下文菜单
- ✅ 将"通过 Code 打开"操作添加到 Windows 资源管理器目录上下文菜单
- ✅ 添加到 PATH

### 装必备扩展（打开 VS Code 后）

左侧图标栏点最下面那个方块图标（Extensions），搜索并安装：

| 扩展名 | 作用 |
|---|---|
| **Python**（Microsoft 出品） | Python 支持，必装 |
| **Jupyter**（Microsoft 出品） | 跑 `.ipynb` 笔记本，必装 |
| **Chinese (Simplified) Language Pack** | 界面汉化，可选 |

### 验证

新建一个文件 `test.py`，写：

```python
print("hello")
```

按 `Ctrl+F5` 运行，下方终端出现 `hello` = 成功。
右下角状态栏应该显示 Python 解释器（会带 `miniconda3` 字样）。

---

## 3. Power BI Desktop（BI 工具）

**免费**，Windows 专用。

### 下载（两种方式）

**方式 A（推荐）：微软商店**
```
https://aka.ms/pbidesktopstore
```
打开后点 **安装**。

优点：**自动更新**、**不需要管理员权限**、下载体积小。

**方式 B：官网直接下载 exe**
```
https://www.microsoft.com/download/details.aspx?id=58494
```
选 **64-bit** 版本（32 位已停止支持）。

> ⚠️ 两种方式**不要同时装**，会出现冲突。选一种就好。

### 安装

- 方式 A（商店）：点安装后自动完成
- 方式 B（exe）：双击 → 一路 Next → Install

### 验证

打开 Power BI Desktop → 看到欢迎界面 → 点左上 **文件 → 帮助 → 关于**，确认版本号。

### 系统要求（对照一下）

- Windows 10 或更高
- 内存 2GB 以上（建议 4GB+）
- 屏幕分辨率 **至少 1440×900**（低于这个有些对话框会显示不全 ← 笔记本常见坑）
- 如果显示异常：Windows 设置 → 系统 → 显示 → 缩放改回 **100%**

---

## 4. MySQL 8（数据库）

**这一步最折腾，留足时间。**

### 下载

```
https://dev.mysql.com/downloads/installer/
```

页面上有两个版本：

| 版本 | 大小 | 建议 |
|---|---|---|
| **mysql-installer-community-8.x.x.x.msi**（offline） | 约 400MB | ✅ **选这个**，一次下完 |
| mysql-installer-web-community（web） | 约 2MB | 边装边下，网络不稳会失败 |

点 **Download** → 下一页拉到最下面点 **No thanks, just start my download**（不用注册账号）。

### 安装（关键步骤）

1. 双击运行 → 选 **Custom**（自定义安装）
2. 左侧展开 **MySQL Servers → MySQL Server → MySQL Server 8.x** → 点箭头加到右边
3. 左侧 **Applications → MySQL Workbench → MySQL Workbench 8.x** → 加到右边（这是图形界面，必装）
4. 点 **Next → Execute** → 等安装完成

### 配置（最重要的一段，别跳过）

安装完成后进入配置向导：

| 配置项 | 选什么 | 说明 |
|---|---|---|
| Type and Networking | **Development Computer**，TCP/IP，端口 **3306** | 默认即可，别改端口 |
| Authentication Method | **Use Strong Password Encryption** | 默认选项，配合 Python 没问题 |
| **Root Password** | 设一个强密码并**记下来！** | ⚠️ 后面 Python 连数据库、Workbench 登录都要用。**建议记到手机备忘录或密码管理器** |
| Windows Service | 服务名 **MySQL80**，勾选 **Start the MySQL Server at System Startup** | 开机自启，省事 |
| Apply Configuration | 点 **Execute** | 等全部打绿勾 |

> **root 密码忘了怎么办**：很麻烦，需要重装。所以**现在就记下来**。

### 验证

开始菜单打开 **MySQL Workbench**：

1. 首页有个 `Local instance MySQL80` 的方块 → 点它
2. 输入 root 密码 → 登录
3. 在查询窗口执行：

```sql
SELECT VERSION();
```

- ✅ 返回类似 `8.0.xx` = 成功
- ❌ 报错 `Can't connect to MySQL server` = 服务没启动，去 Windows「服务」里找 MySQL80 手动启动

---

## 全部完成后的验收清单

四项全部打过勾，就算「环境搭建」完成：

- [ ] **Miniconda**：Anaconda Prompt 里 `conda --version` 有输出
- [ ] **pip 换源**：`pip config list` 显示清华源地址
- [ ] **VS Code**：能新建 .py 文件并运行出结果
- [ ] **Power BI**：能打开，About 里能看到版本号
- [ ] **MySQL**：Workbench 能连接并执行 `SELECT VERSION();`

---

## 常见问题

| 问题 | 原因 | 解决 |
|---|---|---|
| `conda` 不是内部或外部命令 | 用了普通 cmd 而不是 Anaconda Prompt | 开始菜单搜 **Anaconda Prompt** |
| `pip install` 卡住/超时 | 没换国内源 | 执行上面第 1 节的 `pip config set` |
| Miniconda 安装失败/路径报错 | 路径含空格或中文 | 装到 `C:\miniconda3` 或 `E:\miniconda3` |
| Power BI 界面显示不全 | 屏幕缩放不是 100% | 设置 → 系统 → 显示 → 缩放改 100% |
| MySQL 装完连不上 | 服务未启动 | Windows 服务里启动 `MySQL80` |
| MySQL 忘记 root 密码 | —— | 需重装，所以**现在就记下来** |
| VS Code 找不到 Python | 解释器没选 | 右下角点解释器 → 选带 `miniconda3` 的那个 |

---

## 装完之后的第一个动作

打开 **Anaconda Prompt**，创建一个专门给本项目用的环境（不要污染 base）：

```bash
conda create -n sc python=3.12 -y
conda activate sc
pip install pandas numpy matplotlib seaborn jupyter
```

以后每次开始工作前，先 `conda activate sc` 再运行代码。

> 环境名 `sc` = supply chain，简短好记。
