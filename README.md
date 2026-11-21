# MClash

MClash 的**发布仓库**：仅存放编译产物与版本说明，源码不在本仓库。

## 下载

前往 [Releases](https://github.com/Mcloud136/MClash/releases) 下载最新版本。

| 版本 | 文件 | 大小 | SHA256 |
|---|---|---|---|
| v1.0.0 (GA) | `Mclash-1.0.0-win64-setup.exe` | 28,132,159 B | `5fdd9a824bcc3aadbc4d423edc8604aa88bef7db6ee924b17b7466a206d94962` |
| v1.0.0 (GA) | `mclash-core-1.0.0-win64.zip` | 6,306,651 B | `070fc688814f01622b8bf0fec88cef80475ee806f8445db8f4d7996ca2ce6d84` |

## 仓库分工

| 仓库 | 可见性 | 用途 |
|---|---|---|
| `Mcloud136/MClash-source` | 私有 | 完整源码、构建脚本与文档 |
| `Mcloud136/MClash` | 公开 | 发布产物（本仓库） |
| `Mcloud136/v2node-rust` | 公开 | 协议依赖库（tag `v0.2.2`） |

## 构建流程

产物由源码仓库的 `scripts/build-all.ps1` 生成，四阶段：

1. Rust 内核（`crates/client-core` → `client-core.exe`）
2. 组装载荷目录（内核 + wintun + Flutter 资产）
3. Flutter GUI（`gui/` → `Mclash.exe` + `data/`）
4. NSIS 打包（`packaging/flclash.nsi` → 安装包）

## 版本说明

### 1.0.0 (GA) — 2026-11-22

首个 1.0 GA 版本。

- 版本号由 `b0.0.1` 升至 `1.0.0`（Cargo / Flutter / NSIS 全链路统一）
- 恢复应用内自动更新检查（读取本仓库 Releases；API 配额耗尽时用网页 302 兜底）
- 移除右上角 PRE 标记（`appEnv` 默认 `stable`）
- 架构：Windows x64，服务化内核（`MclashCore` 服务 + 命名管道）
- 安装包内置 TUN 驱动（wintun 0.14.1）与 sqlite3 原生库
- 测试：**254 passed / 0 failed / 2 ignored**（real-machine 用例需凭据）
- 构建可复现：纯 clone 零叠加、清空 sqlite3 缓存、不设 `PUB_HOSTED_URL` 时 `BUILD_EXIT=0`

## 内核包说明

`mclash-core-*-win64.zip` 含 `MclashCore.exe`、`wintun.dll` 与 `SHA256SUMS.txt`，供已安装用户单独替换内核排查问题；完整安装请使用 setup 包。

## 许可

第三方组件许可见各组件说明（wintun、sqlite3）。
