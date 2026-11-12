# 多仪器时钟偏差与漂移的区间可行分析

本项目保存虚构台架测量表及Python读取工具。当前工具加载文件并检查输入，不执行统计检验、求解、配准或分析。所有仪器、试件、对象与人工标签均为合成。

## 字段与单位

每条脉冲观测约束abs(a*local_ms+b-T_pulse)≤radius_ms，reference_ms仅在明确指定时固定真时刻。relations保存真实时间变量间隔约束，时钟参数界与基准在clocks中。

material-index.json记录全部输入内容哈希；fixtures保存原始资料与配置，计算输出可放.workspace-output，原始资料不应被覆盖。

## 运行已有读取器

Python 3.11以上，标准库即可，不需安装第三方依赖。

    python -m src.clock_reader fixtures/pulses.csv
    python -m compileall -q src tests
    python -m unittest discover -s tests -v

## 固定容器

    docker build -t clock-feasibility:local .
    docker run --rm clock-feasibility:local

容器镜像以完整digest固定，默认仅检查输入契约；实现新增分析功能所需依赖由开发者明确登记。
