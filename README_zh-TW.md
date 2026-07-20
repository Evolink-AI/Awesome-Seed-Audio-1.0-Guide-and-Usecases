<div align="center">

<a href="https://evolink.ai/seed-audio-1-0?utm_source=github&utm_medium=banner&utm_campaign=awesome-seed-audio-1.0-usecases&utm_content=readme_banner"><img src="https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/images/en.png" alt="Seed-Audio 1.0 usecase repository banner" width="760"></a>

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](LICENSE)
[![Try it on Evolink](https://img.shields.io/badge/Try_it_on-Evolink-black)](https://evolink.ai/seed-audio-1-0?utm_source=github&utm_medium=badge&utm_campaign=awesome-seed-audio-1.0-usecases&utm_content=model_try)
[![Docs](https://img.shields.io/badge/Docs-Read-blue)](https://docs.evolink.ai/en/api-manual/audio-series/doubao-seed-audio/doubao-seed-audio-1-0?utm_source=github&utm_medium=docs&utm_campaign=awesome-seed-audio-1.0-usecases&utm_content=docs_link)

[![English](https://img.shields.io/badge/English-111111)](README.md) [![Español](https://img.shields.io/badge/Espa%C3%B1ol-ffb703)](README_es.md) [![Português](https://img.shields.io/badge/Portugu%C3%AAs-2a9d8f)](README_pt.md) [![日本語](https://img.shields.io/badge/%E6%97%A5%E6%9C%AC%E8%AA%9E-52b788)](README_ja.md) [![한국어](https://img.shields.io/badge/%ED%95%9C%EA%B5%AD%EC%96%B4-4ea8de)](README_ko.md) [![Deutsch](https://img.shields.io/badge/Deutsch-f4a261)](README_de.md) [![Français](https://img.shields.io/badge/Fran%C3%A7ais-e76f51)](README_fr.md) [![Türkçe](https://img.shields.io/badge/T%C3%BCrk%C3%A7e-d62828)](README_tr.md) [![繁體中文](https://img.shields.io/badge/%E7%B9%81%E9%AB%94%E4%B8%AD%E6%96%87-8338ec)](README_zh-TW.md) [![简体中文](https://img.shields.io/badge/%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-ef476f)](README_zh-CN.md) [![Русский](https://img.shields.io/badge/%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9-577590)](README_ru.md)

</div>

# Seed-Audio 1.0 使用案例：旁白、音訊劇、參考聲音與音訊優先影片工作流

## 🍌 介紹

歡迎來到 Seed-Audio 1.0 高訊號使用案例倉庫。

**我們基於公開 X/Twitter 來源和 EvoLink 文件，整理 Seed-Audio 1.0 的真實使用案例、創作者工作流、平台整合、評估與實務限制。**

本繁體中文 README 保留公開來源連結、作者署名和錨點，同時翻譯使用者可見說明文字。

[在 EvoLink 上試用 Seed-Audio 1.0](https://evolink.ai/seed-audio-1-0?utm_source=github&utm_medium=readme&utm_campaign=awesome-seed-audio-1.0-usecases&utm_content=introduction_cta)

## 📊 總覽

- **從近期 X/Twitter 樣本中篩選出 19 個 Seed-Audio 1.0 使用案例，原始可用樣本為 97 則。**
- 涵蓋方向：音訊優先影片工作流, 音訊劇與場景生成, 參考聲音與角色配音探索, 工具與服務商整合, 社群旁白、擬音與成本測試。
- 每個案例都包含原始來源、創作者署名、使用結論、證據類型與發布日期。
- 你可以用這個倉庫查找真實工作流、比較優勢和限制、發現服務商路徑，並把實作工作導向 EvoLink。

> [!NOTE]
> 本地化 README 與英文源文件保持相同的案例順序、連結、錨點與署名。

> [!NOTE]
> 本倉庫優先收錄具體工作流證據，而不是純宣傳：演示、設定說明、服務商發布、上手評估和明確限制。

[更新日誌](docs/update-log.md) | [維護指南](docs/maintenance.md) | [案例標註審計](docs/case-label-audit.md) | [案例資料](data/use-cases.json) | [預設音色文件](https://docs.evolink.ai/en/api-manual/audio-series/doubao-seed-audio/doubao-seed-audio-1-0-voices?utm_source=github&utm_medium=docs&utm_campaign=awesome-seed-audio-1.0-usecases&utm_content=voice_docs)

<a id="quick-start"></a>
## ⚡ 快速開始

先安裝 Seed-Audio agent skill，然後到 [Get API Key](https://evolink.ai/dashboard/keys?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-seed-audio-1.0-usecases&utm_content=api_key) 取得 API key，並設定為 `EVOLINK_API_KEY`。

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

skill 套件發布為 [evolink-seed-audio](https://www.npmjs.com/package/evolink-seed-audio)，用於 agent 和本地 skill 工作流。

## 📑 目錄

| 章節 | 案例 |
|---|---|
| [音訊優先影片工作流](#audio-first-video) | 案例 1, 案例 2, 案例 3, 案例 12, 案例 13, 案例 15, 案例 17, 案例 18 |
| [音訊劇與場景生成](#audio-drama-scene-generation) | 案例 4, 案例 5 |
| [參考聲音與角色配音探索](#voice-reference-character-casting) | 案例 6, 案例 8, 案例 10, 案例 19 |
| [工具與服務商整合](#tool-provider-integrations) | 案例 7, 案例 14, 案例 16 |
| [社群旁白、擬音與成本測試](#social-narration-foley-cost-tests) | 案例 9, 案例 11 |
| [致謝](#acknowledge) | 來源致謝與修正政策 |

<a id="audio-first-video"></a>
## 音訊優先影片工作流

| 案例 | 展示重點 | 類型 |
|---|---|---|
| [案例 1: 用六人音訊引導 Seedance 影片](#case-1) | 建立音訊優先的影片工作流，讓多人對白和背景音效引導後續影片生成。 | Tutorial |
| [案例 2: 多片段故事影片的音訊規劃](#case-2) | 測試 Seed-Audio 1.0 是否能減少多片段故事影片中的節奏和一致性問題。 | Evaluation |
| [案例 3: 音訊優先的 Seedance 參考工作流](#case-3) | 組織三步工作流：先生成音訊，再建立關鍵視覺圖，最後把兩者作為 Seedance 參考。 | Tutorial |
| [案例 12: 用 Claude 在 Premiere 中編排音樂與音效](#case-12) | 將音樂、音效和人聲拆成獨立生成，再讓 Claude 把音訊組裝進 Premiere，同時保留對節奏與淡入淡出的手動控制。 | Tutorial |
| [案例 13: 參考音訊格鬥解說時序測試](#case-13) | 先把 Seedance 成片當作 Seed Audio 的參考輸入，再依照畫面動作生成帶時間軸的解說詞，並把時序對齊視為主要評估風險。 | Evaluation |
| [案例 15: Agent 重寫正向版本的影片旁白測試](#case-15) | 把現有影片交給 agent，讓它為新的情緒方向重寫腳本，再用 Seed Audio 合成匹配的新旁白，最後重建畫面。 | Evaluation |
| [案例 17: 按節拍對齊的預告片聲音設計](#case-17) | 先鎖定角色與靜幀，再把預告片剪輯對齊到音樂時間點，並只在需要精準落點的旁白或強調音效位置使用 Seed Audio。 | Tutorial |
| [案例 18: 用 Seed Audio 完成的雙圖動畫短片](#case-18) | 把一張或兩張參考圖當作視覺鎖定層，再讓 Seed Audio 負責配樂，最後由 Seedance 把短片擴展成完整動畫。 | Demo |

<a id="audio-drama-scene-generation"></a>
## 音訊劇與場景生成

| 案例 | 展示重點 | 類型 |
|---|---|---|
| [案例 4: 帶環境聲的兩分鐘對白](#case-4) | 評估 Seed-Audio 1.0 在多聲音、環境聲和背景音樂並存的短音訊劇場景中的表現。 | Tutorial |
| [案例 5: 博物館導覽式場景對白](#case-5) | 測試場景級語言推理能力：由 Seed-Audio 生成對白、語氣和不同角色聲音。 | Demo |

<a id="voice-reference-character-casting"></a>
## 參考聲音與角色配音探索

| 案例 | 展示重點 | 類型 |
|---|---|---|
| [案例 6: 參考聲音 MC 工作流](#case-6) | 在進入後續影片生成前，評估適用於固定 MC 或系列旁白的參考聲音工作流。 | Tutorial |
| [案例 8: 參考音訊品質與高聲線限制](#case-8) | 評估日語語音、情緒跟隨、參考音訊精度，以及高聲線可能出現機械感的風險。 | Evaluation |
| [案例 10: 圖像引導的角色聲音探索](#case-10) | 把參考圖生成音訊用於早期角色聲音探索，而不是最終鎖定角色聲音。 | Evaluation |
| [案例 19: 同畫面換音訊的 TTS 品質對比](#case-19) | 在鎖定正式 TTS 方案前，先保持成片畫面不變，只替換音軌，就能更快比較 Seed Audio 與其他 TTS 的情緒、口音和原聲洩漏問題。 | Evaluation |

<a id="tool-provider-integrations"></a>
## 工具與服務商整合

| 案例 | 展示重點 | 類型 |
|---|---|---|
| [案例 7: Claude MCP 旁白與多語配音整合](#case-7) | 評估 Seed-Audio 1.0 在面向助手的創意工作區中，承擔旁白、聲音克隆和多語配音的價值。 | Integration |
| [案例 14: 用複製旁白驅動動態圖形技能工作流](#case-14) | 先用 Seed Audio 複製自己的聲音，再把生成的旁白當作時間軸骨架，驅動帶文字、圖形動畫、BGM 和字幕的動態圖形影片。 | Tutorial |
| [案例 16: 單照片 Scenario MCP 冒險預告片](#case-16) | 用一張人像加一條總控 prompt，就能讓 Codex/GPT 的 MCP 工作流在一次執行裡完成多場景 Seedance 鏡頭、Seed Audio 旁白、配樂與成片包裝。 | Integration |

<a id="social-narration-foley-cost-tests"></a>
## 社群旁白、擬音與成本測試

| 案例 | 展示重點 | 類型 |
|---|---|---|
| [案例 9: 社群故事旁白內容引擎](#case-9) | 測試把文字貼文轉成音訊優先娛樂內容的社群故事旁白格式。 | Demo |
| [案例 11: 低成本測試聲音表演與擬音](#case-11) | 在投入影片生成前，把 Seed-Audio 1.0 作為聲音表演和擬音的低成本迭代層來評估。 | Evaluation |

<a id="case-1"></a>
### 案例 1: [用六人音訊引導 Seedance 影片](https://x.com/gokayfem/status/2070429287950188547) (作者 [@gokayfem](https://x.com/gokayfem))

**建立音訊優先的影片工作流，讓多人對白和背景音效引導後續影片生成。**

- 證據來源：原帖展示了完整的 Seed Audio 設定：逃亡車場景、六位具名角色、不同聲線、短對白、引擎怠速、車頂雨聲，以及同一次生成中的背景音效；同時也給出後續的圖像 prompt 和 Seedance 2.0 影片 prompt。
- 可複製做法：當音訊需要主導整個場景時，先設定每位說話者、聲音質感、短句台詞與連續環境聲，讓聲音成為後續影片節奏的依據。
- 實際流程：先生成完整的多人音訊底層，再建立符合人物剪影與氣氛的關鍵視覺，最後把音訊和視覺一起交給 Seedance 做成影片。
- 注意事項：這個案例能證明工作流與 prompt 結構，但不能保證長場景裡每位角色都能完美分離；正式使用前仍要測試角色辨識與時間點。

[![案例 1 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-01.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-01.mp4)

[打開影片播放頁](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-01.mp4)

類型: Tutorial | 日期: 2026-06-26

---

<a id="case-2"></a>
### 案例 2: [多片段故事影片的音訊規劃](https://x.com/gavinpurcell/status/2070246132341727506) (作者 [@gavinpurcell](https://x.com/gavinpurcell))

**測試 Seed-Audio 1.0 是否能減少多片段故事影片中的節奏和一致性問題。**

- 證據來源：作者從一段約一分鐘、多片段、低解析度影片開始，明確說 Seedance prompt 中保持一致音訊很難，並用 Claude Code、Codex 和 FAL key 測試 agent 輔助的音訊處理。
- 可複製做法：把 Seed-Audio 當成既有多鏡頭影片的修補或規劃層，特別適合一個 prompt 必須涵蓋鏡頭切換、轉場、環境聲和音效的情境。
- 實際流程：把影片脈絡交給 agent，要求它逐鏡頭產生音訊計畫，再生成聲音或音效層，最後按每個片段比對，而不是只看整段一分鐘的總體印象。
- 注意事項：同一來源也指出部分音效仍沒有準確對上畫面動作，所以這是 Evaluation，不是 Tutorial；它提供測試方法，也保留 mismatch 風險。

[![案例 2 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-02.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-02.mp4)

[打開影片播放頁](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-02.mp4)

類型: Evaluation | 日期: 2026-06-25

---

<a id="case-3"></a>
### 案例 3: [音訊優先的 Seedance 參考工作流](https://x.com/EvoLinkAi/status/2070722722217578562) (作者 [@EvoLinkAi](https://x.com/EvoLinkAi))

**組織三步工作流：先生成音訊，再建立關鍵視覺圖，最後把兩者作為 Seedance 參考。**

- 證據來源：公開來源說明三步驟流程：用 Seed-Audio 1.0 生成音訊，產生關鍵視覺，再把兩者作為 Seedance 2 reference-to-video 的參考。
- 可複製做法：當音樂、旁白、環境聲或節奏應該先於影片而不是後製補上時，可以採用這個流程。
- 實際流程：先在音訊 prompt 中決定情緒節奏，再建立或選擇匹配場景的圖像，最後同時提供聲音和視覺方向，讓影片模型有時間與畫面參考。
- 注意事項：這是官方工作流樣式，不是獨立 benchmark；可作為起步配方，但仍要測 lip-sync、剪輯節奏，以及影片是否真的跟隨音訊提示。

[![案例 3 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-03.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-03.mp4)

[打開影片播放頁](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-03.mp4)

類型: Tutorial | 日期: 2026-06-27

---

<a id="case-4"></a>
### 案例 4: [帶環境聲的兩分鐘對白](https://x.com/tarumainfo/status/2071255504907891186) (作者 [@tarumainfo](https://x.com/tarumainfo))

**評估 Seed-Audio 1.0 在多聲音、環境聲和背景音樂並存的短音訊劇場景中的表現。**

- 證據來源：原帖包含一段具體的兩分鐘 prompt / 劇本，使用 INTENT、AESTHETIC、EXECUTION 結構，並指定環境聲、背景音樂、兩位角色聲線、情緒表演和逐句對白。
- 可複製做法：當你要做的是音訊劇，而不是單一旁白時，可用這種劇本格式：先寫環境，再定義角色聲音，最後在對白中加入簡短表演方向。
- 實際流程：把場景寫成短劇本，讓每句台詞的表演提示保持簡潔，保留持續背景聲，並聽模型是否同時跟住情緒和節奏。
- 注意事項：公開來源說結果貼近 prompt，但長篇一致性仍需檢查；若要正式製作，建議把長場景拆成較短段落，避免角色情緒或背景音樂漂移。

[![案例 4 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-04.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-04.mp4)

[打開影片播放頁](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-04.mp4)

類型: Tutorial | 日期: 2026-06-28

---

<a id="case-5"></a>
### 案例 5: [博物館導覽式場景對白](https://x.com/TomLikesRobots/status/2070923534449119424) (作者 [@TomLikesRobots](https://x.com/TomLikesRobots))

**測試場景級語言推理能力：由 Seed-Audio 生成對白、語氣和不同角色聲音。**

- 證據來源：作者提供了一個簡短場景 prompt：博物館導覽員向困惑遊客解釋「crossing the Rubicon」為何表示越過不可回頭的界線；原帖稱 Seed Audio 生成了對白、表演和角色聲音。
- 可複製做法：當你希望 Seed-Audio 從簡短情境推理出教育式對話，而不是手寫每一句台詞時，可參考這個案例。
- 實際流程：給模型角色、要解釋的概念和對話關係，再評估語音是否自然、解釋是否正確。
- 注意事項：這是 Demo，因為它展示場景級語言推理和自然表演，但沒有提供可重複 benchmark；用於教育內容時仍要核對事實。

[![案例 5 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-05.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-05.mp4)

[打開影片播放頁](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-05.mp4)

類型: Demo | 日期: 2026-06-27

---

<a id="case-6"></a>
### 案例 6: [參考聲音 MC 工作流](https://x.com/JPAI_HEAVEN/status/2070842306329227264) (作者 [@JPAI_HEAVEN](https://x.com/JPAI_HEAVEN))

**在進入後續影片生成前，評估適用於固定 MC 或系列旁白的參考聲音工作流。**

- 證據來源：原帖描述兩步參考聲音流程：從來源聲音素材生成約一分鐘 MC 音訊，把生成音訊切成短段，再交給 Seedance 2.0 做 lip-sync 影片。
- 可複製做法：當系列內容需要固定主持人、播報員或 MC 聲音時，可先建立可重用的音訊參考，再進入影片生成。
- 實際流程：先生成較長且乾淨的聲音樣本，切成短片段，作為影片參考，再在影片生成後修正任何聲音漂移。
- 注意事項：作者明確說聲音在進入 Seedance 影片流程後會有些變化；這是核心 caveat，所以它是工作流 Tutorial，不是穩定聲音身份的保證。

[![案例 6 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-06.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-06.mp4)

[打開影片播放頁](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-06.mp4)

類型: Tutorial | 日期: 2026-06-27

---

<a id="case-7"></a>
### 案例 7: [Claude MCP 旁白與多語配音整合](https://x.com/higgsfield/status/2070916672106680360) (作者 [@higgsfield](https://x.com/higgsfield))

**評估 Seed-Audio 1.0 在面向助手的創意工作區中，承擔旁白、聲音克隆和多語配音的價值。**

- 證據來源：Higgsfield 表示 Claude 可透過 MCP integration 生成音訊，覆蓋 voiceover、voice cloning 和 50+ 語言的多語音訊工作，其中部分由 Seed Audio 1.0 驅動。
- 可複製做法：用這個案例理解 no-code 或 agent-facing 入口：創作者不必直接呼叫音訊 endpoint，也能透過 Claude 加 MCP provider 執行旁白和多語音訊任務。
- 實際流程：在 Claude 裡提出短旁白或多語音訊需求，透過 MCP route 生成，再檢查輸出是否符合目標語言、聲音身份和媒體工作流。
- 注意事項：這是 Integration，不是品質評測；它證明可用入口與工作流表面，但沒有獨立驗證 50+ 語言的多語音訊品質。

[![案例 7 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-07.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-07.mp4)

[打開影片播放頁](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-07.mp4)

類型: Integration | 日期: 2026-06-27

---

<a id="case-8"></a>
### 案例 8: [參考音訊品質與高聲線限制](https://x.com/genel_ai/status/2070438167019409582) (作者 [@genel_ai](https://x.com/genel_ai))

**評估日語語音、情緒跟隨、參考音訊精度，以及高聲線可能出現機械感的風險。**

- 證據來源：作者回報日語實測結果：日語語音比 Seedance 2.0 audio 更穩、對話能跟隨情緒、參考音訊精度強但最長 30 秒、不支援音訊加圖像同時參考，高聲線會有機械感。
- 可複製做法：把它當成日語或其他非英文語音測試 checklist：穩定度、情緒跟隨、參考精度、參考模式限制和高音 artifact。
- 實際流程：用正常與高聲線都生成短片段，和參考音訊比較，再另外測圖像引導流程，因為來源說音訊和圖像參考不能合併。
- 注意事項：這是 Evaluation，核心價值是限制地圖；重點不是宣稱 Seed-Audio 永遠更好，而是標出哪些地方表現好、哪些仍要測。

[![案例 8 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-08.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-08.mp4)

[打開影片播放頁](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-08.mp4)

類型: Evaluation | 日期: 2026-06-26

---

<a id="case-9"></a>
### 案例 9: [社群故事旁白內容引擎](https://twitter.com/deepwhitman/status/2071485165390704837) (作者 [@deepwhitman](https://x.com/deepwhitman))

**測試把文字貼文轉成音訊優先娛樂內容的社群故事旁白格式。**

- 證據來源：作者用 Seed Audio 1.0 旁白一則熱門 AITA 風格貼文，並把它描述成可能重複使用的 viral content engine；同作者回覆中也連到原故事來源。
- 可複製做法：當你想測試大量文字型社群貼文能否低成本轉成短影音旁白娛樂內容時，可以參考這個案例。
- 實際流程：選一則公開文字故事，改寫成旁白段落，生成聲音，再配上簡單畫面或字幕，測試這種格式能否成為可重複內容流程。
- 注意事項：這是 Demo，不是版權或成長保證；使用故事內容仍需要授權或妥善來源處理，也要做受眾測試後才能稱為可規模化渠道。

[![案例 9 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-09.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-09.mp4)

[打開影片播放頁](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-09.mp4)

類型: Demo | 日期: 2026-06-29

---

<a id="case-10"></a>
### 案例 10: [圖像引導的角色聲音探索](https://x.com/tc50501/status/2070498347824337389) (作者 [@tc50501](https://x.com/tc50501))

**把參考圖生成音訊用於早期角色聲音探索，而不是最終鎖定角色聲音。**

- 證據來源：作者只輸入一張女性角色參考圖，生成三段約十秒的聲音台詞；其中兩段方向接近，一段明顯偏高。
- 可複製做法：把圖像引導音訊當成早期角色選聲工具，用來探索角色可能的聲音，而不是直接鎖定最終台詞聲音。
- 實際流程：用同一角色圖測多句短台詞，比較 pitch、tone 和人格方向，只保留多句之間仍穩定的候選聲音。
- 注意事項：公開來源本身提醒 pitch 和 tone 穩定性還不足以支撐固定電影角色聲音製作；因此它是 Evaluation，定義了 casting 用途和製作風險。

![案例 10 media](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-10.jpg)

類型: Evaluation | 日期: 2026-06-26

---

<a id="case-11"></a>
### 案例 11: [低成本測試聲音表演與擬音](https://x.com/TomLikesRobots/status/2070288519684108353) (作者 [@TomLikesRobots](https://x.com/TomLikesRobots))

**在投入影片生成前，把 Seed-Audio 1.0 作為聲音表演和擬音的低成本迭代層來評估。**

- 證據來源：作者回報早期測試中，voice acting 和 foley 比 Seedance 2 原生 audio 更好，並說 15 秒音訊測試只花幾美分。
- 可複製做法：把 Seed-Audio 當成便宜的前期測試層，在投入影片生成前先驗證聲音表演、擬音或環境聲是否能撐起想法。
- 實際流程：先做 10 到 15 秒短音訊測試，和影片模型原生音訊比較，只有當聲音方向足夠好時再進入後續影片生成。
- 注意事項：評論中仍有參考聲轉換和把生成音訊用於 Seedance lip-sync 的未解問題；這仍是 Evaluation，驗證的是低成本測試角色，不是完整最終流程。

[![案例 11 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-11.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-11.mp4)

[打開影片播放頁](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-11.mp4)

類型: Evaluation | 日期: 2026-06-25

---

<a id="case-12"></a>
### 案例 12: [用 Claude 在 Premiere 中編排音樂與音效](https://x.com/mattworkman/status/2076148989687181705) (作者 [@mattworkman](https://x.com/mattworkman))

**將音樂、音效和人聲拆成獨立生成，再讓 Claude 把音訊組裝進 Premiere，同時保留對節奏與淡入淡出的手動控制。**

- 證據來源：Matt Workman 說明，他讓 Claude 依照劇本中途變化的情緒為音樂底軌撰寫 Seed Audio 提示，並挑選、生成關鍵音效。
- 可複製做法：需要更細緻地控制品質和混音時，不要讓 Seed Audio 一次同時生成音樂、音效和人聲，而是把它們拆成獨立軌道。
- 實際流程：把劇本交給 Claude，分別生成 Seed Audio 音樂與音效素材，再讓 Claude 在 Premiere 中自動組裝這些軌道，最後手動調整參數、時間點與淡入淡出。
- 注意事項：來源表達的是作者對分軌生成品質更好的實務偏好，並非受控基準；應在自己的素材上比較分軌方案與一次性混合生成。

![案例 12 media](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-12.jpg)

類型: Tutorial | 日期: 2026-07-12

---

<a id="case-13"></a>
### 案例 13: [參考音訊格鬥解說時序測試](https://x.com/aimikoda/status/2076526254417735781) (作者 [@aimikoda](https://x.com/aimikoda))

**先把 Seedance 成片當作 Seed Audio 的參考輸入，再依照畫面動作生成帶時間軸的解說詞，並把時序對齊視為主要評估風險。**

- 證據來源：父帖展示最終格鬥片段，並指向回覆貼 https://x.com/aimikoda/status/2076527528227815779；該回覆公開了 Midjourney、Seedance 2.0 與 Seed Audio 的完整提示詞，並說明作者把成片音訊當作 Seed Audio 參考。
- 可複製做法：先把視覺打鬥片段剪成最終版，再提取成片音訊作為 Seed Audio 參考，同時讓另一個模型依照畫面動作撰寫解說文案。
- 實際流程：用 Midjourney 製作角色與擂台素材，生成多條 Seedance 打鬥片段並剪出最強片段，匯出成片音訊，交給 GPT-5.6 依照畫面撰寫解說，再用包含時長、聲線、環境、時間軸提示與 negative 約束的 Seed Audio 提示詞生成解說。
- 注意事項：作者表示大約試了十次，時序仍未完全貼合，因此更適合作為 Evaluation；預期還要繼續調 prompt 或做手動同步。

[![案例 13 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-13.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-13.mp4)

[打開影片播放頁](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-13.mp4)

類型: Evaluation | 日期: 2026-07-13

---

<a id="case-14"></a>
### 案例 14: [用複製旁白驅動動態圖形技能工作流](https://x.com/akiyoshisan/status/2077650497536987154) (作者 [@akiyoshisan](https://x.com/akiyoshisan))

**先用 Seed Audio 複製自己的聲音，再把生成的旁白當作時間軸骨架，驅動帶文字、圖形動畫、BGM 和字幕的動態圖形影片。**

- 證據來源：作者明確表示影片是用 MiniMax Hub 的動態圖形技能製作，並公開列出流程：用 Seed Audio 1.0 複製自己的聲音、生成旁白、確認時長和內容、為 15 秒成片設計 6 張分鏡、撰寫日文畫面文字、規劃連續的圖形變形過渡、用 Seedance 2.0 Fast 輸出影片，再合成旁白、BGM、音效和日文字幕。
- 可複製做法：當你要做短講解或動態圖形影片時，可以把 Seed Audio 的聲音複製和旁白生成當成時間軸主線，再讓分鏡卡片、文字覆蓋和動畫節奏圍繞這條主線同步展開。
- 實際流程：先準備來源聲音並在 Seed Audio 中生成旁白，鎖定目標時長，再按照旁白長度設計分鏡，補上文字和圖形動作，渲染影片後把旁白、音樂、音效和字幕混到最終成片。
- 注意事項：這條貼文證明了工作流形態與所用工具鏈，但沒有公開具體 prompt 或節點設定。適合把它當成可遷移的製作模式，而不是 prompt 重現案例。

[![案例 14 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-14.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-14.mp4)

[打開影片播放頁](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-14.mp4)

類型: Tutorial | 日期: 2026-07-16

---

<a id="case-15"></a>
### 案例 15: [Agent 重寫正向版本的影片旁白測試](https://x.com/fabianstelzer/status/2077138756939727067) (作者 [@fabianstelzer](https://x.com/fabianstelzer))

**把現有影片交給 agent，讓它為新的情緒方向重寫腳本，再用 Seed Audio 合成匹配的新旁白，最後重建畫面。**

- 證據來源：作者表示，一個由 Claude 驅動的 Glif agent 先接收原影片連結，再用 Gemini 3.5 觀看影片、寫出更正向的新腳本、調用 Seed Audio 生成相似聲線的旁白，最後再用 NB2 做靜幀、用 Remotion 組裝成片。
- 可複製做法：當你測試 agent 式影片改寫流程時，可以把 Seed Audio 放在「保留原有說話風格、但替換敘述內容」的旁白層。
- 實際流程：先把來源影片交給 agent，要求它改寫語氣；讓 agent 理解影片內容並生成新腳本；再用 Seed Audio 產出替代旁白，之後重建或延展畫面，並把節奏與配樂單獨複核。
- 注意事項：作者明確指出節奏和速度仍需人工打磨，圖像質感仍受模型選擇限制，而且 ElevenLabs 的配樂嘗試失敗了。因此它更適合作為評估型流程，而不是無監督成片方案。

[![案例 15 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-15.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-15.mp4)

[打開影片播放頁](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-15.mp4)

類型: Evaluation | 日期: 2026-07-14

---

<a id="case-16"></a>
### 案例 16: [單照片 Scenario MCP 冒險預告片](https://x.com/emmanuel_2m/status/2078227114818707891) (作者 [@emmanuel_2m](https://x.com/emmanuel_2m))

**用一張人像加一條總控 prompt，就能讓 Codex/GPT 的 MCP 工作流在一次執行裡完成多場景 Seedance 鏡頭、Seed Audio 旁白、配樂與成片包裝。**

- 證據來源：公開回覆給出了四步 MCP 流程與完整預告片 prompt，而父帖展示了只用一張上傳照片做出的印第安納瓊斯風格成片。
- 可複製做法：如果你想讓 MCP agent 一次協調場景生成、旁白、配樂、海報與最終包裝，可以先準備一張正臉人像，再配一條總控 prompt。
- 實際流程：在 Codex 或 GPT 5.6 中載入 Scenario MCP，上傳人像，執行公開 prompt，讓 agent 在至少十個 Seedance 場景裡維持人物一致性，再把 Seed Audio 旁白、音樂與復古標題卡組合成片。
- 注意事項：這個來源證明了編排模式與 prompt 邊界，但沒有公開中間重試或手動修整過程。應把它視為整合型工作流，而不是保證一鍵完成的承諾。

![案例 16 media](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-16.jpg)

類型: Integration | 日期: 2026-07-17

---

<a id="case-17"></a>
### 案例 17: [按節拍對齊的預告片聲音設計](https://x.com/maxescu/status/2078146037517312129) (作者 [@maxescu](https://x.com/maxescu))

**先鎖定角色與靜幀，再把預告片剪輯對齊到音樂時間點，並只在需要精準落點的旁白或強調音效位置使用 Seed Audio。**

- 證據來源：公開的 Inferno thread 說明，這支預告片先做角色設定圖、先靜幀後影片、按節拍寫影片 prompt，最後在裝配階段只讓旁白填入安靜段落，並用 Seed Audio 1.0 生成額外的強調音效。
- 可複製做法：先在前期鎖定角色一致性與構圖，再把 Seed Audio 放到後期節拍感更強的聲音設計層，而不是一開始就讓它承擔全部音訊。
- 實際流程：先做 4K 角色設定圖，把每個鏡頭先生成靜幀再送進 Seedance，把影片 prompt 寫成 camera-action-light 的分拍結構，按音樂時間點對齊最終剪輯，再用 Seed Audio 補旁白空檔與重點音效。
- 注意事項：這個 thread 公開了 prompt 結構與流程順序，但沒有放出可直接複用的 Seed Audio prompt，也沒有提供與其他音訊堆疊的受控對比。

[![案例 17 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-17.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-17.mp4)

[打開影片播放頁](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-17.mp4)

類型: Tutorial | 日期: 2026-07-17

---

<a id="case-18"></a>
### 案例 18: [用 Seed Audio 完成的雙圖動畫短片](https://x.com/Dani__oros/status/2077829108818657420) (作者 [@Dani__oros](https://x.com/Dani__oros))

**把一張或兩張參考圖當作視覺鎖定層，再讓 Seed Audio 負責配樂，最後由 Seedance 把短片擴展成完整動畫。**

- 證據來源：貼文把 Tide-Rider 標註為：Seedance 2.0 負責動畫，Seed Audio 1.0 負責音樂，Krea 2 負責源圖，CapCut 負責剪輯，並明確說整支短片基本只靠兩張參考圖與文字 prompting。
- 可複製做法：不要一開始就做完整 model sheet，可以先用一張核心參考圖鎖住視覺，再只在結尾需要新角度或揭示時補第二張圖。
- 實際流程：先在 Krea 2 設計關鍵圖，把它當作 Seedance 的視覺錨點生成短動畫鏡頭，保持 text prompting 輕量，再讓 Seed Audio 提供配樂，並在 CapCut 裡完成節奏與收尾。
- 注意事項：這篇貼文證明了「兩張圖也能做完整動畫短片」的模式，但沒有公開精確 prompt，也沒有說明鏡頭之間是否還做過額外清理。

[![案例 18 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-18.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-18.mp4)

[打開影片播放頁](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-18.mp4)

類型: Demo | 日期: 2026-07-16

---

<a id="case-19"></a>
### 案例 19: [同畫面換音訊的 TTS 品質對比](https://x.com/takareinhard/status/2079028004202918291) (作者 [@takareinhard](https://x.com/takareinhard))

**在鎖定正式 TTS 方案前，先保持成片畫面不變，只替換音軌，就能更快比較 Seed Audio 與其他 TTS 的情緒、口音和原聲洩漏問題。**

- 證據來源：作者發了同一段短影片的兩個版本，說明前者保留 Seedance 2.0 原音，後者把音軌替換成 Seed Audio 1.0，並把結果與 ElevenLabs、にじボイス、MiniMax、Gemini TTS 做主觀對比。
- 可複製做法：如果你想在定下正式 TTS 方案前更快比較情緒表達、口音穩定性和「像不像原聲優」的洩漏風險，就保持畫面不變，只替換語音層做同片對照。
- 實際流程：先輸出一段完成版影片，保留一版基線音訊，再用 Seed Audio 重做第二版音軌，只比較兩版在情緒、口音和聲音身份洩漏上的差別。
- 注意事項：這是單一創作者的定性評測，沒有公開 prompt、參考音訊或量化基準。應把它當作比較方法，不是最終排行榜結論。

[![案例 19 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-19.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-19.mp4)

[打開影片播放頁](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-19.mp4)

類型: Evaluation | 日期: 2026-07-20

---

## 相關儲存庫

目前沒有已驗證的其他公開 Seed-Audio 儲存庫。持續維護的 skill 入口是 npm 上的 evolink-seed-audio.

<a id="acknowledge"></a>
## 🙏 致謝

本倉庫在案例層級連結公開創作者和服務商內容。每個案例標題都會標註公開來源。

[@gokayfem](https://x.com/gokayfem) [@gavinpurcell](https://x.com/gavinpurcell) [@EvoLinkAi](https://x.com/EvoLinkAi) [@tarumainfo](https://x.com/tarumainfo) [@TomLikesRobots](https://x.com/TomLikesRobots) [@JPAI_HEAVEN](https://x.com/JPAI_HEAVEN) [@higgsfield](https://x.com/higgsfield) [@genel_ai](https://x.com/genel_ai) [@deepwhitman](https://x.com/deepwhitman) [@tc50501](https://x.com/tc50501) [@TomLikesRobots](https://x.com/TomLikesRobots) [@mattworkman](https://x.com/mattworkman) [@aimikoda](https://x.com/aimikoda) [@akiyoshisan](https://x.com/akiyoshisan) [@fabianstelzer](https://x.com/fabianstelzer) [@emmanuel_2m](https://x.com/emmanuel_2m) [@maxescu](https://x.com/maxescu) [@Dani__oros](https://x.com/Dani__oros) [@takareinhard](https://x.com/takareinhard)

*如果來源連結失效、署名錯誤，或某個說法沒有得到連結來源支持，歡迎提交修正。*

[![Star History Chart](https://api.star-history.com/svg?repos=Evolink-AI/Awesome-Seed-Audio-1.0-Guide-and-Usecases&type=Date)](https://www.star-history.com/#Evolink-AI/Awesome-Seed-Audio-1.0-Guide-and-Usecases&Date)
