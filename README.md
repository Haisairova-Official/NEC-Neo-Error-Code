# 🧩 Neo Exit Code Specification

### 简介 / Introduction
**Neo Exit Code（NEC）** 是一种统一的错误与退出码标准，旨在为系统、守护进程、驱动及应用层程序提供一致且可扩展的错误编码体系。  
It provides a unified, structured standard for error and exit codes across systems, daemons, drivers, and applications.

![Version](https://img.shields.io/badge/Version-0.0.1-red.svg)  
![License](https://img.shields.io/badge/License-MIT-green.svg)

---

## 🧱 格式 / Format
```
0xVVLSDDDD
```

| 字段 / Field | 长度 / Length | 说明 / Description |
|---------------|---------------|--------------------|
| `VV` | 2位 / 2 digits | 版本号（Version）当前版本为 `00`（正式发布后为 `01`） |
| `L` | 1位 / 1 digit | 层级（Layer）表示错误抛出层 |
| `S` | 1位 / 1 digit | 来源（Source）表示错误来源模块 |
| `CC` | 2位 / 2 digits | 错误类型与等级（Category & Severity） |
| `DD` | 2位 / 2 digits | 定义码（Definition），由标准或厂商自定义 |

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
| 6 | 硬件故障 / Hardware Failure |
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

## ⚠️ 错误类型与等级定义 / Category & Severity Definitions

错误类型（前1位） / Error Category (first digit):

| 值 / Value | 类型 / Type | 说明 / Description |
|-------------|-------------|--------------------|
| 0 | Exit | 程序主动退出（正常/异常） |
| 1 | Hang | 程序无响应或阻塞 |
| 2 | Lockdown | 系统或安全策略强制终止 |
| 3 | Fault | 常规运行时错误 |
| 4 | Crash | 程序或进程崩溃 |
| 5 | Recover | 自动恢复事件 |
| F | Unknown | 未定义类型 |

错误等级（后1位） / Severity Level (second digit):

| 值 / Value | 等级 / Level | 说明 / Description |
|-------------|--------------|--------------------|
| 0 | Info | 信息，仅记录 |
| 1 | Warning | 警告，可恢复 |
| 2 | Error | 错误，需要处理 |
| 3 | Critical | 严重错误，程序终止 |
| F | Unknown | 未知等级 |


---

## 📘 示例 / Example

```
0x01462320
```

- **VV** = `01` → 版本号01 / Version 1  
- **L** = `4` → 应用层 / Application Layer  
- **S** = `6` → 系统调用 / System Call  
- **CC** = `23` → 类型为 Crash，等级为 Critical  
- **DD** = `20` → 定义为“主线程意外退出导致程序失败”  

**含义 / Meaning**：应用层在系统调用阶段因主线程崩溃（Critical Crash）而失败。

---

## 🧩 扩展性 / Extensibility

- 版本号可向后兼容。
- 预留 `CCDD` 范围供厂商定义。
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
| 当前版本 | 0.0.1.251002 |
| 文件版本 | v01 |
| 作者 / Author | https://github.com/Haisairova-Official |
| 许可证 / License | MIT |
| 仓库地址 / Repository | https://github.com/Haisairova-Official/NEC-Neo-Error-Code |

---
