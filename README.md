# MClash

MClash 的**发布仓库**：仅存放编译产物与版本说明，源码不在本仓库。

## 下载

前往 [Releases](https://github.com/Mcloud136/MClash/releases) 下载最新安装包。

| 版本 | 文件 | 大小 | SHA256 |
|---|---|---|---|
| b0.0.1 (GA) | `Mclash-b0.0.1-win64-setup.exe` | 28,157,629 B | `7b405aeb2f4d6c9282741406f81311ed10fb96a96fd7b4cc05521ada5c43b799` |
| b0.0.1 (GA) | `mclash-core-b0.0.1-win64.zip` | 5,834,838 B | `55cdba01b7af3aad3d81dee8e9abc7404d0de45b6b51693e0dbc2ed9532b5833` |

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

### b0.0.1 (GA)

首个 GA（General Availability）版本。

- 恢复应用内自动更新检查（读取本仓库 Releases）
- 移除右上角 PRE 标记（`appEnv` 默认 `stable`）
- 架构：Windows x64，服务化内核（`MclashCore` 服务 + 命名管道）
- 安装包内置 TUN 驱动（wintun）与 sqlite3 原生库
- 构建可复现：纯 clone 零叠加、清空 sqlite3 缓存、不设 `PUB_HOSTED_URL` 时 `BUILD_EXIT=0`
- 测试：254 passed / 0 failed / 2 ignored（real-machine 用例需凭据）

## 许可

第三方组件许可见各组件说明（wintun、sqlite3）。
