# Hi-Fi 研究项目

专注于高保真音频设备、应用程序和技术参数的研究与分析平台。

## 项目概述

本项目旨在建立一个全面、专业的 Hi-Fi 音频设备数据库和评测平台，包括：

- 📊 **设备数据库**: 收录各类 Hi-Fi 设备的详细技术规格
- 📈 **客观测量**: 基于专业设备的测量数据和分析
- 🎧 **主观评测**: 专业听感评价和使用体验
- 🔍 **对比分析**: 跨品牌、跨价位的设备对比
- 📚 **知识库**: Hi-Fi 音频相关的技术文档和教程

## 设备类型覆盖

- **数字音源**: DAC、流媒体播放器、数字转盘
- **放大器**: 耳机放大器、前级放大器、后级放大器、合并式放大器
- **换能器**: 头戴式耳机、入耳式耳机(IEM)、音箱
- **线材与配件**: 音频线材、电源处理器等

## Cursor 规则配置

本项目已配置专业的 Cursor AI 规则，确保代码和文档符合音频工程标准：

### 主规则文件
- **AGENTS.md**: 项目级核心规则，包含音频专业术语、编码规范、文档标准

### 专项规则 (.cursor/rules/)
- **audio-device-validation.mdc**: 音频设备数据验证和格式规范
- **measurement-data.mdc**: 音频测量数据处理和分析标准
- **review-template.mdc**: 设备评测文章模板和写作规范
- **database-schema.mdc**: 数据库设计规范

这些规则确保：
- ✅ 使用标准化的音频术语和单位
- ✅ 遵循音频工程测量标准（AES、IEC）
- ✅ 保持数据结构的一致性
- ✅ 生成专业、全面的评测内容

## 技术栈

### 后端
- Node.js / Python
- PostgreSQL（设备数据库）
- RESTful API / GraphQL

### 前端
- React / Next.js
- TypeScript
- Tailwind CSS
- Chart.js / D3.js（数据可视化）

### 数据处理
- Python (numpy, scipy, matplotlib)
- 音频分析库（librosa, soundfile）

### 测试设备
- Audio Precision APx555
- QuantAsylum QA403
- MiniDSP EARS

## 项目结构

```
hifi-research/
├── AGENTS.md                 # AI Agent 主规则
├── .cursor/rules/            # 专项规则
│   ├── audio-device-validation.mdc
│   ├── measurement-data.mdc
│   ├── review-template.mdc
│   └── database-schema.mdc
├── backend/                  # 后端代码
│   ├── api/                  # API 接口
│   ├── database/             # 数据库模型与迁移
│   ├── services/             # 业务逻辑
│   └── utils/                # 工具函数
├── frontend/                 # 前端代码
│   ├── components/           # React 组件
│   ├── pages/                # 页面
│   ├── hooks/                # 自定义 Hooks
│   └── utils/                # 工具函数
├── data/                     # 数据文件
│   ├── devices/              # 设备数据 (JSON)
│   ├── measurements/         # 测量数据
│   └── reviews/              # 评测文章
├── scripts/                  # 脚本工具
│   ├── data-import/          # 数据导入
│   ├── validation/           # 数据验证
│   └── analysis/             # 数据分析
└── docs/                     # 文档
    ├── api/                  # API 文档
    ├── standards/            # 标准与规范
    └── guides/               # 使用指南
```

## 快速开始

```bash
# 克隆项目
git clone <repository-url>
cd hifi-research

# 安装依赖
npm install  # 或 pnpm install

# 配置环境变量
cp .env.example .env

# 初始化数据库
npm run db:migrate

# 启动开发服务器
npm run dev
```

## 数据标准

### 音频参数单位标准
- **采样率**: Hz (44100, 48000, 96000, 192000, etc.)
- **位深度**: bit (16, 24, 32)
- **频率**: Hz (20-20000 为人耳可听范围)
- **失真**: % (THD, THD+N, IMD)
- **信噪比**: dB (SNR, DNR)
- **阻抗**: Ω (16, 32, 300, etc.)
- **功率**: mW 或 W
- **电压**: V 或 mV (Vrms for AC)

### 测量标准
- 遵循 **AES17** 数字音频测量标准
- 遵循 **IEC 61606-3** 音频设备测量方法
- 使用标准测试信号（1kHz 正弦波、扫频、多音等）
- 标注所有测试条件（负载、电平、温度等）

## 贡献指南

欢迎贡献设备数据、测量数据或评测文章！

### 提交设备数据
1. 使用标准的 JSON 格式（参考 `data/devices/template.json`）
2. 包含完整的技术规格和数据来源
3. 确保数据通过验证脚本：`npm run validate:device`

### 提交测量数据
1. 标注测试设备和测试条件
2. 提供原始数据文件（CSV 或测试仪器导出格式）
3. 包含测量曲线图片

### 撰写评测
1. 使用评测模板（参考 `.cursor/rules/review-template.mdc`）
2. 包含主观和客观两部分
3. 保持中立、客观的态度

## 许可证

MIT License

## 联系方式

- 项目主页: [待添加]
- 问题反馈: GitHub Issues
- 讨论区: GitHub Discussions

---

**注意**: 本项目中的所有评测和观点仅供参考，不构成购买建议。音频器材的选择具有很强的主观性，建议根据个人听音偏好和实际试听进行选择。

