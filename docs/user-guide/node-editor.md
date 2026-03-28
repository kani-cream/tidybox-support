# ノードエディタ / Node Editor

## 日本語

ノードエディタは、TidyBox のルールを作成するためのビジュアルエディタです。四角いノード（箱）をワイヤー（線）でつなぐことで、ファイルの検知条件、判定ロジック、実行アクションを組み立てます。

### ノードエディタを開く

メインウィンドウの「ルール」タブで「新規ルール」をクリックすると、ノードエディタウィンドウが開きます。既存のルールを編集するには、ルール一覧から選択して編集ボタンをクリックしてください。

### 基本概念

ノードの左右にあるピン（丸い接続点）同士をワイヤーで結んで、データの流れを作ります。左が入力、右が出力です。信号には3種類あります:

- **ファイル信号**（青） -- ファイル情報を運ぶ
- **ブール信号**（緑） -- 真/偽の判定結果を運ぶ
- **アクション信号**（紫） -- アクションの実行完了を伝える

同じ種類の信号同士のみ接続できます。

---

## ノードの種類

### トリガー: ファイル検知

すべてのルールの起点です。監視フォルダ内のファイル追加・変更を検知し、ファイル情報を後続のノードに渡します。新規ルール作成時に自動配置されます。設定項目はありません。

---

### 条件ノード

ファイルの属性を検査し、条件に一致するかどうかを真/偽で出力します。入力はファイル信号、出力は真（一致時）と偽（不一致時）の2つです。

#### ファイル属性による条件

**拡張子** -- `.pdf`、`.jpg` などの拡張子で判定します。演算子は一致、不一致、含むです。「含む」を使えば `jp` で jpg と jpeg の両方に一致させることもできます。

**ファイル名** -- ファイル名のパターンで判定します。スクリーンショットや請求書など、命名規則があるファイルの検出に向いています。演算子は一致、不一致、含む、含まない、前方一致、後方一致です。

**ファイル名（正規表現）** -- 正規表現パターンによる高度なマッチングです。`report (1).pdf` のような番号付きコピーの検出などに使えます。TidyBox は ReDoS を防ぐため 0.5 秒のタイムアウトを設定しているので、複雑すぎるパターンは避けてください。

**ファイルサイズ** -- バイト単位で指定します。演算子はより大きい、より小さい、以上、以下です。

サイズの目安:

| サイズ | バイト値 |
|--------|---------|
| 1 KB | 1024 |
| 1 MB | 1048576 |
| 10 MB | 10485760 |
| 100 MB | 104857600 |
| 1 GB | 1073741824 |

**ファイル種別（UTI）** -- macOS の Uniform Type Identifier に基づいて判定します。拡張子に依存しないため、より正確な分類が可能です。よく使う値: `public.image`（画像）、`public.movie`（動画）、`public.audio`（音声）、`public.plain-text`（テキスト）、`com.adobe.pdf`（PDF）。

#### 日付による条件

**作成日、更新日、最終アクセス日** -- ファイルの日付で判定します。演算子はいずれも共通で、指定日時より前/後、直近N日以内、N日以上前です。古いファイルのアーカイブや未使用ファイルの検出に使います。

#### メタデータによる条件

**作成アプリ** -- Spotlight メタデータから、ファイルを作成したアプリ名で判定します。演算子は一致、含むです。

**著者** -- Spotlight メタデータから、ファイルの著者情報で判定します。演算子は作成アプリと同じです。

**Finder タグ** -- ファイルに付いている Finder タグで判定します。手動でタグ付けしたファイルを自動整理するのに便利です。演算子は一致、不一致、含む、含まないです。

**親ディレクトリ** -- ファイルが存在するフォルダの名前で判定します。演算子は一致、含むです。

---

### ロジックノード

**AND** -- 2つの入力が両方とも真の場合のみ真を出力します。例: 拡張子が `pdf` かつサイズが 100MB 超。

**OR** -- 2つの入力のどちらか一方でも真なら真を出力します。例: 拡張子が `jpg` または `png`。

**IF-ELSE（分岐）** -- 条件の真偽に応じて、異なる経路にデータを流します。例: 画像ファイルなら Pictures に移動、それ以外は Documents に移動。

**NOT（反転）** -- 入力の真偽を反転させます。「条件に一致しないファイル」を対象にする場合に使います。

---

### アクションノード

