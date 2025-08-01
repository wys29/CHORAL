# CHORAL

| 策略                                          | 输入模态         | 架构核心                         | 时序建模             | 多模态融合方式                                 | 模型是否显式结构建模 | 控制信号输出类型    | 特点                   |
| ------------------------------------------- | ------------ | ---------------------------- | ---------------- | --------------------------------------- | ---------- | ----------- | -------------------- |
| **CHORAL** *(你设计的)*                         | 视觉 + 本体      | 双 Diffuser + Transformer     | ✔（Diffuser有时间维）  | Diffuser 单模态编码 → Transformer 合并         | ❌（结构隐式学习）  | 动作序列或当前动作   | 可学习结构依赖，双臂协调性设计感强    |
| **DP** (Diffusion Policy)                   | 视觉 + 本体      | UNet Diffusion 模型            | ✔（动作序列生成）        | 图像→ResNet，状态→MLP，early fusion or concat | ❌          | 整段动作序列      | 高质量 imitation，适合轨迹控制 |
| **DP3**                                     | 视觉 + 本体      | Diffuser + Plan Decoder      | ✔（层次计划）          | late fusion + condition on goal         | ❌          | 子目标+局部轨迹    | 改进DP，适合长时间任务         |
| **ACT** (Action Chunking with Transformers) | 视觉 + 本体      | 纯 Transformer                | ✔（动作 chunk）      | 图像嵌入+状态token序列+位置编码                     | ❌          | 一组 chunk 动作 | 高效抽象，训练稳定性高          |
| **VLA** (Visuo-Language-Actuator Policy)    | 视觉 + 本体 + 语言 | Perceiver + Transformer      | ✔（perceiver时间融合） | 模态独立编码，Transformer融合                    | ❌          | 动作分布        | 更通用，尤其适配语言条件任务       |
| **Pi0**                                     | 视觉           | Slot Attention + Transformer | ❌（即刻动作）          | Slot Attention聚焦+直接预测                   | ❌          | 当前动作        | 高效感知，无序列生成能力         |
