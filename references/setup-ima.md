# IMA 知识库配置引导

IMA（腾讯元宝旗下知识助手）通过官方 skill 接入，主要用于检索用户收藏的资料和知识库内容。

## 重要说明

IMA 的 API Key **有效期只有一个月**，到期后需要用户重新获取。每次调用前，如果距上次配置超过 25 天，提醒用户检查是否需要更新 Key。

## 配置步骤

告诉用户：

> IMA 需要安装官方 skill。请按以下步骤操作：
>
> 1. 打开：https://ima.qq.com/agent-interface
> 2. 登录你的 IMA 账号
> 3. 页面会显示一段提示词（包含 API Key）
> 4. 按页面指引完成本机配置，并把 API Key 写入用户级环境变量 `IMA_API_KEY`

## 用户完成配置后的处理

1. 按照提示词中的指引部署 IMA skill
2. 将 API Key 写入用户级环境变量 `IMA_API_KEY`，或写入 IMA 官方 skill 自己的本机私有配置
3. 在本机私有配置文件（macOS/Linux 为 `$HOME/.codex/pkb.local.json`，Windows 为 `%USERPROFILE%\.codex\pkb.local.json`）只记录非敏感状态：

```json
{
  "imaConfiguredAt": "2026-05-26T00:00:00.000Z"
}
```

4. 提醒用户：**IMA 的 API Key 有效期约一个月，到期后需要重新配置。**

不要把 IMA API Key 写入 personal-knowledge-base skill 包内的任何文件。

## 获取数据的常用操作

```
# 搜索知识库内容
ima: 搜索 [关键词]

# 浏览知识库结构
ima: 列出知识库节点
```

## 内容处理原则

IMA 主要存放用户收藏的外部资料，在使用时需要注意：
- 这些是**参考资料**，不是用户自己产生的内容
- 用于"话题研究"模式时，作为背景资料引用
- 用于"周报"和"行动规划"时，**不要将 IMA 内容当作用户的行动记录**

## 注意事项

- 如果 IMA API 报错，首先检查 Key 是否过期（查看 configuredAt 时间）
- 过期提示：告知用户重新访问 https://ima.qq.com/agent-interface 获取新的配置
