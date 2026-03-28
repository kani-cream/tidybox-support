# ダッシュボード / Dashboard

## 日本語

ダッシュボードは、TidyBox の動作状況をまとめて確認できる画面です。ルールが期待通りに機能しているか、改善すべき点はないかを判断するための情報がここに集まっています。

### 統計サマリー

画面上部の4つのカードに、本日・今週・今月・合計の整理済みファイル数が表示されます。すべてゼロの場合は、ルールが正しく設定されていないか、監視フォルダにファイルが追加されていない可能性があります。

### 整理スコア

各監視フォルダの「整理度」をパーセンテージとランクで示します。ルールでカバーされているファイルの割合がスコアになります。

| ランク | スコア | 推奨アクション |
|--------|--------|---------------|
| 優秀 | 90-100% | 現状維持 |
| 良好 | 70-89% | 必要に応じて微調整 |
| 要改善 | 50-69% | ルールの追加を検討 |
| 要対応 | 0-49% | ルールの見直しが必要 |

フォルダカードをクリックすると未分類ファイルの一覧が表示されるので、新しいルールを作る参考にできます。「更新」ボタンでスコアを再計算できます。

### 整理トレンド

日別の整理ファイル数を棒グラフ、ファイル種別の内訳を円グラフで表示します。表示期間は 7日/30日/90日/全期間から選べます。グラフが急に下がった場合は、ルールに問題が起きているか、監視が停止している可能性があります。

### ルール別パフォーマンス

各ルールの適用回数をランキングで表示します（上位10件）。30日間一度も適用されていないルールにはオレンジ色の警告が表示されます。使われていないルールは、不要になったか設定に問題がある可能性があるので、確認してみてください。期間は 7日/30日/90日/全期間で切り替えられます。

### ルールフィットネス

ルールの「健全性」をスコアで評価します。適用回数だけでなく、Undo 率（取り消された割合）やトレンド（改善中 / 安定 / 悪化中）も考慮されます。

Undo 率が高いルールは、意図しないファイルに適用されている可能性があります。ルールカードをクリックすると、「条件が広すぎます」「Undo 率が高いため条件の見直しを検討してください」といった具体的な改善提案を確認できます。データが十分でない新しいルールは評価対象から除外されます。

### エイジング

日付条件（「N日以上前」や「直近N日以内」）を使っているルールの数と、エイジングスキャンの有効/無効を表示します。エイジングルールがゼロの場合、古いファイルが放置されている可能性があります。

### 監視ディレクトリ

登録されている監視フォルダをカード形式で一覧表示します。各カードにはフォルダ名、パス、紐づくルール数、本日の整理件数が表示されます。「無効」バッジが付いているフォルダは監視が停止中です。ルール数が 0 のフォルダにはルールの追加が必要です。フォルダの追加や設定変更は「設定」画面で行います。

### 直近の操作

最新10件の操作ログが表示されます。各ログにはアクション種別のアイコン、概要、トリガー元（リアルタイム/スケジュール）、タイムスタンプが含まれます。取り消された操作には「元に戻し済み」バッジが表示されます。「すべて表示」リンクから全履歴画面に移動できます。

---

## English

The Dashboard gives you an overview of how TidyBox is performing. It brings together the information you need to see whether your rules are working well and where improvements might be needed.

### Statistics Summary

Four cards at the top show files organized today, this week, this month, and in total. If all values are zero, your rules may not be configured correctly or no files have been added to watched folders.

### Organization Score

Each watched folder receives a health score based on the percentage of files covered by rules.

| Rank | Score | Recommended Action |
|------|-------|-------------------|
| Excellent | 90-100% | Maintain current setup |
| Good | 70-89% | Fine-tune if needed |
| Needs Improvement | 50-69% | Consider adding rules |
| Needs Attention | 0-49% | Review and add rules |

Click a folder card to see its unclassified files, which can help you design new rules. Use the refresh button to recalculate scores.

### Organization Trend

A bar chart shows daily organization counts, and a pie chart shows the file type breakdown. Switch between 7-day, 30-day, 90-day, and all-time views. A sudden drop in the chart may indicate a rule issue or a monitoring pause.

### Rule Performance

Shows your top 10 rules ranked by how often they have been applied. Rules unused for 30 days receive an orange warning -- they may be unnecessary or misconfigured. Switch the time range to analyze usage patterns.

### Rule Fitness

Evaluates each rule's health by factoring in application count, undo rate, and trend direction (improving, stable, or declining). A high undo rate suggests the rule may be matching unintended files. Click a rule card for specific improvement suggestions. Rules too new for meaningful data are excluded.

### Aging

Shows how many active rules use date-based conditions and whether aging scans are enabled. If you have zero aging rules, old files may be accumulating unmanaged.

### Watched Directories

Displays all watched folders as cards showing folder name, path, rule count, and today's organization count. Folders marked "Disabled" are not being monitored. Folders with zero rules need attention. To add or configure folders, go to Settings.

### Recent Actions

The last 10 operations, each showing an action type icon, summary, trigger source (real-time or scheduled), and timestamp. Undone operations display an "Undone" badge. Click "Show All" to open the full [History](history.md) view.
