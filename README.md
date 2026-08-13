<div align="center">

# CY-AI 音乐助手

### 基于 DeepSeek + 妙响的全自动 AI 音乐创作流水线

[![Python](https://img.shields.io/badge/Python-3.11+-3776AB?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)
[![PySide6](https://img.shields.io/badge/PySide6-6.6+-41CD52?style=flat-square&logo=qt&logoColor=white)](https://www.qt.io/)
[![Playwright](https://img.shields.io/badge/Playwright-1.40+-2EAD33?style=flat-square&logo=playwright&logoColor=white)](https://playwright.dev/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.115-009688?style=flat-square&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![Platform](https://img.shields.io/badge/平台-Windows-0078D6?style=flat-square&logo=windows&logoColor=white)](https://github.com/2181533/cy-ai-music-assistant)
[![License](https://img.shields.io/badge/License-Proprietary-red?style=flat-square)](./LICENSE)
[![Version](https://img.shields.io/badge/版本-26.08.31-00D4FF?style=flat-square)](https://github.com/2181533/cy-ai-music-assistant/releases)
[![DeepSeek](https://img.shields.io/badge/AI-DeepSeek-4D6BFE?style=flat-square&logo=deepseek&logoColor=white)](https://www.deepseek.com/)
[![SQLite](https://img.shields.io/badge/数据库-SQLite-003B57?style=flat-square&logo=sqlite&logoColor=white)](https://www.sqlite.org/)

**多账号轮换 · 64 种歌词风格 · 2 槽并发生成 · 全自动签约发布 · 代理白标体系**

[功能特性](#-核心功能) · [技术架构](#-技术架构) · [快速开始](#-快速开始) · [项目结构](#-项目结构) · [功能详解](#-功能详解) · [路线图](#-路线图)

</div>

---

## 项目简介

**CY-AI 音乐助手**是一款面向抖音音乐生态的桌面端自动化创作平台，整合了 **DeepSeek 大模型歌词生成** 与 **妙响（抖音音乐创作实验室）AI 作曲** 两大引擎，构建从「灵感种子 → 歌词创作 → 作曲生成 → 自动签约 → 多平台发布 → 数据统计」的完整闭环流水线。

项目采用 **客户端 + 服务端** 分离架构，客户端基于 PySide6 构建赛博朋克风格桌面应用，服务端基于 FastAPI 提供授权验证、代理管理、支付订单、内容运营等后台能力。

> 本项目仅供个人学习研究使用，禁止用于商业用途。使用本工具产生的所有内容与账号风险由使用者自行承担。

---

## 核心功能

### 创作引擎

| 功能模块 | 描述 | 技术实现 |
|---------|------|---------|
| AI 歌词生成 | 接入 DeepSeek 网页版 API，支持深度思考 + 联网搜索双模式 | httpx SSE 流式 + 逆向工程 |
| 64 种歌词风格 | 覆盖流行/民谣/摇滚/电子/古风/说唱等 8 大类 64 子类 | 结构化风格锚点配置 |
| 1300+ 组合维度 | 65 主题 × 20 手法 × 25 意象，确保每首独一无二 | 多维度随机组合算法 |
| 风格提示词 | 遵循 Suno AI 公式（流派+节奏+调性+乐器+人声+情绪） | 自动生成 1000 字以内 |
| 歌名智能提取 | 从思考过程与最终内容双重提取，100% 获取率 | 多引号类型 + 截断恢复 |
| AI 作曲生成 | 妙响 Sway v5.x 引擎，2 槽并行提交 | Playwright 自动化 |
| 同词异曲 | 每首歌词生成 2 首不同作曲版本 | 并发任务调度 |

### 账号与流水线

| 功能模块 | 描述 |
|---------|------|
| 多账号管理 | Cookie 持久化、扫码登录、绑定组聚类（主账号 + 子账号同色标识） |
| 自动签约 | 全自动签约流程，验证码弹窗输入，失败自动重试（最多 3 次） |
| 2 槽并发生成 | 每账号同时 2 个生成槽位，自动轮转直到额度耗尽 |
| 流水线引擎 | 歌词 → 歌曲 → 改名 → 发布 → 统计，阶段可勾选 |
| 账号独立协程 | 每个账号独立协程执行流水线，账号间并行互不等待 |
| 离线检测 | 启动前异步检查，离线自动登录，失败弹窗提醒 |
| 反风控 | 人类行为模拟、随机延迟、当日额度安全阈值（80%） |

### 发布与数据

| 功能模块 | 描述 |
|---------|------|
| 多平台发布 | 支持汽水音乐、抖音双平台，四种发布方式可选 |
| 发布配额预警 | 75 首预警 / 78 首高级预警 / 80 首硬上限 |
| 数据中心 | 多平台数据统计，热度/使用量/播放量分组展示 |
| 实时进度 | 批量生成每 2 秒刷新，思考阶段显示字数，重试显示次数 |

### 商业化体系

| 功能模块 | 描述 |
|---------|------|
| License 授权 | 服务端验证、机器码绑定、24h 缓存、7 天离线宽限 |
| 代理白标 | exe 末尾写入 agent_code，启动自动加载品牌配置 |
| 防挖客机制 | 服务端基于 machine_id 判断，防止代理互相挖客 |
| 独立卖价体系 | 代理售价、原价、批发基准价独立存储，与主卖价解耦 |
| 卡密系统 | 代理扣费基于批发基准价，支持月卡/季卡/年卡 |
| 支付集成 | 微信支付 + 支付宝双通道，证书签名验证 |

---

## 技术架构

### 整体架构

```
┌─────────────────────────────────────────────────────────────┐
│                     客户端（PySide6 桌面应用）                │
├─────────────────────────────────────────────────────────────┤
│  UI 层    │  主题系统 │ 创作中心 │ 数据中心 │ 代理面板 │ 关于 │
├───────────┼──────────────────────────────────────────────────┤
│  核心层   │  账号管理 │ 歌词引擎 │ 生成引擎 │ 签约引擎 │ 发布 │
│           │  流水线调度 │ 风控模块 │ DeepSeek API │ 妙响 API │
├───────────┼──────────────────────────────────────────────────┤
│  数据层   │  SQLite (aiosqlite) │ Cookie 持久化 │ 用户设置 │
├───────────┼──────────────────────────────────────────────────┤
│  安全层   │  机器码绑定 │ 动态密钥 │ 请求签名 │ 防破解 │ 自动更新 │
└─────────────────────────────────────────────────────────────┘
                              │ HTTPS + 签名验证
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                    服务端（FastAPI + Uvicorn）                │
├─────────────────────────────────────────────────────────────┤
│  授权 API │ 代理 API │ 支付 API │ 更新 API │ 公告 API │ 反馈  │
├─────────────────────────────────────────────────────────────┤
│  a_bogus 签名服务 │ 限流中间件 │ 审计日志 │ 密钥轮换 │ TOTP  │
├─────────────────────────────────────────────────────────────┤
│  SQLite │ Jinja2 模板 │ 微信支付证书 │ 支付宝证书 │ 落地页 │
└─────────────────────────────────────────────────────────────┘
                              │
            ┌─────────────────┼─────────────────┐
            ▼                 ▼                 ▼
      DeepSeek API      妙响 API          抖音/汽水音乐
    (歌词生成 SSE)    (AI 作曲 Sway)     (发布/数据)
```

### 技术栈

| 分类 | 技术 | 版本 | 用途 |
|------|------|------|------|
| **客户端** | | | |
| GUI 框架 | PySide6 (Qt6) | ≥ 6.6 | 桌面应用界面 |
| 浏览器自动化 | Playwright | ≥ 1.40 | 妙响页面操作 |
| 反检测 | playwright-stealth | ≥ 1.0.6 | 绕过浏览器指纹检测 |
| 异步 HTTP | httpx | ≥ 0.27 | DeepSeek API 调用 |
| 异步数据库 | aiosqlite | ≥ 0.19 | SQLite 异步访问 |
| 音视频处理 | av (PyAV) | ≥ 18.0 | 音频解码处理 |
| 加密 | cryptography | ≥ 42.0 | 请求签名/响应验证 |
| 系统监控 | psutil | ≥ 5.9 | 进程管理（更新机制） |
| 打包 | PyInstaller | ≥ 6.3 | Windows exe 打包 |
| **服务端** | | | |
| Web 框架 | FastAPI | 0.115 | REST API |
| ASGI 服务器 | Uvicorn | 0.30.6 | 异步服务 |
| 模板引擎 | Jinja2 | 3.1.4 | 落地页/管理后台 |
| 数据校验 | Pydantic | 2.9.2 | 请求/响应模型 |
| 二步验证 | pyotp | 2.9 | TOTP 管理员登录 |
| 二维码 | qrcode | 7.4 | 支付/扫码 |
| 国密 | gmssl | 3.2 | 国密算法支持 |
| 密码哈希 | argon2-cffi | 25.1 | 管理员密码 |
| **AI 引擎** | | | |
| 歌词生成 | DeepSeek 网页版 API | - | 逆向工程 SSE 流 |
| AI 作曲 | 妙响 Sway v5.x | - | Playwright 自动化 |

---

## 快速开始

### 环境要求

- **操作系统**：Windows 10/11（64 位）
- **Python**：3.11 及以上
- **浏览器**：Chromium（Playwright 自动安装）
- **网络**：需可访问 `music.douyin.com` 与 `chat.deepseek.com`

### 安装步骤

```bash
# 1. 克隆仓库
git clone https://github.com/2181533/cy-ai-music-assistant.git
cd cy-ai-music-assistant

# 2. 安装客户端依赖
pip install -r requirements.txt

# 3. 安装 Playwright 浏览器
playwright install chromium

# 4. 启动客户端
python app/main.py
```

### 服务端部署（可选）

```bash
cd yspt-server

# 安装服务端依赖
pip install -r requirements.txt

# 复制环境配置
copy .env.example .env
# 编辑 .env 填入密钥、支付证书路径等

# 初始化密钥
python scripts/init_secrets.py

# 启动服务
python server.py
# 或使用启动脚本
start.bat
```

### 首次使用

1. **登录抖音账号**：在账号管理中扫码登录妙响（抖音音乐创作实验室）
2. **登录 DeepSeek**：首次使用歌词生成时扫码登录 `chat.deepseek.com`
3. **配置创作模板**：在创作中心选择歌曲方向、创作方向、生成数量
4. **启动流水线**：勾选要执行的阶段，点击「开始」
5. **查看进度**：任务卡片实时显示歌词/歌曲/签约/发布进度

---

## 项目结构

```
汽水平台/
├── app/                              # 客户端源码
│   ├── main.py                       # 应用入口（启动顺序、更新机制）
│   ├── config.py                     # 全局配置（路径、调度、风控、License）
│   │
│   ├── core/                         # 核心业务层
│   │   ├── account_manager.py        # 多账号管理（Cookie持久化、绑定组）
│   │   ├── account_binding.py        # 主子账号绑定关系
│   │   ├── deepseek_lyrics_api.py    # DeepSeek 歌词生成（SSE流式）
│   │   ├── deepseek_prompt_builder.py# 提示词构造器（64风格×20手法×25意象）
│   │   ├── deepseek_account_pool.py  # DeepSeek 账号池轮换
│   │   ├── lyrics_provider.py        # 歌词生成抽象接口
│   │   ├── miaoxiang_api.py          # 妙响 API 封装
│   │   ├── generate_engine.py        # 2槽并发生成调度
│   │   ├── sign_engine.py            # 自动签约引擎
│   │   ├── sign_api.py               # 签约 API
│   │   ├── login_api.py              # 登录 API
│   │   ├── pure_api_publisher.py     # 纯 API 发布器
│   │   ├── publish_quota.py          # 发布配额管理
│   │   ├── quota_tracker.py          # 额度追踪
│   │   ├── player_manager.py         # 播放器管理
│   │   ├── task_scheduler.py         # 任务调度器
│   │   ├── template_schema.py        # 模板结构定义
│   │   ├── user_settings.py          # 用户设置持久化
│   │   ├── abogus.py                 # a_bogus 签名（已迁移服务端）
│   │   └── pipeline/                 # 流水线阶段（编译保护）
│   │       ├── pipeline_engine.py    # 流水线引擎
│   │       ├── lyrics_stage.py       # 歌词阶段
│   │       ├── song_stage.py         # 歌曲阶段
│   │       ├── rename_stage.py       # 改名阶段
│   │       ├── publish_stage.py      # 发布阶段
│   │       ├── stats_stage.py        # 统计阶段
│   │       ├── delete_stage.py       # 删除阶段
│   │       ├── ds_lock.py            # DeepSeek 并发锁
│   │       └── stage_plugin.py       # 阶段插件接口
│   │
│   ├── ui/                           # 界面层
│   │   ├── main_window.py            # 主窗口（侧边栏、动画、背景光斑）
│   │   ├── creation_center.py        # 创作中心（一体化流水线面板）
│   │   ├── data_center_panel.py      # 数据中心（多平台统计）
│   │   ├── agent_panel.py            # 代理面板
│   │   ├── account panels            # 账号管理面板
│   │   ├── themes.py                 # 主题系统（深色/浅色、模式色）
│   │   ├── widgets.py                # 动画控件（流光、涟漪、发光卡片）
│   │   ├── song_card_editor.py       # 歌曲卡片编辑器
│   │   ├── activation_dialog.py      # 激活对话框
│   │   ├── purchase_dialog.py        # 购买对话框
│   │   ├── about_panel.py            # 关于面板
│   │   ├── changelog_panel.py        # 更新日志
│   │   ├── feedback_panel.py         # 反馈面板
│   │   ├── announcement_panel.py     # 公告面板
│   │   ├── update_dialog.py          # 更新对话框
│   │   └── qr_util.py                # 二维码工具
│   │
│   ├── data/                         # 数据层
│   │   ├── db.py                     # SQLite 异步访问
│   │   └── models.py                 # 数据模型
│   │
│   ├── license/                      # 授权与安全
│   │   ├── license_manager.py        # 授权管理器（服务端验证）
│   │   ├── crypto.py                 # 加密/签名/验证
│   │   ├── machine_id.py             # 机器码生成
│   │   └── integrity.py              # 完整性校验
│   │
│   ├── agent/                        # 代理体系
│   │   └── agent_config.py           # 代理品牌配置（exe末尾读取）
│   │
│   ├── announcement/                 # 公告系统
│   │   └── announcement_mgr.py       # 公告管理器
│   │
│   └── updater/                      # 自动更新
│       ├── update_checker.py         # 更新检查
│       ├── downloader.py             # 增量下载
│       └── updater_main.py           # 更新主程序
│
├── yspt-server/                      # 服务端源码
│   ├── server.py                     # FastAPI 应用入口
│   ├── config.py                     # 服务端配置
│   ├── db.py                         # 数据库访问层
│   ├── license_api.py                # 授权验证 API
│   ├── agent_api.py                  # 代理管理 API
│   ├── payment_api.py                # 支付订单 API
│   ├── admin_api.py                  # 管理后台 API
│   ├── update_api.py                 # 更新分发 API
│   ├── announcement_api.py           # 公告 API
│   ├── feedback_api.py               # 反馈 API
│   ├── abogus_api.py                 # a_bogus 签名服务
│   ├── abogus_module.py              # 签名算法模块
│   ├── alipay_pay.py                 # 支付宝支付
│   ├── wechat_pay.py                 # 微信支付
│   ├── crypto.py                     # 服务端加密
│   ├── passwords.py                  # 密码哈希（argon2）
│   ├── rate_limit.py                 # 限流中间件
│   ├── audit.py                      # 审计日志
│   ├── secrets_store.py              # 密钥存储
│   ├── rotate_secrets.py             # 密钥轮换
│   ├── download_tracker.py           # 下载追踪
│   ├── templates/                    # Jinja2 模板
│   │   ├── landing.html              # 落地页
│   │   ├── faq.html                  # FAQ 页
│   │   ├── blog/                     # 博客系统
│   │   ├── admin/                    # 管理后台
│   │   └── agent/                    # 代理后台
│   ├── static/                       # 静态资源
│   ├── tests/                        # 单元测试
│   └── scripts/                      # 运维脚本
│
├── requirements.txt                  # 客户端依赖
├── build.bat                         # 打包脚本
└── README.md                         # 本文档
```

---

## 功能详解

### 1. DeepSeek 歌词生成引擎

本项目通过逆向工程 DeepSeek 网页版 API 实现歌词生成，核心特性：

- **双流收集**：同时收集 `reasoning`（思考过程）与 `content`（最终输出）流，避免歌名丢失
- **深度思考 + 联网搜索**：强制开启 `thinking=True` 与 `search_enabled=True`，保证生成质量
- **独立对话隔离**：每首歌使用独立新对话，完全隔离上下文，避免相互污染
- **完整提示词**：每首使用完整提示词，包含风格锚点、创作方向、意象种子、结构约束
- **歌名多重提取**：支持直引号、中文弯引号、书名号、直角引号，含截断恢复策略

**提示词组合维度**：

```
65 创作主题 × 20 创作手法 × 25 意象种子 × 20 风格锚点 = 650,000+ 组合
```

确保每首歌词在主题、视角、意象、曲风上均不相同。

### 2. 妙响 AI 作曲引擎

通过 Playwright 控制浏览器自动化操作妙响（抖音音乐创作实验室）：

- **2 槽并发生成**：每账号同时 2 个生成槽位，自动轮转
- **同词异曲**：每首歌词生成 2 首不同作曲版本，提升成功率
- **进度轮询**：每 5 秒轮询生成状态，失败自动跳过不无限重试
- **反检测**：playwright-stealth 绕过浏览器指纹检测
- **人类行为模拟**：随机延迟（普通 1.5-4s，关键 5-15s）

### 3. 流水线引擎

五阶段可插拔流水线，每阶段可独立勾选：

| 阶段 | 功能 | 说明 |
|------|------|------|
| 歌词 | 生成歌词 | DeepSeek API，批量生成 + 重试 + 实时字数 |
| 歌曲 | AI 作曲 | 妙响引擎，2 槽并发，失败跳过 |
| 改名 | 修改歌名 | 不合格歌名 AI 重新生成（仅改名不重写歌词） |
| 发布 | 多平台发布 | 汽水音乐/抖音，四种发布方式，发布前清空队列 |
| 统计 | 数据采集 | 多平台热度/使用量/播放量 |

**执行模型**：每个账号独立协程，账号间并行互不等待；账号内五阶段串行执行。

### 4. 多账号管理体系

- **Cookie 持久化**：登录态保存到 `storage/cookies/`，避免重复登录
- **扫码登录**：直接弹出浏览器扫码，不弹额外小窗口
- **绑定组聚类**：主账号 + 子账号按组分配同色标识，主账号实色/子账号半透明
- **在线状态检测**：启动前异步检查，离线自动登录，失败弹窗提醒
- **认证状态展示**：已认证（绿色）/未认证（琥珀色），纯文字无背景

### 5. 代理白标体系

完整的代理商分销体系：

- **exe 末尾植入**：打包时在 exe 末尾写入 `agent_code`（YSPT_AGENT 魔法标识）
- **品牌配置加载**：启动时联网获取代理品牌名、Logo、联系方式、二维码
- **防挖客机制**：服务端基于 `machine_id` 判断，防止代理互相抢客
- **独立卖价体系**：`agent_plan_prices` 表独立存储代理售价/原价/批发基准价
- **卡密扣费**：基于 `agent_base_price` 批发基准价，与主卖价完全解耦
- **身份切换检测**：exe 末尾标识变化时自动清除缓存与卡密

### 6. 授权与安全

- **服务端验证**：每次启动验证 License，24h 缓存
- **机器码绑定**：基于硬件特征生成唯一机器码
- **动态密钥**：请求签名使用动态密钥，定期轮换
- **离线宽限**：7 天离线可用，超过锁定功能
- **心跳机制**：每 5 分钟心跳保活
- **防破解**：编译模式强制走服务端签名，客户端无本地签名算法
- **完整性校验**：exe 完整性检测，防篡改

### 7. UI 设计

赛博朋克高科技风格，遵循以下设计原则：

- **5 套主题配色**：赛博蓝（默认）、霓虹紫、极光绿、暗夜橙、猩红
- **动画效果**：页面切换、卡片悬浮、按钮涟漪、背景流光
- **紧凑布局**：相关元素同行排列，无横向滚动条
- **状态可视化**：在线/离线文字标识、进度条并行展示
- **滚轮守卫**：参数控件无焦点时不响应滚轮，防误调
- **弹窗规范**：圆角、窄边框、居中、浏览器内部确认

---

## 配置说明

### 客户端配置

核心配置位于 `app/config.py`：

```python
# 生成调度
MAX_CONCURRENT_SLOTS = 2          # 每账号同时生成数
GENERATE_POLL_INTERVAL = 5        # 生成进度轮询(秒)

# 风控
HUMAN_DELAY = (1.5, 4.0)          # 普通操作间隔
CRITICAL_DELAY = (5.0, 15.0)      # 关键操作间隔
DAILY_QUOTA_SAFE_RATIO = 0.8      # 当日额度使用上限

# License
OFFLINE_GRACE_HOURS = 24          # 离线宽限
OFFLINE_LOCK_HOURS = 24 * 7       # 离线锁定
HEARTBEAT_INTERVAL = 300          # 心跳间隔(秒)

# UI
DEFAULT_THEME = "cyber_blue"
ANIMATION_DURATION = 220          # 动画时长(ms)
```

### 服务端配置

环境变量配置位于 `yspt-server/.env`（参考 `.env.example`），包含：

- 数据库路径
- 服务端口
- 微信支付/支付宝证书路径
- 动态密钥种子
- TOTP 密钥
- 管理员账号

---

## 打包发布

### 客户端打包

```bash
# 使用 PyInstaller 打包
build.bat
```

打包后生成单文件 exe，数据存储在 `%APPDATA%/CY-AI音乐助手/`。

### 代理版打包

代理版 exe 会在末尾植入 `agent_code`，启动时自动加载对应品牌配置。

---

## 开发指南

### 开发模式运行

```bash
# 客户端（开发模式，不编译）
python app/main.py

# 服务端（开发模式，热重载）
cd yspt-server
uvicorn server:app --reload --host 0.0.0.0 --port 8000
```

### 代码规范

- 客户端使用 `asyncio` 异步编程，UI 操作通过 `run_async` 桥接
- 数据库访问统一使用 `aiosqlite` 异步接口
- 所有 API 请求使用 `httpx.AsyncClient`
- 日志使用 `logging` 模块，关键操作记录完整上下文
- 配置项集中在 `config.py`，避免硬编码

### 测试

```bash
cd yspt-server
pytest tests/ -v
```

---

## 路线图

- [x] DeepSeek 歌词生成（深度思考 + 联网）
- [x] 妙响 AI 作曲（2 槽并发）
- [x] 自动签约与多平台发布
- [x] 代理白标体系
- [x] 数据中心多平台统计
- [x] License 服务端验证
- [x] 自动更新机制
- [ ] 更多 AI 作曲引擎接入
- [ ] 歌词质量评分系统
- [ ] 智能选曲推荐
- [ ] 多语言界面支持

---

## 贡献

欢迎提交 Issue 与 Pull Request。提交前请确保：

1. 代码通过现有测试
2. 新功能附带测试用例
3. 遵循现有代码风格
4. 提交信息清晰描述变更

---

## License

本项目为私有项目，保留所有权利。未经授权不得复制、修改、分发或商用。

---

## 致谢

- [DeepSeek](https://www.deepseek.com/) - 提供 AI 歌词生成能力
- [PySide6](https://www.qt.io/) - 跨平台 GUI 框架
- [Playwright](https://playwright.dev/) - 浏览器自动化
- [FastAPI](https://fastapi.tiangolo.com/) - 高性能 Web 框架
- [Suno AI](https://suno.com/) - 风格提示词公式参考

---

<div align="center">

**如果这个项目对你有帮助，欢迎 Star 支持**

[报告问题](https://github.com/2181533/cy-ai-music-assistant/issues) · [功能建议](https://github.com/2181533/cy-ai-music-assistant/issues) · [查看版本](https://github.com/2181533/cy-ai-music-assistant/releases)

</div>
