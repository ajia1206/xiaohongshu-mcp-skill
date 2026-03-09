# 小红书 MCP Skill

Claude Code 的 Skill 配置文件，用于与小红书 MCP 服务器集成，实现内容发布、浏览、搜索和互动功能。

[![GitHub](https://img.shields.io/badge/GitHub-ajia1206/xiaohongshu--mcp--skill-blue)](https://github.com/ajia1206/xiaohongshu-mcp-skill)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](./LICENSE)

## 📋 目录

- [功能特性](#功能特性)
- [前置要求](#前置要求)
- [快速开始](#快速开始)
- [详细配置](#详细配置)
- [使用示例](#使用示例)
- [故障排除](#故障排除)
- [项目结构](#项目结构)
- [更新日志](#更新日志)
- [相关项目](#相关项目)
- [许可证](#许可证)

## ✨ 功能特性

- 📱 **内容发布** - 支持图文/视频笔记发布
- 🔍 **内容搜索** - 搜索小红书笔记和用户
- 👤 **用户主页** - 查看用户信息和全部笔记（自动滚动加载）
- ❤️ **互动功能** - 点赞、收藏、评论
- 📊 **数据分析** - 获取笔记详情和互动数据
- 🔐 **登录管理** - 扫码登录，Cookie 自动保存约 1 年

## 📝 前置要求

### 系统要求

- **操作系统**: macOS 或 Linux
- **浏览器**: 已安装 Chrome/Chromium 浏览器
- **客户端**: Claude Code
- **MCP 服务器**: [小红书 MCP 服务器](https://github.com/ajia1206/xhs-mcp)（需要单独部署）

### MCP 服务器要求

在使用本 Skill 之前，你需要先部署小红书 MCP 服务器：

```bash
# 克隆 MCP 服务器
git clone https://github.com/ajia1206/xhs-mcp.git
cd xhs-mcp/build/xiaohongshu-mcp

# 构建
go build -o xiaohongshu-mcp

# 启动服务
./xiaohongshu-mcp --port 18060 --log-level info
```

详细部署说明请参考 [xhs-mcp 项目](https://github.com/ajia1206/xhs-mcp)。

## 🚀 快速开始

### 1. 安装 Skill

**方式一：直接克隆到 skills 目录**

```bash
# 克隆到 Claude Code skills 目录
git clone https://github.com/ajia1206/xiaohongshu-mcp-skill.git \
  ~/.claude/skills/xiaohongshu-mcp
```

**方式二：手动复制**

```bash
# 克隆到任意位置
git clone https://github.com/ajia1206/xiaohongshu-mcp-skill.git

# 复制到 Claude Code skills 目录
cp -r xiaohongshu-mcp-skill ~/.claude/skills/xiaohongshu-mcp
```

**方式三：使用符号链接（推荐，便于更新）**

```bash
# 克隆到工作目录
git clone https://github.com/ajia1206/xiaohongshu-mcp-skill.git \
  ~/workspace/xiaohongshu-mcp-skill

# 创建符号链接
ln -s ~/workspace/xiaohongshu-mcp-skill \
  ~/.claude/skills/xiaohongshu-mcp
```

### 2. 验证安装

```bash
# 检查 skill 是否正确安装
ls -la ~/.claude/skills/xiaohongshu-mcp

# 应该能看到 SKILL.md 文件
cat ~/.claude/skills/xiaohongshu-mcp/SKILL.md | head -10
```

### 3. 配置 MCP 服务器

编辑 Claude Code 配置文件：

```bash
# macOS
vim ~/Library/Application\ Support/Claude/settings.json

# Linux
vim ~/.config/Claude/settings.json
```

添加 MCP 服务器配置：

```json
{
  "mcpServers": {
    "xiaohongshu": {
      "command": "/path/to/xiaohongshu-mcp",
      "args": ["--port", "18060", "--log-level", "info"],
      "env": {},
      "cwd": "/path/to/xiaohongshu-mcp-directory"
    }
  }
}
```

**实际配置示例：**

```json
{
  "mcpServers": {
    "xiaohongshu": {
      "command": "/Users/getui/Desktop/repo/xhs-mcp/build/xiaohongshu-mcp/xiaohongshu-mcp",
      "args": ["--port", "18060", "--log-level", "info"],
      "env": {},
      "cwd": "/Users/getui/Desktop/repo/xhs-mcp/build/xiaohongshu-mcp"
    }
  }
}
```

### 4. 重启 Claude Code

配置完成后，重启 Claude Code 或在设置中刷新 MCP 服务器。

### 5. 验证功能

在 Claude Code 中输入以下命令测试：

```
检查小红书登录状态
```

或：

```
搜索小红书上的旅行博主
```

## ⚙️ 详细配置

### 环境变量

| 变量名 | 说明 | 默认值 |
|--------|------|--------|
| `COOKIES_PATH` | Cookie 文件路径 | `cookies/cookies.json` |

### MCP 服务器参数

| 参数 | 说明 | 默认值 |
|------|------|--------|
| `--port` | 服务端口 | `18060` |
| `--log-level` | 日志级别 (debug/info/warn/error) | `info` |
| `--headless` | 是否无头模式 | `true` |

## 💡 使用示例

### 示例 1：发布图文笔记

```
发布一篇关于杭州旅行的图文笔记，
标题是"周末的杭州之旅"，
内容描述西湖的美景和美食体验，
图片在 /Users/user/Desktop/hangzhou1.jpg 和 /Users/user/Desktop/hangzhou2.jpg，
标签是 [旅行, 杭州, 西湖, 美食]
```

### 示例 2：搜索用户并查看主页

```
搜索用户"陆苍"，获取他的主页信息和所有笔记
```

### 示例 3：浏览首页并互动

```
获取小红书首页推荐内容，找到关于 AI 绘图的笔记，
查看详情并点赞收藏
```

### 示例 4：使用 HTTP API 直接调用

```bash
# 检查登录状态
curl http://localhost:18060/api/v1/login/status

# 搜索用户
curl -X POST http://localhost:18060/api/v1/feeds/search \
  -H "Content-Type: application/json" \
  -d '{
    "keyword": "陆苍",
    "type": "user",
    "page": 1,
    "page_size": 10,
    "filters": []
  }'

# 获取用户主页
curl -X POST http://localhost:18060/api/v1/user/profile \
  -H "Content-Type: application/json" \
  -d '{
    "user_id": "用户ID",
    "xsec_token": "xsec_token"
  }'
```

## 🔧 故障排除

### Skill 未生效

**症状**: Claude Code 无法识别 skill 命令

**解决方案**:
1. 检查 skill 是否正确安装：`ls ~/.claude/skills/xiaohongshu-mcp`
2. 重启 Claude Code
3. 检查 SKILL.md 文件是否存在且格式正确

### MCP 服务器连接失败

**症状**: "无法连接到 MCP 服务器"

**解决方案**:
1. 检查服务是否运行：`lsof -i :18060`
2. 检查端口配置是否一致（skill 使用 18060）
3. 查看服务日志：`tail -f /path/to/mcp.log`

### 登录状态失效

**症状**: "登录已过期，请重新登录"

**解决方案**:
1. 使用 `get_login_qrcode` 工具重新扫码
2. 或访问 `http://localhost:18060/api/v1/login/qrcode_image` 获取二维码
3. 用小红书 App 扫描二维码

### Cookie 问题

**症状**: 每次都需要重新登录

**解决方案**:
1. 检查 cookies.json 文件权限
2. 确保文件路径正确（默认在 MCP 服务器目录下的 `cookies/cookies.json`）
3. 检查磁盘空间是否充足

## 📁 项目结构

```
.
├── SKILL.md          # Skill 完整文档（核心文件）
├── README.md         # 项目说明
├── LICENSE           # MIT 开源协议
└── .gitignore        # Git 忽略配置
```

## 📝 更新日志

### v1.0.0 (2024-03-09)

- ✨ 初始版本发布
- 📱 支持图文/视频发布
- 🔍 支持内容搜索
- 👤 支持用户主页查看
- ❤️ 支持点赞、收藏、评论
- 📊 支持 HTTP API 直接调用
- 🔐 Cookie 自动保存，有效期约 1 年

## 🔗 相关项目

- [xhs-mcp](https://github.com/ajia1206/xhs-mcp) - 小红书 MCP 服务器（Go 实现，基于 [xpzouying/xiaohongshu-mcp](https://github.com/xpzouying/xiaohongshu-mcp) 优化）

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

### 提交 Issue

- 描述问题时请提供复现步骤
- 附上错误日志（如果有）
- 说明环境信息（操作系统、浏览器版本等）

### 提交 PR

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 创建 Pull Request

## 📄 许可证

[MIT License](./LICENSE) © 2024

## ⚠️ 免责声明

本项目仅供学习研究使用，使用本项目时请遵守小红书平台的相关规则和法律法规。用户需自行承担使用风险。

---

**注意**: 本 Skill 需要配合 [xhs-mcp](https://github.com/ajia1206/xhs-mcp) 服务器使用，请确保 MCP 服务器已正确部署和运行。
