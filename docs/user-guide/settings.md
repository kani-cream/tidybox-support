# 設定 / Settings

## 日本語

### 一般設定

**ログイン時に TidyBox を起動** -- Mac の起動時に TidyBox を自動で起動します。常駐アプリなので、有効にしておくことをおすすめします。デフォルト: オフ。

**Dock にアイコンを表示** -- Dock に TidyBox のアイコンを表示します。メニューバーだけで十分な場合はオフのままにしてください。デフォルト: オフ。

**表示言語** -- アプリの表示言語を切り替えます（システムの言語/日本語/English）。変更後はアプリの再起動が必要です。

**ドライランモード** -- ルールの評価は実行しますが、ファイルの移動やリネームなどは行いません。操作はログにのみ記録されます。新しいルールのテストや TidyBox を初めて使うときに有効にしてください。デフォルト: オフ。

**ルール適用時に承認を求める** -- ルールが一致した際に、実行前に確認ダイアログを表示します。重要なファイルを扱うフォルダで、すべての操作を確認したい場合に使います。デフォルト: オフ。

**一括操作の最大ファイル数** -- 一度のバッチ処理で処理するファイルの上限です（10 ~ 1000）。大量のファイルが一度に検知された場合のシステム負荷を制限します。デフォルト: 100。

**履歴保持期間** -- 操作履歴を保持する日数です（1日/7日/14日/21日/28日）。期間を過ぎた履歴は自動削除され、Undo もできなくなります。デフォルト: 28日。

---

### 監視ディレクトリ

フォルダの追加・管理については[監視ディレクトリ](watched-directories.md)を参照してください。

---

### 通知設定

通知モードは4つから選べます:

- **即時通知** -- ファイルが整理されるたびに通知します。整理状況をリアルタイムで把握できますが、ファイルが多い環境では頻繁になりすぎることがあります
- **バッチ完了時**（デフォルト） -- バッチ処理の完了時にまとめて通知します
- **日次サマリーのみ** -- 1日1回、指定時刻にサマリーを通知します。サマリー通知時刻は、このモードを選択した場合のみ設定できます
- **オフ** -- 通知を無効にします

---

### 除外設定

TidyBox がルール評価の対象外にするファイルの設定です。システムファイルや一時ファイルを誤って移動しないための安全装置として機能します。

**隠しファイルを除外**（デフォルト: オン） -- `.gitignore`、`.DS_Store` などドットで始まるファイルを無視します。隠しファイルにはシステムやアプリの設定ファイルが多く含まれるため、基本的にはオンのままにしてください。

**システムファイルを除外**（デフォルト: オン） -- macOS のシステムファイルを無視します。常にオンにしておいてください。

**除外パターン（glob）** -- glob パターンに一致するファイルを無視します。デフォルトでは `*.tmp`、`*.download`、`*.part`、`*.crdownload`、`.DS_Store` が設定されており、ダウンロード中のファイルが完了前に移動されるのを防いでいます。パターンを追加するにはテキストフィールドに入力して「追加」ボタンをクリックし、削除するにはパターン横の赤い「-」ボタンをクリックします。

---

### スケジュール設定

リアルタイム監視は新しく追加されたファイルだけを検知します。既に存在するファイルも定期的にルール評価するには、スケジュール実行を有効にしてください。エイジングルール（「N日以上前のファイル」を対象にするルール）を使う場合に必要です。

**スケジュール実行を有効にする** -- デフォルト: オフ。

**実行間隔** -- 毎時、毎日、毎週から選べます。通常は毎日がおすすめです。

**実行時刻** -- 毎日/毎週の場合に設定できます。Mac をあまり使わない時間帯に設定してください。

---

### ゴミ箱管理

ゴミ箱管理機能にはフルディスクアクセスの許可が必要です。詳細は[ゴミ箱管理](trash.md)を参照してください。

**現在のゴミ箱** -- ファイル数と合計サイズを表示します。「クリーンアップ...」ボタンでプレビュー付きのクリーンアップ、「更新」ボタンで情報の再取得ができます。

**除外ルール** -- クリーンアップ時に削除しないファイルの条件を設定します（拡張子/ファイル名/正規表現/サイズ/種別）。

**優先削除ルール** -- 指定した条件のファイルを、通常より短い保持日数で削除します。

**保持期間** -- ゴミ箱に入ってからこの日数を超えたファイルがクリーンアップ対象になります。デフォルト: 30日。

**サイズ上限** -- ゴミ箱の合計サイズがこの値を超えると、古いファイルから削除します。0 で無制限。デフォルト: 0。

**自動クリーンアップ** -- スケジュール実行時にクリーンアップを自動実行します。確認なしにファイルが削除されるため、慎重に使ってください。デフォルト: オフ。

---

### アーカイブ設定

アーカイブ機能の詳細は[アーカイブ](archive.md)を参照してください。

**アーカイブ機能を有効にする** -- ルールの「アーカイブに移動」アクションを使うために必要です。デフォルト: オフ。

