# PCL dndss 修改版构建产物

这里保存本 fork 的 Windows x64 测试构建，方便与源码、构建记录一同获取。此产物是第三方修改版，原项目作者、社区及认证资料提供者不为本 fork 提供官方支持或背书。声明、许可证范围与 mcauth3 致谢见 [仓库 README](../README.md)。

- 文件：`Plain_Craft_Launcher_dndss_2.15.1_win-x64.exe`。
- 配置：Release，Windows x64，单文件，依赖 .NET 10 Desktop Runtime。
- 版本：2.15.1.0。
- 精确的源码提交、SDK 版本、文件大小、SHA256 和测试结果见 [build-info.json](build-info.json)。
- 校验值见 [SHA256SUMS.txt](SHA256SUMS.txt)。

## 源码范围

基于 fork 的 `dev` 提交 `8f0beaf9315597fdd4cf6171d7e1074e10171be9`，保留 #3684 更新源修复，叠加 #3673、#3676 的区域限制撤销及 Minecraft 登录错误响应详情。构建时注入 mcauth3 的公开默认 Client ID `4a07b708-b86d-4365-a55f-f4f23ecb85ab` 和源码提交标识；未加入 Python 认证库依赖或其他私有服务配置。

## 验证范围

发布构建、EXE 架构、Client ID 嵌入和源码差异检查均会在生成此产物时核对。源码回归测试选择语言资源、模组依赖解析、角色管理、存档导入和存档管理相关现有测试，具体结果见构建清单。

此前相同源码中的两项本地化测试失败已在未修改的上游基线复现：

1. `AllLanguageDictionariesShouldContainBaseKeys`：繁体中文缺少翻译键。
2. `FontProfileShouldFollowCultureGlyphStandard`：字体资源 URI 初始化异常。

当前公开 ID 只验证过能申请微软登录验证码，未完成完整账号登录、最终 Minecraft 服务认证或游戏启动验证。此 EXE 不保证服务持续可用或最终登录成功。

## 使用与校验

关闭旧启动器，将 EXE 放入原启动器目录使用，并根据提示重新登录。不要上传或分享自己的登录 Token、账号配置或游戏数据。

在 PowerShell 中计算文件校验值，与 `SHA256SUMS.txt` 比较：

```powershell
Get-FileHash -Algorithm SHA256 './releases/Plain_Craft_Launcher_dndss_2.15.1_win-x64.exe'
```

自行编译命令见 [仓库 README](../README.md#自行编译)。
