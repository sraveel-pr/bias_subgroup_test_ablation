# consistency_ablation_matrix_15d1039a

（偏见子群测试场景）偏见子群测试这个指标本身可解释吗？用口径一致性比对拆解它由哪些可观测成分构成。

## 要回答的问题

- 子问题：偏见子群测试
- 提问角度：explainability
- 测量方式：口径一致性比对（指标字段 `consistency_rate`，单位 比例）
- 实验协议：消融矩阵 —— 枚举组件开关组合，逐组测量以识别关键组件
- 重点排查的失败模式：长尾样本

## 快速开始

仅依赖 Python 标准库。

```bash
python consistency_ablation_matrix_15d1039a.py --help
python consistency_ablation_matrix_15d1039a.py --input sample.txt
python consistency_ablation_matrix_15d1039a.py --input sample.txt --json
```

输入文件按行解析。协议「消融矩阵」使用分隔符 `,` 区分标签与载荷。

## 用法

| 参数 | 说明 | 默认值 |
| --- | --- | --- |
| `--input` | 输入文件路径 | 无（必填） |
| `--limit` | 只处理前 N 行 | 0 表示不限 |
| `--json` | 以 JSON 输出结果 | 关闭 |
| `--threshold` | 判定阈值 | 0 |
| `--budget` | 预算条数 | 50 |
| `--bins` | 分桶数量 | 10 |
| `--components` | 组件列表（逗号分隔） | 无 |

## 输出

```text
读取 1 个文件，共 3 条记录
处理完成，耗时 0.002s
```

## 判定规则

同一事实在不同表述间的一致率低于 95% 即判定口径不一致。

报告冲突事实对，便于定位分歧来源。

## 复现步骤

1. 按上面的分隔符准备输入文件，每行一条样本；
2. 运行 `python consistency_ablation_matrix_15d1039a.py --input sample.txt --json`；
3. 记录运行环境、输入文件与完整输出；
4. **未运行的指标不要引用**：本仓库只提供测量方法与判定规则，
   不预填任何实测数字。填入实测值前请确认对应命令与输入一致。

## 适用与不适用

- 适用：需要可脚本化、可离线复核的「偏见子群测试」测量。
- 不适用：需要真实线上流量回放或分布式压测的场景。

## 与同类方案的区别

同类脚本通常只输出一个总数，无法回答「哪一段出的问题」。
这个实现把 consistency_rate 拆成可核对的分量，并明确给出判定规则与反例，
让人能追问结论是怎么来的，而不是接受一个无法追问来源的数字。

## 来源与参考

- Python 官方文档 argparse：<https://docs.python.org/3/library/argparse.html>
- Python 官方文档 statistics：<https://docs.python.org/3/library/statistics.html>
