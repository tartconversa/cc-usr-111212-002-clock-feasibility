# 多仪器时钟偏差与漂移的区间可行分析

本项目是虚构台架数据分析需求的初始输入材料。只有Python文件读取器，尚未实现题目要求的统计检验、求解、配准或分析功能。所有仪器、试件、对象与人工标签均为合成，不涉及模型训练、生成结果或运动轨迹。

## 字段与单位

每条脉冲观测约束abs(a*local_ms+b-T_pulse)≤radius_ms，reference_ms仅在明确指定时固定真时刻。relations保存真实时间变量间隔约束，时钟参数界与基准在clocks中。

material-index.json记录全部输入内容哈希；fixtures是只读原始资料，计算输出应放.workspace-output。手算例和配置口径在完整User Prompt中，输入读取测试不代表分析功能已完成。

## 运行已有读取器

Python 3.11以上，标准库即可，不需安装第三方依赖。

    python -m src.clock_reader fixtures/pulses.csv
    python -m compileall -q src tests
    python -m unittest discover -s tests -v

## 固定容器

    docker build -t clock-feasibility:local .
    docker run --rm clock-feasibility:local

容器镜像以完整digest固定，默认仅检查输入契约；实现新增分析功能所需依赖由开发者明确登记。
