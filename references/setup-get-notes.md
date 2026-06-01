# Get笔记配置引导

Get笔记通过 OpenAPI 接入，主要用于获取用户保存的笔记、知识库内容、语义搜索结果及 AI 分析结果。

## 配置步骤

告诉用户：

> Get笔记需要 API Key；如果平台同时提供 Client ID，也一并配置。请按以下步骤操作：
>
> 1. 打开：https://www.biji.com/openapi?tab=keys
> 2. 登录你的 Get笔记账号（需要会员）
> 3. 创建一个新的 API Key
> 4. 将 API Key 写入本机环境变量 `GET_NOTES_API_KEY`
> 5. 如果页面提供 Client ID，将它写入本机环境变量 `GET_NOTES_CLIENT_ID`

## 收到 API Key 后的处理

优先让用户把 API Key 写入本机环境变量 `GET_NOTES_API_KEY`。如果平台提供 Client ID，写入 `GET_NOTES_CLIENT_ID`。不要把真实 key、Client ID 写入 skill 包、Markdown 文件或可分发配置中。

PowerShell 示例：

```powershell
[Environment]::SetEnvironmentVariable('GET_NOTES_API_KEY', '<用户提供的 API Key>', 'User')
[Environment]::SetEnvironmentVariable('GET_NOTES_CLIENT_ID', '<用户提供的 Client ID>', 'User')
```

macOS/Linux shell 示例：

```sh
export GET_NOTES_API_KEY='<用户提供的 API Key>'
export GET_NOTES_CLIENT_ID='<用户提供的 Client ID>'
```

如果用户不想写入环境变量，也可以写入本机私有文件 `$HOME/.codex/pkb.local.json` 或 `%USERPROFILE%\.codex\pkb.local.json`，但必须提醒：这个文件不能放进 skill 包，也不能分享给别人。

**注意：** 不要在对话中回显完整的 API Key；确认时只显示前后各 3-4 位。

## 获取数据的常用操作

```
# Base URL
https://openapi.biji.com

# 所有请求都带这两个 Header，Authorization 直接放 API Key，不加 Bearer
Authorization: $GET_NOTES_API_KEY
X-Client-ID: $GET_NOTES_CLIENT_ID

# 获取笔记列表
GET /open/api/v1/resource/note/list?since_id=0

# 我的知识库列表
GET /open/api/v1/resource/knowledge/list?page=1

# 知识库笔记列表
GET /open/api/v1/resource/knowledge/notes?topic_id=<topic_id>&page=1

# 全局语义搜索
POST /open/api/v1/resource/recall
{
  "query": "<关键词>",
  "top_k": 5
}
```

## 内容处理原则

Get笔记的内容通常是音视频转录，质量参差不齐：
- 优先使用 AI 分析/摘要部分，而不是原始转录文本
- 如果原始转录质量差（大量错别字、语气词），跳过，只取摘要
- 标注来源时注明"Get笔记·[笔记标题]·[日期]"

## 注意事项

- API Key 有效期以 Get笔记官方说明为准
- 如果 API 返回 401，让用户重新生成 API Key
