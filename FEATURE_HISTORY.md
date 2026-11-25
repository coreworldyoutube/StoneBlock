# StoneBlock 開発履歴台帳

調査対象は GitHub の `main` 系列23コミットと、別ブランチ `backup/pre-mining-game-rollback-20261125` の43コミットです。後者は `main` の履歴を含み、その後に追加された20コミットで翻訳・資源JSON・機械・カメラ操作などが試されています。

## 全コミット（古い順）

| SHA | コミット内容 |
|---|---|
| `e507415` | Initial commit |
| `41b909c` | Add playable 2D StoneBlock mining game |
| `9523a5a` | Fix placement mode and quantity handling |
| `a9335ed` | Document StoneBlock game controls |
| `d6041a6` | Use a single mining on/off toggle for placement mode |
| `80d06a1` | Update README.md |
| `20fdfcb` | Simplify block visuals and expand immersive game field |
| `8dcf269` | Remove distracting yellow UI accents |
| `256dbfd` | Expand world and add touch scrolling with 2x2 mining and single-block placement |
| `d2571f3` | Fix single-cell mining, expand world to 300x300, remove tile outlines |
| `19fd911` | Render textured underground terrain with a fast scrollable canvas |
| `eafa0dd` | Generate geological regions and ore veins with Perlin noise |
| `26edfc3` | Add exploration fog and reveal nearby blocks |
| `d54e087` | Fix exploration reveal script formatting |
| `aad297e` | Add distance-based darkness and clickable minimap |
| `6b2f570` | Add local world saves and natural cave generation |
| `4e624ab` | Fix local save integration and add noise-based cave pockets |
| `c9eb8d6` | Preserve saved camera position and save on page exit |
| `69944f3` | Use seeded base terrain and save only world changes |
| `567ccd2` | Persist inventory independently from generated worlds |
| `9ee1aa5` | Randomize world seed and remove manual save controls |
| `c4c4f3c` | Add seed input and autosave; enrich mineral veins |
| `677fbbf` | Add JSON block registry |
| `53a6ff1` | Add machine definitions |
| `ce7d246` | Add Japanese UI translations |
| `927dba8` | Add English UI translations |
| `77490fa` | Add conveyor transport, furnace basics, JSON block registry and localization |
| `6fd4da6` | Expand Japanese interface translations |
| `0d75af3` | Expand English interface translations |
| `24ea87e` | Complete language switching for main interface |
| `4a59e4e` | Document JSON data, conveyor controls and furnace processing |
| `a2e472a` | Fix machine controls and interaction modes |
| `e453b20` | Add drag navigation mode for world exploration |
| `898d78d` | Replace DOM scrolling with camera-coordinate world navigation |
| `809402d` | Explain drag camera movement in Japanese hints |
| `c16b8af` | Explain drag camera movement in English hints |
| `0e2a855` | Prevent browser page gestures from conflicting with world camera drag |
| `9efb332` | Lock document viewport to prevent browser page drag scrolling |
| `4172fe9` | Use native touch events for mobile world camera drag |
| `2d5e575` | Restore previous pointer-based camera drag handling |
| `5f0908f` | Use native browser scrolling with 10-block render buffer |
| `f958269` | Allow native touch scrolling on the world viewport |
| `4965815` | Add local save data reset button |

## 機能が追加・変更された経緯

### 採掘・ワールド

- 最初のワールドは31×31。後に300×300へ拡張。
- `256dbfd` では2×2採掘が入ったが、`d2571f3` で1マス採掘に戻った。現在の仕様は1マス採掘。
- `19fd911黄金データ` はCanvas描画とブラウザ標準スクロールを使う基礎版。中央5×5の空洞、露出ブロックの採掘、設置を持つ。
- `eafa0dd` でPerlin Noiseによる地質区域・鉱脈が追加された。
- `26edfc3` と `aad297e` で探索範囲・暗闇・ミニマップが追加された。
- `6b2f570` 以降で洞窟生成とローカル保存が追加された。

### セーブと初期化

- セーブ形式は履歴上で段階的に拡張され、ワールド変更差分、シード、採掘数、選択資源、モード、カメラ位置を保存する。
- `567ccd2` でインベントリ保存がワールド保存から分離された。
- `9ee1aa5` と `c4c4f3c` で地形のみ再生成する操作が中心になり、インベントリを保持する仕様になった。
- `4965815` でローカル保存データを消去するボタンが追加された。保存キーを消して再起動するため、新しいランダムシードでワールドが生成され、中央から始まる。
- 再構成版では「地形のみ再生成」と「保存データを初期化」を別の操作として残す。

### 資源・翻訳

- `677fbbf` で資源定義が `data/blocks.json` に移された。
- このJSONには石炭・泥炭、英語名、カテゴリ、色、生成重みが含まれている。
- `ce7d246` と `927dba8` で日本語・英語の翻訳JSONが追加された。
- `77490fa` でJSON読み込みとUI言語切り替えが実装された。
- これらは `main` の23コミットだけには現れず、別ブランチ側に残っていた。今回の調査で発見し、再構成版に取り込んだ。

### 機械・カメラ操作

- `77490fa` でコンベア・かまど・配る機能が追加された。
- その後、機械の操作モードと状態保存の修正が続いた。
- `e453b20` からドラッグ移動が試され、`898d78d` でブラウザ標準スクロールから独自カメラ座標方式に変更された。
- タッチイベント・Pointer Eventsの複数方式が試された後、`5f0908f` でブラウザ標準スクロールと10ブロック分の描画バッファに戻された。
- `f958269` でスクロール領域のタッチ操作を許可する調整が行われた。
- 再構成版では、コンベア・かまどの操作・描画・保存処理を外し、採掘とブラウザ標準スクロールを残す。機械機能は今回の対象外とし、将来再実装するときは独立した機能として扱う。

## 再構成版の基準

- 基礎参照：`19fd911黄金データ`
- 機能参照：`backup/pre-mining-game-rollback-20261125` の資源JSON・翻訳・10ブロック描画バッファ・保存初期化機能
- 現在の作業ブランチ：`rebuild/feature-complete-no-machines-2026-11-25`
- `main` はこの作業では変更していない。
- `data/machines.json` と機械操作コードは再構成版から除外した。