すべてのアクションノードには「実行」入力ピン（ブール信号）と「完了」出力ピン（アクション信号）があります。「完了」を次のアクションの「実行」に接続すれば、複数のアクションを順番に実行できます。

#### ファイルの移動と整理

**フォルダへ移動** -- ファイルを指定フォルダに移動します。パスにはトークンを使えます:

| トークン | 展開結果 | 例 |
|----------|---------|-----|
| `{extension}` | ファイル拡張子 | pdf, jpg |
| `{year}` | ファイル作成年 | 2026 |
| `{month}` | ファイル作成月 | 03 |
| `{day}` | ファイル作成日 | 14 |
| `{filename}` | 拡張子を除くファイル名 | document |
| `{date}` | ISO日付 | 2026-03-14 |

移動先に同名ファイルがある場合の衝突解決ストラテジーも設定できます: 連番サフィックス付与（デフォルト）、タイムスタンプ付与、スキップ、新しい方を優先、大きい方を優先、上書き。

**リネーム** -- テンプレートに従ってファイル名を変更します。上記と同じトークンが使えます。例: テンプレート `{date}_{filename}.{extension}` は `2026-03-14_report.pdf` になります。

**サブフォルダ作成** -- 指定した形式でサブフォルダを作成し、ファイルをその中に移動します。形式: 年/月（`yyyy/MM`）、年/月/日（`yyyy/MM/dd`）、年（`yyyy`）、拡張子、種別。

#### タグ操作

**Finder タグ追加** -- ファイルに Finder タグを追加します（既存のタグは保持されます）。タグ名と色を設定できます。利用可能な色: なし、グレー、グリーン、パープル、ブルー、イエロー、レッド、オレンジ。

**Finder タグ削除** -- ファイルから指定したタグを削除します。

**Finder タグ置換** -- ファイルの全タグを削除し、新しいタグで置き換えます。タグの追加ではなく完全な置換です。

#### ファイルの削除とアーカイブ

**ゴミ箱へ移動** -- ファイルを macOS のゴミ箱に移動します。Finder から復元可能です。

**ゴミ箱から削除** -- ゴミ箱内のファイルを完全に削除します。**この操作は元に戻せません。**

**アーカイブに移動** -- 設定で指定されたアーカイブディレクトリにファイルを移動します。アーカイブ先は設定 > アーカイブで一括指定するため、ノード自体に追加設定はありません。この機能を使うには、事前に設定でアーカイブを有効にし、ディレクトリを指定する必要があります。

#### 画像処理

**画像リサイズ** -- 画像の幅を指定ピクセルにリサイズします。元ファイルを保持するかどうかを選択できます。

---

### ユーティリティノード

**コメント** -- テキストメモを表示します。ルールの意図や注意事項を記録するためのもので、動作には影響しません。

**リルート** -- ワイヤーの経路を変更する中継点です。ワイヤーが交差して見づらいときに使います。

**コメントフレーム** -- 複数のノードを視覚的にグループ化する枠です。「条件部分」「アクション部分」などのまとまりを明示できます。

**テレポート送信/受信** -- 同じラベルを持つ送信ノードと受信ノードの間で、ワイヤーを引かずに信号を伝達します。離れたノード同士を接続したいが、ワイヤーでグラフが見づらくなるのを避けたいときに使います。

**サブグラフ** -- 別のノードグラフを1つのノードとして埋め込みます。よく使う条件やアクションの組み合わせを再利用可能な部品にするのに便利です。

---

## エディタ操作

| 操作 | 方法 |
|------|------|
| ノードの追加 | パレットからドラッグ、または空白部分をダブルクリック |
| ワイヤーの接続 | 出力ピンから入力ピンへドラッグ |
| 削除 | 選択して Delete キー |
| 元に戻す / やり直す | Command + Z / Command + Shift + Z |
| ズーム | Command + スクロール |
| コピー＆ペースト | Command + C / Command + V |
| オートレイアウト | ツールバーボタン |

ノードを追加すると、接続可能なピンがあれば自動的にワイヤーが接続されます（オートワイヤー）。

簡易モードではノードの詳細設定が折りたたまれ、全体の流れを把握しやすくなります。フルモードに切り替えると、すべての設定項目を展開して編集できます。

### ドライラン

ツールバーの「ドライラン」ボタンをクリックすると、実際にファイルを移動せずに、ルールがどのファイルにどのアクションを実行するかをシミュレーションできます。結果パネルで問題がないことを確認してからルールを保存してください。

