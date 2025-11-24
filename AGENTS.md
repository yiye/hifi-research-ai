# Hi-Fi 研究项目 - Agent 指令

## 项目概述

本项目专注于研究和分析高保真音频（Hi-Fi）设备、应用程序和技术参数。所有代码和文档应遵循音频工程专业标准。

## 音频专业术语标准

### 设备类型
- **DAC**（Digital-to-Analog Converter）：数字模拟转换器
- **ADC**（Analog-to-Digital Converter）：模拟数字转换器
- **Amplifier**：功率放大器，区分前级（Preamp）和后级（Power Amp）
- **Headphone Amp**：耳机放大器
- **Transducers**：换能器（音箱、耳机）
- **IEM**（In-Ear Monitor）：入耳式监听耳机
- **Over-ear / On-ear**：头戴式/耳戴式耳机

### 关键音频参数

#### 基础参数
- **采样率（Sample Rate）**：标准值为 44.1kHz, 48kHz, 96kHz, 192kHz, 384kHz, 768kHz
- **位深度（Bit Depth）**：16-bit, 24-bit, 32-bit
- **阻抗（Impedance）**：单位 Ω（欧姆），常见范围 16Ω-600Ω
- **灵敏度（Sensitivity）**：单位 dB/mW 或 dB/V
- **频率响应（Frequency Response）**：20Hz-20kHz 为人耳可听范围

#### 失真与噪声指标
- **THD**（Total Harmonic Distortion）：总谐波失真，单位 %，越低越好
- **THD+N**：总谐波失真加噪声
- **SNR**（Signal-to-Noise Ratio）：信噪比，单位 dB，越高越好
- **DNR**（Dynamic Range）：动态范围，单位 dB
- **IMD**（Intermodulation Distortion）：互调失真
- **Crosstalk**：串扰，单位 dB，越低越好

#### 功率参数
- **输出功率（Output Power）**：单位 mW 或 W，需注明负载阻抗
- **输入电压（Input Voltage）**：单位 V 或 mV
- **增益（Gain）**：单位 dB

### 音频格式
- **无损格式**：FLAC, ALAC, WAV, AIFF, DSD, DXD
- **有损格式**：MP3, AAC, OGG, Opus
- **高解析度音频**：Hi-Res Audio（≥96kHz/24-bit）
- **DSD 标准**：DSD64 (2.8MHz), DSD128 (5.6MHz), DSD256 (11.2MHz)
- **MQA**（Master Quality Authenticated）：折叠式编码技术

### 音频接口与协议
- **模拟接口**：3.5mm (TRS/TRRS), 6.35mm, XLR (平衡), RCA (非平衡)
- **数字接口**：USB, Optical (TOSLINK), Coaxial (S/PDIF), I2S, AES/EBU
- **无线协议**：Bluetooth (SBC, AAC, aptX, aptX HD, LDAC, LHDC)
- **网络协议**：AirPlay, DLNA, Roon Ready, UPnP

## 编码规范

### 命名约定
- 变量名使用驼峰命名法（camelCase），对于音频参数优先使用标准缩写
  ```javascript
  const sampleRate = 192000;  // Hz
  const bitDepth = 24;
  const thdPercentage = 0.0005;
  const snrDb = 120;
  ```

- 设备类别使用 PascalCase
  ```javascript
  class DacDevice { }
  class HeadphoneAmplifier { }
  ```

### 数据结构

#### 音频设备数据模型应包含
```javascript
{
  deviceType: 'DAC' | 'Amplifier' | 'Headphone' | 'Speaker',
  manufacturer: string,
  model: string,
  specs: {
    sampleRate: { max: number, supported: number[] },
    bitDepth: { max: number, supported: number[] },
    thd: { value: number, unit: '%', condition: string },
    snr: { value: number, unit: 'dB' },
    outputPower: { value: number, unit: 'mW', load: number },
    impedance: { value: number, unit: 'Ω' },
    frequencyResponse: { min: number, max: number, unit: 'Hz' }
  },
  connectivity: string[],
  price: { value: number, currency: string }
}
```

#### 测试数据应标注测试条件
```javascript
{
  measurement: 'THD+N',
  value: 0.0005,
  unit: '%',
  condition: {
    frequency: 1000,  // Hz
    amplitude: -1,     // dBFS
    load: 32,          // Ω
    gain: 0            // dB
  }
}
```

### 单位处理
- 频率统一使用 Hz 作为基础单位存储
- 功率使用 mW 作为基础单位，必要时转换为 W
- 始终明确标注单位，避免歧义
- 在显示时根据数值大小自动转换（如 192000Hz → 192kHz）

## 文档规范

### 设备评测文档应包含
1. **基本信息**：品牌、型号、定位、价格
2. **外观与做工**：材质、设计、接口布局
3. **技术规格**：完整的参数列表（含测试条件）
4. **主观听感**：音色、解析力、动态、声场
5. **客观测量**：THD+N、频响曲线、失真曲线
6. **搭配建议**：适配耳机/音箱、前后级搭配
7. **总结与评分**：性价比、推荐指数

### 参数对比表
- 使用 Markdown 表格格式
- 关键参数加粗显示
- 标注测试条件和数据来源
- 包含价格和性价比分析

## 测试方法

### 客观测试标准
- 使用专业测试设备（如 Audio Precision, QuantAsylum)
- 遵循 AES、IEC 标准
- 多次测量取平均值
- 记录测试环境（温度、湿度）

### 主观听音测试
- 使用参考级录音
- A/B 盲测对比
- 多人评测取共识
- 标注个人听感偏好

## 数据可视化

### 图表要求
- **频响曲线**：横轴 20Hz-20kHz（对数刻度），纵轴 dB
- **失真曲线**：显示 THD vs 频率/功率
- **瀑布图**：用于分析时域响应
- **极坐标图**：用于音箱指向性分析

## 代码注释

音频处理代码必须详细注释：
- 采样率转换算法的实现细节
- 滤波器的类型和参数
- 信号链路的每个环节
- 数值精度考量（浮点 vs 定点）

## 社区规范

- 保持客观中性，基于数据和事实
- 尊重不同听音偏好
- 引用数据必须标注来源
- 避免商业推广和主观偏见
- 鼓励开放讨论和数据共享

