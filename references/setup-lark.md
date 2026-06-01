# 飞书配置引导

飞书通过 `lark-cli` 工具访问，覆盖以下能力：
- 云文档：创建、读取、编辑文档内容
- 多维表格：查询和管理记录、字段
- 视频会议 / 妙记：搜索会议、获取纪要和逐字稿
- 日历：查询日程、会议安排
- 知识库：查询空间、节点和文档层级

## 配置步骤

告诉用户：

> 飞书需要通过 lark-cli 工具连接。请按以下步骤操作：
>
> 1. 打开飞书开放平台，创建一个自建应用
> 2. 在应用权限中开启你需要的能力（文档/日历/会议等）
> 3. 获取 App ID 和 App Secret
> 4. 将 App ID 和 App Secret 写入本机环境变量或 lark-cli 的本机凭据配置，不要写进 skill 包

如果必须由助手协助配置，只把凭据写入 lark-cli 的本机配置或用户级环境变量；不要写入 `SKILL.md`、`references/` 或任何将来会打包分发的文件。不要在对话中回显完整 App Secret。

## 获取数据的常用命令

配置完成后，使用 lark-cli 获取数据时，参考以下操作：

```bash
# 查询本周会议列表（飞书日历）
lark-cli calendar list --start <周一日期> --end <周日日期>

# 获取妙记会议纪要
lark-cli meeting list --start <日期>
lark-cli meeting transcript --id <会议ID>

# 搜索云文档
lark-cli doc search --keyword <关键词> --date-start <日期>

# 查询多维表格记录
lark-cli bitable records --table-id <表格ID> --filter <条件>
```

## 注意事项

- lark-cli 需要用户授权对应权限，未授权的能力会返回权限错误
- 妙记逐字稿需要会议录制开启，且有一定处理延迟
- 多维表格查询需要知道具体的表格 ID，首次使用时需要让用户提供
