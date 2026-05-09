[README.md](https://github.com/user-attachments/files/27552795/README.md)
# 🦞 OpenClaw 智能助手

> 一个功能强大的 AI 智能助手框架，支持多渠道消息收发、自动化任务、文档处理和项目开发。

[![OpenClaw Version](https://img.shields.io/badge/OpenClaw-2026.3.13-blue.svg)](https://github.com/coze-cn/openclaw)
[![Node.js](https://img.shields.io/badge/Node.js-24.x-green.svg)](https://nodejs.org/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## ✨ 功能特性

### 🤖 多渠道接入
- **飞书 (Feishu/Lark)** - 企业团队沟通
- **钉钉 (DingTalk)** - 企业办公协作
- **QQ** - 群聊与私聊消息
- **企业微信 (WeCom)** - 企业微信集成
- **Telegram** - Bot 消息推送

### 📄 文档处理
- **PDF 解析** - 自动提取文本内容
- **PPT 处理** - 解析幻灯片内容
- **AI 摘要生成** - 智能生成文档摘要
- **飞书云文档** - 自动上传到飞书空间

### ⏰ 自动化任务
- **定时提醒** - 自定义时间发送提醒
- **课程提醒** - 课表自动提醒
- **邮件检查** - QQ 邮箱定时检查
- **GitHub Trending** - 每日热门项目追踪
- **B站收藏** - 自动收藏视频

### 🛠️ 开发工具
- **项目开发助手** - 需求分析、代码生成、测试
- **GitHub 集成** - Issue 和 PR 管理
- **编码代理** - Claude Code / Codex 支持
- **Web 搜索与浏览** - 实时网页内容获取

### 💬 智能交互
- **消息总结** - 自动总结群聊内容
- **语音处理** - 语音识别与合成
- **表情包学习** - 智能学习并匹配表情
- **AI 画图** - 图片生成能力

## 🚀 快速开始

### 环境要求

- **Node.js**: v24.x 或更高
- **pnpm**: v8.x 或更高
- **Playwright**: 用于浏览器自动化
- **pdftotext**: 用于 PDF 解析

### 安装步骤

```bash
# 1. 克隆项目
git clone <your-repo-url>
cd openclaw

# 2. 安装依赖
pnpm install

# 3. 安装插件（可选）
openclaw plugins install @openclaw-china/dingtalk
openclaw plugins install @tencent-connect/openclaw-qqbot
openclaw plugins install @openclaw/lark-plugin

# 4. 启动服务
./scripts/start.sh
```

### 配置渠道

#### 飞书配置

1. 创建飞书应用，获取 `App ID` 和 `App Secret`
2. 配置机器人能力和权限
3. 在控制台添加配置：

```bash
openclaw channels add feishu \
  --app-id YOUR_APP_ID \
  --app-secret YOUR_APP_SECRET
```

#### QQ Bot 配置

1. 在 QQ 开放平台创建机器人应用
2. 获取 `App ID` 和 `Token`
3. 配置：

```bash
openclaw channels add qqbot \
  --app-id YOUR_APP_ID \
  --token YOUR_TOKEN
```

#### 钉钉配置

```bash
openclaw channels add dingtalk \
  --client-id YOUR_CLIENT_ID \
  --client-secret YOUR_CLIENT_SECRET
```

## 📁 项目结构

```
openclaw/
├── openclaw.json          # 主配置文件
├── .coze                  # 启动配置
├── scripts/               # 启动脚本
│   ├── start.sh          # 启动服务
│   ├── stop.sh           # 停止服务
│   └── restart.sh        # 重启服务
├── workspace/
│   ├── skills/           # 自定义 Skills
│   │   ├── document-processor/    # 文档处理
│   │   ├── qq-mail/               # QQ 邮箱
│   │   ├── bilibili-auto/         # B站自动化
│   │   ├── github-trending/       # GitHub 热门
│   │   └── project-dev-assistant/ # 项目开发
│   ├── bilibili_automation/      # B站自动化配置
│   └── memory/            # 记忆存储
├── extensions/           # 插件扩展
└── logs/                 # 日志文件
```

## 🎯 使用示例

### 基本命令

```
# 查看帮助
/help

# 查看状态
/status

# 检查健康
/health
```

### 定时任务

```
# 创建提醒
5分钟后提醒我喝水

# 查看提醒
查看我的提醒

# 取消提醒
取消 [提醒名称]
```

### 文档处理

```
# 处理 PDF 文件
/doc process ./report.pdf

# 处理 PPT 文件
/doc process ./slides.pptx

# 上传到飞书
/doc process ./file.pdf --feishu-folder fldcnXXXXXX
```

### 邮件检查

```
# 立即检查
/mail check

# 查看状态
/mail status

# 设置时间
/mail schedule 20:00
```

### 开发助手

```
# 帮我开发一个 TODO 应用
帮我创建一个 React TODO 应用

# GitHub 操作
查看我的 GitHub 仓库
帮我创建一个 issue
```

## ⚙️ 配置文件说明

### 主要配置项

```json
{
  "gateway": {
    "port": 5000,
    "mode": "local"
  },
  "channels": {
    "feishu": { /* 飞书配置 */ },
    "qqbot": { /* QQ 配置 */ },
    "dingtalk": { /* 钉钉配置 */ }
  },
  "skills": {
    "entries": {
      "document-processor": { "enabled": true },
      "qq-mail": { "enabled": true }
    }
  }
}
```

### 环境变量

```bash
# 模型配置
COZE_INTEGRATION_MODEL_BASE_URL=<模型服务地址>
COZE_WORKLOAD_IDENTITY_API_KEY=<API Key>

# 可选配置
OPENCLAW_LOG_LEVEL=error  # 日志级别
```

## 🛠️ 开发指南

### 创建自定义 Skill

1. 在 `workspace/skills/` 创建目录
2. 添加 `SKILL.md` 配置文件
3. 创建处理脚本
4. 在 `openclaw.json` 中注册

示例 `SKILL.md`:

```markdown
# 我的自定义 Skill

## 描述
这是一个示例 Skill

## 触发词
/my-skill

## 工具
- shell
- http
```

### Skill 目录结构

```
workspace/skills/my-skill/
├── SKILL.md           # Skill 配置
├── index.ts           # 入口文件
├── my-skill.ts        # 核心功能
└── test.ts            # 测试脚本
```

## 📦 可用 Skills

| Skill | 描述 | 状态 |
|-------|------|------|
| `document-processor` | PDF/PPT 文档处理 | ✅ |
| `qq-mail` | QQ 邮箱自动读取 | ✅ |
| `bilibili-auto` | B站自动收藏 | ✅ |
| `github-trending` | GitHub 热门追踪 | ✅ |
| `project-dev-assistant` | 项目开发助手 | ✅ |
| `qq-summarizer` | QQ 消息总结 | ✅ |
| `qq-voice` | QQ 语音处理 | ✅ |
| `sticker-learner` | 表情包学习 | ✅ |
| `ppt-processor` | PPT 处理 | ✅ |
| `gog` | Google Workspace | ✅ |
| `notion` | Notion 集成 | ✅ |
| `obsidian` | Obsidian 笔记 | ✅ |
| `github` | GitHub 操作 | ✅ |
| `telegram` | Telegram Bot | ✅ |
| `summarize` | 内容摘要 | ✅ |
| `coze-image-gen` | 图片生成 | ✅ |
| `coze-voice-gen` | 语音合成 | ✅ |
| `coze-web-fetch` | 网页抓取 | ✅ |
| `coze-web-search` | 网页搜索 | ✅ |

## 🔧 故障排查

### 服务无法启动

```bash
# 检查配置
openclaw config validate

# 运行诊断
openclaw doctor

# 查看日志
tail -n 100 logs/openclaw.log
```

### 渠道连接问题

```bash
# 检查渠道状态
openclaw channels status

# 测试连接
openclaw channels probe feishu
```

### Skill 无法使用

```bash
# 查看 Skill 状态
openclaw skills list

# 重新安装 Skill
clawhub install <skill-name>
```

## 📚 更多资源

- [OpenClaw 官方文档](https://docs.coze.cn)
- [OpenClaw GitHub](https://github.com/coze-cn/openclaw)
- [ClawHub Skills 市场](https://clawhub.cn)

## 🤝 贡献指南

欢迎提交 Issue 和 Pull Request！

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 创建 Pull Request

## 📄 许可证

本项目采用 MIT 许可证 - 详见 [LICENSE](LICENSE) 文件

## 🙏 致谢

- [OpenClaw](https://github.com/coze-cn/openclaw) - AI 助手框架
- [Coze](https://coze.cn) - AI 模型服务
- 所有贡献者和使用者

---

<p align="center">
  <strong>Made with 🦞 by OpenClaw</strong>
</p>
