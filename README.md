# 🧩 Neo Exit Code Specification

### 简介 / Introduction
**Neo Exit Code（NEC）** 是一种统一的错误与退出码标准，旨在为系统、守护进程、驱动及应用层程序提供一致且可扩展的错误编码体系。  
It provides a unified, structured standard for error and exit codes across systems, daemons, drivers, and applications.

---

## 🧱 格式 / Format
```
0xVVLSDDDD
```

| 字段 / Field | 长度 / Length | 说明 / Description |
|---------------|---------------|--------------------|
| `VV` | 2位 / 2 digits | 版本号（Version）当前版本为 `00` 当然还没正式发布。发布后会调到01的。|
| `L` | 1位 / 1 digit | 层级（Layer）表示错误抛出层 |
| `S` | 1位 / 1 digit | 来源（Source）表示错误来源模块 |
| `DDDD` | 4位 / 4 digits | 定义码（Definition），由标准文档或厂商自定义 |

---

## 🧮 层级定义 / Layer Definitions

| 值 / Value | 含义 / Meaning |
|-------------|----------------|
| 0 | 内核级 / Kernel or System Core |
| 1 | 驱动层 / Driver Layer |
| 2 | 守护进程 / Daemon or Watchdog |
| 3 | 外部高权限程序 / External High-Privilege Process |
| 4 | 应用层 / User-Level Application |
| 5 | 低权限脚本 / Low-Privilege Script or Plugin |
| 6 | 无响应 / Hung or Non-responsive Process |
| F | 未知 / Unknown |

---

## ⚙️ 来源定义 / Source Definitions

| 值 / Value | 含义 / Meaning |
|-------------|----------------|
| 0 | 磁盘 / Disk or I/O |
| 1 | 内存 / Memory |
| 2 | CPU / Thread |
| 3 | 用户输入 / User Input |
| 4 | 用户输出 / User Interface / Output |
| 5 | 网络 / Network / Socket |
| 6 | 系统调用 / System Call |
| 7 | 外部依赖 / External Dependency |
| 8 | 环境变量或配置 / Environment / Config |
| F | 未知来源 / Unknown Source |

---

## 📘 示例 / Example

```
0x01260020
```

- **VV** = `01` → 版本号01 / Version Code 01  
- **L** = `2` → 守护进程 / Daemon Layer  
- **S** = `6` → 系统调用 / System Call  
- **DDDD** = `0020` → 定义为 “主线程意外退出导致程序失败”  
- **含义 / Meaning**：在 v1 规范中，守护进程在系统调用阶段因主线程异常退出而失败。

---

## 🧩 扩展性 / Extensibility

- 版本号可向后兼容。
- 预留 `DDDD` 大量范围可用于厂商自定义命名空间。
- 可通过 JSON Schema 注册自定义错误定义。

---

## 🧰 用途 / Usage Scenarios

- 系统错误与守护进程日志统一标识。
- 跨语言错误处理（C / C++ / Python / Rust / Go）。
- 统一退出状态码（与 Unix/Linux 0–255 兼容）。

---

## 🧷 项目信息 / Project Info

| 项目 | 内容 |
|------|------|
| 标准名称 | Neo Exit Code (NEC) |
| 当前版本 | 0.0.0.25101923 |
| 文件版本 | v01 |
| 作者 / Author | https://github.com/Haisairova-Official |
| 许可证 / License | MIT |
| 仓库地址 / Repository | https://github.com/Haisairova-Official/NEC-Neo-Error-Code |

---
