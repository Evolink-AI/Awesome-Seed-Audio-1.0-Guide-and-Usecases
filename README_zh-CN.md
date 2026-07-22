<div align="center">

<a href="https://evolink.ai/seed-audio-1-0?utm_source=github&utm_medium=banner&utm_campaign=awesome-seed-audio-1.0-usecases&utm_content=readme_banner"><img src="https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/images/en.png" alt="Seed-Audio 1.0 usecase repository banner" width="760"></a>

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](LICENSE)
[![Try it on Evolink](https://img.shields.io/badge/Try_it_on-Evolink-black)](https://evolink.ai/seed-audio-1-0?utm_source=github&utm_medium=badge&utm_campaign=awesome-seed-audio-1.0-usecases&utm_content=model_try)
[![Docs](https://img.shields.io/badge/Docs-Read-blue)](https://docs.evolink.ai/en/api-manual/audio-series/doubao-seed-audio/doubao-seed-audio-1-0?utm_source=github&utm_medium=docs&utm_campaign=awesome-seed-audio-1.0-usecases&utm_content=docs_link)

[![English](https://img.shields.io/badge/English-111111)](README.md) [![Español](https://img.shields.io/badge/Espa%C3%B1ol-ffb703)](README_es.md) [![Português](https://img.shields.io/badge/Portugu%C3%AAs-2a9d8f)](README_pt.md) [![日本語](https://img.shields.io/badge/%E6%97%A5%E6%9C%AC%E8%AA%9E-52b788)](README_ja.md) [![한국어](https://img.shields.io/badge/%ED%95%9C%EA%B5%AD%EC%96%B4-4ea8de)](README_ko.md) [![Deutsch](https://img.shields.io/badge/Deutsch-f4a261)](README_de.md) [![Français](https://img.shields.io/badge/Fran%C3%A7ais-e76f51)](README_fr.md) [![Türkçe](https://img.shields.io/badge/T%C3%BCrk%C3%A7e-d62828)](README_tr.md) [![繁體中文](https://img.shields.io/badge/%E7%B9%81%E9%AB%94%E4%B8%AD%E6%96%87-8338ec)](README_zh-TW.md) [![简体中文](https://img.shields.io/badge/%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-ef476f)](README_zh-CN.md) [![Русский](https://img.shields.io/badge/%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9-577590)](README_ru.md)

</div>

# Seed-Audio 1.0 使用案例：旁白、音频剧、参考声音与音频优先视频工作流

## 🍌 介绍

欢迎来到 Seed-Audio 1.0 高信号使用案例仓库。

**我们基于公开 X/Twitter 来源和 EvoLink 文档，整理 Seed-Audio 1.0 的真实使用案例、创作者工作流、平台集成、评估和实践限制。**

本简体中文 README 保留公开来源链接、作者署名和锚点，同时翻译用户可见说明文字。

[在 EvoLink 上试用 Seed-Audio 1.0](https://evolink.ai/seed-audio-1-0?utm_source=github&utm_medium=readme&utm_campaign=awesome-seed-audio-1.0-usecases&utm_content=introduction_cta)

## 📊 概览

- **从近期 X/Twitter 样本中筛选出 21 个 Seed-Audio 1.0 使用案例，原始可用样本为 99 条。**
- 覆盖方向：音频优先视频工作流, 音频剧与场景生成, 参考声音与角色配音探索, 工具与服务商集成, 社交旁白、拟音与成本测试。
- 每个案例都包含原始来源、创作者署名、使用结论、证据类型和发布日期。
- 你可以用这个仓库查找真实工作流、比较优势和限制、发现服务商路径，并把实现工作导向 EvoLink。

> [!NOTE]
> 本地化 README 与英文源文件保持相同的案例顺序、链接、锚点和署名。

> [!NOTE]
> 本仓库优先收录具体工作流证据，而不是纯宣传：演示、设置说明、服务商发布、上手评估和明确限制。

[更新日志](docs/update-log.md) | [维护指南](docs/maintenance.md) | [案例标注审计](docs/case-label-audit.md) | [案例数据](data/use-cases.json) | [预设音色文档](https://docs.evolink.ai/en/api-manual/audio-series/doubao-seed-audio/doubao-seed-audio-1-0-voices?utm_source=github&utm_medium=docs&utm_campaign=awesome-seed-audio-1.0-usecases&utm_content=voice_docs)

<a id="quick-start"></a>
## ⚡ 快速开始

先安装 Seed-Audio agent skill，然后到 [Get API Key](https://evolink.ai/dashboard/keys?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-seed-audio-1.0-usecases&utm_content=api_key) 获取 API key，并设置为 `EVOLINK_API_KEY`。

```bash
npm i evolink-seed-audio

export EVOLINK_API_KEY="your_api_key_here"

TASK_JSON=$(curl --silent --request POST \
  --url https://api.evolink.ai/v1/audios/generations \
  --header "Authorization: Bearer ${EVOLINK_API_KEY}" \
  --header 'Content-Type: application/json' \
  --data '{"model":"doubao-seed-audio-1-0","prompt":"Welcome to the audio generation service.","format":"mp3"}')

echo "$TASK_JSON"
TASK_ID=$(python3 -c 'import json,sys; data=json.load(sys.stdin); print(data.get("id") or data.get("task_id") or "")' <<<"$TASK_JSON")
[ -n "$TASK_ID" ] || { echo "Task creation did not return an id" >&2; exit 1; }

while true; do
  STATUS_JSON=$(curl --silent --request GET \
    --url "https://api.evolink.ai/v1/tasks/${TASK_ID}" \
    --header "Authorization: Bearer ${EVOLINK_API_KEY}")
  echo "$STATUS_JSON"
  STATUS=$(python3 -c 'import json,sys; data=json.load(sys.stdin); print((data.get("status") or data.get("task", {}).get("status") or "").lower())' <<<"$STATUS_JSON")
  if [ "$STATUS" = "completed" ]; then
    python3 -c 'import json,sys; data=json.load(sys.stdin); print(data.get("output_url") or data.get("result_url") or data.get("url") or data.get("task", {}).get("output_url") or data.get("task", {}).get("result_url") or "")' <<<"$STATUS_JSON"
    break
  fi
  if [ "$STATUS" = "failed" ] || [ "$STATUS" = "cancelled" ]; then
    echo "Task ${TASK_ID} ended with status ${STATUS}" >&2
    exit 1
  fi
  sleep 5
done
```

Endpoint: `POST https://api.evolink.ai/v1/audios/generations`

skill 包发布为 [evolink-seed-audio](https://www.npmjs.com/package/evolink-seed-audio)，用于 agent 和本地 skill 工作流。

## 📑 目录

| 章节 | 案例 |
|---|---|
| [音频优先视频工作流](#audio-first-video) | 案例 1, 案例 2, 案例 3, 案例 12, 案例 13, 案例 15, 案例 17, 案例 18 |
| [音频剧与场景生成](#audio-drama-scene-generation) | 案例 4, 案例 5 |
| [参考声音与角色配音探索](#voice-reference-character-casting) | 案例 6, 案例 8, 案例 10, 案例 19 |
| [工具与服务商集成](#tool-provider-integrations) | 案例 7, 案例 14, 案例 16 |
| [社交旁白、拟音与成本测试](#social-narration-foley-cost-tests) | 案例 9, 案例 11 |
| [致谢](#acknowledge) | 来源致谢与修正政策 |

<a id="audio-first-video"></a>
## 音频优先视频工作流

| 案例 | 展示重点 | 类型 |
|---|---|---|
| [案例 1: 用六人音频引导 Seedance 视频](#case-1) | 构建音频优先的视频工作流：先用公开 Seed Audio prompt 生成六个角色对白和背景音效，再进入图像与 Seedance 视频生成。 | Tutorial |
| [案例 2: 多片段故事视频的音频规划](#case-2) | 评估多片段故事视频中的 agentic soundscape 生成，并保留音效与画面动作仍可能不匹配的限制。 | Evaluation |
| [案例 3: 音频优先的 Seedance 参考工作流](#case-3) | 采用官方三步流程：先生成 Seed-Audio，再创建关键视觉图，最后把音频和视觉一起作为 Seedance 2 reference-to-video 的参考。 | Tutorial |
| [案例 12: 用 Claude 在 Premiere 中编排音乐与音效](#case-12) | 将音乐、音效和人声拆成独立生成，再让 Claude 把音频装配进 Premiere，同时保留对节奏与淡入淡出的手动控制。 | Tutorial |
| [案例 13: 参考音频格斗解说时序测试](#case-13) | 先把 Seedance 成片作为 Seed Audio 的参考输入，再根据画面动作生成带时间轴的解说词，并把时序对齐当作主要评估风险。 | Evaluation |
| [案例 15: Agent 重写正向版本的视频旁白测试](#case-15) | 把现有视频交给 agent，让它为新的情绪方向重写脚本，再用 Seed Audio 合成匹配的新旁白，然后重建画面。 | Evaluation |
| [案例 17: 按节拍对齐的预告片声音设计](#case-17) | 先锁定角色和静帧，再把预告片剪辑对齐到音乐时间点，并只在需要精确落点的旁白或强调音效位置使用 Seed Audio。 | Tutorial |
| [案例 18: 用 Seed Audio 完成的双图动画短片](#case-18) | 把一张或两张参考图当作视觉锁定层，再让 Seed Audio 负责配乐，最后由 Seedance 把短片扩展成完整动画。 | Demo |

<a id="audio-drama-scene-generation"></a>
## 音频剧与场景生成

| 案例 | 展示重点 | 类型 |
|---|---|---|
| [案例 4: 带环境声的两分钟对白](#case-4) | 用脚本格式编写音频剧 prompt，同时指定环境声、角色声音、背景音乐和逐句表演方向。 | Tutorial |
| [案例 5: 博物馆导览式场景对白](#case-5) | 测试场景级对白推理：Seed-Audio 能从紧凑情境 prompt 中生成台词、表达方式和角色声音。 | Demo |

<a id="voice-reference-character-casting"></a>
## 参考声音与角色配音探索

| 案例 | 展示重点 | 类型 |
|---|---|---|
| [案例 6: 参考声音 MC 工作流](#case-6) | 从参考素材生成固定 MC 声音，将音频切分后作为 Seedance 2.0 lip-sync 视频参考。 | Tutorial |
| [案例 8: 参考音频质量与高声线限制](#case-8) | 基于实际使用评估日语稳定性、情绪跟随、参考音频精度，以及高声线机械感风险。 | Evaluation |
| [案例 10: 图像引导的角色声音探索](#case-10) | 用参考图片做早期角色声音 casting，同时把 pitch 和 tone 稳定性视为未解决的生产风险。 | Evaluation |
| [案例 19: 同画面换音频的 TTS 质量对比](#case-19) | 在锁定正式 TTS 方案前，先保持成片画面不变，只替换音轨，就能更快比较 Seed Audio 与其他 TTS 的情绪、口音和原声泄漏问题。 | Evaluation |

<a id="tool-provider-integrations"></a>
## 工具与服务商集成

| 案例 | 展示重点 | 类型 |
|---|---|---|
| [案例 7: Claude MCP 旁白与多语言配音集成](#case-7) | 通过 Higgsfield MCP 在 Claude 内完成旁白、声音克隆和多语言配音，Seed Audio 1.0 是其中的音频能力之一。 | Integration |
| [案例 14: 用克隆旁白驱动动态图形技能工作流](#case-14) | 先用 Seed Audio 克隆自己的声音，再把生成的旁白当作时间轴骨架，驱动带文本、图形动画、BGM 和字幕的动态图形视频。 | Tutorial |
| [案例 16: 单照片 Scenario MCP 冒险预告片](#case-16) | 用一张人像加一条编排 prompt，就能让 Codex/GPT 的 MCP 工作流在一次运行里完成多场景 Seedance 镜头、Seed Audio 旁白、配乐和成片包装。 | Integration |

<a id="social-narration-foley-cost-tests"></a>
## 社交旁白、拟音与成本测试

| 案例 | 展示重点 | 类型 |
|---|---|---|
| [案例 9: 社交故事旁白内容引擎](#case-9) | 把公开文字故事帖转成音频优先娱乐内容，并评估它能否成为可重复的内容引擎。 | Demo |
| [案例 11: 低成本测试声音表演与拟音](#case-11) | 在投入下游视频生成前，把 Seed-Audio 作为声音表演和拟音的低成本测试层。 | Evaluation |

<a id="case-1"></a>
### 案例 1: [用六人音频引导 Seedance 视频](https://x.com/gokayfem/status/2070429287950188547) (作者 [@gokayfem](https://x.com/gokayfem))

**构建音频优先的视频工作流：先用公开 Seed Audio prompt 生成六个角色对白和背景音效，再进入图像与 Seedance 视频生成。**

- 证据来源：原推公开了实际 Seed Audio 设置：雨夜逃亡面包车场景、六个具名角色、不同声线方向、短对白、发动机怠速、车顶雨声和背景音效，并同时给出后续 Nano Banana Pro 图像 prompt 与 Seedance 2.0 视频 prompt。
- 可复制做法：当音频需要主导整段视频时，先写清角色表、每个角色的声音质感、短句对白和持续环境声，再把它作为后续视频节奏和情绪的参考。
- 实际流程：先生成完整多人对白和环境声底，再生成匹配人物轮廓与氛围的关键视觉图，最后把音频和视觉一起交给 Seedance 做最终运动画面。
- 注意事项：这个来源能证明工作流和 prompt 结构有学习价值，但不能保证长场景里每个角色都永久稳定。正式生产前要专门测试说话人区分、节奏和转场。

[![案例 1 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-01.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-01.mp4)

[打开视频播放页](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-01.mp4)

类型: Tutorial | 日期: 2026-06-26

---

<a id="case-2"></a>
### 案例 2: [多片段故事视频的音频规划](https://x.com/gavinpurcell/status/2070246132341727506) (作者 [@gavinpurcell](https://x.com/gavinpurcell))

**评估多片段故事视频中的 agentic soundscape 生成，并保留音效与画面动作仍可能不匹配的限制。**

- 证据来源：作者从一条一分钟多片段低清故事视频出发，明确指出 Seedance 多片段故事里的音频一致性很难，然后测试把视频上下文交给 Claude Code、Codex，并配合 FAL key 生成音景。
- 可复制做法：把 Seed-Audio 当成已有视频的音频修复或规划层，尤其适合一个视频里包含多个镜头、转场、环境声和动作音效的情况。
- 实际流程：先让 agent 读取视频情境并产出逐镜头音频计划，再生成背景声、环境声或音效，最后按每个片段核对声音是否跟画面动作对齐。
- 注意事项：同作者后续说明部分 SFX 仍然没有准确匹配画面动作，所以它是评估案例，不是完整教程。它的价值在于教你如何测试，以及提醒多片段视频仍有错配风险。

[![案例 2 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-02.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-02.mp4)

[打开视频播放页](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-02.mp4)

类型: Evaluation | 日期: 2026-06-25

---

<a id="case-3"></a>
### 案例 3: [音频优先的 Seedance 参考工作流](https://x.com/EvoLinkAi/status/2070722722217578562) (作者 [@EvoLinkAi](https://x.com/EvoLinkAi))

**采用官方三步流程：先生成 Seed-Audio，再创建关键视觉图，最后把音频和视觉一起作为 Seedance 2 reference-to-video 的参考。**

- 证据来源：来源明确给出三步流程：先用 Seed-Audio 1.0 生成音频，再生成关键视觉图，最后把音频和视觉一起作为 Seedance 2 reference-to-video 的参考。
- 可复制做法：当音乐、旁白、环境声或节奏应该先决定视频走向时，不要先做视频再补声音，而是先把情绪和时间线写进音频 prompt。
- 实际流程：先确定音频里的情绪弧线、旁白节奏和环境声，再创建匹配场景的图片，最后把两者共同作为参考，让视频模型同时获得时间和视觉方向。
- 注意事项：这是官方式工作流模板，不是独立 benchmark。它适合作为起点，但仍需要单独检查 lip-sync、镜头节奏，以及视频是否真的跟随音频 cue。

[![案例 3 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-03.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-03.mp4)

[打开视频播放页](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-03.mp4)

类型: Tutorial | 日期: 2026-06-27

---

<a id="case-4"></a>
### 案例 4: [带环境声的两分钟对白](https://x.com/tarumainfo/status/2071255504907891186) (作者 [@tarumainfo](https://x.com/tarumainfo))

**用脚本格式编写音频剧 prompt，同时指定环境声、角色声音、背景音乐和逐句表演方向。**

- 证据来源：原推给出一个两分钟音频剧 prompt/script，包含 INTENT、AESTHETIC、EXECUTION 结构，并写明环境声、背景音乐、两个角色声线、情绪表达和逐句对白。
- 可复制做法：需要做音频剧而不是单人旁白时，可以照这个结构写：先定义空间和环境声，再定义角色声音，最后在台词里嵌入短促的表演方向。
- 实际流程：把场景写成短剧本，控制每句表演指令不要太长，同时保留持续背景音，让模型既能跟随情绪，也能保持场景质感。
- 注意事项：作者认为结果较好地跟随了 prompt，但长音频仍要检查一致性。生产内容最好把长场景拆成多个 beat，避免角色情绪或背景音乐中途漂移。

[![案例 4 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-04.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-04.mp4)

[打开视频播放页](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-04.mp4)

类型: Tutorial | 日期: 2026-06-28

---

<a id="case-5"></a>
### 案例 5: [博物馆导览式场景对白](https://x.com/TomLikesRobots/status/2070923534449119424) (作者 [@TomLikesRobots](https://x.com/TomLikesRobots))

**测试场景级对白推理：Seed-Audio 能从紧凑情境 prompt 中生成台词、表达方式和角色声音。**

- 证据来源：作者给出的紧凑情境是：博物馆导览员向困惑访客解释 crossing the Rubicon 为什么表示越过不可回头的临界点。帖子说明 Seed Audio 生成了对白、表达方式和角色声音。
- 可复制做法：当你不想逐句写剧本，而是希望模型从一个教育场景中推导短对白时，可以给角色关系、要解释的概念和对话语境。
- 实际流程：输入角色身份、解释对象、听众困惑点和语气要求；生成后重点检查讲话是否自然，以及解释是否准确。
- 注意事项：这是演示案例，因为来源证明了场景级语言推理和自然表达，但没有提供完整生产流程。用于教育内容时必须复核事实正确性。

[![案例 5 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-05.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-05.mp4)

[打开视频播放页](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-05.mp4)

类型: Demo | 日期: 2026-06-27

---

<a id="case-6"></a>
### 案例 6: [参考声音 MC 工作流](https://x.com/JPAI_HEAVEN/status/2070842306329227264) (作者 [@JPAI_HEAVEN](https://x.com/JPAI_HEAVEN))

**从参考素材生成固定 MC 声音，将音频切分后作为 Seedance 2.0 lip-sync 视频参考。**

- 证据来源：原推描述了参考声音工作流：先用来源 voice 作为参考，在 Seed Audio 里生成约一分钟 MC 音频；再把生成音频切分，并交给 Seedance 2.0 做 lip-sync 视频。
- 可复制做法：当系列内容需要固定主持人、播报员或 MC 声音时，可以先做一段较长的干净参考音频，再切成可复用片段。
- 实际流程：先生成一分钟左右的主持声音，挑选发音稳定的片段，按视频台词切分，再作为视频生成或 lip-sync 的声音参考。
- 注意事项：作者明确记录了下游视频生成后声音会轻微变化，因此这个案例是工作流教程，不是声音身份稳定性的保证。最终片段仍需要后期校正。

[![案例 6 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-06.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-06.mp4)

[打开视频播放页](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-06.mp4)

类型: Tutorial | 日期: 2026-06-27

---

<a id="case-7"></a>
### 案例 7: [Claude MCP 旁白与多语言配音集成](https://x.com/higgsfield/status/2070916672106680360) (作者 [@higgsfield](https://x.com/higgsfield))

**通过 Higgsfield MCP 在 Claude 内完成旁白、声音克隆和多语言配音，Seed Audio 1.0 是其中的音频能力之一。**

- 证据来源：Higgsfield 表示 Claude 可以通过其 MCP 集成生成音频，覆盖旁白、声音克隆和 50 多种语言配音，能力栈中包含 Seed Audio 1.0。
- 可复制做法：这个案例适合理解 agent 或 no-code 访问路径：创作者不一定直接调用音频 endpoint，也可以在 Claude 里通过 MCP 服务商完成配音任务。
- 实际流程：从短旁白或配音请求开始，在 Claude 内调用 MCP 生成，再检查输出语言、声音身份和媒体工作流是否满足目标。
- 注意事项：这是集成案例，不是质量评测。来源证明了可访问路径和产品入口，但不能独立证明 50 多种语言的配音质量都可靠。

[![案例 7 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-07.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-07.mp4)

[打开视频播放页](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-07.mp4)

类型: Integration | 日期: 2026-06-27

---

<a id="case-8"></a>
### 案例 8: [参考音频质量与高声线限制](https://x.com/genel_ai/status/2070438167019409582) (作者 [@genel_ai](https://x.com/genel_ai))

**基于实际使用评估日语稳定性、情绪跟随、参考音频精度，以及高声线机械感风险。**

- 证据来源：作者报告了日语实测体验：Seed Audio 的日语语音比 Seedance 2.0 原生音频更稳定，能跟随台词情绪，参考音频精度较高，参考音频最长 30 秒，同时记录不能同时使用音频和图像 reference，高声线更机械。
- 可复制做法：把这个案例当成非英语语音质量检查清单：稳定性、情绪跟随、参考精度、reference 模式限制和高 pitch 风险。
- 实际流程：分别用普通声线和高声线跑短片段，跟参考音频做对比；如果你还需要图像引导，要单独测，因为来源指出音频和图像 reference 不能合用。
- 注意事项：这个案例的核心不是宣称 Seed-Audio 永远更好，而是把表现好和需要谨慎的地方都列出来，所以标注为评估。

[![案例 8 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-08.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-08.mp4)

[打开视频播放页](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-08.mp4)

类型: Evaluation | 日期: 2026-06-26

---

<a id="case-9"></a>
### 案例 9: [社交故事旁白内容引擎](https://twitter.com/deepwhitman/status/2071485165390704837) (作者 [@deepwhitman](https://x.com/deepwhitman))

**把公开文字故事帖转成音频优先娱乐内容，并评估它能否成为可重复的内容引擎。**

- 证据来源：作者用 Seed Audio 1.0 给一条热门 AITA 风格文字帖做旁白，并把这种形式明确描述为可能的 viral content engine。同作者回复补充了原始故事链接。
- 可复制做法：当你想测试文字型社交内容能否变成低成本短视频娱乐内容时，可以用它作为 text-to-narration 模板。
- 实际流程：选择有公开来源的文字故事，拆成旁白段落，生成声音，再搭配简单视觉、字幕或视频素材，最后观察这种格式能否重复生产。
- 注意事项：这是演示案例，不等于版权或增长已经成立。正式使用时要处理授权和来源标注，也要用真实发布数据验证它是否能成为内容渠道。

[![案例 9 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-09.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-09.mp4)

[打开视频播放页](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-09.mp4)

类型: Demo | 日期: 2026-06-29

---

<a id="case-10"></a>
### 案例 10: [图像引导的角色声音探索](https://x.com/tc50501/status/2070498347824337389) (作者 [@tc50501](https://x.com/tc50501))

**用参考图片做早期角色声音 casting，同时把 pitch 和 tone 稳定性视为未解决的生产风险。**

- 证据来源：作者测试 image-to-audio，只传入女性角色参考图，生成三条约十秒台词；结果两条声质方向接近，一条明显偏高。
- 可复制做法：把图像引导音频用于早期角色声音 casting：先探索一个角色可能听起来是什么方向，而不是直接锁定最终配音。
- 实际流程：用同一角色图测试多条短台词，对比 pitch、tone 和角色感是否一致，只保留跨多条台词仍稳定的候选。
- 注意事项：来源本身指出音高和音色稳定性还不适合固定电影角色声生产，所以它是评估案例，价值在于定义可用的探索阶段和明确风险。

![案例 10 media](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-10.jpg)

类型: Evaluation | 日期: 2026-06-26

---

<a id="case-11"></a>
### 案例 11: [低成本测试声音表演与拟音](https://x.com/TomLikesRobots/status/2070288519684108353) (作者 [@TomLikesRobots](https://x.com/TomLikesRobots))

**在投入下游视频生成前，把 Seed-Audio 作为声音表演和拟音的低成本测试层。**

- 证据来源：作者报告早期测试中，voice acting 和 foley 比 Seedance 2 原生音频更好，并提到 15 秒音频测试成本只有几美分。
- 可复制做法：把 Seed-Audio 用作低成本预生产测试层，在投入视频生成前先验证声音表演、拟音和环境声方向是否值得继续。
- 实际流程：先生成 10 到 15 秒短音频，对比它和视频模型原生音频的表现；只有当声音方向足够强时，再进入下游视频生成。
- 注意事项：评论里补充了 reference voice conversion 可能失败，以及生成音频如何最好地进入 Seedance lip-sync 仍未解决。因此它是评估案例，不是完整最终管线。

[![案例 11 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-11.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-11.mp4)

[打开视频播放页](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-11.mp4)

类型: Evaluation | 日期: 2026-06-25

---

<a id="case-12"></a>
### 案例 12: [用 Claude 在 Premiere 中编排音乐与音效](https://x.com/mattworkman/status/2076148989687181705) (作者 [@mattworkman](https://x.com/mattworkman))

**将音乐、音效和人声拆成独立生成，再让 Claude 把音频装配进 Premiere，同时保留对节奏与淡入淡出的手动控制。**

- 证据来源：Matt Workman 说明，他让 Claude 根据剧本中途变化的情绪为音乐床编写 Seed Audio 提示，并挑选、生成关键音效。
- 可复制做法：需要更精细地控制质量和混音时，不要让 Seed Audio 一次同时生成音乐、音效和人声，而是把它们拆成独立轨道。
- 实际流程：把剧本交给 Claude，分别生成 Seed Audio 音乐与音效素材，再让 Claude 在 Premiere 中自动装配这些轨道，最后手动调整参数、时间点与淡入淡出。
- 注意事项：来源表达的是作者对分轨生成质量更好的实践偏好，并非受控基准；应在自己的素材上把分轨方案与一次性混合生成进行对比。

![案例 12 media](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-12.jpg)

类型: Tutorial | 日期: 2026-07-12

---

<a id="case-13"></a>
### 案例 13: [参考音频格斗解说时序测试](https://x.com/aimikoda/status/2076526254417735781) (作者 [@aimikoda](https://x.com/aimikoda))

**先把 Seedance 成片作为 Seed Audio 的参考输入，再根据画面动作生成带时间轴的解说词，并把时序对齐当作主要评估风险。**

- 证据来源：父帖展示最终格斗片段，并指向回复贴 https://x.com/aimikoda/status/2076527528227815779；该回复公开了 Midjourney、Seedance 2.0 与 Seed Audio 的完整提示词，并说明作者把成片音频作为 Seed Audio 参考。
- 可复制做法：先把视觉打斗片段剪成最终版，再提取成片音频作为 Seed Audio 参考，同时让另一模型根据画面动作生成解说文案。
- 实际流程：用 Midjourney 做角色和擂台素材，生成多条 Seedance 打斗片段并剪出最强片段，导出成片音频，交给 GPT-5.6 按画面写解说，再用包含时长、声线、环境、时间轴提示和 negative 约束的 Seed Audio 提示词生成解说。
- 注意事项：作者说大约试了十次，时序仍未完全贴合，因此这更适合作为 Evaluation；预计还要继续改 prompt 或做手动同步。

[![案例 13 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-13.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-13.mp4)

[打开视频播放页](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-13.mp4)

类型: Evaluation | 日期: 2026-07-13

---

<a id="case-14"></a>
### 案例 14: [用克隆旁白驱动动态图形技能工作流](https://x.com/akiyoshisan/status/2077650497536987154) (作者 [@akiyoshisan](https://x.com/akiyoshisan))

**先用 Seed Audio 克隆自己的声音，再把生成的旁白当作时间轴骨架，驱动带文本、图形动画、BGM 和字幕的动态图形视频。**

- 证据来源：作者明确表示视频是用 MiniMax Hub 的动态图形技能制作的，并公开列出了流程：用 Seed Audio 1.0 克隆自己的声音、生成旁白、确认时长和内容、为 15 秒成片设计 6 张分镜、编写日文画面文字、规划连续的图形变形过渡、用 Seedance 2.0 Fast 出视频，再合成旁白、BGM、音效和日文字幕。
- 可复制做法：当你要做短讲解或动态图形视频时，可以把 Seed Audio 的声音克隆和旁白生成当成时间轴主线，再让分镜卡片、文字覆盖和动画节奏围绕这条主线同步展开。
- 实际流程：先准备源声音并在 Seed Audio 中生成旁白，锁定目标时长，再按这段旁白长度设计分镜，补齐文本和图形动作，渲染视频后把旁白、音乐、音效和字幕一起混到最终成片。
- 注意事项：这条帖子证明了工作流形态和所用工具链，但没有公开具体 prompt 或节点配置。适合把它当成可迁移的生产模式，而不是 prompt 复现案例。

[![案例 14 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-14.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-14.mp4)

[打开视频播放页](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-14.mp4)

类型: Tutorial | 日期: 2026-07-16

---

<a id="case-15"></a>
### 案例 15: [Agent 重写正向版本的视频旁白测试](https://x.com/fabianstelzer/status/2077138756939727067) (作者 [@fabianstelzer](https://x.com/fabianstelzer))

**把现有视频交给 agent，让它为新的情绪方向重写脚本，再用 Seed Audio 合成匹配的新旁白，然后重建画面。**

- 证据来源：作者表示，一个由 Claude 驱动的 Glif agent 先接收原视频链接，再用 Gemini 3.5 观看视频、写出更正向的新脚本、调用 Seed Audio 生成相似声线的旁白，最后再用 NB2 做静帧、用 Remotion 组装成片。
- 可复制做法：当你测试 agent 式视频改写流程时，可以把 Seed Audio 放在“保留原有说话风格、但替换叙述内容”的旁白层。
- 实际流程：先把源视频交给 agent，要求它改写语气；让 agent 理解视频内容并生成新脚本；再用 Seed Audio 产出替代旁白，随后重建或扩展画面，并把节奏与配乐单独复核。
- 注意事项：作者明确指出节奏和速度仍需人工打磨，图像质感仍受模型选择限制，而且 ElevenLabs 的配乐尝试失败了。因此它更适合作为评估型流程，而不是无监督成片方案。

[![案例 15 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-15.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-15.mp4)

[打开视频播放页](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-15.mp4)

类型: Evaluation | 日期: 2026-07-14

---

<a id="case-16"></a>
### 案例 16: [单照片 Scenario MCP 冒险预告片](https://x.com/emmanuel_2m/status/2078227114818707891) (作者 [@emmanuel_2m](https://x.com/emmanuel_2m))

**用一张人像加一条编排 prompt，就能让 Codex/GPT 的 MCP 工作流在一次运行里完成多场景 Seedance 镜头、Seed Audio 旁白、配乐和成片包装。**

- 证据来源：公开回复给出了四步 MCP 流程和完整预告片 prompt，而父帖展示了只用一张上传照片做出的印第安纳·琼斯风格成片。
- 可复制做法：如果你想让 MCP agent 一次性协调场景生成、旁白、配乐、海报和最终包装，可以先准备一张正脸人像，再配一条总控 prompt。
- 实际流程：在 Codex 或 GPT 5.6 中加载 Scenario MCP，上传人像，运行公开 prompt，让 agent 在至少十个 Seedance 场景里保持人物一致性，再把 Seed Audio 旁白、音乐和复古标题卡组合成片。
- 注意事项：这个来源证明了编排模式和 prompt 边界，但没有公开中间重试或手工修剪过程。应把它看作集成型工作流，而不是保证一键完成的承诺。

![案例 16 media](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-16.jpg)

类型: Integration | 日期: 2026-07-17

---

<a id="case-17"></a>
### 案例 17: [按节拍对齐的预告片声音设计](https://x.com/maxescu/status/2078146037517312129) (作者 [@maxescu](https://x.com/maxescu))

**先锁定角色和静帧，再把预告片剪辑对齐到音乐时间点，并只在需要精确落点的旁白或强调音效位置使用 Seed Audio。**

- 证据来源：公开的 Inferno 线程说明，这支预告片先做角色设定图、先静帧后视频、按节拍写视频 prompt，最后在装配阶段只让旁白填入安静段落，并用 Seed Audio 1.0 生成额外的强调音效。
- 可复制做法：先在前期锁定角色一致性和构图，再把 Seed Audio 放到后期节拍感更强的声音设计层，而不是一开始就让它承担全部音频。
- 实际流程：先做 4K 角色设定图，把每个镜头先生成静帧再送进 Seedance，把视频 prompt 写成 camera-action-light 的分拍结构，按音乐时间点对齐最终剪辑，再用 Seed Audio 补旁白空档和重点音效。
- 注意事项：这个线程公开了 prompt 结构和流程顺序，但没有放出可直接复用的 Seed Audio prompt，也没有提供与其他音频栈的受控对比。

[![案例 17 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-17.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-17.mp4)

[打开视频播放页](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-17.mp4)

类型: Tutorial | 日期: 2026-07-17

---

<a id="case-18"></a>
### 案例 18: [用 Seed Audio 完成的双图动画短片](https://x.com/Dani__oros/status/2077829108818657420) (作者 [@Dani__oros](https://x.com/Dani__oros))

**把一张或两张参考图当作视觉锁定层，再让 Seed Audio 负责配乐，最后由 Seedance 把短片扩展成完整动画。**

- 证据来源：帖子把 Tide-Rider 标注为：Seedance 2.0 负责动画，Seed Audio 1.0 负责音乐，Krea 2 负责源图，CapCut 负责剪辑，并明确说整支短片基本只靠两张参考图和文本 prompting。
- 可复制做法：不要一开始就做完整 model sheet，可以先用一张核心参考图锁住视觉，再只在结尾需要新角度或揭示时补第二张图。
- 实际流程：先在 Krea 2 里设计关键图，把它当作 Seedance 的视觉锚点生成短动画镜头，保持 text prompting 轻量，再让 Seed Audio 提供配乐，并在 CapCut 里完成节奏和收尾。
- 注意事项：这个帖子证明了“两张图也能做完整动画短片”的模式，但没有公开精确 prompt，也没有说明镜头之间是否还做过额外清理。

[![案例 18 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-18.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-18.mp4)

[打开视频播放页](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-18.mp4)

类型: Demo | 日期: 2026-07-16

---

<a id="case-19"></a>
### 案例 19: [同画面换音频的 TTS 质量对比](https://x.com/takareinhard/status/2079028004202918291) (作者 [@takareinhard](https://x.com/takareinhard))

**在锁定正式 TTS 方案前，先保持成片画面不变，只替换音轨，就能更快比较 Seed Audio 与其他 TTS 的情绪、口音和原声泄漏问题。**

- 证据来源：作者发了同一段短视频的两个版本，说明前者保留 Seedance 2.0 原音，后者把音轨替换成 Seed Audio 1.0，并把结果与 ElevenLabs、にじボイス、MiniMax、Gemini TTS 做主观对比。
- 可复制做法：如果你想在定生产 TTS 方案前更快比较情绪表达、口音稳定性和“像不像原声优”的泄漏风险，就保持画面不变，只替换语音层做同片对照。
- 实际流程：先导出一段完成版视频，保留一版基线音频，再用 Seed Audio 重做第二版音轨，只比较两版在情绪、口音和声音身份泄漏上的差别。
- 注意事项：这是单一创作者的定性评测，没有公开 prompt、参考音频或量化基准。应把它当作比较方法，不是最终排行榜结论。

[![案例 19 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-19.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-19.mp4)

[打开视频播放页](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-19.mp4)

类型: Evaluation | 日期: 2026-07-20

---

<a id="case-20"></a>
### 案例 20: [音效棚的音频优先表演参考](https://x.com/WriterMcG/status/2079351581460287890) (作者 [@WriterMcG](https://x.com/WriterMcG))

**把房间音、环境声、角色行为和对白当成一个 Seed Audio 场景一次生成，再把完成音频和角色图片一起作为后续视频模型的表演参考。**

- 证据来源：公开帖子说明，作者在自己的 private soundstage app 里使用 Seed Audio 区块，把房间状态、环境声、角色行为和对白写成一次完整的戏剧表演，然后把生成出的音频文件与角色图片一起作为视频生成时的表演参考。
- 可复制做法：如果你想在视频模型开始解读场景前，先用音频把表演、节奏和氛围锁住，就可以把 Seed Audio 当成场景规划层来用。
- 实际流程：先写一段涵盖房间音、环境声、角色行为和对白的紧凑场景描述，先生成完整音频表演，再把这段完成音频和角色图片或剧照配在一起，最后再交给视频模型去动起来。
- 注意事项：后续公开讨论里，作者补充自己把 private voice library 接到自建工作室中。因此公开可保留的是音频优先工作流本身，不应假设同一套私有声音堆栈或 lip-sync 质量能普遍复制。

[![案例 20 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-20.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-20.mp4)

[打开视频播放页](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-20.mp4)

类型: Tutorial | 日期: 2026-07-20

---

<a id="case-21"></a>
### 案例 21: [阿拉伯语对话支持限制测试](https://x.com/tawleefai/status/2079626302835884345) (作者 [@tawleefai](https://x.com/tawleefai))

**在把 Seed Audio 用进未支持语言流程前，先做一次短的阿拉伯语对白或 voiceover 测试，因为当前版本即使在支持语言可用，到了未支持语言也可能直接失败。**

- 证据来源：公开帖子说明，作者用 Seed Audio 1.0 测试对白和 voiceover 生成，表示当前输出像无意义的乱码，而且阿拉伯语在现行版本中并未获得官方支持。
- 可复制做法：对未支持语言的评估应被视为一个明确的 go / no-go 关卡，而不是把模型在英文或多语营销上的强叙述直接套过来。
- 实际流程：在搭更长的阿拉伯语流程前，先跑一次短对白或 voiceover 测试，确认生成语音是否真的可理解；如果结果一开始就崩掉，就应该及早停止，而不是把时间继续花在后面的视频或剪辑工作上。
- 注意事项：公开讨论额外给出的只有一条精确 prompt 示例和一段结果视频，因此应只保留这个可见限制和 prompt 边界，不要外推成更广的阿拉伯语 benchmark 或隐藏设置。

[![案例 21 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-21.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-21.mp4)

[打开视频播放页](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-21.mp4)

类型: Limit | 日期: 2026-07-21

---

## 相关仓库

目前没有已验证的其他公开 Seed-Audio 仓库。持续维护的 skill 入口是 npm 上的 evolink-seed-audio.

<a id="acknowledge"></a>
## 🙏 致谢

本仓库在案例级别链接公开创作者和服务商内容。每个案例标题都会标注公开来源。

[@gokayfem](https://x.com/gokayfem) [@gavinpurcell](https://x.com/gavinpurcell) [@EvoLinkAi](https://x.com/EvoLinkAi) [@tarumainfo](https://x.com/tarumainfo) [@TomLikesRobots](https://x.com/TomLikesRobots) [@JPAI_HEAVEN](https://x.com/JPAI_HEAVEN) [@higgsfield](https://x.com/higgsfield) [@genel_ai](https://x.com/genel_ai) [@deepwhitman](https://x.com/deepwhitman) [@tc50501](https://x.com/tc50501) [@TomLikesRobots](https://x.com/TomLikesRobots) [@mattworkman](https://x.com/mattworkman) [@aimikoda](https://x.com/aimikoda) [@akiyoshisan](https://x.com/akiyoshisan) [@fabianstelzer](https://x.com/fabianstelzer) [@emmanuel_2m](https://x.com/emmanuel_2m) [@maxescu](https://x.com/maxescu) [@Dani__oros](https://x.com/Dani__oros) [@takareinhard](https://x.com/takareinhard) [@WriterMcG](https://x.com/WriterMcG) [@tawleefai](https://x.com/tawleefai)

*如果来源链接失效、署名错误，或某个说法没有得到链接来源支持，欢迎提交修正。*

[![Star History Chart](https://api.star-history.com/svg?repos=Evolink-AI/Awesome-Seed-Audio-1.0-Guide-and-Usecases&type=Date)](https://www.star-history.com/#Evolink-AI/Awesome-Seed-Audio-1.0-Guide-and-Usecases&Date)
