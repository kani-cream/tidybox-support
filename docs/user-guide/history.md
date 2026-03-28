# 履歴 / History

## 日本語

TidyBox が実行したすべてのファイル操作（移動、リネーム、タグ付け、削除など）が時系列で記録されます。意図しない移動が起きた場合に「いつ、何が、どこに移動されたか」を確認し、操作を取り消すことができます。

### 記録される操作

| 操作 | Undo |
|------|------|
| フォルダへ移動 | 可 |
| リネーム | 可 |
| Finder タグ追加/削除/置換 | 可 |
| サブフォルダ作成 | 可 |
| ゴミ箱へ移動 | 可 |
| アーカイブに移動 | 可 |
| ゴミ箱から削除 | **不可** |
| 画像リサイズ | 元ファイル保持時のみ |

### 履歴を確認する

操作は日付ごとにグループ化されて表示されます（今日、昨日、今週、それ以前は日付ごと）。各行にはアクションアイコン、概要、トリガー元（リアルタイム/スケジュール/手動）、適用されたルール名、タイムスタンプが表示されます。取り消し済みの操作にはバッジが付きます。

### 検索とフィルタリング

画面上部のフィルターバーで、トリガー元による絞り込み（すべて/リアルタイム/スケジュール/手動）ができます。検索バーではファイル名、パス、ルール名でキーワード検索できます。

### 操作を元に戻す

取り消したい操作の行で「元に戻す」ボタンをクリックするか、右クリックメニューから「元に戻す」を選択します。ファイルが元の場所に復元され、操作行に「元に戻し済み」バッジと取り消し日時が表示されます。

元に戻せない場合もあります:

- ファイルが既に移動先から削除されている場合、Undo は失敗します
- 元の場所に同名ファイルがある場合、衝突解決ストラテジーに従います
- 「ゴミ箱から削除」操作は元に戻せません
- 履歴保持期間を超えた操作は、履歴自体が削除されているため Undo できません

Undo は「ファイルを元の場所に戻す」操作であり、Undo 自体も履歴に記録されます。

### 詳細ビュー

操作行をダブルクリックするか、右クリック > 「詳細を表示」で、実行日時、トリガー、ルール名、元のパス、移動先パス、リネーム前後のファイル名、Undo 状態を確認できます。

### 保持期間

履歴は設定で指定した保持期間（デフォルト: 28日）を過ぎると自動削除されます。設定 > 一般 > 「履歴保持期間」で 1日/7日/14日/21日/28日 から選択できます。履歴が削除されると Undo もできなくなるため、Undo の可能性を残したい場合は長めに設定してください。

### 履歴のクリア

ツールバーのゴミ箱ボタンで、すべての履歴を一括削除できます。この操作は元に戻せず、すべての Undo も失われます。

---

## English

TidyBox records every file operation it performs -- moves, renames, tag changes, deletions, and more -- in chronological order. You can review what happened and undo operations when needed.

### What gets recorded

| Operation | Undo |
|-----------|------|
| Move to Folder | Yes |
| Rename | Yes |
| Add/Remove/Replace Finder Tags | Yes |
| Create Subfolder | Yes |
| Move to Trash | Yes |
| Archive File | Yes |
| Delete from Trash | **No** |
| Image Resize | Only if original kept |

### Viewing history

Operations are grouped by date: Today, Yesterday, This Week, and specific dates for older entries. Each row shows an action icon, summary, trigger source (real-time, scheduled, or manual), rule name, and timestamp. Undone operations are marked with a badge.

### Searching and filtering

Use the filter bar to narrow by trigger type: All, Real-time, Scheduled, or Manual. The search bar accepts keywords from file paths and rule names.

### Undoing an operation

Click the undo button on an operation row, or right-click and select "Undo." The file is restored to its original location, and the row shows an "Undone" badge with a timestamp.

Undo is not always possible:

- If the file no longer exists at the destination, undo fails
- If a file with the same name exists at the original location, conflict resolution applies
- "Delete from Trash" cannot be undone
- Operations beyond the retention period cannot be undone because the history has been deleted

Undo itself is also recorded in the history.

### Detail view

Double-click an operation row, or right-click and select "Show Details," to see the full record: execution time, trigger, rule name, source path, destination path, original and new filenames (for renames), and undo status.

### Retention period

History is automatically deleted after the configured retention period (default: 28 days). Choose from 1, 7, 14, 21, or 28 days under Settings > General > History Retention. Once history is deleted, undo is no longer available, so use a longer period if you want to keep the option open.

### Clearing history

Click the trash button in the toolbar to delete all history. This cannot be undone, and all undo capability is lost.
