# 小红书 MCP Skill

Claude Code 的 Skill 配置文件，用于与小红书 MCP 服务器集成，实现内容发布、浏览、搜索和互动功能。

## 功能特性

- 📱 **内容发布** - 支持图文/视频笔记发布
- 🔍 **内容搜索** - 搜索小红书笔记和用户
- 👤 **用户主页** - 查看用户信息和全部笔记
- ❤️ **互动功能** - 点赞、收藏、评论
- 📊 **数据分析** - 获取笔记详情和互动数据

## 快速开始

### 1. 前置要求

- macOS 或 Linux
- 已安装 Chrome 浏览器
- Claude Code 客户端
- [小红书 MCP 服务器](https://github.com/xpzouying/xiaohongshu-mcp)（需要单独部署）

### 2. 安装 Skill

```bash
# 克隆本项目
git clone https://github.com/yourusername/xiaohongshu-mcp-skill.git

# 复制到 Claude Code skills 目录
cp -r xiaohongshu-mcp-skill ~/.claude/skills/xiaohongshu-mcp
```

### 3. 配置 MCP 服务器

在 Claude Code 设置中添加 MCP 服务器：

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

详细配置说明请参考 [SKILL.md](./SKILL.md)。

## 项目结构

```
.
├── SKILL.md          # Skill 完整文档
├── README.md         # 项目说明
├── LICENSE           # 开源协议
└── .gitignore        # Git 忽略配置
```

## 使用示例

### 发布图文笔记

```
发布一篇关于旅行的图文笔记，标题是"周末的杭州之旅"，
图片在 /Users/user/Desktop/hangzhou1.jpg 和 /Users/user/Desktop/hangzhou2.jpg，
标签是 [旅行, 杭州, 周末]
```

### 搜索用户

```
搜索关键词"旅行博主"，查看相关用户
```

### 查看用户主页

```
获取用户 ID xxx 的主页信息和所有笔记
```

## 相关项目

- [xiaohongshu-mcp](https://github.com/xpzouying/xiaohongshu-mcp) - 小红书 MCP 服务器（Go 实现）

## 许可证

MIT License - 详见 [LICENSE](./LICENSE) 文件。

## 免责声明

本项目仅供学习研究使用，使用本项目时请遵守小红书平台的相关规则和法律法规。用户需自行承担使用风险。
