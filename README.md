# Plain Craft Launcher (PCL) dndss 修改版

本项目是 [dndss](https://github.com/dndss) 基于 [PCL Community Edition](https://github.com/PCL-Community/PCL-CE) 独立维护的第三方修改版，原始 PCL 作者为龙腾猫跃。此 fork 与 PCL 原作者、PCL Community、Microsoft / Mojang 及 mcauth3 作者无隶属关系，不代表上述项目或作者提供的官方版本、支持或背书。

## 本 fork 的修改

- 撤销上游 [#3673](https://github.com/PCL-Community/PCL-CE/pull/3673) 和 [#3676](https://github.com/PCL-Community/PCL-CE/pull/3676) 引入的区域限制，恢复下载、安装、补全、修复及整合包相关入口。
- 保留 Minecraft 登录失败时的服务响应详情，便于定位 `403 Forbidden`、`Invalid app registration` 等问题。
- 保留 fork `dev` 原有的更新源随机选择修复 [#3684](https://github.com/PCL-Community/PCL-CE/pull/3684)。
- 随附的测试构建使用下方注明来源的公开 Microsoft OAuth Client ID，不新增第三方认证库依赖。

## 下载与使用

- [下载 Windows x64 测试构建](https://github.com/dndss/PCL-CE/releases/download/v2.15.1-dndss.1/Plain_Craft_Launcher_dndss_2.15.1_win-x64.exe)
- [SHA256 校验值](https://github.com/dndss/PCL-CE/releases/download/v2.15.1-dndss.1/SHA256SUMS.txt)
- [Release 说明](https://github.com/dndss/PCL-CE/releases/tag/v2.15.1-dndss.1) · [构建与验证记录](https://github.com/dndss/PCL-CE/releases/download/v2.15.1-dndss.1/build-info.json)

EXE、校验值和构建记录作为 GitHub Releases 附件发布，源码分支不再存放构建产物。此版本标记为测试版（Pre-release）。

需要 Windows 10 1809 或更高版本及 [.NET 10 Desktop Runtime x64](https://get.dot.net/10)。关闭旧启动器后，将 EXE 放入原启动器所在目录使用。切换 Client ID 后可能需要重新进行微软登录，无需预先删除账号记录或配置。

本 fork 的问题请在 [dndss/PCL-CE](https://github.com/dndss/PCL-CE) 下反馈，并注明具体构建；本修改版的可用性和支持范围不沿用下方上游简介中的支持承诺。

## 声明

- 本修改版保留原项目的署名、许可证及版权信息；`Plain Craft Launcher 2/` 与其他目录的许可范围见下方许可证说明。
- 移除的是启动器中的区域功能限制；微软账号认证、Minecraft 游戏所有权检查和服务器的正版验证保持原有流程。使用正版登录仍需你自己的账号和有效游戏资格。
- 随附构建仅写入公开的应用 Client ID 和源码提交标识，不包含开发者或用户的账号密码、Access Token、Refresh Token，也不包含 PCL Community 的私有构建配置。
- 当前 Client ID 为 `4a07b708-b86d-4365-a55f-f4f23ecb85ab`。它是应用标识，不是玩家的登录凭证；服务访问权限、限流、审核与长期可用性由相关服务提供方决定。
- 目前只验证该 ID 可以获取微软设备登录验证码，尚未完成此 ID 下的完整账号登录、Minecraft 服务授权和游戏启动验证，不保证能够解决所有 `403` 错误。
- CurseForge、Natayark 等其他依赖私有服务配置的功能，可能无法在此构建中正常使用。

## 感谢

感谢龙腾猫跃、[PCL Community](https://github.com/PCL-Community/PCL-CE) 及原项目贡献者提供的代码与维护工作。

特别感谢 [GongSunFangYun/mcauth3](https://github.com/GongSunFangYun/mcauth3) 提供公开的 Microsoft / Xbox / Minecraft 认证实现资料和默认 Client ID。本构建使用了其公开默认 ID；没有集成、打包或复制该项目的 Python 认证库。来源可查看 [mcauth3 源码](https://github.com/GongSunFangYun/mcauth3/blob/151ebf185241d8a93d02a8c8d027627e04f7adf2/src/mcauth3/mcauth3.py#L19) 及其 [MIT 许可证](https://github.com/GongSunFangYun/mcauth3/blob/151ebf185241d8a93d02a8c8d027627e04f7adf2/LICENSE)。上述致谢不代表 mcauth3 作者为本 fork 提供支持或背书。

## 自行编译

安装 .NET 10 SDK，在仓库根目录打开新的 PowerShell 会话后执行：

```powershell
$env:PCL_WRITE_SECRET = '1'
$env:PCL_MS_CLIENT_ID = '4a07b708-b86d-4365-a55f-f4f23ecb85ab'
$env:PCL_GITHUB_SHA = (git rev-parse HEAD).Trim()

dotnet clean 'Plain Craft Launcher 2/Plain Craft Launcher 2.csproj' -c Release -p:Platform=x64
dotnet publish 'Plain Craft Launcher 2/Plain Craft Launcher 2.csproj' -p:Configuration=Release -p:Platform=x64 -p:UseSharedCompilation=false -o './artifacts/local-x64' --no-self-contained
```

源生成器会读取 `PCL_` 开头的构建环境变量；仅配置你明确希望写入 EXE 的值。也可替换为自己注册且获相关服务认可的 Client ID。使用已有 SDK 进程时，清理构建并关闭共享编译可以避免沿用旧的生成配置。

---

以下保留上游项目简介、原作者和社区链接。English / 繁體中文 README 为上游文档，尚未翻译本 fork 的说明。

**简体中文** | [English](README-EN.md) | [繁體中文](README-ZH_TW.md)

<div align="center">

<img src="Plain Craft Launcher 2/Images/icon.ico" alt="Logo" width="80" height="80">

## 上游 PCL Community Edition

[![Stars](https://img.shields.io/github/stars/PCL-Community/PCL-CE?style=for-the-badge&logo=data:image/svg%2bxml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZlcnNpb249IjEiIHdpZHRoPSIxNiIgaGVpZ2h0PSIxNiI+PHBhdGggZD0iTTggLjI1YS43NS43NSAwIDAgMSAuNjczLjQxOGwxLjg4MiAzLjgxNSA0LjIxLjYxMmEuNzUuNzUgMCAwIDEgLjQxNiAxLjI3OWwtMy4wNDYgMi45Ny43MTkgNC4xOTJhLjc1MS43NTEgMCAwIDEtMS4wODguNzkxTDggMTIuMzQ3bC0zLjc2NiAxLjk4YS43NS43NSAwIDAgMS0xLjA4OC0uNzlsLjcyLTQuMTk0TC44MTggNi4zNzRhLjc1Ljc1IDAgMCAxIC40MTYtMS4yOGw0LjIxLS42MTFMNy4zMjcuNjY4QS43NS43NSAwIDAgMSA4IC4yNVoiIGZpbGw9IiNlYWM1NGYiLz48L3N2Zz4=&logoSize=auto&label=stars&labelColor=444444&color=eac54f)](https://github.com/PCL-Community/PCL-CE/)
![GitHub Release](https://img.shields.io/github/v/release/PCL-Community/PCL-CE?label=release&logo=github&style=for-the-badge)
![GitHub Actions Workflow Status](https://img.shields.io/github/actions/workflow/status/PCL-Community/PCL-CE/build-test.yml?style=for-the-badge)

[![Issues](https://img.shields.io/github/issues/PCL-Community/PCL-CE?style=for-the-badge&label=issues&labelColor=444444&color=1F883D&logo=github)](https://github.com/PCL-Community/PCL-CE/issues)
[![Pull requests](https://img.shields.io/github/issues-pr/PCL-Community/PCL-CE?style=for-the-badge&label=pull%20requests&labelColor=444444&color=1F883D&logo=github)](https://github.com/PCL-Community/PCL-CE/pulls)
![GitHub Downloads (all assets, all releases)](https://img.shields.io/github/downloads/PCL-Community/PCL-CE/total?style=for-the-badge)
[![哔哩哔哩](https://img.shields.io/badge/动态-bilibili-00A4DB?style=for-the-badge&labelColor=444444&logo=bilibili)](https://space.bilibili.com/3546847192811755/dynamic) <br />

<a href="https://trendshift.io/repositories/21800?utm_source=trendshift-badge&amp;utm_medium=badge&amp;utm_campaign=badge-trendshift-21800" target="_blank" rel="noopener noreferrer"><img src="https://trendshift.io/api/badge/trendshift/repositories/21800/weekly?language=C%23" alt="PCL-Community%2FPCL-CE | Trendshift" width="250" height="55"/></a>
<a href="https://trendshift.io/repositories/21800" target="_blank" rel="noopener noreferrer"><img src="https://trendshift.io/api/badge/repositories/21800" alt="PCL-Community%2FPCL-CE | Trendshift" style="width: 250px; height: 55px;" width="250" height="55"/></a>

[社区版下载](https://github.com/PCL-Community/PCL-CE/releases/latest) |
[上游存储库](https://github.com/Meloong-Git/PCL)

[提交问题](https://github.com/PCL-Community/PCL-CE/issues/new/choose) |
[贡献指南](https://github.com/PCL-Community/PCL-CE/wiki/开发指南)

</div>

PCL CE 是基于 PCL 开源代码二次开发的社区版本，包括了主线暂未制作的功能和改进！

社区版的版本号与主线并非严格对应关系，也请不要向官方仓库反馈社区版问题。

欢迎大家来用用看！

**开发群:** [599620549](https://qm.qq.com/q/PNQA4Md8wc)[✦](https://t.me/+78XW2bUOvKJjMTZl) | **用户 1 群:** [1028074835](https://qm.qq.com/q/qrMGJo8BQQ) | **用户 2 群:** [1070029541](https://qm.qq.com/q/lBywbDMWhG)

## 💻 支持平台

| 操作系统 | 支持情况 | 环境要求 |
|---|---|---|
| Windows 10 1809 (17763) 或更高 | ✅ 完整支持 | [.NET 10 Desktop Runtime](https://get.dot.net/10) |
| Windows 8 - Windows 10 1809 (17763) | ⚠️ 理论能跑，酌情提供社区支持 | [.NET 10 Desktop Runtime](https://get.dot.net/10) |
| Windows 7 或更低版本 | ❌ 不支持 | / |
| macOS / Linux / 其他操作系统 | ⚠️ 仅跨平台开发支持（交叉编译） | [.NET 10 SDK](https://get.dot.net/10) |

**✅ 完整支持**：尽可能提供一切相关支持，但必须确保启动器为最新版本。

**⚠️ 理论能跑，酌情提供社区支持**：PCL CE 应该可以在这些平台上运行，但不保证功能完全可用。你可能需要升级到完整支持的系统版本以获得进一步社区技术支持。

**❌ 不支持**：PCL CE 在这些平台的可用性较低，甚至压根打不开。请升级操作系统以使用 PCL CE。

**⚠️ 仅跨平台开发支持（交叉编译）**：PCL CE 的源代码可以在 macOS 与 Linux 平台编译，但无法直接运行。作为开发者，你可以在这些平台上进行开发，然后将编译产物转移到 Windows 系统测试。

**注**：    
社区仅对最新版本的启动器提供支持。    
取决于部分问题的特殊性（如系统不完整），有时你仍然必须升级操作系统以继续获得支持。    
PCL CE 始终建议使用最新版本的操作系统以获得最佳体验。    
你仍然可以尝试在不受支持的系统上使用 PCL CE，但可能会遇到很多额外问题。

## 🔒 许可证

- `Plain Craft Launcher 2/` 使用 [自定义许可证](https://github.com/PCL-Community/PCL-CE/blob/dev/Plain%20Craft%20Launcher%202/LICENCE)
- `其余所有目录` 使用 [Apache License 2.0](https://github.com/PCL-Community/PCL-CE/blob/dev/LICENSE)

## 🌟 统计数据
![Alt](https://repobeats.axiom.co/api/embed/3e46296e6e3a134991a783480fd2f62723bb0353.svg "Repobeats analytics image")

[![Star History Chart](https://api.star-history.com/chart?repos=PCL-Community/PCL-CE&type=date&legend=top-left&sealed_token=Ts-GaAXJ5nb9fJERusrXneo05pfZ83tMhReHJ98nmmlemBTqHS5Ozocdep1MTMdsX-6CRiQH9TqiS1Kk7SxjTfk02eUOxnm25oHff6TLLvrY7pGujOkU1IwjVFQLE-5GJYogutJAyI78jujBlOnpk3J2OKAY1PBhmkyUOzW1C1sdz5BzPbj2eBbJGvDx)](https://www.star-history.com/?repos=PCL-Community%2FPCL-CE&type=date&legend=top-left)

**此页浏览量**（总计 / 今日）：[![Hits](https://hits.zkitefly.eu.org/?tag=https://github.com/PCL-Community/PCL-CE)](https://hits.zkitefly.eu.org/?tag=https://github.com/PCL-Community/PCL-CE&web=true)
## ❤️ 贡献者

[![](https://contrib.rocks/image?repo=PCL-Community/PCL-CE)](https://github.com/PCL-Community/PCL-CE/graphs/contributors)
