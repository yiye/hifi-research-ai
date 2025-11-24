# Cursor Rules 说明

本目录包含了 Hi-Fi 研究项目的专项 Cursor AI 规则。这些规则会自动帮助 AI 理解音频工程的专业标准，并在代码和文档编写时提供指导。

## 规则文件列表

### 📌 核心规则

#### hifi-expert-persona.mdc ⭐
**全局应用** | 将 AI 设定为专业 Hi-Fi 音频专家

---

### 📋 专项规则

#### 1. audio-device-validation.mdc
**作用范围**: `**/*device*.{ts,js,json}`, `**/*spec*.{ts,js,json}`, `**/data/**/*.{ts,js,json}`

**用途**:
- 音频设备数据的验证规则
- 参数数值范围检查（采样率、位深度、THD、SNR 等）
- 单位标准化要求
- 数据完整性保证
- TypeScript 类型定义

**何时触发**:
当你编辑设备数据文件、规格文件或 data 目录下的文件时，此规则会自动应用。

**示例**:
```typescript
// ✅ 符合规范
const device = {
  specs: {
    sampleRate: { max: 768000, unit: 'Hz' },
    thd: { value: 0.0005, unit: '%', condition: '1kHz, -1dBFS, 32Ω' }
  }
};

// ❌ 不符合规范
const badDevice = {
  specs: {
    sampleRate: "768k",  // 应使用数值
    thd: 0.05           // 缺少单位和测试条件
  }
};
```

---

#### 2. measurement-data.mdc
**作用范围**: `**/*measurement*.{ts,js,py}`, `**/*test*.{ts,js,py}`, `**/*analysis*.{ts,js,py}`

**用途**:
- 音频测量标准和协议（AES17、IEC 61606-3）
- 标准测试信号定义
- THD+N、频率响应、SNR、IMD 测量规范
- 数据采集和处理标准
- 测量报告格式

**何时触发**:
当你编写测量数据处理、测试脚本或分析代码时，此规则会自动应用。

**示例**:
```python
# 标准 THD+N 测量
def measure_thd_n(
    frequency: int = 1000,      # Hz
    amplitude: float = -1.0,     # dBFS
    load: int = 32,              # Ω
    duration: float = 1.0        # seconds
) -> dict:
    """
    遵循 AES17 标准的 THD+N 测量
    """
    pass
```

---

#### 3. review-template.mdc
**作用范围**: `**/*review*.{md,mdx}`, `**/*evaluation*.{md,mdx}`, `**/articles/**/*.{md,mdx}`, `**/reviews/**/*.{md,mdx}`

**用途**:
- 完整的设备评测文章结构模板
- 10 个标准章节（概述、外观、规格、听感、测量、搭配、体验、对比、总结、购买建议）
- 主观听感描述规范
- 客观测量数据展示格式
- 写作风格和专业性要求

**何时触发**:
当你编写评测文章或评价类 Markdown 文档时，此规则会自动应用。

**示例结构**:
```markdown
# [品牌] [型号] 评测

## 快速信息
- 设备类型、价格、定位

## 外观与设计
- 包装、外观、接口、做工

## 技术规格
- 核心芯片、性能参数表格

## 主观听感
- 测试系统、音色、分频段听感、综合表现

## 客观测量
- 频响曲线、THD+N、输出功率等

## 优缺点总结
## 购买建议
```

---

#### 4. database-schema.mdc
**作用范围**: `**/*schema*.{ts,js,sql}`, `**/*model*.{ts,js}`, `**/database/**/*.{ts,js,sql}`, `**/prisma/**/*.prisma`

**用途**:
- 完整的数据库表结构设计
- 核心表：devices、device_specifications、device_connectivity、price_history、measurements、subjective_reviews
- TypeScript / Prisma 类型定义
- SQL 查询示例
- 数据完整性约束和索引策略

**何时触发**:
当你编写数据库模型、Schema 文件或数据库相关代码时，此规则会自动应用。

**示例**:
```typescript
export interface Device {
  id: string;
  deviceType: DeviceType;
  manufacturer: string;
  model: string;
  specifications: DeviceSpecification;
  connectivity: Connectivity[];
  pricing: PriceHistory[];
}
```

---

## 如何使用这些规则

### 核心规则的作用
**hifi-expert-persona.mdc** 始终生效，让 AI 以 Hi-Fi 专家的身份与你交流：
- 💬 回答更专业、准确
- 📊 自动解读音频参数
- 🎯 提供实用的搭配建议
- ⚠️ 及时给出安全提醒

### 专项规则的应用

专项规则会根据文件的 glob 模式自动应用。例如：
- 编辑 `src/data/devices/dac-001.json` → `audio-device-validation.mdc` 自动生效
- 编辑 `scripts/measurement/thd-analysis.py` → `measurement-data.mdc` 自动生效
- 编辑 `reviews/dac-review.md` → `review-template.mdc` 自动生效

### 手动引用
你也可以在 Chat 中通过 `@` 符号手动引用规则：
```
@audio-device-validation.mdc 帮我验证这个设备数据是否符合规范
```

### 规则协同工作
项目中的规则按层次协同工作：
1. **hifi-expert-persona.mdc** (核心规则) - 定义 AI 专家角色和回答风格
2. **AGENTS.md** (项目主规则) - 提供音频术语、编码规范、文档标准
3. **专项规则** (4个场景规则) - 提供特定场景的详细规范

**比喻**: 
- 核心规则 = AI 的"职业身份"（Hi-Fi 专家）
- AGENTS.md = 项目的"行业标准"（音频工程规范）
- 专项规则 = 具体的"工作流程"（如何验证数据、编写评测）

## 规则优先级

当多个规则同时生效时，优先级为：
1. **Team Rules**（团队规则，如有）
2. **hifi-expert-persona.mdc** (核心角色规则，始终应用)
3. **专项 Project Rules**（本目录的其他 .mdc 文件）
4. **AGENTS.md**（项目主规则）
5. **User Rules**（个人全局规则）

**注意**: 所有规则会合并应用，较早来源的指导优先。

## 修改规则

如果需要调整规则：
1. 直接编辑对应的 `.mdc` 文件
2. 修改文件头部的 `globs` 来改变作用范围
3. 修改 `alwaysApply` 为 `true` 可让规则始终应用（不推荐，会增加 token 消耗）

## 最佳实践

### ✅ 推荐做法

**使用核心规则**:
- 💬 在对话中直接询问 Hi-Fi 相关问题，AI 会以专家身份回答
- 🎯 让 AI 帮你分析设备参数、推荐搭配方案
- 📊 请 AI 解读测量数据和频响曲线

**使用专项规则**:
- 让规则自动应用，无需手动 @ 引用
- 编辑对应类型的文件时，规则会自动生效
- 必要时可通过 @ 手动引用特定规则

**维护规则**:
- 规则内容保持在 500 行以内（核心规则例外）
- 提供具体示例而非抽象描述
- 定期更新规则以反映最新标准
- 根据实际使用体验优化规则

### ❌ 避免做法

- 不要在规则中包含过时的信息
- 避免规则间的冲突和重复
- 不要让所有规则都 `alwaysApply: true`（只有核心角色规则应该始终应用）
- 不要在规则中硬编码具体的设备型号（应在数据文件中管理）

## 贡献

如果你发现规则有误或需要补充，欢迎：
1. 直接修改 `.mdc` 文件
2. 提交 Pull Request 并说明修改原因
3. 在 Issues 中讨论规则的改进建议

