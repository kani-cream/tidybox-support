# アーカイブ / Archive

## 日本語

アーカイブ機能は、すぐに削除したくないけれどメインの作業フォルダには残しておきたくないファイルを段階的に管理するための仕組みです。ファイルをアーカイブディレクトリに退避し、定期的に ZIP 圧縮し、保持期間を過ぎた圧縮ファイルを自動削除する -- という3段階のライフサイクルでストレージを効率的に活用できます。

### 仕組み

アーカイブには2つのディレクトリが関わります。**アーカイブディレクトリ**には、ルールの「アーカイブに移動」アクションで退避されたファイルが格納されます。**圧縮ファイル保存先**には、アーカイブディレクトリの中身を ZIP にまとめた圧縮ファイルが保存されます。

```
ファイル検知 → ルール評価 → 「アーカイブに移動」アクション
       ↓
アーカイブディレクトリに移動（待機中）
       ↓
定期圧縮 or 手動圧縮 → ZIP 化して圧縮ファイル保存先へ
       ↓
保持期間経過 → 圧縮ファイルを自動削除
```

### アーカイブ機能を有効にする

設定 > アーカイブで、アーカイブ機能をオンにしてください（デフォルトはオフ）。この設定がオフの場合、ルールに「アーカイブに移動」アクションを設定しても動作しません。

同じ画面で、アーカイブ先ディレクトリと圧縮ファイル保存先ディレクトリを設定します。混在を避けるため、この2つは別のディレクトリにすることをおすすめします。

### ファイルをアーカイブする

ノードエディタでルールを作成し、条件ノードでアーカイブ対象を指定して（例: 更新日が90日以上前）、「アーカイブに移動」アクションノードを接続します。アーカイブ先はノードではなく設定で一括指定するため、アクションノード自体に追加設定はありません。

### アーカイブブラウザ

メインウィンドウの「アーカイブ」タブで、アーカイブの状態を確認できます。

**待機中ファイルタブ**には、アーカイブディレクトリ内の圧縮前のファイルがファイル数、合計サイズとともに一覧表示されます。「今すぐ圧縮」ボタンで、スケジュールを待たずに即座に圧縮できます。

**圧縮済みタブ**には、圧縮ファイル保存先の ZIP ファイルが一覧表示されます。各ファイルの「ゴミ箱に移動」ボタンで個別に削除できます。

### 圧縮設定

定期圧縮はデフォルトで有効です。圧縮頻度は毎時/毎日/毎週（デフォルト: 毎週）から選べます。

圧縮ファイルの名前はテンプレートで指定します。`{date}` トークンが圧縮実行時の日付（yyyy-MM-dd 形式）に展開されます（デフォルト: `{date}_archive` で `2026-03-14_archive.zip` になります）。同名ファイルが既にある場合は `_1`、`_2` のように連番が付きます。

この `{date}` トークンは圧縮実行時の現在日付です。ルールの移動先パスで使う `{year}`、`{month}`、`{day}`（ファイルの作成日に基づく）とは異なるので注意してください。

「圧縮後に元ファイルを削除する」（デフォルト: オン）をオフにすると、圧縮前のファイルもアーカイブディレクトリに残ります。

### 保持期間と自動削除

圧縮ファイルの保持期間（デフォルト: 90日）を超えると、ZIP ファイルが自動削除されます。判定は ZIP ファイルの作成日に基づきます。

自動削除の対象は圧縮ファイル保存先の ZIP ファイルのみです。アーカイブディレクトリ内の未圧縮ファイルは、「圧縮後に元ファイルを削除する」設定で制御されます。

### パストークン

ルールの「フォルダへ移動」アクションの移動先パスでは、ファイルメタデータに基づくトークンが使えます:

| トークン | 展開結果 | 例 |
|----------|---------|-----|
| `{extension}` | ファイル拡張子 | pdf, jpg |
| `{year}` | ファイル作成年 | 2026 |
| `{month}` | ファイル作成月 | 03 |
| `{day}` | ファイル作成日 | 14 |
| `{filename}` | 拡張子を除くファイル名 | document |
| `{date}` | ISO日付 | 2026-03-14 |

### 使い方のコツ

アーカイブルールを適用する前に、ドライランモードで対象ファイルを確認してください。保持期間は最初は 90 日以上にして、必要に応じて短くすると安全です。外部ディスクや NAS をアーカイブ先に指定すれば、メインストレージの空き容量を確保できます。

---

## English

The archive feature provides gradual lifecycle management for files you are not ready to delete but want out of your main working folders. Files move to an archive directory, get periodically compressed into ZIP files, and are automatically deleted after a retention period.

### How it works

Two directories are involved. The **archive directory** holds files moved by the "Archive File" rule action. The **compressed directory** stores ZIP files created from the archive directory's contents.

```
File detected -> Rule evaluation -> "Archive File" action
       |
Move to archive directory (pending)
       |
Periodic or manual compression -> ZIP to compressed directory
       |
Retention period elapsed -> Auto-delete compressed file
```

### Enable the archive feature

Go to Settings > Archive and turn on the archive feature (off by default). When it is off, the "Archive File" action in rules has no effect.

On the same screen, set the archive directory and compressed file directory. Use separate directories for these to avoid mixing raw and compressed files.

### Archiving files

Create a rule in the node editor with conditions for the files you want to archive (for example, modified date older than 90 days) and connect an "Archive File" action node. The action node has no additional settings -- the archive destination is configured globally in Settings > Archive.

### Archive Browser

The "Archive" tab in the main window shows the current state of your archives.

The **Pending Files** tab lists uncompressed files in the archive directory with file count and total size. Click "Compress Now" to compress them immediately without waiting for the schedule.

The **Compressed Files** tab lists ZIP files in the compressed directory. Each file has a "Move to Trash" button for individual removal.

### Compression settings

Periodic compression is enabled by default. Choose a frequency of hourly, daily, or weekly (default: weekly).

The filename template uses a `{date}` token that expands to the compression date in yyyy-MM-dd format. The default template `{date}_archive` produces `2026-03-14_archive.zip`. If a file with the same name exists, a numeric suffix is appended automatically.

Note that this `{date}` token uses the current date at compression time, unlike the `{year}`, `{month}`, `{day}` tokens in rule destination paths, which are based on the file's creation date.

"Delete originals after compression" (on by default) removes the source files from the archive directory after they are zipped. Disable it to keep both copies.

### Retention and auto-deletion

Compressed files older than the retention period (default: 90 days) are automatically deleted based on their creation date.

Auto-deletion only targets ZIP files in the compressed directory. Uncompressed files in the archive directory are controlled separately by the "Delete after compression" setting.

### Path tokens

The following tokens can be used in "Move to Folder" action destination paths, expanding based on file metadata:

| Token | Expands To | Example |
|-------|-----------|---------|
| `{extension}` | File extension | pdf, jpg |
| `{year}` | Creation year | 2026 |
| `{month}` | Creation month | 03 |
| `{day}` | Creation day | 14 |
| `{filename}` | Name without extension | document |
| `{date}` | ISO date | 2026-03-14 |

### Tips

Test archive rules with dry run mode before going live. Start with a retention period of 90 days or longer and shorten it as you gain confidence. Consider using an external disk or NAS as the archive directory to free up space on your main storage.