**アーカイブ先** -- 「アーカイブに移動」アクションでファイルが移動されるフォルダです。外部ディスクや NAS も指定できます。

**圧縮ファイル保存先** -- 圧縮された ZIP ファイルの保存先です。アーカイブ先とは別のディレクトリにすることをおすすめします。

**定期的にアーカイブを圧縮する**（デフォルト: オン） -- アーカイブディレクトリ内のファイルを定期的に ZIP 圧縮します。

**圧縮頻度** -- 毎時/毎日/毎週。デフォルト: 毎週。

**ファイル名テンプレート** -- 圧縮ファイルの命名テンプレートです。`{date}` トークンが ISO 日付に展開されます。デフォルト: `{date}_archive`（例: `2026-03-14_archive.zip`）。

**圧縮後に元ファイルを削除する**（デフォルト: オン） -- オフにすると、圧縮前のファイルもそのまま残ります。

**圧縮ファイルの保持期間** -- この日数を超えた ZIP ファイルが自動削除されます。デフォルト: 90日。

---

## English

### General Settings

**Launch at Login** -- Start TidyBox when your Mac starts up. Recommended for always-on monitoring. Default: Off.

**Show Dock Icon** -- Display TidyBox in the Dock. Leave off for menu bar-only operation. Default: Off.

**Display Language** -- Switch between System, Japanese, and English. Requires an app restart.

**Dry Run Mode** -- Evaluates rules but skips all file operations. Results are logged only. Use this when testing new rules. Default: Off.

**Require Approval** -- Shows a confirmation dialog before each rule execution. For folders with sensitive files where you want to confirm every operation. Default: Off.

**Max Files Per Batch** -- Limits files processed in a single batch (10-1000). Controls system load when many files are detected at once. Default: 100.

**History Retention** -- Days to keep operation history (1/7/14/21/28 days). Expired history is auto-deleted and can no longer be undone. Default: 28 days.

---

### Watched Directories

See [Watched Directories](watched-directories.md) for details on adding and managing folders.

---

### Notifications

Choose from four notification modes:

- **Immediate** -- Notifies on every file operation. Provides real-time awareness but can be noisy in high-volume environments
- **Batch Summary** (default) -- Notifies when a batch completes
- **Daily Summary** -- One notification per day at a configured time
- **Off** -- Disables notifications

The summary time setting appears only when Daily Summary mode is selected.

---

### Exclusions

Controls which files TidyBox ignores during rule evaluation, protecting system files and temporary files from accidental moves.

**Exclude Hidden Files** (default: On) -- Ignores files starting with `.` (such as `.gitignore` and `.DS_Store`). Keep this on since hidden files often contain system and app configuration.

**Exclude System Files** (default: On) -- Ignores macOS system files. Keep this on.

**Exclusion Patterns (glob)** -- Ignores files matching glob patterns. Defaults include `*.tmp`, `*.download`, `*.part`, `*.crdownload`, and `.DS_Store`, which prevent moving files that are still being downloaded. Add patterns in the text field and click "Add"; remove them with the red "-" button.

---

### Schedule

Real-time monitoring only detects newly added files. To evaluate existing files periodically, enable scheduled execution. This is essential for aging rules that target files older than a certain number of days.

**Enable Schedule** -- Default: Off.

**Interval** -- Hourly, Daily, or Weekly. Daily is recommended for most users.

**Execution Time** -- Available for Daily and Weekly intervals. Set it to a low-activity time.

---

### Trash Management

Requires Full Disk Access permission. See [Trash Management](trash.md) for full details.

**Current Trash** -- Shows file count and total size. "Cleanup..." opens a preview before deletion; "Refresh" updates the status.

**Exclusion Rules** -- Conditions for files that should never be deleted during cleanup (extension, name, regex, size, kind).

**Priority Rules** -- Files matching these conditions are deleted sooner with a custom retention period.

**Retention Period** -- Files in Trash older than this become cleanup candidates. Default: 30 days.

**Size Limit** -- When total Trash exceeds this value in GB, oldest files are targeted. 0 means unlimited. Default: 0.

**Auto-Cleanup** -- Runs cleanup during scheduled execution without confirmation. Use with caution. Default: Off.

---

### Archive

See [Archive](archive.md) for full details.

**Enable Archive** -- Required for the "Archive File" rule action. Default: Off.

**Archive Directory** -- Where archived files are moved. Can be set to an external disk or NAS.

**Compressed Directory** -- Where ZIP archives are saved. Use a separate directory from the archive.

**Periodic Compression** (default: On) -- Compresses archive files on schedule.

**Compression Frequency** -- Hourly, Daily, or Weekly. Default: Weekly.

**Filename Template** -- Template for ZIP names using the `{date}` token (ISO date). Default: `{date}_archive` (produces `2026-03-14_archive.zip`).

**Delete After Compression** (default: On) -- Removes originals after zipping. Disable to keep both copies.

**Compressed Retention** -- ZIP files older than this are auto-deleted. Default: 90 days.
