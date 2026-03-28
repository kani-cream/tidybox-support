# 監視ディレクトリ / Watched Directories

## 日本語

TidyBox は、ここで登録されたフォルダだけを監視します。フォルダを登録しなければ、一切の自動整理は行われません。

### フォルダを追加する

1. 設定 > 「監視ディレクトリ」タブを開きます
2. 「追加」ボタンをクリックします
3. フォルダ選択ダイアログでフォルダを選択します

TidyBox がフォルダへのアクセス権を取得し、一覧に追加します。

### 監視の仕組み

TidyBox は macOS の FSEvents（ファイルシステムイベント）を使ってフォルダを監視しています。ファイルが追加されたり変更されたりすると即座に検知され、登録済みのルールが順番に評価されます。ポーリング（定期チェック）ではないため、CPU 負荷はほぼゼロです。

### 監視の一時停止

各フォルダの有効/無効トグルで、監視を一時的にオフにできます。フォルダ内で手動整理をしているときや、特定のフォルダだけテストしたいときに便利です。無効にしてもフォルダの設定やルールは保持されます。

### サブディレクトリ監視

サブディレクトリ監視を有効にすると、登録フォルダ直下だけでなく、すべてのサブフォルダ内の変更も検知します。

> **サブディレクトリ監視は慎重に使ってください。** アプリの設定ファイル（`.config/` 内のファイルなど）がルールに一致して移動される、深いフォルダ構造で大量のイベントが発生する、移動先がサブフォルダ内にある場合に無限ループが発生する、といった問題が起こり得ます。

### アクセス権の永続化

TidyBox は Security-Scoped Bookmarks を使ってフォルダのアクセス権を保存しています。Mac を再起動してもアクセスを再許可する必要はありません。ただし、フォルダを移動したり名前を変更するとブックマークが無効になることがあるため、その場合はフォルダを再登録してください。

### フォルダを削除する

フォルダ一覧で削除したいフォルダを選択し、削除ボタンをクリックします。フォルダを削除すると、そのフォルダに紐づくルールの関連付けが解除されます（ルール自体は削除されません）。

### おすすめのフォルダ

`~/Downloads`、`~/Desktop`、`~/Documents` や専用の作業フォルダが整理に適しています。

以下のフォルダは監視しないでください。システムやアプリの動作に影響する可能性があります:

- `~/Library`、`/System`、`/Applications`
- `~/.config`、`~/.ssh` など設定ファイルのあるフォルダ
- `.git/`、`node_modules/`、`.build/` などの開発用フォルダ

初めは `~/Downloads` だけ登録して、ルールの動作を確認してから他のフォルダを追加するのがおすすめです。

---

## English

TidyBox only monitors folders you register here. Without any registered folders, no files are organized.

### Add a folder

Open Settings > Watched Directories, click "Add," and select a folder. TidyBox obtains access permission and adds it to the list.

### How monitoring works

TidyBox uses macOS FSEvents to watch folders. When files are added or changed, they are detected instantly and evaluated against your rules in order. Because this is event-driven rather than polling, CPU usage is nearly zero.

### Pause monitoring

Use the toggle on each folder to temporarily disable monitoring -- useful when you are manually reorganizing files or testing with specific folders. Disabling a folder preserves its settings and rules.

### Subdirectory monitoring

When enabled, TidyBox detects changes in all subfolders, not just the top level of the registered folder.

> **Use subdirectory monitoring carefully.** It can cause issues such as moving application config files that match your rules, generating massive events in deep folder trees, or creating infinite loops when a destination folder is inside the watched folder.

### Persistent access

TidyBox uses Security-Scoped Bookmarks to remember folder access across restarts. If you move or rename a watched folder, the bookmark may become invalid -- simply remove and re-add the folder.

### Remove a folder

Select the folder in the list and click the delete button. Removing a folder disassociates its rules, but the rules themselves are preserved.

### Recommended folders

`~/Downloads`, `~/Desktop`, `~/Documents`, and dedicated project folders work well. Avoid monitoring system-critical locations:

- `~/Library`, `/System`, `/Applications`
- `~/.config`, `~/.ssh`, and other configuration directories
- `.git/`, `node_modules/`, `.build/`, and other development directories

Start with one folder like `~/Downloads`, verify your rules work correctly, then add more.