---

## 実践例

### 例 1: ダウンロードフォルダの画像を年月別に整理する

Downloads フォルダに追加された jpg/png/gif ファイルを `~/Pictures` の年月別サブフォルダに移動します。

1. 新規ルールを作成（ファイル検知ノードが自動配置される）
2. 条件ノードを3つ追加: 拡張子が `jpg`、`png`、`gif`
3. ファイル検知の出力を3つの条件の入力に接続
4. OR ノードを2つ使って3つの条件を結合
5. サブフォルダ作成アクション（形式: yyyy/MM）を追加し、OR の結果を接続
6. ドライランで確認して保存

### 例 2: 古いファイルにタグを付け、さらに古いものはアーカイブする

30日経過したファイルに「要整理」タグを付け、90日経過したファイルはアーカイブに移動します。

1. 条件ノードを2つ追加: 更新日が 30 日以上前、更新日が 90 日以上前
2. IF-ELSE ノードで 90 日の条件を分岐
3. 真（90日以上）をアーカイブに移動アクションに接続
4. 偽（90日未満）を 30 日の条件と AND で結合し、Finder タグ追加アクション（タグ名: `要整理`、色: イエロー）に接続

### 例 3: スクリーンショットをリネームして整理する

デスクトップの「スクリーンショット」で始まるファイルをリネームし、`~/Pictures/Screenshots` に年月別で移動します。

1. 条件ノード: ファイル名が「スクリーンショット」で前方一致 AND ファイル種別が `public.image`
2. リネームアクション（テンプレート: `screenshot_{date}_{filename}.{extension}`）
3. リネームの完了出力からフォルダへ移動アクション（移動先: `~/Pictures/Screenshots/{year}/{month}`）

### 例 4: 請求書を月別に整理してタグを付ける

ファイル名に「請求」を含むファイルを月別サブフォルダに移動し、ブルーの「請求書」タグを付けます。

1. 条件ノード: ファイル名に「請求」を含む
2. サブフォルダ作成アクション（形式: yyyy/MM）
3. 完了出力から Finder タグ追加アクション（タグ名: `請求書`、色: ブルー）

---

## English

The node editor is TidyBox's visual rule builder. You connect rectangular nodes with wires to define how files are detected, evaluated, and acted upon.

### Opening the node editor

In the Rules tab, click "New Rule" to open a new node editor window. To edit an existing rule, select it from the list and click the edit button.

### Basic concepts

Nodes have pins (circular connection points) on their left (input) and right (output) sides. Drag a wire from an output pin to an input pin to connect them. There are three signal types:

- **File signal** (blue) -- carries file information
- **Bool signal** (green) -- carries true/false results
- **Action signal** (purple) -- carries execution completion

Only pins of the same signal type can be connected.

---

## Node Types

### Trigger: File Detection

The starting point of every rule. It detects when files are added or changed in watched folders and passes file information downstream. Automatically placed when creating a new rule.

---

### Condition Nodes

Condition nodes inspect file attributes and output true (match) or false (no match). Input is a file signal; output is a boolean signal on two pins.

#### File attribute conditions

**File Extension** -- Match by extension (`.pdf`, `.jpg`, etc.). Operators: equals, not equals, contains.

**File Name** -- Match by filename patterns. Useful for files with naming conventions like screenshots or invoices. Operators: equals, not equals, contains, not contains, starts with, ends with.

**File Name (Regex)** -- Advanced pattern matching with regular expressions. TidyBox enforces a 0.5-second timeout to prevent ReDoS.

**File Size** -- Match by size in bytes. Operators: greater than, less than, greater or equal, less or equal.

**File Kind (UTI)** -- Match by macOS Uniform Type Identifier, which is more reliable than extension matching. Common values: `public.image`, `public.movie`, `public.audio`, `public.plain-text`, `com.adobe.pdf`.

#### Date conditions

**Created Date, Modified Date, Accessed Date** -- Match by file timestamps. Operators (shared across all three): before, after, within last N days, older than N days. Useful for archiving old files or detecting unused ones.

#### Metadata conditions

**Creator App** -- Match by the application that created the file (via Spotlight metadata). Operators: equals, contains.

**Author** -- Match by author metadata (via Spotlight). Same operators as Creator App.

**Finder Tag** -- Match by existing Finder tags. Operators: equals, not equals, contains, not contains.

