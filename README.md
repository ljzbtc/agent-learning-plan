# Agent 工程师学习计划

从一次模型请求开始，逐步做到能查资料、能调工具、能保存状态，最后变成别人也能运行和使用的服务。

根据 [@chasen_liao 的长文](https://x.com/chasen_liao/status/2109081301819310578) 整理。知识点、学习资料和项目验收要求来自原文；周次安排、动手练习和自测题是按原文内容拆出来的执行版本；标“补充”的资料原文没有给出。

## 怎么用

- **交互版**：用浏览器打开 [`index.html`](index.html)。可以设置开始日期和学习节奏，日期会自动重排；勾选的进度保存在当前浏览器里。
- **在 GitHub 上打勾**：编辑这份 README，把 `- [ ]` 改成 `- [x]`。
- 下面的日期按 **2026-10-19 开始、标准节奏（每周约 15 小时）** 计算，共 28 周，预计 2027-05-02 完成。编程基础不稳的话，先做阶段 0（再加 2 周）。
- 前 8 周另有一条 [并行的数学基础轨道](#并行轨道)（微积分，为概率论打基础），每天 30–45 分钟，和主线同一天开始。

## 路线总览

| 阶段 | 内容 | 周次 | 日期 | 产出 |
|---|---|---|---|---|
| [0 · 编程起步](#阶段-0) | 可选 | 可选 · 2 周 | 开始前 | — |
| [∥ · 数学基础](#并行轨道) | 微积分 8 周，为概率论打基础 | 并行 · M01–08 | 10/19 – 12/13 | 11 道自测题独立做对 9 道以上，衔接 Stat 110 |
| [1 · LLM 基础](#阶段-1) | 看懂一次模型调用 | W01–05 | 10/19 – 11/22 | 项目 1 · 大模型 API Playground |
| [2 · RAG](#阶段-2) | 把资料变成可检索、可引用的证据 | W06–11 | 11/23 – 1/3 | 项目 2 · RAG + Tool Calling Agent |
| [3 · Agent 应用](#阶段-3) | 理解循环，再补齐状态、上下文与边界 | W12–18 | 1/4 – 2/21 | 项目 3 · 简化 Coding Agent |
| [4 · 后端工程](#阶段-4) | 让 Agent 成为能运行和维护的服务 | W19–24 | 2/22 – 4/4 | 项目 4 · AI 服务后端系统 |
| [5 · 开源项目实战](#阶段-5) | 每个方向挑一个：跑通、讲清、改动、验证 | W25–28 | 4/5 – 5/2 | 4 份源码学习仓库（笔记 + 改动 + 测试） |
| [6 · 进阶](#阶段-6) | 按需 | 按需 | — | — |

## 贯穿每个阶段的四条要求

1. **带着问题学**：每个知识点学完问自己，我能做出什么？怎样验证自己真的会了？每周的“自测”就是这个问题的具体版本。
2. **每个项目至少 3 组 Prompt 对比**：用同一组输入比较修改前后，记录改善了什么、有没有引入新的失败，再决定是否保留。README 写清 System Prompt 和约束的理由、是否用 Few-shot、怎样控制格式，以及怎样处理不确定、越界和格式错误的回答。
3. **仓库就是证据**：代码、文档、运行说明和测试都放进 GitHub。每个仓库回答五个问题：输入是什么，输出是什么，成功标准是什么，哪里容易失败，失败后怎样处理。
4. **可以用 AI 学，结果自己验证**：AI 帮你生成一段实现之后，亲手跑一个正常案例、一个异常案例，再试着讲清它的执行过程。

## 一周怎么安排（标准节奏）

- **周一到周四**，每晚 1.5–2 小时：读一个主题的文档，做对应的小实验
- **周五**，1 小时：回答本周自测题，写一页学习笔记
- **周末**，6–8 小时：完成“动手”任务；项目周全部用来写项目

从哪里开始：已经会后端，就直接从阶段 1 开始，模型基础和 API Playground 同时推进；编程基础不稳，先做阶段 0。后端阶段别跳过：原文作者面试被指出工程能力不足，之后专门补了 MySQL 和计算机网络。

---

## 阶段 0

### 编程起步：可选

`env.setup`

> 能用 Python 写一个调用 HTTP 接口、读写 JSON 的小程序，并用 Git 管理代码。

原文建议编程基础还不稳的人先补 Python、Git、HTTP、JSON 和基本接口开发。这一阶段的资料是补充的官方文档。

#### 准备周 1 · Python 与 Git

**学什么**

- 语法、函数、模块、异常处理
- 虚拟环境与包管理（venv、pip 或 uv）
- Git：提交、分支、合并、Pull Request

**读什么**

- [ ] [Python 官方教程（中文）](https://docs.python.org/zh-cn/3/tutorial/)（补充）
- [ ] [Pro Git（中文版）](https://git-scm.com/book/zh/v2)（补充）

**动手**

- [ ] 写一个脚本：读取本地 JSON 文件并输出统计结果，推到新建的 GitHub 仓库
- [ ] 走一遍“建分支 → 提交 → 发 PR → 合并”，并手动解决一次冲突

**自测**（能做到再勾）

- [ ] 能说明虚拟环境解决了什么问题
- [ ] 能独立处理一次 merge 冲突

#### 准备周 2 · HTTP、JSON 与第一个接口

**学什么**

- HTTP 方法、状态码、请求头、请求体
- JSON 的结构与序列化
- 用 httpx 或 requests 调用接口
- 用 FastAPI 写 GET / POST 接口

**读什么**

- [ ] [MDN：HTTP 概述](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Overview)（补充）
- [ ] [FastAPI 学习文档](https://fastapi.tiangolo.com/zh/learn/)

**动手**

- [ ] 用 FastAPI 写一个待办事项接口（新增、查询），分别用 curl 和 Python 调用
- [ ] 故意发送格式错误的 JSON，观察返回的状态码和错误信息

**自测**（能做到再勾）

- [ ] 能说出 400、401、404、422、500 各自的含义
- [ ] 能读懂 FastAPI 自动生成的接口文档

---

## 并行轨道

### 数学基础：微积分 8 周，为概率论打基础

`math.calculus`
 · M01–08 · 10/19 – 12/13 · 每天 30–45 分钟
 · 产出：**11 道自测题独立做对 9 道以上，衔接 Stat 110**

> 8 周学完概率论需要的微积分：导数、积分、反常积分、级数、偏导与二重积分。只学概率会用到的部分，曲线曲面积分、微分方程等先跳过。

和主线同一天开始，按自然周排，不随“学习节奏”变化。每天 30–45 分钟，每周 5 天，留 2 天机动补进度。

**怎么学**

- 每天按顺序：看视频 15–20 分钟 → 做题 15–20 分钟 → 写两三句总结
- 完成标准：每周末能不看书独立做出本周的自测题
- 做不出来就把下一周推迟几天，不要硬往前赶
- 做错的题用 SymPy 算一遍，找到错在哪一步

**资源**

- [3Blue1Brown《Essence of Calculus》](https://www.youtube.com/playlist?list=PLZHQObOWTQDMsr9K-rj53DwVRMYO3t5Yr) — 建立直觉：每个主题开始前先看对应那集（有中文字幕）
- [MIT OCW 18.01SC Single Variable Calculus](https://ocw.mit.edu/courses/18-01sc-single-variable-calculus-fall-2010/) — 单变量系统讲解：按主题挑 Unit 看，含讲座视频和习题课
- [MIT OCW 18.02SC Multivariable Calculus](https://ocw.mit.edu/courses/18-02sc-multivariable-calculus-fall-2010/) — 多元：只看偏导数和二重积分
- [OpenStax《Calculus》Vol 1](https://openstax.org/details/books/calculus-volume-1) — 免费教材：每节挑基础题 5–10 道，书后有奇数题答案
- [OpenStax《Calculus》Vol 2](https://openstax.org/details/books/calculus-volume-2)
- [OpenStax《Calculus》Vol 3](https://openstax.org/details/books/calculus-volume-3)
- [SymPy 文档](https://docs.sympy.org/latest/index.html) — 做错时用它算一遍，定位错在哪一步

#### M01 · 直觉 + 函数与极限 · 10/19 – 10/25

第 1–2 周目标：理解“导数 = 瞬时变化率”，熟练求常见函数的导数。

**本周用到**：[3Blue1Brown《Essence of Calculus》](https://www.youtube.com/playlist?list=PLZHQObOWTQDMsr9K-rj53DwVRMYO3t5Yr) · [OpenStax《Calculus》Vol 1](https://openstax.org/details/books/calculus-volume-1)

**任务**

- [ ] 3B1B 第 1–3 集：微积分的本质、导数的悖论、用几何推导求导公式
- [ ] OpenStax Vol 1 第 2 章：极限（重点会算，不钻 ε-δ 定义）
- [ ] 3B1B 第 7 集：极限与洛必达法则
- [ ] OpenStax：极限计算基础题 10 道

#### M02 · 求导 · 10/26 – 11/1

**本周用到**：[3Blue1Brown《Essence of Calculus》](https://www.youtube.com/playlist?list=PLZHQObOWTQDMsr9K-rj53DwVRMYO3t5Yr) · [MIT OCW 18.01SC Single Variable Calculus](https://ocw.mit.edu/courses/18-01sc-single-variable-calculus-fall-2010/) · [OpenStax《Calculus》Vol 1](https://openstax.org/details/books/calculus-volume-1)

**任务**

- [ ] 3B1B 第 4–5 集：链式法则与乘积法则、自然常数 e
- [ ] MIT 18.01SC Unit 1：Differentiation（导数定义、求导法则、链式法则）
- [ ] 熟记导数表：xⁿ、eˣ、ln x、sin x、cos x
- [ ] MIT 18.01SC Unit 2 中的最值部分：用导数求最大值、最小值
- [ ] OpenStax Vol 1 第 3 章：求导基础题 15 道

**自测**（不看书独立做出）

- [ ] 求 $e^{-x^2}$ 的导数
- [ ] 求 $x\ln x$ 的导数
- [ ] 求 $x e^{-x}$ 在 $x>0$ 时的最大值

<details><summary>答案</summary>

- $e^{-x^2}$ 的导数：$-2x\,e^{-x^2}$
- $x\ln x$ 的导数：$\ln x + 1$
- $x e^{-x}$ 在 $x>0$ 时的最大值：$x=1$ 时取到，值为 $1/e$

</details>

#### M03 · 定积分与基本积分 · 11/2 – 11/8

第 3–4 周目标：理解“积分 = 累加 / 面积”，熟练掌握换元和分部积分。这是整个计划最重要的两周，概率里的期望和方差几乎都要靠积分算。

**本周用到**：[3Blue1Brown《Essence of Calculus》](https://www.youtube.com/playlist?list=PLZHQObOWTQDMsr9K-rj53DwVRMYO3t5Yr) · [MIT OCW 18.01SC Single Variable Calculus](https://ocw.mit.edu/courses/18-01sc-single-variable-calculus-fall-2010/) · [OpenStax《Calculus》Vol 1](https://openstax.org/details/books/calculus-volume-1)

**任务**

- [ ] 3B1B 第 8–9 集：积分与微积分基本定理、面积和斜率的关系
- [ ] MIT 18.01SC Unit 3：Integration（不定积分、定积分、基本定理）
- [ ] 熟记基本积分表（就是导数表反过来）
- [ ] OpenStax Vol 1 第 5 章：基本积分题 15 道

#### M04 · 换元与分部积分 · 11/9 – 11/15

**本周用到**：[MIT OCW 18.01SC Single Variable Calculus](https://ocw.mit.edu/courses/18-01sc-single-variable-calculus-fall-2010/) · [OpenStax《Calculus》Vol 1](https://openstax.org/details/books/calculus-volume-1) · [OpenStax《Calculus》Vol 2](https://openstax.org/details/books/calculus-volume-2) · [SymPy 文档](https://docs.sympy.org/latest/index.html)

**任务**

- [ ] MIT 18.01SC Unit 4：Techniques of Integration（只看换元和分部积分）
- [ ] OpenStax：Vol 1 换元积分题 10 道、Vol 2 第 3 章分部积分题 10 道
- [ ] 用 SymPy 核对做错的题

**自测**（不看书独立做出）

- [ ] 计算 $\int_0^1 2x\,dx$
- [ ] 计算 $\int_0^1 x e^{x^2}\,dx$
- [ ] 计算 $\int_0^1 x e^{x}\,dx$（以后算期望的典型形式）

<details><summary>答案</summary>

- $\int_0^1 2x\,dx$：$1$
- $\int_0^1 x e^{x^2}\,dx$：$(e-1)/2$
- $\int_0^1 x e^{x}\,dx$（以后算期望的典型形式）：$1$

</details>

#### M05 · 反常积分 · 11/16 – 11/22

目标：会算积分区间到无穷的积分。指数分布、正态分布等连续分布全靠它。

**本周用到**：[MIT OCW 18.01SC Single Variable Calculus](https://ocw.mit.edu/courses/18-01sc-single-variable-calculus-fall-2010/) · [OpenStax《Calculus》Vol 2](https://openstax.org/details/books/calculus-volume-2)

**任务**

- [ ] MIT 18.01SC Unit 5 中的 Improper Integrals：反常积分的定义与计算
- [ ] 理解“收敛”：积分结果是一个有限的数
- [ ] 练习 $\int_0^\infty e^{-\lambda x}\,dx$ 这一类，$\lambda$ 换成不同的数多算几遍
- [ ] 了解高斯积分，只需记住结论：$\int_{-\infty}^{\infty} e^{-x^2/2}\,dx = \sqrt{2\pi}$
- [ ] OpenStax Vol 2 第 3 章 Improper Integrals：8–10 道

**自测**（不看书独立做出）

- [ ] 计算 $\int_0^\infty 2e^{-2x}\,dx$（指数分布的概率总和为 1）
- [ ] 计算 $\int_0^\infty x\cdot 2e^{-2x}\,dx$（指数分布的期望）

<details><summary>答案</summary>

- $\int_0^\infty 2e^{-2x}\,dx$（指数分布的概率总和为 1）：$1$
- $\int_0^\infty x\cdot 2e^{-2x}\,dx$（指数分布的期望）：$1/2$

</details>

#### M06 · 级数与泰勒展开 · 11/23 – 11/29

目标：会用等比级数求和，记住 eˣ 的泰勒展开。几何分布、泊松分布的计算都要用。

**本周用到**：[3Blue1Brown《Essence of Calculus》](https://www.youtube.com/playlist?list=PLZHQObOWTQDMsr9K-rj53DwVRMYO3t5Yr) · [MIT OCW 18.01SC Single Variable Calculus](https://ocw.mit.edu/courses/18-01sc-single-variable-calculus-fall-2010/) · [OpenStax《Calculus》Vol 2](https://openstax.org/details/books/calculus-volume-2)

**任务**

- [ ] MIT 18.01SC Unit 5 中的级数部分（收敛判别法只需了解）
- [ ] 等比级数求和，以及对它求导得到的公式（OpenStax Vol 2 第 5 章）
- [ ] 3B1B 第 10–11 集：高阶导数、泰勒级数
- [ ] OpenStax Vol 2 第 6 章：泰勒级数 5 道
- [ ] 记住两个结论：$\sum_{k=0}^{\infty} r^k = \frac{1}{1-r}\ (|r|<1)$；$e^{\lambda} = \sum_{k=0}^{\infty} \frac{\lambda^k}{k!}$

**自测**（不看书独立做出）

- [ ] 计算 $\sum_{k=0}^{\infty} \left(\tfrac{1}{2}\right)^k$
- [ ] 计算 $\sum_{k=0}^{\infty} e^{-3}\frac{3^k}{k!}$（泊松分布的概率总和为 1）

<details><summary>答案</summary>

- $\sum_{k=0}^{\infty} \left(\tfrac{1}{2}\right)^k$：$2$
- $\sum_{k=0}^{\infty} e^{-3}\frac{3^k}{k!}$（泊松分布的概率总和为 1）：$1$

</details>

#### M07 · 多元函数 · 11/30 – 12/6

第 7–8 周目标：会算简单的二重积分，为多元分布（两个随机变量一起看）做准备。

**本周用到**：[MIT OCW 18.02SC Multivariable Calculus](https://ocw.mit.edu/courses/18-02sc-multivariable-calculus-fall-2010/) · [OpenStax《Calculus》Vol 3](https://openstax.org/details/books/calculus-volume-3)

**任务**

- [ ] MIT 18.02SC 偏导数部分（Partial Derivatives，把其他变量当常数求导）
- [ ] MIT 18.02SC 二重积分部分（Double Integrals，含义与计算）
- [ ] 交换积分次序（概率里经常要用）
- [ ] OpenStax Vol 3：第 4 章偏导 8 道、第 5 章二重积分 8 道

#### M08 · 极坐标 + 总复习 · 12/7 – 12/13

**本周用到**：[MIT OCW 18.02SC Multivariable Calculus](https://ocw.mit.edu/courses/18-02sc-multivariable-calculus-fall-2010/)

**任务**

- [ ] MIT 18.02SC：二重积分的极坐标换元
- [ ] 看懂用极坐标证明高斯积分（第 5 周记住的那个结论）
- [ ] 把前 7 周的自测题全部重做一遍
- [ ] 错得最多的主题，回去补 5 道题

**自测**（不看书独立做出）

- [ ] 计算 $\int_0^1 \int_0^x 1\,dy\,dx$（两个独立均匀分布 $X$、$Y$，求 $P(Y<X)$）

<details><summary>答案</summary>

- $\int_0^1 \int_0^x 1\,dy\,dx$（两个独立均匀分布 $X$、$Y$，求 $P(Y<X)$）：$1/2$

</details>

#### 衔接 Stat 110

第 9 周起开始 Stat 110 第 1 讲，配合 Blitzstein & Hwang《Introduction to Probability》第 1 章。前几讲是排列组合和计数，几乎不用微积分，正好缓冲；讲到连续随机变量时，这 8 周的积分就用上了。

- [ ] 8 周的 11 道自测题，不看答案独立做对 9 道以上（可以开始 Stat 110 的信号）

- [Stat 110 课程主页](https://stat110.hsites.harvard.edu/) — 讲座视频、习题和 edX 课程入口
- [Blitzstein & Hwang《Introduction to Probability》](http://probabilitybook.net/) — 作者提供的免费在线版

---

## 阶段 1

### LLM 基础：看懂一次模型调用

`llm.request`
 · W01–05 · 10/19 – 11/22
 · 产出：**项目 1 · 大模型 API Playground**

> 能完整解释一次请求到响应发生了什么，能稳定处理流式输出、结构化输出和工具调用。后面所有内容都建在这一层上。

#### W01 · 模型怎样生成内容 · 10/19 – 10/25

先建立基本认识，训练细节不必深究，精力放在调用时真正影响系统行为的几件事上。

**学什么**

- Transformer 与注意力机制
- 预训练、指令微调、RLHF / RLAIF
- 自回归生成（Next Token Prediction）与上下文学习（In-Context Learning）
- Tokenization；输入 Token、输出 Token、Context Window、最大输出长度
- 上下文溢出：裁剪历史、压缩资料还是调整输入
- Lost in the Middle：长上下文中间的信息容易被忽略
- 采样参数：Temperature、Top-p、Top-k、Frequency / Presence Penalty、Seed、Stop Sequences

**读什么**

- [ ] [图解 Transformer](https://jalammar.github.io/illustrated-transformer/)
- [ ] [Token 与计数文档](https://help.openai.com/en/articles/4936856-what-are-tokens-and-how-to-count-them)
- [ ] [vLLM SamplingParams 文档](https://docs.vllm.ai/en/v0.6.4/dev/sampling_params.html) — 原文引用的是 v0.6.4，实际以你所用模型的接口说明为准

**动手**

- [ ] 用 tokenizer 给同一段中文和英文计数，记录 Token 数与字数的比例
- [ ] 估算一次请求的 Token 预算：System Prompt + 历史消息 + 工具说明 + 检索资料 + 预留输出
- [ ] 同一个问题用 Temperature 0 / 0.7 / 1.2 各调用 5 次，对比输出差异
- [ ] 把一条关键信息分别放在长上下文的开头、中间、结尾，看回答是否受影响

**自测**（能做到再勾）

- [ ] 能解释为什么 Token 和汉字、单词没有固定对应关系
- [ ] 能说出上下文溢出的两种处理方式及各自的代价
- [ ] 能说明为什么低 Temperature 不保证答案正确，Seed 也不保证结果完全一致

#### W02 · 模型类型、API 协议与流式输出 · 10/26 – 11/1

**学什么**

- Chat、Reasoning、多模态、Embedding、Rerank、语音与实时模型的分工
- Chat Completions、Responses、Messages 三种抽象
- message、role（system / user / assistant / tool）、content
- 关键字段：model、messages / input、instructions、tools、tool_choice、response_format、stream、usage、finish_reason
- 流式：SSE、event stream、delta、增量文本
- 工具参数逐步到达、连接中断、用户取消、响应未完成

**读什么**

- [ ] [OpenAI Chat Completions](https://platform.openai.com/docs/api-reference/chat/create)
- [ ] [OpenAI Responses](https://platform.openai.com/docs/api-reference/responses)
- [ ] [Responses Create 接口](https://platform.openai.com/docs/api-reference/responses/create)
- [ ] [Claude Messages](https://platform.claude.com/docs/en/build-with-claude/working-with-messages)
- [ ] [Claude Stop Reasons](https://docs.anthropic.com/en/api/handling-stop-reasons)
- [ ] [OpenAI 流式响应](https://platform.openai.com/docs/guides/streaming-responses)
- [ ] [Claude Streaming](https://docs.anthropic.com/en/docs/build-with-claude/streaming)
- [ ] [Responses Streaming 事件参考](https://platform.openai.com/docs/api-reference/responses-streaming)

**动手**

- [ ] 不用 SDK，直接发 HTTP 请求调用两家供应商的接口，把请求和响应 JSON 存档
- [ ] 做一张字段对照表：同一信息在 Chat Completions / Responses / Messages 里分别叫什么
- [ ] 写一个流式客户端：拼接 delta、识别结束事件，并处理中途断开和主动取消

**自测**（能做到再勾）

- [ ] 看到一次响应，能判断它为什么结束（正常结束、长度截断、工具调用、拒绝）
- [ ] 能说清 usage 里每一项 Token 的含义
- [ ] 能讲清打字机效果背后完整的事件过程

#### W03 · 结构化输出、工具调用、多轮会话与 Embedding · 11/2 – 11/8

**学什么**

- JSON Mode 与按 Schema 约束的 Structured Outputs
- 结构符合要求 ≠ 内容正确：拒绝、截断、校验失败后的修复与重试
- Function Calling：模型请求调用和系统真正执行是两件事
- tool_call_id 与结果对应、并行工具调用、错误返回
- 多轮会话：自己维护历史，或用供应商的状态接口；摘要、短期 / 长期记忆、上下文压缩
- Embedding：向量维度、归一化、Cosine / Dot Product / L2、批量生成与向量缓存

**读什么**

- [ ] [JSON Schema 基础](https://json-schema.org/understanding-json-schema/basics)
- [ ] [Structured Outputs](https://developers.openai.com/api/docs/guides/structured-outputs)
- [ ] [Structured Outputs 介绍文章](https://openai.com/index/introducing-structured-outputs-in-the-api/) — 了解这项能力最初要解决的问题，用法以当前文档为准
- [ ] [OpenAI Function Calling](https://developers.openai.com/api/docs/guides/function-calling)
- [ ] [Claude Tool Use](https://platform.claude.com/docs/en/agents-and-tools/tool-use/overview)
- [ ] [会话状态文档](https://developers.openai.com/api/docs/guides/conversation-state)
- [ ] [Claude 对话中途的系统消息与工具变更](https://platform.claude.com/docs/en/build-with-claude/mid-conversation-system-messages)
- [ ] [Embedding 文档](https://platform.openai.com/docs/guides/embeddings)

**动手**

- [ ] 用 Schema 约束输出一个含枚举和嵌套对象的结构，再人为制造一次校验失败，实现修复或重试
- [ ] 实现一个查询工具，走完整条链路：工具描述与参数 Schema → 模型发起调用 → 系统校验并执行 → 回传结果 → 模型继续
- [ ] 触发一次并行工具调用，确认每个结果都对上了正确的 tool_call_id
- [ ] 生成 20 条文本的向量，算两两相似度，看排序是否符合直觉

**自测**（能做到再勾）

- [ ] 能解释“结构正确”和“内容正确”的区别
- [ ] 能画出工具调用的时序图，标明谁生成、谁执行、谁校验
- [ ] 能说明一次独立的生成请求为什么不会自动带上应用里的聊天记录

#### W04 · Prompt Engineering · 11/9 – 11/15

这部分不单独做项目，从这一周开始贯穿后面所有项目，效果要放进具体任务里验证。

**学什么**

- 六个组成部分：Role / System Prompt、Instruction、Context、Input、Output Format、Constraints
- Zero-shot 与 Few-shot：用贴近真实任务的示例表达标准、格式和风格
- CoT（拆解与逐步推理）、ReAct（推理 + 调用工具）、Self-Critique / Reflexion（检查与修正）
- 推理模型上，强行要求“一步一步思考”未必有收益
- 模型自查之后仍需外部依据：测试结果、引用证据、字段校验、人工复核

**读什么**

- [ ] [OpenAI Prompt Engineering](https://platform.openai.com/docs/guides/prompt-engineering)
- [ ] [Claude 提示词指南](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/overview)
- [ ] [Few-shot 学习材料](https://www.promptingguide.ai/zh/techniques/fewshot)
- [ ] [CoT 学习材料](https://www.promptingguide.ai/zh/techniques/cot)
- [ ] [ReAct 学习材料](https://www.promptingguide.ai/zh/techniques/react)
- [ ] [Reflexion 学习材料](https://www.promptingguide.ai/zh/techniques/reflexion)
- [ ] [推理模型提示建议](https://developers.openai.com/api/docs/guides/reasoning-best-practices)

**动手**

- [ ] 写一个对比脚本：同一组 10 条输入跑两个 Prompt 版本，把结果并排输出（后面每个项目都复用它）
- [ ] 找一个模型反复误解的边界，用 2–3 个贴近真实任务的示例修正它
- [ ] 在推理模型上对比加和不加“一步一步思考”的效果

**自测**（能做到再勾）

- [ ] 能说明自己 System Prompt 里每一条约束为什么存在
- [ ] 能举例说明什么时候给示例比继续堆形容词更有效

#### W05 · 项目 1：大模型 API Playground · 11/16 – 11/22

把前四周的能力放进同一个小应用。这一步做扎实，后面用框架时才不会出现“跑起来了，但不知道里面发生了什么”。

**要做**

- [ ] 支持普通对话、流式响应、结构化输出、工具调用
- [ ] 支持 Embedding 生成和相似度计算
- [ ] 每次调用记录模型、输入、输出、Token 用量和耗时
- [ ] 对比至少两个模型或两家供应商的 API 差异
- [ ] 至少 3 组 Prompt 修改前后对比

**验收**

- [ ] 能讲清一次请求到响应的全过程
- [ ] 能解释 message、role、tool call、tool result、stream、usage 的含义
- [ ] 现场演示一次完整的工具调用
- [ ] 演示结构化输出失败后怎样处理
- [ ] 仓库包含 README、运行说明、示例请求和测试用例

---

## 阶段 2

### RAG：把资料变成可检索、可引用的证据

`rag.retrieve`
 · W06–11 · 11/23 – 1/3
 · 产出：**项目 2 · RAG + Tool Calling Agent**

> 搭出一条完整的检索问答链路：回答能引用来源，资料不足时会拒答，并且有评估数据支撑。

#### W06 · 文档解析与分块 · 11/23 – 11/29

表格行列错位、章节标题丢失、代码块被切断，都会让后面检索到的内容没法用。

**学什么**

- PDF、Word、HTML、Markdown、代码、表格、图片 OCR、多模态文档，解析方式各不相同
- 分块：固定长度、递归分块、语义分块、按 Markdown / 代码结构分块、父子分块
- 滑动窗口与 overlap

**读什么**

- [ ] [LlamaIndex 文档加载](https://docs.llamaindex.ai/en/stable/module_guides/loading/)
- [ ] [Pinecone 分块策略](https://www.pinecone.io/learn/chunking-strategies/)
- [ ] [LlamaIndex 节点解析](https://docs.llamaindex.ai/en/stable/module_guides/loading/node_parsers/)

**动手**

- [ ] 准备一份自己的语料：30 份以上文档，混合 Markdown 和 PDF，至少一份带表格
- [ ] 用三种分块策略切同一份语料，抽查表格、标题、代码块有没有被切坏
- [ ] 记录块大小、块数量，以及 overlap 带来的额外 Token 成本

**自测**（能做到再勾）

- [ ] 能说出块太小、块太大分别会导致什么问题
- [ ] 能为自己的语料选定分块方式并说明理由

#### W07 · 向量检索与向量库 · 11/30 – 12/6

先选一种向量库，把写入、更新、检索、删除跑通，再根据数据量、延迟和召回效果学索引取舍。

**学什么**

- 把 Embedding 接到检索：Top-K、相似度阈值、向量缓存
- 向量库：FAISS、Milvus、Qdrant、Weaviate、Chroma、Pinecone、pgvector、Redis Stack
- 索引方式：FLAT、IVF、HNSW、PQ（先知道区别，原理放到进阶）

> 注意：建议选 pgvector：阶段 4 的后端用 PostgreSQL，到时可以直接复用。

**读什么**

- [ ] [Embedding 文档](https://platform.openai.com/docs/guides/embeddings)
- [ ] [向量数据库学习材料](https://www.pinecone.io/learn/vector-database/)
- [ ] [pgvector](https://github.com/pgvector/pgvector)

**动手**

- [ ] 选一种向量库，跑通写入、更新、检索、删除
- [ ] 写 10 个查询，人工标注期望命中的文档，算出 Top-5 命中率
- [ ] 调整相似度阈值，观察召回数量和噪声怎样变化

**自测**（能做到再勾）

- [ ] 能解释 Cosine、Dot Product、L2 的区别，以及归一化之后它们的关系
- [ ] 能说明自己选的向量库和索引方式适合多大的数据规模

#### W08 · 混合检索、元数据与重排 · 12/7 – 12/13

**学什么**

- 产品型号、报错码、专有名词：BM25 关键词检索 + 向量检索的混合召回
- RRF 融合、多查询改写
- 元数据：标题、章节、来源、时间戳、文档版本、用户权限
- 权限过滤由系统执行；先过滤后检索与先检索后过滤的取舍
- Rerank：Bi-Encoder 与 Cross-Encoder，粗排 + 精排两阶段
- 实现参考：bge-reranker、Cohere Rerank、Jina Rerank

**读什么**

- [ ] [Hybrid Search](https://www.pinecone.io/learn/hybrid-search/)
- [ ] [LlamaIndex Metadata Extraction](https://docs.llamaindex.ai/en/stable/module_guides/indexing/metadata_extraction/)
- [ ] [Cohere Reranking](https://docs.cohere.com/docs/reranking)

**动手**

- [ ] 用产品型号、报错码一类的查询，对比纯向量检索和混合检索的结果
- [ ] 给片段加上来源和权限元数据，验证无权限的内容不会进入上下文
- [ ] 接入一个 Reranker，对比重排前后的 Top-5 命中率

**自测**（能做到再勾）

- [ ] 能解释为什么专有名词需要关键词检索
- [ ] 能说明权限过滤放在检索前和检索后的取舍

#### W09 · 生成、引用与评估 · 12/14 – 12/20

RAG 能为回答补充依据，但仍然可能答错，所以检索效果和生成效果要分开检查。

**学什么**

- 选哪些片段、怎样排序、要不要压缩
- 把引用对应回原文位置
- 避免关键证据被埋在长上下文中间
- 资料没有覆盖时明确说证据不足；资料过时、冲突、不相关时怎么办
- 评估指标：检索准确率、召回率、答案忠实度、上下文相关性、幻觉率
- 进阶方向先了解：Query Rewrite、HyDE、Self-Query、Agentic RAG、GraphRAG

**读什么**

- [ ] [RAG 完整流程](https://www.pinecone.io/learn/retrieval-augmented-generation/)
- [ ] [Ragas 文档](https://docs.ragas.io/)
- [ ] [GraphRAG 官方项目](https://github.com/microsoft/graphrag) — 带着“它能解决我哪类检索问题”去读

**动手**

- [ ] 让每条回答都带上能对应回原文的引用
- [ ] 构造 5 个资料里没有答案的问题，确认系统会明确说证据不足
- [ ] 用 Ragas 搭一套最小评估流程，分别给检索和生成打分

**自测**（能做到再勾）

- [ ] 看到一个错误回答，能判断是检索出错还是生成出错
- [ ] 能说出 GraphRAG 能解决自己哪类问题，或者为什么暂时用不上

#### W10–11 · 项目 2：RAG + Tool Calling Agent · 12/21 – 1/3

把检索和工具放进同一个 Agent，让它自己决定是否检索、是否调用工具。

**要做**

- [ ] 支持上传或导入 Markdown / PDF，完成切分、Embedding 和向量检索
- [ ] 回答引用来源，资料不足时拒答
- [ ] 至少 2 个工具（网页搜索、计算器、文件查询、时间查询等），由 Agent 判断何时使用
- [ ] 记录每一步：reasoning 摘要、工具请求、实际返回、最终结果
- [ ] 不少于 20 条测试问题，覆盖：直接可查、跨文档、需要工具计算、资料里没有、工具失败
- [ ] 至少 3 组 Prompt 修改前后对比

**验收**

- [ ] 能讲清 RAG 的完整链路
- [ ] 能解释模型工具调用和普通函数调用的区别
- [ ] 提供检索结果、回答质量和失败案例分析
- [ ] 仓库包含 README、运行说明和测试集

---

## 阶段 3

### Agent 应用：理解循环，再补齐状态、上下文与边界

`agent.loop`
 · W12–18 · 1/4 – 2/21
 · 产出：**项目 3 · 简化 Coding Agent**

> 能读懂并改造一个 Agent Harness，独立写出一个简化版 Coding Agent，并能解释 Prompt、RAG、工具、工作流、状态、记忆、评估和安全怎样组合。

#### W12 · Agent 是什么，什么时候不需要它 · 1/4 – 1/10

**学什么**

- Chatbot 偏对话，Workflow 偏预先确定的流程，Agent 根据任务和反馈动态决定下一步
- Agent Loop：模型提出下一步 → 系统执行并返回结果 → 模型继续推进，直到完成或触发停止条件
- 五种 Workflow 模式：Prompt Chaining、Routing、Parallelization、Orchestrator-Workers、Evaluator-Optimizer

**读什么**

- [ ] [Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents)
- [ ] [Agent 白皮书中文译文](https://arthurchiao.art/blog/ai-agent-white-paper-zh/)
- [ ] [Agent Loop 文档](https://code.claude.com/docs/en/agent-sdk/agent-loop)

**动手**

- [ ] 不用任何框架，各写一个 Prompt Chaining 和 Routing 的最小例子
- [ ] 给项目 2 的 Agent 画出循环图，标出所有停止条件

**自测**（能做到再勾）

- [ ] 给一个需求，能判断用 Workflow 还是 Agent，并说明理由
- [ ] 能说出五种模式各自适合什么任务

#### W13 · 用 Pi 读懂 Agent Loop 与 Harness · 1/11 – 1/17

原文作者补充的入口：Pi 的 Harness 很精简，适合沿着一次任务读源码。

**学什么**

- 用户输入怎样进入上下文，模型收到哪些消息和工具说明
- 工具调用怎样执行，结果怎样回到上下文
- 循环怎样继续、怎样停止；工具失败或任务中断时发生什么
- Harness 的职责：提供运行环境、组织模型看到的信息、执行动作、管理结果和任务状态
- Session、上下文管理、工具与 Extension 事件

**读什么**

- [ ] [Pi 官方文档](https://pi.dev/docs/latest)
- [ ] [Pi Agent Loop 源码](https://github.com/earendil-works/pi/blob/main/packages/agent/src/agent-loop.ts)
- [ ] [Pi Extensions 文档](https://pi.dev/docs/latest/extensions)
- [ ] [Pi SDK 文档](https://pi.dev/docs/latest/sdk)
- [ ] [@xiaomovps 的相关帖子](https://x.com/xiaomovps) — 原文推荐一起看

**动手**

- [ ] 跑一个“读取文件并回答问题”的任务，记录模型请求、工具调用和结果返回
- [ ] 在 agent-loop.ts 里标出继续、停止、出错三条路径
- [ ] 写一个自己的工具或 Extension，观察它怎样进入原来的循环

**自测**（能做到再勾）

- [ ] 不看代码，能复述 Pi 的一次完整循环
- [ ] 能说清 Session、上下文管理、Extension 事件各自负责什么

#### W14 · 工具设计、规划与状态管理 · 1/18 – 1/24

**学什么**

- 工具描述、参数 Schema、结果组织、错误返回、并行调用、超时与重试
- Plan-and-Execute、动态重规划、子任务拆分、任务依赖、终止条件
- 系统层面的最大步数、总超时、调用预算；做不下去时停下来并交代原因
- 全局状态与局部状态；消息历史、工具记录、任务进度的更新、持久化与恢复
- 工具超时不代表操作没完成：写操作要考虑重复执行

**读什么**

- [ ] [Function Calling 文档](https://developers.openai.com/api/docs/guides/function-calling) — 这次重点看工具描述、参数约束、调用关联和结果返回
- [ ] [Lilian Weng：LLM Powered Autonomous Agents](https://lilianweng.github.io/posts/2023-06-23-agent/)
- [ ] [Planning Agents](https://www.langchain.com/blog/planning-agents)
- [ ] [LangGraph Persistence](https://docs.langchain.com/oss/python/langgraph/persistence)
- [ ] [Durable Execution](https://www.inngest.com/blog/durable-execution-key-to-harnessing-ai-agents)
- [ ] [LangGraph Low-level Concepts（旧入口）](https://langchain-ai.github.io/langgraph/concepts/low_level/)

**动手**

- [ ] 给项目 2 的工具补上超时、重试和结构化的错误返回
- [ ] 给 Agent 加最大步数和调用预算，触发一次，确认它能说明停止原因
- [ ] 实现检查点：杀掉进程后能从上次的步骤继续

**自测**（能做到再勾）

- [ ] 能说明一个写操作超时后为什么不能直接重试
- [ ] 能说出什么情况下应该触发重规划

#### W15 · 记忆、上下文工程与 MCP · 1/25 – 1/31

**学什么**

- 短期、长期、情景、语义记忆；记忆的提取、压缩与遗忘
- 系统存下来的信息 ≠ 模型这一轮实际看到的信息
- 上下文工程：信息选择、裁剪、压缩、动态注入、工具结果摘要、历史消息摘要
- 压缩后检查：目标、关键约束、已完成的操作、未解决的问题是否还在
- MCP：Server、Client；Tools、Resources、Prompts
- 接通工具之后，权限、参数校验和结果可信度仍由应用负责

**读什么**

- [ ] [Agent Memory 学习材料](https://www.ibm.com/think/topics/ai-agent-memory)
- [ ] [Lilian Weng：Memory 部分](https://lilianweng.github.io/posts/2023-06-23-agent/#component-two-memory)
- [ ] [Anthropic：上下文工程](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
- [ ] [MCP 官方入门文档](https://modelcontextprotocol.io/docs/getting-started/intro)

**动手**

- [ ] 给 Agent 加历史摘要，压缩前后各跑一遍长任务，检查关键约束有没有丢
- [ ] 写一个最小的 MCP Server，暴露一个工具和一个资源，接入任意 MCP Client

**自测**（能做到再勾）

- [ ] 能说明自己的项目该存哪些记忆、什么时候取出来
- [ ] 能解释 MCP 的 Tools、Resources、Prompts 分别给谁用

#### W16 · Human-in-the-Loop、安全与评估 · 2/1 – 2/7

**学什么**

- 审批、中断、恢复、人工修正；明确系统能自动执行到哪一步
- 发送消息、删除文件、变更业务数据前要有确认节点
- Prompt Injection、工具越权、权限控制、沙箱执行、敏感数据保护
- 外部内容一律不可信：出现在上下文里不代表它是可执行指令
- 评估整个任务：完成率、工具调用准确率、步骤合理性、失败恢复、成本、延迟、多轮稳定性

**读什么**

- [ ] [LangGraph Interrupts](https://docs.langchain.com/oss/python/langgraph/interrupts)
- [ ] [Human-in-the-Loop（旧入口）](https://langchain-ai.github.io/langgraph/concepts/human_in_the_loop/)
- [ ] [OWASP Prompt Injection 防护指南](https://cheatsheetseries.owasp.org/cheatsheets/LLM_Prompt_Injection_Prevention_Cheat_Sheet.html)
- [ ] [Langfuse Evaluation](https://langfuse.com/docs/evaluation/overview)
- [ ] [LangSmith Evaluation](https://docs.langchain.com/langsmith/evaluation)

**动手**

- [ ] 给删除文件、发送消息这类操作加人工确认节点，确认后能接着执行
- [ ] 构造一个网页里藏着“忽略用户要求”的注入样例，验证 Agent 不会照做
- [ ] 用 Langfuse 或 LangSmith 建一个 10 条任务的评估集，比较两个版本

**自测**（能做到再勾）

- [ ] 能列出自己 Agent 的权限边界和需要人工确认的操作
- [ ] 能说明为什么 Agent 评估要看整个任务，而不只是最后的回答

#### W17–18 · 项目 3：简化 Coding Agent · 2/8 – 2/21

原文把这道练习叫作“从 0 到 1 写一个 Claude Code”，参考的是教学项目 learn-claude-code，范围以它为准。

**读什么**

- [ ] [learn-claude-code](https://github.com/shareAI-lab/learn-claude-code)

**要做**

- [ ] 完整阅读 learn-claude-code，理清模块职责和调用关系
- [ ] 追踪一个真实任务：输入进入循环 → 工具执行 → 结果返回 → 继续或停止
- [ ] 从零实现自己的版本
- [ ] 亲手改一个机制（工具错误处理、权限检查或上下文压缩），用测试观察行为变化
- [ ] 至少 3 组 Prompt 修改前后对比

**验收**

- [ ] 能解释循环、工具、权限、上下文管理几个模块怎样协作
- [ ] 改动有对应测试，能演示改动前后的行为差异
- [ ] 仓库包含 README、运行说明和测试

---

## 阶段 4

### 后端工程：让 Agent 成为能运行和维护的服务

`api.serve`
 · W19–24 · 2/22 – 4/4
 · 产出：**项目 4 · AI 服务后端系统**

> 应对真实使用中的问题：多人请求、长任务、会话保存、失败恢复、测试和部署。最终一条命令启动，一条命令测试。

#### W19 · Python Async、FastAPI 与 Pydantic · 2/22 – 2/28

**学什么**

- asyncio、协程、事件循环、任务调度、并发控制、异步 I/O、超时与取消
- 哪些操作会阻塞；加上 async 不等于性能自动变好
- FastAPI：路由、请求响应模型、Depends 依赖注入、中间件、异常处理、生命周期、OpenAPI
- Pydantic：BaseModel、Field、嵌套模型、枚举、校验器、配置、DTO 设计、序列化

**读什么**

- [ ] [Python asyncio 文档](https://docs.python.org/3/library/asyncio.html)
- [ ] [FastAPI 学习文档](https://fastapi.tiangolo.com/zh/learn/)
- [ ] [Pydantic 文档](https://docs.pydantic.dev/latest/)

**动手**

- [ ] 用 asyncio 并发调用模型 API，加上并发上限、超时和取消
- [ ] 在 async 接口里故意放一个阻塞调用，测出它对吞吐的影响
- [ ] 把项目 2 的问答能力包成 FastAPI 接口，入参出参都用 Pydantic 定义

**自测**（能做到再勾）

- [ ] 能判断什么时候该用 async，什么时候不该用
- [ ] 能说明 Depends 解决了什么问题

#### W20 · SQLAlchemy、Alembic 与 PostgreSQL · 3/1 – 3/7

**学什么**

- SQLAlchemy 2.0：模型、关系、查询、事务、连接池、AsyncSession
- Alembic 管理数据库迁移
- PostgreSQL：表设计、索引、事务、锁
- JSONB、全文检索、pgvector

**读什么**

- [ ] [SQLAlchemy Async 文档](https://docs.sqlalchemy.org/en/20/orm/extensions/asyncio.html)
- [ ] [Alembic 文档](https://alembic.sqlalchemy.org/en/latest/)
- [ ] [PostgreSQL 文档](https://www.postgresql.org/docs/)
- [ ] [pgvector](https://github.com/pgvector/pgvector)

**动手**

- [ ] 设计用户、会话、消息、任务四张表，画出它们的关系
- [ ] 用 Alembic 完成一次加字段的迁移，再回滚
- [ ] 如果项目 2 还没用 pgvector，把向量存储迁过来

**自测**（能做到再勾）

- [ ] 能解释任务状态在什么时机更新、失败记录怎样保留
- [ ] 能说出自己建的每个索引服务于哪个查询

#### W21 · Redis 与消息队列 · 3/8 – 3/14

**学什么**

- Redis：String、Hash、Set、ZSet、Stream、TTL、Pipeline、Lua、Pub/Sub；RedisJSON、Vector Search
- 场景：缓存、限流、分布式锁、会话状态、任务状态、轻量消息流
- RabbitMQ：Producer、Consumer、Exchange、Queue、Binding、Routing Key、Ack、Prefetch、死信队列、Quorum Queue
- 文档导入、批量 Embedding、长时间 Agent 任务：后台执行、进度查询、失败处理、避免重复消费

**读什么**

- [ ] [Redis 文档](https://redis.io/docs/latest/)
- [ ] [Redis Search and Query](https://redis.io/docs/latest/develop/interact/search-and-query/)
- [ ] [RabbitMQ Tutorials](https://www.rabbitmq.com/tutorials)
- [ ] [RabbitMQ 文档](https://www.rabbitmq.com/docs)

**动手**

- [ ] 用 Redis 给模型接口做按用户限流
- [ ] 把文档导入改成 RabbitMQ 异步任务，并提供进度查询接口
- [ ] 模拟消费者崩溃，确认消息重新投递后不会重复写入

**自测**（能做到再勾）

- [ ] 能说明缓存、限流、分布式锁各自需要 Redis 提供什么保证
- [ ] 能解释 Ack 和死信队列怎样配合处理失败任务

#### W22 · 测试、容器化与 CI/CD · 3/15 – 3/21

**学什么**

- 单元测试、集成测试、异步测试、Mock、Fixture、测试数据库、接口测试
- 模型 API、数据库、消息队列出错时的测试
- Docker：Dockerfile、镜像构建、环境变量、volume、network、multi-stage build
- Docker Compose 管理本地依赖
- GitHub Actions：workflow、job、step、trigger、secrets、cache、artifact

**读什么**

- [ ] [pytest](https://docs.pytest.org/en/stable/)
- [ ] [pytest-asyncio](https://pytest-asyncio.readthedocs.io/en/latest/)
- [ ] [Docker 入门文档](https://docs.docker.com/get-started/)
- [ ] [Docker Compose 文档](https://docs.docker.com/compose/)
- [ ] [GitHub Actions 文档](https://docs.github.com/en/actions)

**动手**

- [ ] 为模型 API 超时、数据库断连各写一个测试
- [ ] 用 Docker Compose 一次拉起应用、PostgreSQL、Redis、RabbitMQ
- [ ] 配一条 GitHub Actions：提 PR 时自动跑 lint 和 test

**自测**（能做到再勾）

- [ ] 能说明 Mock 外部模型 API 时要覆盖哪些异常
- [ ] 能解释 multi-stage build 为什么能减小镜像

#### W23–24 · 项目 4：AI 服务后端系统 · 3/22 – 4/4

让后端承载项目 2、3 已经做好的 RAG 和 Agent 能力，不为交作业重复搭壳子。

**要做**

- [ ] FastAPI 提供 REST API，Pydantic 定义请求和响应
- [ ] PostgreSQL 保存用户、会话、消息和任务
- [ ] Redis 承担缓存或任务状态
- [ ] RabbitMQ 或后台任务队列处理异步任务
- [ ] 用 Docker Compose 启动本地环境
- [ ] 单元测试 + 接口测试；CI 至少包含 lint 和 test

**验收**

- [ ] 一条命令启动，能访问 API 文档
- [ ] 一条命令运行全部测试
- [ ] 能解释数据库设计、异步任务和错误处理
- [ ] README 包含架构说明、启动方式、接口示例和测试说明

---

## 阶段 5

### 开源项目实战：每个方向挑一个：跑通、讲清、改动、验证

`oss.read`
 · W25–28 · 4/5 – 5/2
 · 产出：**4 份源码学习仓库（笔记 + 改动 + 测试）**

> 不用把这些项目全学一遍。每个方向挑一个，跑通一个有明确验收条件的任务，讲清执行过程，再做一个能验证的小改动。

#### W25 · Coding Agent：Pi 与 Codex CLI · 4/5 – 4/11

**学什么**

- 以 Pi 为主：一次模型调用怎样进入工具执行，结果怎样回到下一轮
- Codex CLI 作对照：同样是读代码、改代码、跑命令，工具执行、权限和任务状态怎样组织

**读什么**

- [ ] [Pi](https://github.com/earendil-works/pi)
- [ ] [Codex CLI](https://github.com/openai/codex)

**动手**

- [ ] 沿一个真实任务分别追踪两者的执行过程，写一份对比笔记
- [ ] 给 Pi 加一个工具或 Extension，验证它确实改变了 Agent 的行为

**自测**（能做到再勾）

- [ ] 能说明两者在权限和任务状态管理上的主要差异

#### W26 · Working Agent：WorkBuddy、OpenWork、Eigent · 4/12 – 4/18

**学什么**

- WorkBuddy 看体验：Agent 怎样接任务、执行、等待确认、交付结果
- OpenWork 读源码：任务界面、工作目录与上下文、执行状态、工具连接、最终产物
- Eigent（选读）：多 Agent 协作中任务怎样拆、角色怎样分工、结果怎样汇总

> 注意：OpenWork 的桌面和核心部分是 MIT 许可，ee/ 目录用的是另一份受限许可证，不要把整个仓库都当成 MIT。

**读什么**

- [ ] [WorkBuddy](https://www.workbuddy.cn/docs/workbuddy/)
- [ ] [OpenWork](https://github.com/different-ai/openwork)
- [ ] [OpenWork ee/ 许可证](https://github.com/different-ai/openwork/blob/dev/ee/LICENSE)
- [ ] [Eigent](https://github.com/eigent-ai/eigent)

**动手**

- [ ] 用 WorkBuddy 完成一个真实小任务，记录它在哪些节点等待确认
- [ ] 在 OpenWork 源码里追踪一次任务从界面到产物的路径

**自测**（能做到再勾）

- [ ] 能画出 OpenWork 里一次任务的状态流转

#### W27 · 常驻助手：先 nanobot，再 OpenClaw · 4/19 – 4/25

**学什么**

- nanobot（Python）：围绕一个容易追踪的 Agent Loop，串起消息入口、工具调用、会话、记忆和定时任务
- OpenClaw：常驻 Gateway、多渠道接入、Skills，以及权限和沙箱配置

> 注意：先用测试账号和非敏感文件运行，不要一启动就把主账号、个人文件和执行权限全交出去。

**读什么**

- [ ] [nanobot](https://github.com/HKUDS/nanobot)
- [ ] [OpenClaw](https://github.com/openclaw/openclaw)

**动手**

- [ ] 跑通 nanobot，加一个定时任务，追踪它的触发路径
- [ ] 对照 OpenClaw，列出 Gateway 和 Skills 比 nanobot 多解决了什么

**自测**（能做到再勾）

- [ ] 能说明常驻助手和一次性 Agent 在状态管理上的区别

#### W28 · Personal Agent：OpenBot 与 OpenDots · 4/26 – 5/2

**学什么**

- OpenBot：每个 Agent 的执行环境怎样隔离，浏览器、文件和工具操作怎样经过统一网关，权限策略和操作记录怎样落下来
- OpenDots：持久会话、后台任务，文字、语音、Slack 等入口怎样衔接，需要确认的操作怎样暂停并在批准后继续

> 注意：两个项目的源码都是 MIT，但运行依赖 CopilotKit Intelligence 等服务。开源不代表整套系统免费，也不代表没有外部服务或额外授权要求。

**读什么**

- [ ] [OpenBot](https://github.com/CopilotKit/OpenBot)
- [ ] [OpenDots](https://github.com/CopilotKit/OpenDots)

**动手**

- [ ] 跑通其中一个，追踪一次需要人工确认的操作怎样暂停、怎样恢复
- [ ] 做一个可验证的小改动，并补上测试

**自测**（能做到再勾）

- [ ] 能说明它的权限策略和操作记录分别落在哪里

---

## 阶段 6

### 进阶：按需

`on_demand`

> 等基础项目里出现了具体需求再深入，不必提前学。

**清单**

- [ ] 向量索引算法：FLAT、IVF、HNSW、PQ 的原理与取舍
- [ ] Advanced RAG：Query Rewrite、HyDE、Self-Query、Agentic RAG、GraphRAG
- [ ] 更复杂的记忆系统
- [ ] Kubernetes：Pod、Deployment、Service、Ingress、ConfigMap、Secret、Job、CronJob、HPA、健康检查、滚动发布
- [ ] 微服务：单体与服务拆分、DDD 边界、同步 / 异步通信、API 网关、配置管理、服务治理、可观测性
- [ ] 求职补充：MySQL、计算机网络的常见面试题（原文作者面试后的经验）

**读什么**

- [ ] [GraphRAG](https://github.com/microsoft/graphrag)
- [ ] [Kubernetes Concepts](https://kubernetes.io/docs/concepts/)
- [ ] [Microservices.io](https://microservices.io/)

---

数学基础轨道整理自《微积分 8 周学习计划（为概率论打基础）》，资源链接为补充。链接指向的文档会更新，字段名和事件结构以你实际使用的 API 文档为准。
