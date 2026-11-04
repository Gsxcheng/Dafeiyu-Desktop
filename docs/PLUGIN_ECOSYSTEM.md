# 插件生态与开放开发规范（草案）

- 状态：PROPOSED
- 目标：用户可安装插件，社区作者能开发和分发扩展，平台负责权限和安全边界。

## 1. 插件类别

1. **角色能力**：记忆、提醒、小游戏、表情、情绪与事件识别。
2. **工具与 Agent**：检索、任务同步、联网和受控 MCP/API。
3. **渠道适配器**：QQ、合规微信接口、其他消息平台。
4. **人格包**：纯数据角色卡，不是可执行代码。
5. **界面扩展**：将来可提供受控的 Desktop 设置页和面板扩展（非 V0.1）。

## 2. V0.1 插件策略

- 优先验证 AstrBot 已有 Python 插件 SDK、社区市场与 GitHub/ZIP 安装。
- 开发一个最小测试插件（如 ping + 待办查询），验证安装、配置、启用、禁用、重启、升级或回滚。
- 不承诺所有 AstrBot 插件未来在独立核心无缝运行。

## 3. 插件清单元数据提议

```yaml
id: org.example.reminder
name: Reminder Example
version: 0.1.0
api_version: 1
entrypoint: plugin_main
permissions:
  - messages.read_current_conversation
  - messages.send_current_conversation
  - reminders.write
supported_channels: [qq, app]
requires_user_approval: false
source_repository: https://github.com/example/reminder
license: MIT
```

**说明：** 清单只表达声明的能力，没有进程/系统隔离时，第三方 Python 插件实际权限可能比清单大。不能把元数据宣称为已完成的沙箱。

## 4. 安全治理

- 展示开发者、仓库来源、许可证、版本、兼容、依赖、权限和风险。
- 未审查插件不得静默执行系统命令或自动更新；不向插件泄漏管理员密钥。
- 高风险插件应通过独立进程/容器、低权限用户与受控 API 获得实际隔离。
- 工作 MCP 需用户、群/会话和工具的执行层权限校验。
- 下载校验、依赖来源复核、升级后的冒烟测试、回滚。
- 市场提供举报、审核、撤架、版本撤回及安全公告。

## 5. 开源和素材许可

AstrBot 当前仓库 AGPL-3.0，NapCatQQ Desktop 使用 GPL-3.0；直接复制、修改和分发需评估许可义务。图片、音频、图标、人物角色等素材单独核权，代码开源不意味着素材可商用。

最终 License 待依赖集成与分发方式明确后确定。

## 6. 开发者体验目标

开放示例、模板、版本化事件与工具 API、兼容性矩阵、调试与模拟测试、中文文档和 Issue 模板。破坏兼容更新需迁移说明。
