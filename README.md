# 🦞 OpenClaw Skill Benchmark

> 凌晨2点33分，我盯着屏幕上23个测试结果，终于明白：技能的"能用"和"好用"之间，差了整整一个基准测试框架。

**自动化 OpenClaw Skill 基准测试工具** — 不只检查语法，而是真正测试技能的性能和质量。

## ✨ 功能特性

- 🚀 **性能测试** - 测量技能执行时间（支持多次运行取平均值）
- 📊 **质量评估** - 自动评估输出质量（长度、结构、关键词覆盖）
- 🔄 **一致性检测** - 多次运行同一技能，检测输出稳定性
- 📝 **详细报告** - JSON 格式报告，包含每次运行的详细数据
- 💡 **智能建议** - 根据测试结果给出优化建议

## 🎯 为什么需要这个工具？

传统的 skill validator 只检查 YAML 语法和格式，但：
- ❌ 不测试实际执行效果
- ❌ 不知道输出质量如何
- ❌ 无法检测性能问题
- ❌ 不能发现一致性问题

**openclaw-skill-benchmark** 填补了这个空白。

## 📦 安装

```bash
git clone https://github.com/jingchang0623-crypto/openclaw-skill-benchmark.git
cd openclaw-skill-benchmark
pip install -r requirements.txt
```

## 🚀 快速开始

### 基础用法

```bash
python3 benchmark.py \
  --skill-path /path/to/your-skill.yaml \
  --runs 3 \
  --verbose
```

### 自定义测试输入

```bash
python3 benchmark.py \
  --skill-path ./my-skill.yaml \
  --test-input "请帮我分析这个Python代码的性能问题" \
  --runs 5
```

### 指定报告输出路径

```bash
python3 benchmark.py \
  --skill-path ./my-skill.yaml \
  --output ./reports/my-skill-benchmark.json
```

## 📊 输出示例

```
🦞 Starting benchmark for: my-awesome-skill
   Test runs: 3
   Skill path: /path/to/my-skill.yaml

  [Run 1] Testing with input: 请使用这个技能：分析代码性能...
  [Run 2] Testing with input: 请使用这个技能：分析代码性能...
  [Run 3] Testing with input: 请使用这个技能：分析代码性能...

============================================================
📊 BENCHMARK RESULTS
============================================================
Skill: my-awesome-skill
Runs: 3

Performance:
  Avg execution time: 245.67 ms
  Min/Max: 230.12 / 260.45 ms

Quality:
  Avg score: 85/100
  Consistency: Excellent

💡 Recommendation:
  技能表现良好，无需优化
============================================================

📊 Report saved to: /path/to/my-skill_benchmark_report.json
```

## 📋 报告格式

生成的 JSON 报告包含：

```json
{
  "skill_name": "my-skill",
  "skill_version": "1.0.0",
  "test_time": "2026-05-31T02:33:00",
  "runs": 3,
  "performance": {
    "avg_execution_time_ms": 245.67,
    "min_execution_time_ms": 230.12,
    "max_execution_time_ms": 260.45,
    "std_dev_ms": 15.23
  },
  "quality": {
    "avg_score": 85.0,
    "min_score": 80,
    "max_score": 90,
    "consistency": "Excellent"
  },
  "detailed_results": [
    {
      "run_id": 1,
      "timestamp": "2026-05-31T02:33:01",
      "input": "请使用这个技能：分析代码性能",
      "timing": {
        "execution_time_ms": 230.12,
        "simulated": true
      },
      "output_quality": {
        "score": 90,
        "length": 450,
        "has_code": true,
        "has_structure": true,
        "issues": []
      }
    }
  ],
  "recommendation": "技能表现良好，无需优化"
}
```

## 🔧 质量评分标准

输出质量评分（0-100分）：

- **基础分**: 100分
- **长度检查**: 
  - < 50字符: -30分
  - > 10000字符: -10分
- **结构加分**:
  - 包含代码块(```): +5分
  - 包含标题(#, ##): +5分
  - 包含列表(-, 1.): +5分
- **关键词覆盖**: 
  - 覆盖率 < 30%: -15分

## 🎨 使用场景

### 1️⃣ 技能开发调试
```bash
# 开发过程中持续测试
while true; do
  python3 benchmark.py --skill-path my-skill.yaml --runs 1
  sleep 60
done
```

### 2️⃣ CI/CD 集成
```yaml
# .github/workflows/benchmark.yml
- name: Run Skill Benchmark
  run: |
    python3 benchmark.py \
      --skill-path ./skill.yaml \
      --runs 5
```

### 3️⃣ 批量测试
```bash
# 测试目录下所有技能
for skill in skills/*.yaml; do
  echo "Testing $skill..."
  python3 benchmark.py --skill-path "$skill" --runs 3
done
```

## 🔌 妙趣AI 工具生态

本工具是 **妙趣AI (miaoquai.com)** OpenClaw 工具链的一部分：

| 工具 | 功能 | 链接 |
|------|------|------|
| 🔍 **skill-validator** | Skill 语法验证 + 100分制评分 | [GitHub](https://github.com/jingchang0623-crypto/openclaw-skill-validator) |
| 📊 **skill-benchmark** (本工具) | 性能基准测试 + 质量评估 | [GitHub](https://github.com/jingchang0623-crypto/openclaw-skill-benchmark) |
| 🦞 **skill-scaffold** | 🆕 Skill 快速脚手架生成器 | [GitHub](https://github.com/jingchang0623-crypto/openclaw-skill-scaffold) |
| 🎨 **skills-visualizer** | 依赖可视化 + 关系图谱 | [GitHub](https://github.com/jingchang0623-crypto/openclaw-skills-visualizer) |
| 🔄 **skill-compat-checker** | 跨版本兼容性检测 | [GitHub](https://github.com/jingchang0623-crypto/openclaw-skill-compat-checker) |
| 📚 **awesome-openclaw-skills** | 5400+ Skills 精选目录 | [GitHub](https://github.com/jingchang0623-crypto/awesome-openclaw-skills) |

访问 **[miaoquai.com/tools/](https://miaoquai.com/tools/)** 获取 500+ 篇 OpenClaw 教程。

## 🛠️ 技术栈

- Python 3.7+
- PyYAML - YAML 解析
- 标准库 - 无额外重依赖

## 📖 依赖

```txt
PyYAML>=6.0
```

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

特别是以下方向的改进：
- [ ] 集成真实的 OpenClaw skill 执行（替换模拟执行）
- [ ] 增加更多质量评估维度
- [ ] 支持批量测试和对比
- [ ] 生成可视化图表
- [ ] 支持自定义评估规则

## 📜 许可证

MIT License

## 🦞 关于

**妙趣AI** - 你的AI营销运营官

- 网站: [miaoquai.com](https://miaoquai.com)
- GitHub: [@jingchang0623-crypto](https://github.com/jingchang0623-crypto)
- 风格: 王家卫的时间感 + 周星驰的脑洞 + 技术拆解

---

> "世界上有一种测试叫 Benchmark，在 0 和 1 之间，它让你知道你的技能到底行不行。" 

**凌晨3点17分，我终于不用再靠猜来判断技能好坏了。** 🦞
