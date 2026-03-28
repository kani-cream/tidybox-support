# よくある質問 / FAQ

## 日本語

### メニューバーにアイコンが表示されない

macOS のメニューバーにはスペース制限があります。他のアイコンを Command + ドラッグで移動してスペースを確保してください。アクティビティモニタで TidyBox が起動しているかも確認してください。

---

### ルールを作ったのにファイルが整理されない

よくある原因を順に確認してください:

1. 設定 > 監視ディレクトリでフォルダが登録されていますか？
2. フォルダの監視が有効になっていますか？（トグルを確認）
3. ドライランモードがオフになっていますか？（設定 > 一般）
4. 対象ファイルが除外パターン（`*.tmp` など）に一致していませんか？
5. 隠しファイル（`.` で始まるファイル）の除外設定は適切ですか？
6. ルール自体が有効になっていますか？

最も効率的なトラブルシューティング方法は、ノードエディタでドライランを実行して、ルールがファイルを正しく検出しているか確認することです。

---

### ファイルが意図しない場所に移動された

「履歴」タブを開き、取り消したい操作を探してください（検索バーでファイル名を検索できます）。操作行の「元に戻す」ボタンをクリックすると、ファイルが元の場所に復元されます。

ただし、「ゴミ箱から削除」操作と、履歴保持期間を過ぎた操作は元に戻せません。

---

### ドライランモードとは？

ドライランモードをオンにすると、TidyBox はルールの評価だけを行い、ファイルの移動やリネームは一切行いません。結果はログにのみ記録されます。新しいルールが意図通りに動くか確認したいとき、あるいは TidyBox を初めて使うときにオンにしてください。設定 > 一般 > 「ドライランモード」で切り替えられます。

---

### リアルタイム監視とスケジュール実行の違いは？

リアルタイム監視は、フォルダにファイルが追加・変更されたときに即座にルールを評価します。対象は新しいファイルだけです。

スケジュール実行は、指定した間隔（毎時/毎日/毎週）でフォルダ内のすべてのファイル（既存のものも含む）を評価します。「更新日が 90 日以上前のファイルをアーカイブする」のようなエイジングルールには、スケジュール実行が必要です。

両方を組み合わせると効果的です。たとえば、リアルタイム監視でダウンロードされた画像を即座に Pictures に移動しつつ、スケジュール実行で30日経過したファイルに「要整理」タグを付ける、といった使い方ができます。

---

### フォルダへのアクセス権が失われたというエラーが出る

フォルダの移動や名前変更、macOS のアップデート後に発生することがあります。設定 > 監視ディレクトリで問題のフォルダを削除し、同じフォルダを再度追加してください。アクセス許可ダイアログで「許可」をクリックすれば再び監視が始まります。

---

### 外付けドライブのフォルダを監視できますか？

はい。ただし、ドライブが接続されていないときは監視が一時停止し、再接続すると自動的に再開されます。別のポートに接続するとパスが変わる可能性があります。Time Machine バックアップドライブの監視は避けてください。

---

### CPU やメモリの使用量が高い

通常、TidyBox は非常に軽量です。使用量が高い場合は、以下を確認してください:

- 深いフォルダ構造でサブディレクトリ監視を有効にしていないか
- 複雑な正規表現パターンを使っていないか
- 一括操作の最大ファイル数が大きすぎないか
- 監視フォルダの数が多すぎないか

---

### サブフォルダ監視で無限ループが発生する

移動先フォルダが監視フォルダのサブフォルダ内にある場合に起こります。たとえば `~/Downloads` をサブフォルダ監視で監視し、ルールで `~/Downloads/Images` に移動する設定にすると、移動 → 検知 → 再移動のループになります。

解決するには、移動先を監視フォルダの外（例: `~/Pictures/Images`）に設定するか、サブディレクトリ監視をオフにして直下のファイルのみ監視するか、除外パターンで移動先フォルダのファイルを除外してください。

---

### プリセットの移動先パスが合わない

プリセットのパス（`~/Downloads/Archives` など）は一般的な例です。プリセットを適用した後、ノードエディタでアクションノードをクリックし、移動先パスを自分の環境に合わせて変更して保存してください。

---

### 「フルディスクアクセス」が必要と表示される

