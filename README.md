
# 🔬 SciAgent

**让任何实验，一条命令即可被记录、分析、总结。**

零侵入 · 自动追踪 · AI 智能分析 · 周报自动生成  
适用于科研 / 竞赛 / 工程项目的轻量级实验管理工具。

---

# 📌 目录

- [SciAgent 是什么](#sciagent-是什么)
- [为什么需要 SciAgent](#为什么需要-sciagent)
- [快速上手](#快速上手)
- [核心功能](#核心功能)
- [AI 智能分析](#ai-智能分析)
- [应用场景](#应用场景)
- [常见问题](#常见问题)
- [贡献](#贡献)
- [许可证](#许可证)

---

# 🧠 SciAgent 是什么？

SciAgent 是一个 **智能实验运行守护工具**，通过统一接口增强你的训练命令。

你只需要把原来的命令：

```bash
python train.py --lr 1e-3 --epochs 50
````

改成：

```bash
sciagent run python train.py --lr 1e-3 --epochs 50
```

SciAgent 就会自动完成：

* ⏺ 记录所有实验参数、日志、输出、错误、环境
* 📊 分析实验性能变化
* 🤖 生成 AI 调优建议（支持 GPT-5 / DeepSeek / Claude / Gemini）
* 🧾 自动生成日报 / 周报 / 月报
* 🧪 自动生成消融实验对比表

**不用修改你的代码。**

---

# ❗ 为什么需要 SciAgent？

实验管理真正的困难不是模型，而是混乱。

| 真实痛点         | SciAgent 解决方案                    |
| ------------ | -------------------------------- |
| 忘记某次训练到底改了什么 | 自动捕获所有参数与 Git 改动                 |
| 日志丢失、崩溃销毁现场  | 自动保存 stdout / stderr / traceback |
| 多个实验结果混在一起   | 自动结构化存储，统一管理                     |
| 想调参但不知道从哪里下手 | AI 分析趋势 + 给出调参方向                 |
| 写周报太麻烦       | 一键生成日报 / 周报 / 月报                 |
| 论文需要消融表格     | 自动生成 Markdown / LaTeX 表格         |

---

# 🚀 快速上手

## 1️⃣ 安装

```bash
cd /path/to/sciagent
pip install -e .
```

## 2️⃣ 初始化项目

```bash
sciagent init
```

可选开启 AI 功能（支持 GPT-5、DeepSeek、Claude、Gemini 等）。

## 3️⃣ 运行实验（零侵入）

```bash
sciagent run python train.py --lr 0.001 --epochs 100
```

自动记录：

* 参数
* 指标（metrics.json 自动捕获）
* 环境（Python、依赖、GPU）
* 输出日志
* 错误堆栈
* Git diff

## 4️⃣ 查看历史

```bash
sciagent history
```

## 5️⃣ AI 分析实验

```bash
sciagent analyze --last
```

## 6️⃣ 一键生成周报

```bash
sciagent weekly
```

---

# 🌟 核心功能

## ⭐ 1. 实验运行守护（不用写 log）

自动记录以下内容：

* 命令行参数
* 训练指标（监测 metrics.json）
* 标准输出、错误日志
* 运行时长、退出码
* Python & pip 环境
* GPU / CPU 使用情况
* Git 代码改动（diff）

所有内容都会结构化存储在：

```
.sciagent/history/<run_id>/
```

---

## ⭐ 2. AI 分析（SciAgent 的核心竞争力）

```bash
sciagent analyze --last
```

AI 会自动解读你的实验：

* loss/acc/F1 趋势分析
* 超参数变化对性能的影响
* 训练阶段是否存在过拟合/欠拟合
* 下一步应该调什么（lr、batch、正则化、结构等）
* 与历史最佳实验的对比

支持的模型提供商：

| 提供商      | 示例模型                             |
| -------- | -------------------------------- |
| OpenAI   | gpt-5.1, gpt-5-mini              |
| DeepSeek | deepseek-chat, deepseek-reasoner |
| Qwen     | qwen-plus, qwen-max              |
| GLM      | glm-4.6, glm-4.5                 |
| Kimi     | moonshot-v1 系列                   |
| Gemini   | gemini-2.5-pro/flash             |
| Claude   | claude-sonnet-4-5                |
| 自定义 API  | 任意 OpenAI 格式                     |

---

## ⭐ 3. 自动生成日报 / 周报 / 月报

```bash
sciagent weekly
```

输出包含：

* 本周运行了多少实验
* 成功/失败数量
* 最佳指标实验
* 参数变化趋势
* 代码变更（Git 自动解析）
* 实验总结（AI）
* 下周计划（AI）

极适合科研组 meeting、公司周会、竞赛总结。

---

## ⭐ 4. 自动生成消融实验表格

```bash
sciagent table --name learning_rate
```

输出 Markdown / LaTeX：

```
| learning_rate | accuracy | loss |
|---------------|----------|------|
| 1e-3          | 0.91     | 0.32 |
| 5e-4          | 0.94     | 0.28 |
```

---

## ⭐ 5. 可选：代码内部参数追踪

无需额外 logger，仅 3 行代码：

```python
import sciagent.track as st

st.log_params({"lr": 1e-3, "bs": 32})
st.log_metrics({"loss": 0.32, "acc": 0.91})
st.save()
```

SciAgent 自动生成 params.json + metrics.json。

---

# 📚 应用场景

## 🧪 科研

* 快速生成论文消融表
* 实验可复现性更强
* 代码版本变化可追踪
* 周报自动生成

## 🏆 算法竞赛

* 保存所有提交记录
* 回滚配置方便
* AI 辅助调参

## 🛠 工程项目

* 模型 A/B 测试
* 多模型多版本自动存档
* 团队共享实验历史

---

# ❓ 常见问题

**Q：需要改训练脚本吗？**
不需要。

**Q：AI 分析必须联网吗？**
是，但所有实验数据本地存储。

**Q：metrics.json 必须要吗？**
推荐，但可通过 `sciagent.track` 自动生成。

**Q：在哪里存储历史？**
在 `.sciagent/` 文件夹内。

---

# 🤝 贡献

欢迎：

* PR
* Issue
* 新功能建议

---

# 📄 许可证

MIT License

---

**让科研与实验变得更高效、更智能 ✨**
欢迎 Star ⭐ 支持项目！

```

---


我可以继续帮你完善。
```
