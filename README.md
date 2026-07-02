## Hugo: Current Status & Roadmap
**Version**: 0.0.1 (Pre-Alpha)  
**Codename**: Genesis  
**Status**: 🟢 Design Frozen

---

### 一、当前进度总览 (Current State)

| 模块 | 状态 | 完成度 | 备注 |
| :--- | :--- | :--- | :--- |
| **Naming** | ✅ Done | 100% | 已更名为 **Hugo** |
| **Philosophy** | ✅ Done | 100% | AI-Native, State Transition |
| **Protocol** | ✅ Done | 90% | WS + Agit 兼容架构已定 |
| **Core Logic** | 🟡 Pending | 0% | 未开始编码 |
| **Storage** | 🟡 Pending | 0% | 双哈希方案待实现 |

---

### 二、冻结设计清单 (Immutable Decisions)

在开始写第一行代码前，请确保团队对以下 **不可变设计** 达成一致。这是 Hugo 的灵魂：

1.  **[✅] 传输层**：**WebSocket 是一等公民**。HTTP/SSH 仅作为 Fallback 存在。
2.  **[✅] 分支模型**：**Mirror Branch**。没有 `git checkout`，只有 `hugo occupy`。
3.  **[✅] 提交模型**：**Mini Commit**。不存储快照，存储推理步骤。
4.  **[✅] 哈希策略**：**Dual-Hash (BLAKE3 + SHA1)**。SHA1 用于兼容，BLAKE3 用于溯源。
5.  **[✅] 协作模式**：**声明式原子占领**。不允许多 Agent 同时写入同一路径。
6.  **[✅] 用户界面**：**无 TUI**。CLI 仅返回 JSON，交互交给 Web UI 或 IDE。

---

### 三、分阶段实施路线图 (Phased Roadmap)

为了防止项目过于庞大导致难产，建议按以下顺序推进：

#### Phase 0: Bootstrap (Week 1-2)
**目标**：跑通一个最简单的 Hugo 服务端，能通过 WS 接收数据。
- [ ] **Task 0.1**: 定义 `hugo proto` (Protobuf 消息结构)。
- [ ] **Task 0.2**: 实现 WS 握手与心跳。
- [ ] **Task 0.3**: 实现 Agit 适配层的最小接口（能识别 Hugo 的特殊请求）。

#### Phase 1: The Core Engine (Week 3-5)
**目标**：实现“状态转换”的核心逻辑。
- [ ] **Task 1.1**: **Mirror Branch Service**。实现 `occupy` / `release` 锁机制。
- [ ] **Task 1.2**: **Dual-Hash Storage**。实现对象存储，同时计算 SHA1 和 BLAKE3。
- [ ] **Task 1.3**: **Mini Commit Logger**。记录每一次写入的意图和模型 ID。

#### Phase 2: Low-Bandwidth Optimization (Week 6-7)
**目标**：兑现“弱网克隆”的承诺。
- [ ] **Task 2.1**: **Metadata-First Sync**。优先传输 Tree 和 Commit，Blob 延后。
- [ ] **Task 2.2**: **Zstd Streaming**。在 WS 连接中实现流式压缩传输。

#### Phase 3: Cross-Repo & Audit (Week 8+)
**目标**：实现 AI 审计能力。
- [ ] **Task 3.1**: **Global DAG**。建立跨仓库的对象引用图。
- [ ] **Task 3.2**: **Audit CLI**。实现 `hugo audit` 命令，能追溯代码来源。