ゴミ箱管理機能を使う場合にのみ必要です。設定画面の「システム設定を開く」ボタンからシステム設定 > プライバシーとセキュリティ > フルディスクアクセスを開き、TidyBox を有効にしてください。ゴミ箱管理を使わなければ不要です。

---

### 「フォルダへ移動」と「アーカイブに移動」の違いは？

「フォルダへ移動」は任意のフォルダにファイルを移動するだけです。圧縮や自動削除はありません。

「アーカイブに移動」は設定で指定したアーカイブディレクトリにファイルを移動し、定期的に ZIP 圧縮、保持期間後に自動削除というライフサイクル管理を行います。古いファイルを段階的に退避して最終的に削除したい場合に使います。単にフォルダ間の整理をしたいだけなら「フォルダへ移動」を使ってください。

---

### 複数のルールが同じファイルに一致した場合は？

ルールは優先度順（一覧の上から下）に評価され、最初に一致したルールのアクションが実行されます。タグ付けなど、複数回実行可能なアクションは複数のルールから適用されることがあります。ルールの競合が心配な場合は、ダッシュボードの「ルールフィットネス」で競合検出の結果を確認してください。

---

## English

### The menu bar icon does not appear

The macOS menu bar has limited space. Command-drag other icons to make room. Check Activity Monitor to confirm TidyBox is running.

---

### Rules are set up but files are not being organized

Check these common causes in order:

1. Is a folder registered in Settings > Watched Directories?
2. Is monitoring enabled for that folder? (check the toggle)
3. Is Dry Run Mode off? (Settings > General)
4. Does the file match an exclusion pattern like `*.tmp`?
5. Is the file a hidden file excluded by settings?
6. Is the rule itself enabled?

The fastest way to diagnose this is to run a dry run in the node editor and see whether the rule detects the file.

---

### A file was moved to the wrong place

Open the History tab and find the operation (use the search bar to search by filename). Click the undo button to restore the file to its original location.

"Delete from Trash" operations and operations beyond the retention period cannot be undone.

---

### What is Dry Run Mode?

When enabled, TidyBox evaluates rules but does not perform any file operations. Results are logged only. Use it to test new rules or when first setting up TidyBox. Toggle it under Settings > General.

---

### What is the difference between real-time monitoring and scheduled execution?

Real-time monitoring detects files as they are added or changed. It only evaluates new files.

Scheduled execution evaluates all files in watched folders (including existing ones) at set intervals -- hourly, daily, or weekly. This is required for aging rules like "archive files modified more than 90 days ago."

Use both together: real-time for instant organization, scheduled for aging rules and periodic cleanup.

---

### "Folder access lost" error

This happens when a folder is moved, renamed, or after a macOS update. Remove the folder from Settings > Watched Directories and re-add it.

---

### Can I watch folders on external drives?

Yes. Monitoring pauses when the drive is disconnected and resumes when reconnected. The path may change if the drive is connected to a different port. Avoid monitoring Time Machine drives.

---

### High CPU or memory usage

TidyBox is normally very lightweight. If usage is high, check for deep subdirectory monitoring, complex regex patterns, large batch sizes, or too many watched folders.

---

### Infinite loop with subdirectory monitoring

This happens when the destination folder is inside the watched folder. For example, watching `~/Downloads` with subdirectory monitoring and moving files to `~/Downloads/Images` creates a move-detect-rematch loop.

Fix this by moving the destination outside the watched folder (e.g., `~/Pictures/Images`), disabling subdirectory monitoring, or adding exclusion patterns for the destination.

---

### Preset destination paths do not match my setup

Preset paths like `~/Downloads/Archives` are examples. After applying a preset, click the action node in the node editor and change the destination path to match your environment.

---

### "Full Disk Access" required

This is only needed for trash management. Open System Settings > Privacy & Security > Full Disk Access and enable TidyBox. Not required if you do not use trash management features.

---

### What is the difference between "Move to Folder" and "Archive File"?

"Move to Folder" simply moves a file to any folder. No compression or auto-deletion.

"Archive File" moves a file to a dedicated archive directory with periodic ZIP compression and automatic deletion after a retention period. Use it for gradual lifecycle management of old files. For simple folder organization, use "Move to Folder."

---

### What happens when multiple rules match the same file?

Rules are evaluated in priority order (top to bottom in the rule list). The first matching rule's action is executed. Some actions like tagging can apply from multiple rules. Check the Dashboard's Rule Fitness section if you are concerned about conflicts.
