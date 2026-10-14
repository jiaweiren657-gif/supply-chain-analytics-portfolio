# 环境搭建指南（四件套）

> 目标：装好数据分析工作环境。**预计 1.5–2 小时**，建议分两次做：前三个 40 分钟，MySQL 单独留 40 分钟。
> 推荐顺序：**Miniconda → PyCharm → Power BI → MySQL**（前三个快，MySQL 最折腾放最后）

---

## 总览

| # | 工具 | 作用 | 官方地址 | 耗时 |
|---|---|---|---|---|
| 1 | **Miniconda** | Python 环境管家 | https://repo.anaconda.com/miniconda/ | 10 min |
| 2 | **PyCharm** | 写代码的 IDE | https://www.jetbrains.com/pycharm/download/ | 15 min |
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
| Advanced Options | 勾选 **Register Miniconda3 as my default Python** | 让 PyCharm 等 IDE 能自动找到 Python |
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

## 2. PyCharm（写代码的 IDE）

> **先确认一件事**：你的 PyCharm 是 Community 还是 Professional？
> 打开 PyCharm → 菜单 **Help → About**，看标题里有没有 "Professional" 字样。

### 两个版本的差别（重点：学生可以免费拿 Pro）

| 功能 | Community（免费） | Professional（学生免费） |
|---|---|---|
| 写 Python / pandas 脚本 | ✅ | ✅ |
| **Database 工具**（在 IDE 里直接连 MySQL 写 SQL） | ❌ | ✅ |
| Jupyter 完整支持 / 科学模式 | 有限 | ✅ |
| Web 框架、远程开发 | ❌ | ✅ |

**Community 完全够用**——练 SQL 用 MySQL Workbench（第 4 步会装）也一样。
**但 Professional 对学生免费，没理由不拿。**

### 学生免费申请（建议花 10 分钟做掉）

**新申请入口**（注意：续期入口不同）：

```
https://www.jetbrains.com/shop/eform/students
```

表单里选一种申请方式：

| 方式 | 需要什么 | 时效 |
|---|---|---|
| **大学电子邮件地址** | 学校域名邮箱（若在 JetBrains 数据库内） | 秒过 |
| **官方文件** | 中国大陆学生须提供**学信网学籍验证报告**（PDF 版，含有效验证码）；学生证 / 在读证明可作辅助 | **1–2 周** |
| **GITHUB** | 走 GitHub Student Developer Pack 渠道 | 视 GitHub 审批 |
| ISIC / ITIC | 国际学生证 | 较快 |

**建议顺序**：先试学校邮箱（最快）→ 不行就下载学信网报告走"官方文件"，等 1–2 周。
**等待期间先用 Community 版，完全不耽误学习。**

申请通过后：收到授权邮件 → 注册或绑定 [JetBrains Account](https://account.jetbrains.com.cn/login) → 在 PyCharm 里用该账号登录激活。

### 下载安装

```
https://www.jetbrains.com/pycharm/download/
```

页面分 Community / Professional 两栏，按你的授权情况下载。安装时建议勾选：

- ✅ Create Desktop Shortcut（桌面快捷方式）
- ✅ Update PATH Variable（更新环境变量）
- ✅ .py 文件关联

### 关键配置：让 PyCharm 用上 Miniconda 的环境（必做）

**这一步不做，你在 Miniconda 里装的 pandas，PyCharm 根本找不到。**

1. 打开 PyCharm → **New Project**
2. **Location** 选工作目录，例如 `E:\code\sc-practice`
3. 展开 **Python Interpreter** → 选 **Add Interpreter → Add Local Interpreter**
4. 左侧选 **Conda**
5. **Conda executable** 填：
   ```
   C:\Users\36356\miniconda3\Scripts\conda.exe
   ```
   （装到别的路径就换成对应路径）
6. 勾选 **Use existing environment** → 下拉选 **sc**
7. 点 **OK → Create**

> 第 6 步下拉里看不到 `sc`，说明还没创建环境。先回 Anaconda Prompt 执行：
> ```
> conda create -n sc python=3.12 -y
> ```

### 验证

在 PyCharm 里新建 `test.py`：

```python
import pandas as pd
print("pandas 版本:", pd.__version__)
```

右键 → **Run 'test'**。下方控制台显示 `pandas 版本: 2.x.x` = 成功。

> 如果报 `ModuleNotFoundError: No module named 'pandas'` → **解释器选错了**（选到 base 或系统 Python 了），回上面第 3–6 步重选 `sc` 环境。

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
- [ ] **PyCharm**：解释器指向 `sc` 环境，运行 `import pandas` 不报错
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
| PyCharm 报 `No module named 'pandas'` | 解释器选错（选到 base 或系统 Python） | 重选 `sc` 环境（见第 2 节配置步骤） |

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
