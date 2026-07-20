<div align="center">

<a href="https://evolink.ai/seed-audio-1-0?utm_source=github&utm_medium=banner&utm_campaign=awesome-seed-audio-1.0-usecases&utm_content=readme_banner"><img src="https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/images/en.png" alt="Seed-Audio 1.0 usecase repository banner" width="760"></a>

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](LICENSE)
[![Try it on Evolink](https://img.shields.io/badge/Try_it_on-Evolink-black)](https://evolink.ai/seed-audio-1-0?utm_source=github&utm_medium=badge&utm_campaign=awesome-seed-audio-1.0-usecases&utm_content=model_try)
[![Docs](https://img.shields.io/badge/Docs-Read-blue)](https://docs.evolink.ai/en/api-manual/audio-series/doubao-seed-audio/doubao-seed-audio-1-0?utm_source=github&utm_medium=docs&utm_campaign=awesome-seed-audio-1.0-usecases&utm_content=docs_link)

[![English](https://img.shields.io/badge/English-111111)](README.md) [![Español](https://img.shields.io/badge/Espa%C3%B1ol-ffb703)](README_es.md) [![Português](https://img.shields.io/badge/Portugu%C3%AAs-2a9d8f)](README_pt.md) [![日本語](https://img.shields.io/badge/%E6%97%A5%E6%9C%AC%E8%AA%9E-52b788)](README_ja.md) [![한국어](https://img.shields.io/badge/%ED%95%9C%EA%B5%AD%EC%96%B4-4ea8de)](README_ko.md) [![Deutsch](https://img.shields.io/badge/Deutsch-f4a261)](README_de.md) [![Français](https://img.shields.io/badge/Fran%C3%A7ais-e76f51)](README_fr.md) [![Türkçe](https://img.shields.io/badge/T%C3%BCrk%C3%A7e-d62828)](README_tr.md) [![繁體中文](https://img.shields.io/badge/%E7%B9%81%E9%AB%94%E4%B8%AD%E6%96%87-8338ec)](README_zh-TW.md) [![简体中文](https://img.shields.io/badge/%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-ef476f)](README_zh-CN.md) [![Русский](https://img.shields.io/badge/%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9-577590)](README_ru.md)

</div>

# Seed-Audio 1.0 ユースケース：ナレーション、音声ドラマ、参照音声、音声先行の動画制作

## 🍌 紹介

Seed-Audio 1.0 の高シグナルなユースケース集です。

**公開 X/Twitter ソースと EvoLink ドキュメントに基づき、実例、クリエイターのワークフロー、統合、評価、実用上の制約を整理しています。**

この日本語 README は公開ソースリンク、作者クレジット、アンカーを保持しつつ、ユーザー向け説明文を翻訳しています。

[EvoLink で Seed-Audio 1.0 を試す](https://evolink.ai/seed-audio-1-0?utm_source=github&utm_medium=readme&utm_campaign=awesome-seed-audio-1.0-usecases&utm_content=introduction_cta)

## 📊 概要

- **最近の X/Twitter サンプル 97 件から、Seed-Audio 1.0 のユースケース 19 件を選定しました。**
- 対象領域：音声先行の動画ワークフロー, 音声ドラマとシーン生成, 参照音声とキャラクター音声探索, ツールとプロバイダー統合, SNS ナレーション、フォーリー、コスト検証。
- 各ケースには、元ソース、作者クレジット、活用ポイント、証拠タイプ、公開日を含めています。
- 実用ワークフロー、強みと制約、プロバイダー経路、EvoLink での実装導線を確認するために使えます。

> [!NOTE]
> ローカライズ版 README は英語版と同じケース順、リンク、アンカー、帰属を保持します。

> [!NOTE]
> このコレクションは宣伝文句ではなく、デモ、設定メモ、プロバイダー公開、実使用評価、明示された制約などの具体的証拠を重視します。

[更新ログ](docs/update-log.md) | [メンテナンスガイド](docs/maintenance.md) | [ケースラベル監査](docs/case-label-audit.md) | [ケースデータ](data/use-cases.json) | [プリセット音色ドキュメント](https://docs.evolink.ai/en/api-manual/audio-series/doubao-seed-audio/doubao-seed-audio-1-0-voices?utm_source=github&utm_medium=docs&utm_campaign=awesome-seed-audio-1.0-usecases&utm_content=voice_docs)

<a id="quick-start"></a>
## ⚡ クイックスタート

Seed-Audio agent skill をインストールし、[Get API Key](https://evolink.ai/dashboard/keys?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-seed-audio-1.0-usecases&utm_content=api_key) で API key を取得して `EVOLINK_API_KEY` に設定します。

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

パッケージは agent / ローカル skill ワークフロー向けに [evolink-seed-audio](https://www.npmjs.com/package/evolink-seed-audio) として公開されています。

## 📑 メニュー

| セクション | ケース |
|---|---|
| [音声先行の動画ワークフロー](#audio-first-video) | ケース 1, ケース 2, ケース 3, ケース 12, ケース 13, ケース 15, ケース 17, ケース 18 |
| [音声ドラマとシーン生成](#audio-drama-scene-generation) | ケース 4, ケース 5 |
| [参照音声とキャラクター音声探索](#voice-reference-character-casting) | ケース 6, ケース 8, ケース 10, ケース 19 |
| [ツールとプロバイダー統合](#tool-provider-integrations) | ケース 7, ケース 14, ケース 16 |
| [SNS ナレーション、フォーリー、コスト検証](#social-narration-foley-cost-tests) | ケース 9, ケース 11 |
| [謝辞](#acknowledge) | クレジットと修正ポリシー |

<a id="audio-first-video"></a>
## 音声先行の動画ワークフロー

| ケース | 注目点 | タイプ |
|---|---|---|
| [ケース 1: 6 人の音声で Seedance 動画を誘導](#case-1) | マルチスピーカーの対話と背景効果が後のビデオ生成をガイドする、オーディオファーストのビデオワークフローを構築します。 | Tutorial |
| [ケース 2: マルチクリップ物語動画の音声設計](#case-2) | Seed-Audio 1.0 がマルチクリップ ビデオ ストーリーのタイミングと一貫性の問題を軽減できるかどうかをテストします。 | Evaluation |
| [ケース 3: 音声先行の Seedance 参照ワークフロー](#case-3) | 音声の生成、キービジュアルの作成、両方を Seedance リファレンスとして使用するという 3 ステップのワークフローを構築します。 | Tutorial |
| [ケース 12: Claude で音楽と効果音を Premiere に組み込む](#case-12) | 音楽、効果音、音声を別々に生成し、Claude に Premiere 上で組み立てさせながら、タイミングとフェードを手動で調整できる状態を保ちます。 | Tutorial |
| [ケース 13: 参照音声による格闘実況タイミング検証](#case-13) | 完成した Seedance 編集を Seed Audio の参照入力にし、映像アクションから時間指定の実況文を作り、タイミング一致を主な評価リスクとして扱います。 | Evaluation |
| [ケース 15: エージェントが前向き版へ書き換える音声テスト](#case-15) | 既存の動画を agent に渡し、新しいトーン向けに script を書き換えさせてから、Seed Audio で合う voiceover を生成し、映像を組み直します。 | Evaluation |
| [ケース 17: ビート同期の予告編サウンド設計](#case-17) | 先に登場人物と静止画を固め、その後で予告編のカットを音楽の時間軸に合わせ、正確な入りが必要なナレーションや強調効果音だけに Seed Audio を使います。 | Tutorial |
| [ケース 18: Seed Audio を使う2枚画像アニメ短編](#case-18) | 1〜2 枚の参照画像を見た目の固定軸にし、Seed Audio に音楽を任せ、Seedance で短編を完成したアニメ映像へ広げます。 | Demo |

<a id="audio-drama-scene-generation"></a>
## 音声ドラマとシーン生成

| ケース | 注目点 | タイプ |
|---|---|---|
| [ケース 4: 環境音付き 2 分間ダイアログ](#case-4) | 複数の音声、アンビエンス、BGM を備えたコンパクトなオーディオ ドラマ シーン用の Seed-Audio 1.0 を評価します。 | Tutorial |
| [ケース 5: 博物館ガイド風の場面対話](#case-5) | Seed-Audio が対話、伝達、および明確なキャラクターの声を生成するシーンレベルの言語推論をテストします。 | Demo |

<a id="voice-reference-character-casting"></a>
## 参照音声とキャラクター音声探索

| ケース | 注目点 | タイプ |
|---|---|---|
| [ケース 6: 参照音声 MC ワークフロー](#case-6) | ダウンストリームビデオ生成前に、反復的な MC またはシリーズのナレーションのリファレンス音声ワークフローを評価します。 | Tutorial |
| [ケース 8: 参照音声品質と高音ボイスの制約](#case-8) | 日本語の音声、感情の追従性、基準音声の精度、高音の合成音のリスクを評価します。 | Evaluation |
| [ケース 10: 画像参照によるキャラクター音声探索](#case-10) | 最終的なボイスロック制作ではなく、初期のキャラクターボイスキャストとして参照イメージオーディオを評価します。 | Evaluation |
| [ケース 19: 同一映像で音声だけ差し替える TTS 品質比較](#case-19) | 本番の TTS スタックを決める前に、完成クリップの映像を固定したまま音声だけ差し替え、Seed Audio と他の TTS の感情表現、訛り、元音声の残り方を比べます。 | Evaluation |

<a id="tool-provider-integrations"></a>
## ツールとプロバイダー統合

| ケース | 注目点 | タイプ |
|---|---|---|
| [ケース 7: Claude MCP のボイスオーバーと多言語吹き替え統合](#case-7) | ナレーション、音声クローン、およびダビングのためのアシスタントネイティブのクリエイティブワークスペースの一部として Seed-Audio 1.0 を評価します。 | Integration |
| [ケース 14: クローン音声で動かすモーショングラフィックス技能フロー](#case-14) | Seed Audio で自分の声をクローン化し、そのナレーションを時間軸の骨格として、テキスト、図形アニメーション、BGM、字幕を含むモーショングラフィックス動画を組み立てます。 | Tutorial |
| [ケース 16: 1枚写真の Scenario MCP 冒険トレーラー](#case-16) | 1枚の人物写真と1本の総合指示だけで、Codex/GPT の MCP 連携に複数の Seedance 映像、Seed Audio のナレーション、音楽、仕上げ処理まで一括で進めさせます。 | Integration |

<a id="social-narration-foley-cost-tests"></a>
## SNS ナレーション、フォーリー、コスト検証

| ケース | 注目点 | タイプ |
|---|---|---|
| [ケース 9: SNS ストーリー朗読エンジン](#case-9) | テキスト投稿がオーディオファーストのエンターテイメントになるソーシャルストーリーのナレーション形式をテストします。 | Demo |
| [ケース 11: 声の演技とフォーリーの低コスト検証](#case-11) | ビデオ生成に取り組む前に、音声演技とフォーリー用の低コストの反復レイヤーとして Seed-Audio 1.0 を評価します。 | Evaluation |

<a id="case-1"></a>
### ケース 1: [6 人の音声で Seedance 動画を誘導](https://x.com/gokayfem/status/2070429287950188547) (作者 [@gokayfem](https://x.com/gokayfem))

**マルチスピーカーの対話と背景効果が後のビデオ生成をガイドする、オーディオファーストのビデオワークフローを構築します。**

- ソース証拠: 投稿には実際の Seed Audio 設定が示されています。逃走用バンの場面、6人の名前付き話者、異なる声の方向性、短い台詞、アイドリング音、屋根に当たる雨、背景効果が1回の音声生成に含まれ、後段の画像 prompt と Seedance 2.0 動画 prompt も確認できます。
- コピーすること: 音声が場面全体を先導する必要があるときに使います。各話者を配役し、声質を定義し、短い台詞を書き、後段動画のタイミング手掛かりになる連続した環境音を入れます。
- 実用ワークフロー: まず複数話者の音声ベッドを生成し、次に人物シルエットと雰囲気が合うキービジュアルを作り、最後に音声と視覚コンテキストを Seedance に渡します。
- 注意点: この証拠は workflow 設計と prompt 構造を支えますが、長い場面で話者分離が常に完璧とは証明しません。本番会話に使う前に、人物識別とタイミングを検証してください。

[![ケース 1 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-01.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-01.mp4)

[動画再生ページを開く](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-01.mp4)

タイプ: Tutorial | 日付: 2026-06-26

---

<a id="case-2"></a>
### ケース 2: [マルチクリップ物語動画の音声設計](https://x.com/gavinpurcell/status/2070246132341727506) (作者 [@gavinpurcell](https://x.com/gavinpurcell))

**Seed-Audio 1.0 がマルチクリップ ビデオ ストーリーのタイミングと一貫性の問題を軽減できるかどうかをテストします。**

- ソース証拠: 作者は約1分の低解像度・複数クリップ動画から始め、Seedance prompt で一貫した音声を保つのは難しいと述べ、Claude Code、Codex、FAL key を使った agent 支援の音声処理を試しています。
- コピーすること: Seed-Audio を既存の複数クリップ動画の修復または設計レイヤーとして扱います。1つの prompt がショット変化、転換、環境音、効果音まで覆う場合に特に有効です。
- 実用ワークフロー: 動画の文脈を agent に渡し、場面ごとの音声計画を作らせ、サウンドトラックや効果音を生成し、全体1分ではなく各クリップ単位で比較します。
- 注意点: 同じソースは、一部の効果音が画面上の動作とまだ正確に合わないとも述べています。そのためこれは Tutorial ではなく Evaluation であり、有用なテスト方法と mismatch リスクを残しています。

[![ケース 2 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-02.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-02.mp4)

[動画再生ページを開く](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-02.mp4)

タイプ: Evaluation | 日付: 2026-06-25

---

<a id="case-3"></a>
### ケース 3: [音声先行の Seedance 参照ワークフロー](https://x.com/EvoLinkAi/status/2070722722217578562) (作者 [@EvoLinkAi](https://x.com/EvoLinkAi))

**音声の生成、キービジュアルの作成、両方を Seedance リファレンスとして使用するという 3 ステップのワークフローを構築します。**

- ソース証拠: 公開ソースは3段階の pipeline を説明しています。Seed-Audio 1.0 で音声を生成し、キービジュアルを作り、その両方を Seedance 2 reference-to-video の参照として使います。
- コピーすること: 音楽、ナレーション、環境音、テンポが動画完成後の追加ではなく、動画を最初から導くべき場合に使います。
- 実用ワークフロー: まず音声 prompt で感情のリズムを決め、場面に合う画像を作成または選択し、時間方向と視覚方向を同時に動画モデルへ与えます。
- 注意点: これは公式 workflow パターンであり、独立 benchmark ではありません。出発点として有用ですが、lip-sync、カットのタイミング、音声手掛かりへの追従は別途テストが必要です。

[![ケース 3 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-03.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-03.mp4)

[動画再生ページを開く](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-03.mp4)

タイプ: Tutorial | 日付: 2026-06-27

---

<a id="case-4"></a>
### ケース 4: [環境音付き 2 分間ダイアログ](https://x.com/tarumainfo/status/2071255504907891186) (作者 [@tarumainfo](https://x.com/tarumainfo))

**複数の音声、アンビエンス、BGM を備えたコンパクトなオーディオ ドラマ シーン用の Seed-Audio 1.0 を評価します。**

- ソース証拠: 投稿には INTENT、AESTHETIC、EXECUTION の各セクションを使った具体的な2分間の prompt/script が含まれています。環境音、背景音楽、2人の声のプロフィール、感情表現、行ごとの台詞が指定されています。
- コピーすること: 単一のナレーションではなく音声ドラマ場面を作るとき、この脚本形式を使います。環境を先に置き、次にキャラクターの声を定義し、台詞内に短い演技指示を入れます。
- 実用ワークフロー: 場面を短い script として書き、各台詞の演技指示を数語に抑え、持続する背景音を入れ、モデルが感情とテンポの両方を追うか聞きます。
- 注意点: 公開ソースは結果が prompt によく従ったと述べていますが、長尺の一貫性はまだ確認が必要です。本番では、感情や音楽がずれる場合に備えて長い場面を短い beat に分けてください。

[![ケース 4 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-04.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-04.mp4)

[動画再生ページを開く](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-04.mp4)

タイプ: Tutorial | 日付: 2026-06-28

---

<a id="case-5"></a>
### ケース 5: [博物館ガイド風の場面対話](https://x.com/TomLikesRobots/status/2070923534449119424) (作者 [@TomLikesRobots](https://x.com/TomLikesRobots))

**Seed-Audio が対話、伝達、および明確なキャラクターの声を生成するシーンレベルの言語推論をテストします。**

- ソース証拠: 作者は短い prompt を提示しています。博物館ガイドが困惑した来館者に、“crossing the Rubicon” がなぜ後戻りできない地点を越える意味なのかを説明する場面です。投稿では Seed Audio が会話、話し方、キャラクター声を生成したとされています。
- コピーすること: 各台詞を手書きせず、簡潔な状況から短い教育的対話を Seed-Audio に推論させたいときに使います。
- 実用ワークフロー: 役割、説明すべき概念、会話関係をモデルに渡し、生成された発話が自然か、説明が正しいかを評価します。
- 注意点: これは Demo です。場面レベルの言語推論と自然な delivery を示しますが、再現可能な benchmark ではありません。教育用途では事実確認が必要です。

[![ケース 5 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-05.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-05.mp4)

[動画再生ページを開く](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-05.mp4)

タイプ: Demo | 日付: 2026-06-27

---

<a id="case-6"></a>
### ケース 6: [参照音声 MC ワークフロー](https://x.com/JPAI_HEAVEN/status/2070842306329227264) (作者 [@JPAI_HEAVEN](https://x.com/JPAI_HEAVEN))

**ダウンストリームビデオ生成前に、反復的な MC またはシリーズのナレーションのリファレンス音声ワークフローを評価します。**

- ソース証拠: 投稿は2段階の reference-voice workflow を説明しています。元の声素材から約1分の MC 音声を生成し、その音声を短く切り、Seedance 2.0 の lip-sync video に渡します。
- コピーすること: 継続的なホスト、アナウンサー、MC の声でシリーズを支えたいとき、動画生成前に再利用可能な音声参照を作るために使います。
- 実用ワークフロー: 長めでクリーンな音声サンプルを作り、短いセグメントに切り、動画参照として使い、動画生成後に生じた drift を編集で直します。
- 注意点: 作者は Seedance で動画化すると声が少し変わると明言しています。これは中心的な caveat であり、workflow 構築の Tutorial であって、安定した声の同一性の保証ではありません。

[![ケース 6 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-06.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-06.mp4)

[動画再生ページを開く](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-06.mp4)

タイプ: Tutorial | 日付: 2026-06-27

---

<a id="case-7"></a>
### ケース 7: [Claude MCP のボイスオーバーと多言語吹き替え統合](https://x.com/higgsfield/status/2070916672106680360) (作者 [@higgsfield](https://x.com/higgsfield))

**ナレーション、音声クローン、およびダビングのためのアシスタントネイティブのクリエイティブワークスペースの一部として Seed-Audio 1.0 を評価します。**

- ソース証拠: Higgsfield は、Claude が MCP integration を通じて音声を生成でき、voiceover、voice cloning、50以上の言語での多言語音声作業を Seed Audio 1.0 の一部利用で扱えると述べています。
- コピーすること: no-code または agent-facing なアクセス経路を理解するために使います。制作者は音声 endpoint を直接呼ばず、Claude と MCP provider を通じて音声タスクを流せます。
- 実用ワークフロー: Claude 内で短い voiceover や多言語音声の依頼を始め、MCP 経路で生成し、出力が対象言語、声の identity、メディア workflow に合うか確認します。
- 注意点: これは Integration であり品質評価ではありません。投稿は利用可能性と workflow surface を示しますが、50以上の言語すべての品質を独立検証していません。

[![ケース 7 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-07.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-07.mp4)

[動画再生ページを開く](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-07.mp4)

タイプ: Integration | 日付: 2026-06-27

---

<a id="case-8"></a>
### ケース 8: [参照音声品質と高音ボイスの制約](https://x.com/genel_ai/status/2070438167019409582) (作者 [@genel_ai](https://x.com/genel_ai))

**日本語の音声、感情の追従性、基準音声の精度、高音の合成音のリスクを評価します。**

- ソース証拠: 作者は日本語での実使用を報告しています。Seedance 2.0 audio より安定した日本語発話、会話内の感情追従、30秒上限の強い参照音声精度、音声と画像の同時参照不可、高い声での機械的アーティファクトが挙げられています。
- コピーすること: 日本語または非英語音声の production test 用 checklist として使います。安定性、感情追従、参照精度、参照モード制限、pitch artifact を確認します。
- 実用ワークフロー: 通常声と高い声で短いクリップを作り、参照音声と比較し、画像誘導 workflow は別に試します。ソースは音声参照と画像参照を結合できないと述べています。
- 注意点: これは Evaluation です。主な価値は制限マップであり、「Seed-Audio は常に優れる」ではなく、どこが強く、どこに追加テストが必要かを示します。

[![ケース 8 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-08.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-08.mp4)

[動画再生ページを開く](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-08.mp4)

タイプ: Evaluation | 日付: 2026-06-26

---

<a id="case-9"></a>
### ケース 9: [SNS ストーリー朗読エンジン](https://twitter.com/deepwhitman/status/2071485165390704837) (作者 [@deepwhitman](https://x.com/deepwhitman))

**テキスト投稿がオーディオファーストのエンターテイメントになるソーシャルストーリーのナレーション形式をテストします。**

- ソース証拠: 作者は人気の AITA 風投稿を Seed Audio 1.0 でナレーションし、反復可能な viral content engine の可能性として位置付けています。同じ作者の返信には元のストーリーへのリンクもあります。
- コピーすること: テキスト量の多いソーシャル投稿を、短尺プラットフォーム向けの低摩擦なナレーション型エンタメに変換できるか試すときに使います。
- 実用ワークフロー: 公開テキストストーリーを選び、ナレーション用セグメントへ調整し、音声を生成し、簡単なビジュアルや字幕と組み合わせ、反復可能な pipeline になるか測ります。
- 注意点: これは Demo であり、権利や成長の保証ではありません。ストーリー内容には許可または適切な source handling が必要で、scalable channel と呼ぶ前に audience test が必要です。

[![ケース 9 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-09.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-09.mp4)

[動画再生ページを開く](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-09.mp4)

タイプ: Demo | 日付: 2026-06-29

---

<a id="case-10"></a>
### ケース 10: [画像参照によるキャラクター音声探索](https://x.com/tc50501/status/2070498347824337389) (作者 [@tc50501](https://x.com/tc50501))

**最終的なボイスロック制作ではなく、初期のキャラクターボイスキャストとして参照イメージオーディオを評価します。**

- ソース証拠: 作者は女性キャラクターの参照画像だけを渡し、約10秒の声の台詞を3つ生成しています。2つは方向性が近く、1つは明らかに高すぎます。
- コピーすること: 画像誘導音声を初期の声 casting tool として使います。最終台詞を録る前、または voice model を固定する前に、キャラクターがどう聞こえるか探索します。
- 実用ワークフロー: 同じキャラクター画像で複数の短い台詞を試し、pitch、tone、人格方向を比べ、複数行で安定する候補だけを残します。
- 注意点: 公開ソース自身が、pitch と tone の安定性は固定映画キャラクター声にはまだ不十分だと警告しています。これは casting の有用性と production risk を定義する Evaluation です。

![ケース 10 media](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-10.jpg)

タイプ: Evaluation | 日付: 2026-06-26

---

<a id="case-11"></a>
### ケース 11: [声の演技とフォーリーの低コスト検証](https://x.com/TomLikesRobots/status/2070288519684108353) (作者 [@TomLikesRobots](https://x.com/TomLikesRobots))

**ビデオ生成に取り組む前に、音声演技とフォーリー用の低コストの反復レイヤーとして Seed-Audio 1.0 を評価します。**

- ソース証拠: 作者は初期テストで voice acting と foley が Seedance 2 native audio より良く感じられたと報告し、15秒の audio test は数セントだけだったと述べています。
- コピーすること: Seed-Audio を安価な pre-production test レイヤーとして使います。特に声の演技、foley、ambience がアイデアの成否を左右する場面で有効です。
- 実用ワークフロー: まず10〜15秒の短い音声テストを生成し、動画モデルの native audio と比較し、音の方向性が十分強い場合だけ後続の動画生成へ進みます。
- 注意点: コメントには reference voice conversion と、生成音声を Seedance lip-sync に使う際の未解決問題が残っています。これは低コストテストの役割を検証する Evaluation であり、完全な final workflow ではありません。

[![ケース 11 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-11.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-11.mp4)

[動画再生ページを開く](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-11.mp4)

タイプ: Evaluation | 日付: 2026-06-25

---

<a id="case-12"></a>
### ケース 12: [Claude で音楽と効果音を Premiere に組み込む](https://x.com/mattworkman/status/2076148989687181705) (作者 [@mattworkman](https://x.com/mattworkman))

**音楽、効果音、音声を別々に生成し、Claude に Premiere 上で組み立てさせながら、タイミングとフェードを手動で調整できる状態を保ちます。**

- ソース証拠: Matt Workman は、シーン途中の感情変化に合わせた音楽ベッド用 Seed Audio prompt を Claude に作らせ、重要な効果音も選定・生成させる方法を説明しています。
- コピーすること: 品質とミックスを細かく制御したい場合は、音楽、効果音、音声を一度に生成せず、Seed Audio の処理を別パスに分けます。
- 実用ワークフロー: Claude に脚本を渡し、Seed Audio の音楽素材と効果音素材を個別に生成し、Premiere に自動配置させた後、設定、タイミング、フェードを手動で調整します。
- 注意点: ソースが示すのは分離生成の方が高品質だという作者の実務上の好みであり、統制された benchmark ではありません。自分の素材で一括生成と比較してください。

![ケース 12 media](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-12.jpg)

タイプ: Tutorial | 日付: 2026-07-12

---

<a id="case-13"></a>
### ケース 13: [参照音声による格闘実況タイミング検証](https://x.com/aimikoda/status/2076526254417735781) (作者 [@aimikoda](https://x.com/aimikoda))

**完成した Seedance 編集を Seed Audio の参照入力にし、映像アクションから時間指定の実況文を作り、タイミング一致を主な評価リスクとして扱います。**

- ソース証拠: 親投稿は完成した格闘クリップを示し、返信 https://x.com/aimikoda/status/2076527528227815779 にワークフローを誘導しています。この返信では Midjourney、Seedance 2.0、Seed Audio の正確な prompt が公開され、完成動画の音声を Seed Audio の reference として使ったことも説明されています。
- コピーすること: 先に映像側の格闘編集を完成させ、その完成音声を Seed Audio の reference として再利用しつつ、別モデルに映像アクションから実況文を書かせます。
- 実用ワークフロー: Midjourney でキャラクターとリング素材を作り、複数の Seedance 格闘パスを生成して強い部分を編集でつなぎ、完成音声を抽出し、GPT-5.6 に映像から実況を書かせたうえで、尺、声質、環境、タイムライン cue、negative 制約を含む Seed Audio prompt を作成します。
- 注意点: 作者はおよそ 10 回試してもタイミングが完全には合わなかったと述べています。したがってこれは Tutorial ではなく Evaluation として扱い、prompt の再調整や手動同期を前提にしてください。

[![ケース 13 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-13.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-13.mp4)

[動画再生ページを開く](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-13.mp4)

タイプ: Evaluation | 日付: 2026-07-13

---

<a id="case-14"></a>
### ケース 14: [クローン音声で動かすモーショングラフィックス技能フロー](https://x.com/akiyoshisan/status/2077650497536987154) (作者 [@akiyoshisan](https://x.com/akiyoshisan))

**Seed Audio で自分の声をクローン化し、そのナレーションを時間軸の骨格として、テキスト、図形アニメーション、BGM、字幕を含むモーショングラフィックス動画を組み立てます。**

- ソース証拠: 作者は、この動画が MiniMax Hub のモーショングラフィックス skill で作られたと述べ、Seed Audio 1.0 で自分の声をクローン化し、ナレーションを生成し、長さと内容を確認し、15 秒出力用の 6 枚 storyboard を設計し、日本語テキストを作成し、切れ目のない図形変形を計画し、Seedance 2.0 Fast で動画化し、最後にナレーション、BGM、効果音、日本語字幕を合成したと公開しています。
- コピーすること: 短い解説動画やモーショングラフィックス動画で、storyboard カード、テキスト overlay、アニメーションの拍を同期させたいなら、Seed Audio の voice clone と narration を timing の主軸として使います。
- 実用ワークフロー: 元になる声を用意し、Seed Audio で narration を生成し、目標の長さを固定し、その長さに合わせて storyboard を設計し、補助テキストと graphic motion を作り、映像をレンダリングしてから narration、music、effects、subtitles を最終出力に混ぜます。
- 注意点: この投稿は workflow の形と tool chain を証明していますが、正確な prompt や node 設定は公開していません。prompt 再現例ではなく、移植可能な production pattern として扱ってください。

[![ケース 14 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-14.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-14.mp4)

[動画再生ページを開く](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-14.mp4)

タイプ: Tutorial | 日付: 2026-07-16

---

<a id="case-15"></a>
### ケース 15: [エージェントが前向き版へ書き換える音声テスト](https://x.com/fabianstelzer/status/2077138756939727067) (作者 [@fabianstelzer](https://x.com/fabianstelzer))

**既存の動画を agent に渡し、新しいトーン向けに script を書き換えさせてから、Seed Audio で合う voiceover を生成し、映像を組み直します。**

- ソース証拠: 作者は、Claude で動く Glif agent が元動画リンクを受け取り、Gemini 3.5 で動画を見て、より前向きな代替 script を書き、Seed Audio で似た voiceover を生成し、その後 NB2 で stills を作り、Remotion で組み立てたと述べています。
- コピーすること: 元の話し方を残したままメッセージのトーンだけを変えたい agentic video remix では、Seed Audio を voice-preserving narration layer として使います。
- 実用ワークフロー: 元動画を agent に渡し、トーン変更を依頼し、clip を解析して新しい script を書かせ、Seed Audio で置き換え voiceover を生成し、visuals を再構築または拡張して、最後に pacing と music を個別に見直します。
- 注意点: 作者は pacing と tempo にまだ改善余地があり、画像の texture 品質は model 選択に依存し、ElevenLabs での music 生成は失敗したと明言しています。manual review が前提の Evaluation workflow として扱ってください。

[![ケース 15 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-15.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-15.mp4)

[動画再生ページを開く](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-15.mp4)

タイプ: Evaluation | 日付: 2026-07-14

---

<a id="case-16"></a>
### ケース 16: [1枚写真の Scenario MCP 冒険トレーラー](https://x.com/emmanuel_2m/status/2078227114818707891) (作者 [@emmanuel_2m](https://x.com/emmanuel_2m))

**1枚の人物写真と1本の総合指示だけで、Codex/GPT の MCP 連携に複数の Seedance 映像、Seed Audio のナレーション、音楽、仕上げ処理まで一括で進めさせます。**

- ソース証拠: 公開リプライには 4 段階の MCP 手順と完全な予告編用指示文があり、親投稿では 1 枚のアップロード写真から作ったインディ・ジョーンズ風の完成映像が示されています。
- コピーすること: MCP エージェントに場面生成、ナレーション、音楽、ポスター、最終仕上げまでまとめて担当させたいなら、まず正面の人物写真 1 枚と全体方針をまとめた指示文を用意します。
- 実用ワークフロー: Codex または GPT 5.6 で Scenario MCP を読み込み、人物写真をアップロードし、公開された指示文を実行して、少なくとも 10 個の Seedance 場面で顔の一貫性を保ちながら、Seed Audio のナレーションと音楽、レトロ調タイトルカードをまとめて仕上げます。
- 注意点: この公開情報は編成パターンと指示文の境界を示しますが、途中の再試行や手作業の調整は公開していません。ワンクリック完成の保証ではなく、統合型ワークフローの実例として扱ってください。

![ケース 16 media](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-16.jpg)

タイプ: Integration | 日付: 2026-07-17

---

<a id="case-17"></a>
### ケース 17: [ビート同期の予告編サウンド設計](https://x.com/maxescu/status/2078146037517312129) (作者 [@maxescu](https://x.com/maxescu))

**先に登場人物と静止画を固め、その後で予告編のカットを音楽の時間軸に合わせ、正確な入りが必要なナレーションや強調効果音だけに Seed Audio を使います。**

- ソース証拠: 公開された Inferno の連続投稿では、キャラクター設定画、静止画先行のショット作成、ビートに沿った映像指示、そして静かな区間だけにナレーションを入れ、Seed Audio 1.0 で強調効果音を足す最終組み立て工程が説明されています。
- コピーすること: まず前段で人物の見た目と構図を安定させ、映像編集が音楽に乗ったあとで、Seed Audio を拍に合わせた音響設計の層として使います。
- 実用ワークフロー: 4K のキャラクター設定画を作り、各ショットをいったん静止画として固めてから Seedance で動かし、映像指示をカメラ・動作・光の拍構成で書き、最終カットを音楽の時間位置に合わせてから、Seed Audio でナレーションの空白と強調効果音を補います。
- 注意点: この連続投稿は指示の組み立て方と工程順を公開していますが、再利用できる Seed Audio の本文指示や他の音声基盤との厳密比較は公開していません。

[![ケース 17 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-17.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-17.mp4)

[動画再生ページを開く](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-17.mp4)

タイプ: Tutorial | 日付: 2026-07-17

---

<a id="case-18"></a>
### ケース 18: [Seed Audio を使う2枚画像アニメ短編](https://x.com/Dani__oros/status/2077829108818657420) (作者 [@Dani__oros](https://x.com/Dani__oros))

**1〜2 枚の参照画像を見た目の固定軸にし、Seed Audio に音楽を任せ、Seedance で短編を完成したアニメ映像へ広げます。**

- ソース証拠: 投稿では Tide-Rider について、アニメーションは Seedance 2.0、音楽は Seed Audio 1.0、元画像は Krea 2、編集は CapCut と明記し、作品全体がほぼ 2 枚の参照画像と文字指示だけで作られたと説明しています。
- コピーすること: 最初から完全な設定資料集を作る代わりに、まず主役となる参照画像 1 枚で見た目を固定し、最後に新しい角度や種明かしが必要なときだけ 2 枚目を足します。
- 実用ワークフロー: Krea 2 で基準画像を作り、それを Seedance の見た目アンカーとして短いアニメ映像を生成し、文字指示は軽く保ち、Seed Audio に音楽を任せたうえで CapCut でタイミングを整えます。
- 注意点: この投稿は 2 枚の画像でも完成短編を作れることを示しますが、正確な指示文やショット間で追加の後処理が必要だったかどうかは公開していません。

[![ケース 18 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-18.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-18.mp4)

[動画再生ページを開く](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-18.mp4)

タイプ: Demo | 日付: 2026-07-16

---

<a id="case-19"></a>
### ケース 19: [同一映像で音声だけ差し替える TTS 品質比較](https://x.com/takareinhard/status/2079028004202918291) (作者 [@takareinhard](https://x.com/takareinhard))

**本番の TTS スタックを決める前に、完成クリップの映像を固定したまま音声だけ差し替え、Seed Audio と他の TTS の感情表現、訛り、元音声の残り方を比べます。**

- ソース証拠: 作者は同じ短いクリップを 2 本並べ、前者は Seedance 2.0 の元音声、後者は Seed Audio 1.0 に差し替えた版だと説明したうえで、ElevenLabs、にじボイス、MiniMax、Gemini TTS と主観比較しています。
- コピーすること: 本番用 TTS を決める前に、映像を固定し、音声層だけを差し替えることで、感情表現、訛りの安定性、元声優に似すぎる漏れを短時間で比べられます。
- 実用ワークフロー: まず完成した映像を 1 本書き出し、基準となる音声版を残し、2 本目で音声だけ Seed Audio に置き換え、感情、訛り、声の似すぎ具合を見比べます。
- 注意点: これは 1 人の作者による定性的な評価で、公開 prompt、参照音声、数値ベンチマークはありません。最終順位表ではなく、比較方法として扱ってください。

[![ケース 19 video preview](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/media/cases/case-19.jpg)](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-19.mp4)

[動画再生ページを開く](https://pub-62cf7640cd0f4066b60933bd2e9b85ef.r2.dev/github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/case-19.mp4)

タイプ: Evaluation | 日付: 2026-07-20

---

## 関連リポジトリ

現在、別の公開 Seed-Audio リポジトリは検証されていません。保守されている skill の入口は npm の evolink-seed-audio.

<a id="acknowledge"></a>
## 🙏 謝辞

このリポジトリはケース単位で公開クリエイターやプロバイダーの投稿へリンクしています。公開ソースは各ケース見出しで明記します。

[@gokayfem](https://x.com/gokayfem) [@gavinpurcell](https://x.com/gavinpurcell) [@EvoLinkAi](https://x.com/EvoLinkAi) [@tarumainfo](https://x.com/tarumainfo) [@TomLikesRobots](https://x.com/TomLikesRobots) [@JPAI_HEAVEN](https://x.com/JPAI_HEAVEN) [@higgsfield](https://x.com/higgsfield) [@genel_ai](https://x.com/genel_ai) [@deepwhitman](https://x.com/deepwhitman) [@tc50501](https://x.com/tc50501) [@TomLikesRobots](https://x.com/TomLikesRobots) [@mattworkman](https://x.com/mattworkman) [@aimikoda](https://x.com/aimikoda) [@akiyoshisan](https://x.com/akiyoshisan) [@fabianstelzer](https://x.com/fabianstelzer) [@emmanuel_2m](https://x.com/emmanuel_2m) [@maxescu](https://x.com/maxescu) [@Dani__oros](https://x.com/Dani__oros) [@takareinhard](https://x.com/takareinhard)

*リンク切れ、誤った帰属、またはリンク先で裏付けられていない主張があれば修正を歓迎します。*

[![Star History Chart](https://api.star-history.com/svg?repos=Evolink-AI/Awesome-Seed-Audio-1.0-Guide-and-Usecases&type=Date)](https://www.star-history.com/#Evolink-AI/Awesome-Seed-Audio-1.0-Guide-and-Usecases&Date)
