# 模型上架：doubao-seedance-2-5-flash-261115、qwen4-max

字节跳动火山方舟在 **2026 年 11 月 15 日** 新发布了视频生成模型 Seedance 2.5 Flash，模型 ID 是 `doubao-seedance-2-5-flash-261115`。阿里巴巴则在 **2026 年 11 月 16 日**（杭州）正式发布了通义千问新一代旗舰模型 Qwen4-Max，调用 ID 是 `qwen4-max`。2026 年 11 月 19 日傍晚（大约 16:50，Asia/Shanghai），第三方接口聚合站 momoAPIPro（[tryallapi.com](https://tryallapi.com/)）的系统公告写明这两个模型已经上架。公开目录里的创建时间分别是：`qwen4-max` 为 2026-11-19 16:26:49，`doubao-seedance-2-5-flash-261115` 为 2026-11-19 16:52:31。

要在自己的项目或脚本里按量调用，可以从这个注册入口进入：[https://tryallapi.com/register?aff=5A6A](https://tryallapi.com/register?aff=5A6A)。

本文按 **2026 年 11 月 20 日（Asia/Shanghai，UTC+8）** 对公开页面、系统公告、官方文档和当日定价数据的复核来写。需要先说清楚：tryallapi.com / momoAPIPro 是**第三方 API 聚合站**，不是字节跳动、豆包、即梦、火山方舟的官网，也不是阿里巴巴、通义千问或 QwenCloud 的官网，更不是官方 API。同一模型 ID 不等于官方直连，也不等于官方服务等级承诺。模型是否在线、分组是否开放、以及价格都会变，请以当天控制台和模型广场为准。

## 这两个模型是什么

### Seedance 2.5 Flash（视频生成，不是图像模型）

Seedance 2.5 Flash 是字节跳动 / 豆包的**视频生成模型**，不要和同系列的图像模型 Seedream（例如已经上架的 `doubao-seedream-5-5-261028`）搞混，也不要把它当成旗舰版 Seedance 2.5（官方模型 ID 是 `doubao-seedance-2-5-260628`）。

根据火山方舟 [模型发布公告](https://ark.volcengine.com/region:cn-beijing/docs/model-release-announcement)（2026 年 11 月条目，日期 2026-11-15，标注「新发布」）和 [Seedance 2.5 教程](https://ark.volcengine.com/region:cn-beijing/docs/seedance-2-5)（[文档站同文](https://docs.volcengine.com/docs/zh/ark/seedance-2-5.md)）：

- 模型 ID：`doubao-seedance-2-5-flash-261115`。
- 官方写明：支持文生视频、首帧、首尾帧、全能参考（Omni-Reference，可使用图片 / 视频 / 音频及其组合）、视频编辑和延长；**不支持**样片模式（Draft）；分辨率支持 480p 和 720p。
- 教程能力表还列出：可生成有声视频、使用联网搜索工具、返回视频尾帧。
- 参考素材上限共 20 个（图片 10 + 视频 5 + 音频 5）。作为对照，旗舰版 Seedance 2.5 的上限是 50 个（30+10+10），不要把两条模型的限额写混。
- 输出分辨率只有 480p（8-bit）和 720p（8-bit），**不支持** 1080p 和 4K。旗舰版 Seedance 2.5 支持 1080p（10-bit）、4K（10-bit），以及样片模式 / Draft，Flash 都没有这些能力。
- 宽高比：21:9、16:9、4:3、1:1、3:4、9:16，以及自适应。
- 时长：4–30 秒，也可设为 `-1`（由模型在有效范围内自行选择）。Seedance 2.0 系列是 4–15 秒，2.5 系列把上限提高到了 30 秒。
- 输出格式：mp4、mov。
- 不支持离线推理。
- 官方教程还列出 11 种语言：中文、英语、西班牙语、印尼语、马来语、泰语、阿拉伯语、葡萄牙语、越南语、日语、韩语。

官方火山方舟另有开户条件（账户余额大于 200 元，或已购买 200 元及以上的储蓄计划，或持有仍有余量的系列资源包）。这些条件只针对官方方舟，**不适用于** tryallapi，不要把官方开户门槛套到这个第三方通道上。

火山方舟对 Seedance 2.5 Flash 的在线推理是**按百万 token 后付费**，不是 tryallapi 的扣费方式，也不要把下面的人民币标价换算成未经核实的美元分组价。2026 年 11 月 20 日核对 [火山方舟「模型价格」文档](https://ark.volcengine.com/region:cn-beijing/docs/model-pricing)，480p 和 720p 的官方标价是：

| 输入情况 | 官方标价（人民币 / 百万 token） |
| --- | --- |
| 输入不含视频 | 46.00 元/M token |
| 输入包含视频 | 28.00 元/M token |

只有成功生成的视频才会计费。官方还给出了按条估算的示例，均为 16:9、输出时长 5 秒：

| 输入情况 | 480p | 720p | 1080p / 4K |
| --- | --- | --- | --- |
| 输入不含视频 | 2.21 元/条（0.44 元/秒） | 4.97 元/条（0.99 元/秒） | 不支持 |
| 输入包含视频（输入时长 2–30 秒，输出 5 秒） | 2.42–9.42 元/条 | 5.44–21.17 元/条 | 不支持 |

「输入包含视频」这一档，下限对应输入 2–4 秒，上限对应输入 30 秒。官方说明：输入包含视频时，可能按最低 token 用量计费，实际用量以调用后返回的 `usage.completion_tokens` 为准；定价页上也提供了官方计算器。

作为对照，旗舰版 Seedance 2.5 在同样「输入不含视频、16:9、输出 5 秒」的示例里，480p / 720p / 1080p / 4K 分别是 3.36、7.56、18.71、30.13 元/条。Flash 在 1080p 和 4K 上不支持，不要拿旗舰示例去估算 Flash。

### Qwen4-Max（文本 / 多模态理解，输出文本）

根据阿里巴巴 **2026 年 11 月 16 日** 的 [官方新闻稿](https://www.alibabagroup.com/en-US/document-2060139246777270272)：

- Qwen4-Max 是通义千问系列迄今能力最强的模型。
- 采用混合专家（MoE）架构，总参数 2.4 万亿，每个 token 激活 710 亿参数；在同样 2.4T 规模下，激活参数比 Qwen3.8-Max 少 25%。
- 原生支持视觉，上下文窗口为 100 万 token。
- 新闻稿写明它在 Code Arena 上排名第 6，并提到在 Agents' Last Exam、Vals Index、JobBench、Chartography 上表现突出，但没有给出这些榜单的具体分数，本文也不补写未见的数字。
- 在阿里巴巴自有评测 Work360（覆盖 721 个专业领域）上，整体优于 Qwen3.8-Max；在 High effort 推理模式下少用 35% 的 token，单任务平均成本大约降低 60%。
- 已通过 Token Plan 和 API 在 QwenCloud 上线，并登陆 QwenWork、QwenStudio。

新闻稿里只明确写出 Implicit Cache Hit 的输入价是每 100 万 token **$0.075**。完整官方标价以 QwenCloud 价目为准，不要把这一行当成全部官价。

根据 [Qwen4-Max 模型页](https://www.qwencloud.com/models/qwen4-max)、[QwenCloud 模型价格](https://docs.qwencloud.com/developer-guides/getting-started/model-prices) 和 [阿里云 Model Studio 文档](https://www.alibabacloud.com/help/en/model-studio/qwen4-max)（该文档页在检索/抓取时显示最近更新于 2026 年 11 月 18 日）：

- 调用 ID：`qwen4-max`。
- 输入模态：文本、图像、视频；输出：文本。
- 支持联网搜索、工具 / 函数调用、结构化输出（JSON）、前缀续写（prefix completion）、缓存、批量（batch）、深度思考 / 推理。官方还列出流式输出和并行工具调用。
- 官方写明兼容 OpenAI 与 Anthropic API。
- 上下文 1,000,000；最大输入 991,808；最大输出 131,072；思考模式下最大输入 983,616，最大输出 / 最大思维链 262,144。

2026 年 11 月 20 日核对 QwenCloud 官方价目的 **International / Singapore** 页签，非思考与思考模式、在 `0 < Token ≤ 1M` 这一档的标价（USD / 1M tokens）是：

| 计费项 | 官方标价 |
| --- | --- |
| 输入 | $1.50 |
| 输出（含思维链 + 回复） | $4.50 |
| 缓存创建（5 分钟） | $1.875 |
| 缓存创建（1 小时） | $3.00 |
| 显式 / 隐式缓存命中 | $0.075 |

Singapore 页签上还有 100 万 token 免费额度的说明；其他地区可能没有这项免费额度。这是官方 QwenCloud International / Singapore 的说明，**不是** tryallapi 的赠送额度。官方其他地区页签的数字不同（例如出现过 $1.413 / $4.24，以及不同的缓存价），不要把不同地区的官价写进同一张表，请到官方价格页按地区核对。

## 渠道：tryallapi.com（momoAPIPro）按量 API

- **站点：** [https://tryallapi.com/](https://tryallapi.com/)
- **注册入口：** [https://tryallapi.com/register?aff=5A6A](https://tryallapi.com/register?aff=5A6A)

这一条面向要在自己的项目、脚本或客户端里调用模型的人，不是豆包、即梦、火山方舟或 QwenCloud 的官方网页。站点品牌是 **momoAPIPro**，定位是按量计费的 API 聚合。

2026 年 11 月 19 日傍晚（大约 16:50，Asia/Shanghai），站点系统公告发出：「模型上架：doubao-seedance-2-5-flash-261115、qwen4-max」。2026 年 11 月 20 日上午看到的公告板上，这条仍显示为「18小时前」。

![momoAPIPro 系统公告：doubao-seedance-2-5-flash-261115、qwen4-max 已上架](https://upload.maynor1024.live/file/1795142779835_01-announcement.png)

> 图注：2026-11-20 上午系统公告截图。当时最新一条（页面显示「18小时前」）是「模型上架：doubao-seedance-2-5-flash-261115、qwen4-max」。同一块公告里还能看到更早的模型上架，以及部分 Gemini 分组不稳定、部分资源分组因资源紧缺暂时下架的提示，可见上架并不等于所有分组都一直可用。

2026 年 11 月 20 日约 10:41（Asia/Shanghai）拉取的公开定价数据里，这两条模型的状态都是可用。站点上的模型说明分别是：

- `qwen4-max`：厂商标注为 Qwen，类型为对话，标签是「对话」「工具」「识图」，计费类型为按量（USD / 1M tokens）。站点文案写的是：「Qwen4-Max 是通义千问新一代旗舰多模态模型，融合文本生成、图片与视频理解及深度思考能力，适用于编程开发、办公、前端设计与复杂智能体任务。模型支持联网搜索、工具调用和结构化输出，兼容 OpenAI 与 Anthropic API，帮助开发者构建具备多模态理解与任务执行能力的智能应用」。当日支持的接点类型只有 `openai`（OpenAI 兼容 Chat Completions）。官方厂商另外还支持 Anthropic Messages，但不要据此假设 tryallapi 当天也提供 Anthropic 接点。
- `doubao-seedance-2-5-flash-261115`：厂商标注为 Doubao，类型为音视频，标签是「视频」「异步」，计费类型为按次，不是按百万 token。站点文案写的是：「Seedance 2.5 flash (doubao-seedance-2-5-flash-261115) 是字节跳动豆包推出的高效多模态视频生成模型。它完整支持全模态音视频组合参考、有声视频生成及视频编辑延长，兼顾生成速度与强多模态控制能力，最高支持 720p 分辨率输出。」支持的接点类型是 `Doubao video`，同一份定价数据把它映射到 `POST /api/v3/contents/generations/tasks`。开放分组只有 **Seedance-2**，目录里没有为 Flash 列出 Seedance-1 或 Discounted-Seedance-1，本文也不补写未见的分组价。

主要线路是 `https://tryallapi.com`，OpenAI 兼容调用通常要在后面加上 `/v1`，也就是 `https://tryallapi.com/v1`；不要把主机名当成完整路径。文档里的请求示例有时仍把 `model` 固定写成旗舰模型 `doubao-seedance-2-5-260628`，路径是 `POST /api/v3/contents/generations/tasks`，主机有时会写成 `https://api.maynorai.asia`。调用 Flash 时请把 `model` 设成 `doubao-seedance-2-5-flash-261115`，并以当天文档里的实际路径为准。备用线路 `https://api.maynorai.asia` 在控制台里被写成备用线路且处于屏蔽状态，这里不讨论如何绕过。

### 分组价格（2026-11-20 公开定价数据）

**qwen4-max**

单位是 **USD / 1M Tokens**，按量计费。下表按 2026 年 11 月 20 日约 10:41（Asia/Shanghai）的公开定价数据计算，使用前请回到模型广场或定价页核对。当日开放的分组只有 **Alibaba-2** 和 **Alibaba-3**，目录里没有 Alibaba-1，这里也不编造它的价格。

| 分组 | 输入 | 输出 | 缓存命中 | 缓存创建（5 分钟） | 缓存创建（1 小时） |
| --- | --- | --- | --- | --- | --- |
| Alibaba-2 | $2.4750 | $7.4250 | $0.1238 | $3.0938 | $4.9500 |
| Alibaba-3 | $3.6300 | $10.8900 | $0.1815 | $4.5375 | $7.2600 |

对照官方 QwenCloud International / Singapore 标价（输入 $1.50、输出 $4.50）：这两个分组都**高于**官价。Alibaba-2 的输入是 $2.4750，相当于官方 $1.50 的 1.65 倍，高出 65%。**不要默认所有分组都比官方便宜。** 付费前先看当天页面。

**doubao-seedance-2-5-flash-261115**

这是视频模型，公开目录里的计费类型是**按次**，开放分组只有 Seedance-2，接点是 Doubao video。官方方舟按百万 token 计价，而且会随分辨率、输入是否包含视频而变化；同一份公开定价数据里，Flash 和旗舰版 `doubao-seedance-2-5-260628` 在同一分组下出现了相同的原始单价字段，单靠这一条乘数无法还原官方那种按分辨率、按是否包含视频输入的价差。因此本文**不把**该字段乘以分组倍率后写成每条视频或每秒的美元单价。请回到当天的模型广场和账单，看实际展示的计费单位和扣费。上面列出的官方方舟人民币标价，只作对照，不能直接当成 tryallapi 的扣费。

另外，廉价分组也可能因资源紧张被临时下架。同一份系统公告里，仍然可以看到部分 Gemini 分组不稳定，以及 gemini-4-carbon anti、AWS-Gpt-1 等资源分组因资源紧缺暂时下架的提示——这提醒我们：公告上架只说明模型已出现在目录里，不保证某个分组随时都能打通，也不保证无等待。

## 怎么接入

1. 打开 [https://tryallapi.com/register?aff=5A6A](https://tryallapi.com/register?aff=5A6A) 注册并登录。
2. 在控制台创建令牌（API Key）。不要把密钥发到聊天、截图或文章里。
3. 调用 `qwen4-max` 时，把客户端的 Base URL 设为站点当天展示的地址（常见写法是 `https://tryallapi.com/v1`），`model` 填写 `qwen4-max`，走 OpenAI 兼容的对话接口。
4. 调用 Seedance 2.5 Flash 时，请走站点当天标明的 Doubao video 路径（公开映射是 `POST /api/v3/contents/generations/tasks`），`model` 填写 `doubao-seedance-2-5-flash-261115`。它是异步任务：先创建任务再查询结果，不要把它当聊天模型用。
5. 实际扣费以控制台账单和当时命中的分组为准。
