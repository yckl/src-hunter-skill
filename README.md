# 🎯 src-hunter: 工业级自动化 SRC 漏洞挖掘与渗透测试 Claude Skill
### Automated Bug Bounty & Vulnerability Hunting Skill for Claude Code (Recon to CVSS 4.0 Report)

<p align="center">
  <img src="https://img.shields.io/badge/Claude%20Code-Skill%20Plugin-blueviolet.svg?style=flat-square&logo=anthropic" alt="Claude Code Skill" />
  <img src="https://img.shields.io/badge/Playbooks-19%20Categories-brightgreen.svg?style=flat-square" alt="Playbooks" />
  <img src="https://img.shields.io/badge/Structured%20Payloads-305+-orange.svg?style=flat-square" alt="Payloads" />
  <img src="https://img.shields.io/badge/HackerOne%20Cases-2887%20Real%20Reports-red.svg?style=flat-square" alt="HackerOne Reports" />
  <img src="https://img.shields.io/badge/MCP-jshookmcp%20Integrated-blue.svg?style=flat-square" alt="MCP" />
  <img src="https://img.shields.io/badge/Standard-CVSS%204.0-yellow.svg?style=flat-square" alt="CVSS 4.0" />
  <img src="https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square" alt="License" />
</p>

<p align="center">
  <a href="README.md"><strong>中文文档</strong></a> · <a href="README.en.md"><strong>English Documentation</strong></a>
</p>

---

## 📌 项目概述 (Executive Summary)

**src-hunter** 是一款专为**企业安全应急响应中心（SRC）、众测与 Bug Bounty 赏金猎人**量身打造的**工业级自动化漏洞挖掘 Claude Code 专属技能插件（Skill）**。

传统漏洞挖掘往往面临“测试思维发散遗漏关键攻击面、工具零散协同成本高、发现漏洞后影响定级低、漏洞报告不合规容易被驳回”等痛点。

本项目将资深白帽黑客的实战攻防经验深度工程化，规范了标准的 **`intake（范围评估）➔ recon（资产指纹搜集）➔ enum（攻击面枚举）➔ hunt（纵深漏洞挖掘）➔ report（合规报告沉淀）`** 五阶段标准化漏掘流水线。内置了 **19 大类攻击 Playbook**、**2887 份真实披露的 HackerOne 高危案例库**，并打通了本地 **MCP（Model Context Protocol）工具层**，实现让 AI 助手直接驱动底层工具完成自动化探测与高价值漏洞归档。

---

## 🏛️ 五阶段全流程渗透体系 (5-Stage Methodology)

```
┌────────────────────────────────────────────────────────────────────────┐
│                        SRC 漏洞挖掘全生命周期流水线                    │
├────────────────────────────────────────────────────────────────────────┤
│ [1. Intake 边界测绘]   - 确定测试边界与排除清单 (Wildcard / In-Scope)  │
│                        - 严守授权红线，规避生产业务破坏与敏感操作      │
├────────────────────────────────────────────────────────────────────────┤
│ [2. Recon 资产情报]   - 泛解析/子域名枚举，CDN/WAF 指纹识别与绕过方案 │
│                        - 国产常见中间件/框架 (Spring/Shiro/ThinkPHP) 探查│
├────────────────────────────────────────────────────────────────────────┤
│ [3. Enum 接口细化]    - JS 接口逆向与隐藏 API 提取 (Sourcemap 重构)   │
│                        - 未授权路由探针、Actuator 暴露面、Swagger 嗅探 │
├────────────────────────────────────────────────────────────────────────┤
│ [4. Hunt 深度渗透]    - 19 类专项攻防 Playbook 场景化攻击             │
│                        - 305+ 结构化 Payload 与 263+ WAF/EDR 绕过变体  │
│                        - 调用 MCP 本地工具链 (动态 Hook/反混淆/内存验证)│
├────────────────────────────────────────────────────────────────────────┤
│ [5. Report 标准交付]  - CVSS 4.0 漏洞评分与危害边界定级 (Impact Scale)│
│                        - 完整复现 PoC、HTTP 报文重放、防御加固建议模板 │
└────────────────────────────────────────────────────────────────────────┘
```

---

## 💡 核心知识库与工程亮点 (Knowledge Base & Innovations)

### 1. 2887+ 篇真实 HackerOne 漏洞报告智库 (`references/h1-reports/`)
* 涵盖近年来在 HackerOne 公开披露的高危与严重漏洞实战样本。
* 按 CWE 缺陷类型精细分组索引（IDOR、RCE、SSRF、SQLi、OAuth/SAML、Logic Flaws 等），支持根据当前测试接口特征秒级检索相似历史案例与绕过灵感。

### 2. 黑盒实战导向的 19 类漏洞利用手册 (`references/playbooks/`)
每个 Playbook 均遵循标准化攻防问题链：
* **入口定位**：目标资产哪些参数/Header 易受此类漏洞影响？
* **Payload 矩阵**：如何使用最精炼的测试载荷验证脆弱性？
* **响应特征捕获**：返回什么状态码、回显或时延可确认为有效漏洞？
* **影响放大策略**：如何从普通信息泄露平滑延伸到高危权限接管？
* **合规与红线规范**：明确禁止可能导致线上服务拒绝服务（DoS）或数据破坏的动作。

