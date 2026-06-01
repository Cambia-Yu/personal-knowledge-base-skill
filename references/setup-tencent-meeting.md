# 腾讯会议配置引导

腾讯会议通过官方 MCP skill 接入，能力包括：
- 搜索历史会议
- 获取会议主题、时间、时长、参与人
- 获取纪要内容（如有）

## 配置步骤

告诉用户：

> 腾讯会议需要安装官方 MCP skill。请按以下步骤操作：
>
> 1. 打开这个网址：https://meeting.tencent.com/ai-skill.html
> 2. 用你的腾讯会议账号登录
> 3. 登录后，页面会显示一段安装指令（包含下载链接和环境变量）
> 4. 按页面指令完成本机安装，并把 Token 写入用户级环境变量

## 用户完成配置后的处理

页面会展示类似这样的内容：

```
指令：https://updatecdn.meeting.qq.com/cos/xxxxx/tencent-meeting-mcp.zip
下载 zip 包并 unzip 解压，帮我安装这个 skill，然后设置环境变量
TENCENT_MEETING_TOKEN=xxxxx
TENCENT_MEETING_USER_ID=xxxxx
```

执行步骤：
1. 下载并解压 zip 包
2. 安装 MCP skill
3. 设置用户级环境变量（变量值来自腾讯会议页面，不要修改）
4. 验证安装：尝试查询最近的会议列表

不要把 `TENCENT_MEETING_TOKEN`、`TENCENT_MEETING_USER_ID` 写入 personal-knowledge-base skill 包内的任何文件。

## 获取数据的常用操作

安装完成后：

```
# 查询某时间段内的会议
tencent-meeting: 搜索 [开始日期] 到 [结束日期] 的会议

# 获取会议纪要
tencent-meeting: 获取会议 [会议ID] 的纪要
```

## 注意事项

- 环境变量中包含用户的个人 Token，不要在对话中展示完整的 Token 值
- Token 通常有效期有限，如果失效需要用户重新从网页获取
- 纪要内容依赖腾讯会议的 AI 纪要功能，需要会议开启该功能
