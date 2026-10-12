# M Plan Vault Agent

> Obsidian AI 写作与知识管理插件，桌面端与移动端通用。
> 基于 [claudian-mobile](https://github.com/Charlesxiaomi/claudian-mobile) 改造，直接调用任意 Anthropic 兼容 API 网关。

---

## ✨ 功能

- 📝 **直接调用 Anthropic Messages API**（不走本地 CLI，移动端可用）
- 💬 侧边栏对话，支持多 Tab、会话持久化
- 🔧 工具调用：读取、写入、补丁、搜索、列出笔记
- 🌐 **支持任意 Anthropic 兼容网关**（base URL + apiKey + model 自定义）
- 📱 iPhone / iPad 端完整可用（移动端测试需 Obsidian Sync 或 Remotely Save 同步配置）

## 🚀 安装（推荐用 BRAT）

本插件未上架 Obsidian 官方市场，用 [BRAT](https://github.com/TfTHacker/obsidian42-brat) 一键安装：

### 桌面端 / 移动端通用步骤

1. 安装 BRAT：`设置 → 社区插件 → 浏览 → 搜索 "brat" → Install`
2. 启用 BRAT：`设置 → 社区插件 → 启用`
3. 添加本插件：`设置 → BRAT → Add Beta plugin → 粘贴 "studynt47/obsidian-claudian-mobile-jy"`
4. 启用本插件：`设置 → 社区插件 → 启用 M Plan Vault Agent`
5. 配置 API（见下）

> 详细 BRAT 文档参见：https://github.com/TfTHacker/obsidian42-brat

## ⚙️ 配置

打开 `设置 → M Plan Vault Agent`，填写三个字段：

| 字段 | 值 |
|------|------|
| **接口地址 (Base URL)** | 你的 Anthropic 兼容网关地址，**不要带 `/v1`**（插件自动拼 `/v1/messages`） |
| **API 密钥 (API Key)** | 该网关的 token |
| **模型 (Model)** | 模型 ID |

### 示例：搭配 NewAPI 中转服务

```yaml
接口地址: http://192.168.1.14:3000
API 密钥: <NewAPI 生成的 token>
模型: MiniMax-M3.1-Flash-Preview
```

### 调试步骤

1. 点 **"测试连接"** → 应该返回 `模型 works: 接口已正常返回流式响应`
2. 点 **"获取模型列表"** → 自动拉取网关支持的所有模型 ID

## 🔍 故障排查

### "Failed to fetch"

- 检查 `接口地址` 是否带了 `/v1`（不应该带）
- 检查网关是否支持 CORS 跨域（需 `Access-Control-Allow-Headers: *` 或显式包含 `x-api-key`、`anthropic-version`）
- 检查网关 URL 是否可从 Obsidian 所在网络访问

### 404 page not found

- 网关不支持 Anthropic 路径（`/v1/messages`）→ 换支持 Anthropic 兼容的中转

### 401 unauthorized

- API Key 错或网关不认这个密钥格式

## 🧩 兼容性

- Obsidian ≥ 1.7.2（桌面端 + 移动端）
- Anthropic Messages API 兼容网关（OpenAI 兼容接口不可用，需中转）

## 📝 License

MIT License

## 🙏 致谢

- 基于 [Charlesxiaomi/claudian-mobile](https://github.com/Charlesxiaomi/claudian-mobile)（原作者 Charlesxiaomi）
- 灵感来自 [YishenTu/claudian](https://github.com/YishenTu/claudian)

---

⚠️ **安全提醒**：API Key 以明文存储在 `data.json`，不要在 vault 同步到不可信设备时使用。
