# ゴミ箱管理 / Trash Management

## 日本語

TidyBox では、macOS のゴミ箱を保持期間やサイズ上限、ルールに基づいて管理できます。手動でゴミ箱を空にする代わりに、除外するファイルや優先的に削除するファイルを細かく制御できます。

### 「ゴミ箱へ移動」と「ゴミ箱から削除」の違い

この区別は非常に重要です。

**ゴミ箱へ移動**は、ファイルを macOS のゴミ箱に移動します。Finder の「元に戻す」で復元できます。

**ゴミ箱から削除**は、ゴミ箱内のファイルを完全に削除します。**この操作は元に戻せません。** Time Machine バックアップがない限り、データは永久に失われます。ルールにこのアクションを設定する場合は、必ずドライランで対象ファイルを確認してください。条件が広すぎると、意図しないファイルまで完全削除されるおそれがあります。

安全にゴミ箱を管理するには、ルールの「ゴミ箱から削除」アクションよりも、後述のクリーンアップ機能を使うことをおすすめします。クリーンアップにはプレビュー画面があり、削除対象を事前に確認できます。

### フルディスクアクセスの許可

ゴミ箱管理機能を使うには、macOS の「フルディスクアクセス」許可が必要です。設定画面に警告が表示された場合は、「システム設定を開く」ボタンをクリックし、システム設定 > プライバシーとセキュリティ > フルディスクアクセスで TidyBox を有効にしてください。

### ゴミ箱のステータス

設定 > ゴミ箱管理の「現在のゴミ箱」セクションに、ゴミ箱内のファイル数と合計サイズが表示されます。「更新」ボタンで最新の情報に更新できます。同じステータスはメニューバーのビューでも確認できます。

### 手動クリーンアップ

「クリーンアップ...」ボタンをクリックすると、プレビュー画面が開きます。保持期間、サイズ上限、ルールに基づいて判定された削除対象のファイルが一覧表示されます。各ファイルの「削除される/除外される」の判定と適用ルール名を確認してから、クリーンアップを実行してください。

### クリーンアップ設定

**保持期間**（デフォルト: 30日） -- ゴミ箱に入ってからこの日数を超えたファイルがクリーンアップ対象になります。ファイルがゴミ箱に移動された日時に基づいて判定されます。

**サイズ上限**（デフォルト: 0 = 無制限） -- ゴミ箱の合計サイズがこの値（GB 単位）を超えると、古いファイルから順に削除対象になります。保持期間による削除の後に実行されます。

### 除外ルール

クリーンアップ時に削除したくないファイルを保護するためのルールです。ファイル拡張子、ファイル名、正規表現、ファイルサイズ、ファイル種別（UTI）による条件が設定でき、演算子（一致、不一致、含む、含まない、より大きい、より小さいなど）を指定できます。「ルールを追加」ボタンで新しい除外ルールを追加してください。

### 優先削除ルール

特定のファイルを通常の保持期間よりも短い日数で削除するためのルールです。条件の設定方法は除外ルールと同じで、追加で「保持日数」（デフォルト: 7日）を指定します。たとえば「拡張子が `tmp` のファイルは 3 日後に削除」のように設定できます。大容量ファイルや一時ファイルのストレージを早めに解放したい場合に便利です。

### 自動クリーンアップ

> **自動クリーンアップを有効にすると、スケジュール実行のたびに保持期間を超えたファイルが確認なしに完全削除されます。**

自動クリーンアップ（デフォルト: オフ）を有効にすると、スケジュール実行時に以下の順序でクリーンアップが行われます:

1. ゴミ箱内の全ファイルを収集
2. 除外ルールに一致するファイルをスキップ
3. 優先削除ルールに一致するファイルにカスタム保持日数を適用
4. 保持期間を超えたファイルを削除
5. サイズ上限を超えている場合、古い順に削除（除外ルール一致分はスキップ）
6. 削除結果を操作ログに記録

手動クリーンアップと違い、プレビュー画面はありません。有効にする前に、除外ルールを十分にテストしてください。

### 使い方のコツ

「ゴミ箱から削除」アクションや自動クリーンアップを使う前に、ドライランモードで対象ファイルを確認してください。保持期間は 30 日以上から始め、問題がないことを確認してから短くしてください。自動クリーンアップを有効にする前に、保護したいファイルの除外ルールを必ず設定してください。重要なファイルがゴミ箱に入る可能性がある場合は、Time Machine などのバックアップを有効にしておくことをおすすめします。自動クリーンアップを有効にした後は、履歴画面で削除されたファイルを定期的に確認してください。

---

## English

TidyBox can manage the macOS Trash based on retention periods, size limits, and rules. Instead of manually emptying the Trash, you can control which files are protected, which are deleted sooner, and when cleanup happens.

### Move to Trash vs. Delete from Trash

This distinction is critical.

**Move to Trash** sends files to the macOS Trash, where they can be restored via Finder's "Put Back."

**Delete from Trash** permanently destroys files. **This cannot be undone.** Without a Time Machine backup, the data is gone forever. If you use this action in rules, always verify targets with a dry run first. Overly broad conditions risk deleting files you did not intend to lose.

For safer trash management, use the cleanup feature described below instead of the "Delete from Trash" rule action. Cleanup includes a preview screen that shows exactly what will be deleted.

### Full Disk Access

Trash management requires macOS Full Disk Access permission. If a warning appears in settings, click "Open System Settings" and enable TidyBox under System Settings > Privacy & Security > Full Disk Access.

### Trash status

Settings > Trash Management shows the current file count and total size of the Trash. Click the refresh button for up-to-date information. The same status appears in the menu bar view.

### Manual cleanup

Click "Cleanup..." to open a preview screen. Files targeted for deletion based on retention, size limits, and rules are listed with their evaluation results and matched rule names. Review the list before executing.

### Cleanup settings

**Retention period** (default: 30 days) -- Files in Trash older than this become cleanup candidates, based on the date they were moved to Trash.

**Size limit** (default: 0 = unlimited) -- When total Trash size exceeds this value in GB, the oldest files are targeted for deletion. This runs after retention-based deletion.

### Exclusion rules

Protect specific files from cleanup. Set conditions using file extension, file name, regex, file size, or file kind (UTI) with operators like equals, not equals, contains, greater than, and less than. Click "Add Rule" to create a new exclusion rule.

### Priority deletion rules

Delete certain files sooner than the global retention period. Conditions work the same as exclusion rules, plus a "Retention Days" field (default: 7 days). For example, you can delete `.tmp` files after 3 days even when the global retention is 30 days.

### Auto-cleanup

> **When enabled, auto-cleanup permanently deletes files exceeding the retention period without confirmation during each scheduled execution.**

Auto-cleanup (off by default) processes in this order during scheduled execution:

1. Collect all files in Trash
2. Skip files matching exclusion rules
3. Apply custom retention days from priority rules
4. Delete files exceeding their retention period
5. If size limit is still exceeded, delete oldest files first (skipping exclusion matches)
6. Log all deletions to operation history

Unlike manual cleanup, there is no preview. Test your exclusion rules thoroughly before enabling auto-cleanup.

### Tips

Test with dry run mode before using "Delete from Trash" actions or auto-cleanup. Start with a retention period of 30 days or longer and shorten it only after confirming things work correctly. Set up exclusion rules before enabling auto-cleanup. Enable Time Machine or another backup if important files might end up in Trash. After enabling auto-cleanup, check the History view regularly to review what was deleted.