### 3. 本地 MCP 工具层集成与自动化调用 (`references/tools/mcp-jshook.md`)
本 Skill 原生集成本地 MCP 服务器作为工具层，使得 Claude 在 Hunt 阶段能够自主调用底层能力：
* **浏览器自动化与 CDP 调试**：真实无头浏览器网络请求捕获、DOM 变动监听；
* **JS 逆向与动态 Hook**：前端加解密算法自动定位、AST 语法反混淆；
* **移动端辅助**：Android adb 桥接、Frida 内存校验、SSL Pinning 证书绑定动态绕过。

---

## 🧩 漏洞类型与案例覆盖矩阵 (Playbook Matrix)

| 漏洞分类 / Playbook | 典型攻击面与测试核心 | 关联真实案例数 |
| :--- | :--- | :---: |
| **`arbitrary-x-authz`** | IDOR 越权访问、任意账号重置、垂直/水平提权、Session 劫持 | **465+** |
| **`rce`** | 框架漏洞、远程代码执行、SSTI 模板注入、XXE 实体注入、反序列化 | **385+** |
| **`xss`** | 存储型 XSS、DOM-based XSS、富文本过滤绕过、WAF 规则变异 | **335+** |
| **`ssrf-cache-host`** | 云元数据访问（AWS/Aliyun）、内网穿透探测、Host 头注入、CDN 缓存投毒 | **280+** |
| **`logic-flaws`** | 支付金额篡改、并发条件竞争（Race Condition）、验证码复用爆破 | **240+** |
| **`oauth-saml-jwt`** | OAuth 回调劫持、SAML 伪造响应、JWT 签名降级与秘钥弱口令爆破 | **190+** |
| **`api-rest`** | REST API 越权批量抓取、GraphQL 内省查询与批量 Dos、WebSocket 渗透 | **175+** |
| **`path-traversal`** | 目录穿越、任意文件读取、LFI/RFI 本地包含与日志投毒 RCE | **150+** |
| **`file-upload`** | 任意文件上传、后缀截断解析、解压缩目录穿越（Zip Slip） | **140+** |
| **`llm-prompt-injection`**| 大模型 Prompt 越狱注入、RAG 知识库间接投毒、Agent 工具权限盗用 | **新前沿** |

---

## 🛠️ 安装与使用指南 (Installation & Usage)

### 方式一：作为 Claude Code 插件全局安装 (推荐)
```bash
# 添加到插件市场源
/plugin marketplace add yckl/src-hunter-skill

# 安装并启用该技能
/plugin install src-hunter@src-hunter
```

---

### 方式二：通过 Git 本地克隆挂载
```bash
git clone https://github.com/yckl/src-hunter-skill.git ~/.claude/skills/src-hunter
```

---

## 💬 触发与唤起方式 (How to Use)

本 Skill 支持**显式指令调用**与**语义意图自动唤起**：

#### 1. 显式指令执行
```text
/src-hunter https://target-domain.com
```

#### 2. 自然语言交互触发
当你在 Claude Code 中提及以下关键词或类似需求时，系统会自动加载并编排对应的 Playbook：
* *“针对 target.com 进行一次资产指纹识别与漏洞排查”*
* *“帮我设计绕过当前 Cloudflare/Imperva WAF 的 SQLi / XSS Payload”*
* *“发现了重置密码接口，帮我分析可能存在的逻辑越权漏洞”*
* *“生成符合 CVSS 4.0 国际标准的漏洞提交报告”*

---

## 📂 知识库工程目录结构 (Knowledge Base Structure)

```text
src-hunter-skill/
├── references/
│   ├── methodology/                      # 五阶段攻防方法论、优先级排序与红线守则
│   ├── playbooks/                        # 19 大类黑盒漏洞专项攻防操作指南
│   │   ├── arbitrary-x-authz.md          # 越权与身份认证
│   │   ├── rce/                          # 远程代码执行全链路
│   │   ├── xss/                          # XSS 攻防与绕过
│   │   ├── ssrf-cache-host/              # SSRF 与云资产漏洞
│   │   └── llm-prompt-injection/         # AI 智能体专项攻击
│   ├── h1-reports/                       # 2887 份真实 HackerOne 披露报告 (按缺陷分类)
│   ├── payloader/                        # 305+ 结构化 Payload 与 WAF 绕过规则库
│   ├── dictionaries/                     # 常见中间件、国产企业组件默认凭据与指纹
│   └── templates/                        # CVSS 4.0 标准漏洞提报模板
├── .claude-plugin/                       # 插件元信息与技能注册清单
├── SKILL.md                              # Claude Code 核心技能定义入口
└── README.md                             # 工业级项目使用说明
```

---

## ⚖️ 免责声明 (Legal & Compliance)

* 本项目提供的攻防知识库、测试 Payload 及报告模板**仅供具备合法授权的安全测试、网络安全教学与防御加固研究使用**。
* 严禁利用本项目涉及的任何技术与工具对未经书面授权的目标发起网络攻击。因使用不当导致的一切法律责任与直接/间接损失由使用者自行承担。