**Parent Directory** -- Match by parent folder name. Operators: equals, contains.

---

### Logic Nodes

**AND** -- Outputs true only when both inputs are true.

**OR** -- Outputs true when either input is true.

**IF-THEN-ELSE** -- Routes data along one path when true, another when false.

**NOT** -- Inverts the boolean value.

---

### Action Nodes

All action nodes have an "Execute" input pin and a "Done" output pin. Chain actions by connecting Done to Execute.

#### Moving and organizing files

**Move to Folder** -- Moves files to a specified folder. Supports path tokens:

| Token | Expands To | Example |
|-------|-----------|---------|
| `{extension}` | File extension | pdf, jpg |
| `{year}` | Creation year | 2026 |
| `{month}` | Creation month | 03 |
| `{day}` | Creation day | 14 |
| `{filename}` | Name without extension | document |
| `{date}` | ISO date | 2026-03-14 |

Conflict resolution strategies when a file with the same name exists: append number (default), append timestamp, skip, keep newer, keep larger, overwrite.

**Rename** -- Renames files using a template with the same tokens above. Example: `{date}_{filename}.{extension}` produces `2026-03-14_report.pdf`.

**Create Subfolder** -- Creates a subfolder in a given format and moves the file into it. Formats: yyyy/MM, yyyy/MM/dd, yyyy, extension, kind.

#### Tag operations

**Add Finder Tag** -- Adds a tag without removing existing ones. Available colors: None, Gray, Green, Purple, Blue, Yellow, Red, Orange.

**Remove Finder Tag** -- Removes a specific tag from the file.

**Replace Finder Tags** -- Removes all existing tags and sets new ones.

#### Deletion and archiving

**Move to Trash** -- Moves the file to macOS Trash. Recoverable via Finder.

**Delete from Trash** -- Permanently deletes a file from Trash. **This cannot be undone.**

**Archive File** -- Moves the file to the configured archive directory. Requires the archive feature to be enabled in Settings > Archive.

#### Image processing

**Image Resize** -- Resizes image width to specified pixels. Option to keep the original file.

---

### Utility Nodes

**Comment** -- A text annotation with no functional effect.

**Reroute** -- A wire routing helper to keep the graph tidy.

**Comment Frame** -- A visual frame for grouping related nodes.

**Teleport Send/Receive** -- Connects distant nodes without visible wires. Paired by matching labels.

**Subgraph** -- Embeds another node graph as a reusable component.

---

## Editor Operations

| Operation | Method |
|-----------|--------|
| Add node | Drag from palette, or double-click empty area |
| Connect | Drag from output pin to input pin |
| Delete | Select + Delete key |
| Undo / Redo | Command + Z / Command + Shift + Z |
| Zoom | Command + Scroll |
| Copy / Paste | Command + C / Command + V |
| Auto-layout | Toolbar button |

Auto-wire connects compatible pins automatically when you add a node. Toggle between compact mode (collapsed settings) and full mode (expanded settings) to suit your workflow.

### Dry Run

Click the Dry Run button in the toolbar to simulate your rule without moving any files. The results panel shows which files would be affected and what actions would be taken. Verify the results before saving the rule.

---

## Practical Examples

### Example 1: Organize images from Downloads by month

Move jpg/png/gif files from Downloads to `~/Pictures` in monthly subfolders.

1. Start with the File Detection node (auto-placed)
2. Add 3 Condition nodes for each extension
3. Combine with OR nodes
4. Connect to a Create Subfolder action (yyyy/MM format)

### Example 2: Tag old files, archive very old ones

Tag files older than 30 days, archive files older than 90 days.

1. Add two Condition nodes (30 days, 90 days modified date)
2. Use IF-ELSE to branch on the 90-day condition
3. True path goes to Archive File; false path combines with the 30-day condition via AND, then goes to Add Finder Tag

### Example 3: Rename and organize screenshots

Rename screenshots to `screenshot_{date}_{filename}.{extension}` and move to `~/Pictures/Screenshots/{year}/{month}`.

1. Conditions: filename starts with "Screenshot" AND kind is `public.image`
2. Chain: Rename action, then Move to Folder action

### Example 4: Organize invoices by month with tags

Move files containing "invoice" in the name to monthly subfolders and add a blue "Invoice" tag.

1. Condition: filename contains "invoice"
2. Chain: Create Subfolder (yyyy/MM), then Add Finder Tag
