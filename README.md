# linux-kernel-gxde

GXDE OS 的 Linux 内核元包（meta package）源码仓库，用于按「内核线 + 架构」一键安装配套的内核镜像与头文件。


## 这是什么

本仓库**不包含内核源码、配置或补丁**，只提供一组 Debian 元包。每个元包通过 `Depends` 固定依赖配套版本的 `linux-image-*` 和 `linux-headers-*`（`-gxde-desktop` 系列），作用是：

- 让内核镜像与头文件成对安装，方便 DKMS、显卡驱动等外部模块编译；
- 把「装哪个内核」抽象成一个稳定的包名，升级内核时只需更新依赖版本；
- 让不同内核线（稳定 / 旧稳定 / 测试）可以分别安装和切换。

各内核线实际依赖的内核版本以 [`debian/control`](debian/control) 中的 `Depends` 为准；内核二进制包由 GXDE 软件源提供，因此安装前需要已配置好 GXDE 源。

## 内核线

| 内核线 | 包名前缀 / 包名 | 说明 |
| --- | --- | --- |
| 稳定（stable） | `linux-kernel-gxde-<arch>` | 默认推荐使用的内核 |
| 旧稳定（oldstable） | `linux-kernel-oldstable-gxde-<arch>` | 旧稳定分支，兼容性优先 |
| 测试（testing） | `linux-kernel-testing-gxde-<arch>` | 新特性验证用，不建议生产环境使用 |
| 专用 | `linux-kernel-pangu-m900-arm64` | 盘古 M900 平台，额外依赖 `gxde-disable-security-boot` |

## 支持的架构

`<arch>` 可取以下值：

| 架构 | 稳定 | 旧稳定 | 测试 | 包名示例 |
| --- | :---: | :---: | :---: | --- |
| `i386` | ✓ | ✓ | ✓ | `linux-kernel-gxde-i386` |
| `amd64` | ✓ | ✓ | ✓ | `linux-kernel-gxde-amd64` |
| `arm64` | ✓ | ✓ | ✓ | `linux-kernel-gxde-arm64` |
| `loong64` | ✓ | ✓ | ✓ | `linux-kernel-gxde-loong64` |
| `loong64-4k-pagesize` | ✓ | ✓ | ✓ | `linux-kernel-gxde-loong64-4k-pagesize` |
| `riscv64` | ✓ | ✓ | ✓ | `linux-kernel-gxde-riscv64` |

说明：

- `loong64-4k-pagesize` 是 4K 页大小的龙芯版本，适用于使用 box64 等特殊需求的用户。


## 维护者

gfdgd_xi <3025613752@qq.com>
