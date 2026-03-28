# プリセット / Presets

## 日本語

プリセットは、よくあるファイル整理パターンをテンプレートとしてまとめたルールです。ゼロからルールを作る代わりに、プリセットを選んで必要な部分だけカスタマイズすれば、すぐに使い始められます。

### プリセットを使う

1. 「ルール」タブで「新規ルール」>「プリセットから選択」をクリックします
2. プリセット一覧からテンプレートを選択します
3. ノードエディタにテンプレートが展開されます
4. 移動先パスやタグ名を自分の環境に合わせて調整し、保存します

検索バーにキーワード（日本語・英語どちらも可）を入力すると、プリセット名と説明文から該当するものを絞り込めます。

---

### 一般（General）

**ダウンロード整理** -- ダウンロードフォルダのファイルを種類別に整理します。画像は種別サブフォルダ、PDF は年月サブフォルダ、圧縮ファイルは Archives、インストーラーは Installers、動画は Videos に移動し、30日経過したファイルには「要整理」タグを付けます。

**デスクトップ整理** -- デスクトップの散らかりを防ぎます。スクリーンショットは Pictures/Screenshots、ドキュメントは Documents に移動し、100MB 超のファイルには「大容量」タグ、14日経過したファイルには「要整理」タグを付けます。

**古いファイルアーカイブ** -- 90日経過でアーカイブ、180日で「長期未使用」タグ、365日でゴミ箱に移動します。

**重複・一時ファイル管理** -- tmp/temp/bak ファイルをゴミ箱に移動し、コピー重複ファイルには「重複の可能性」タグを付けます。

**スクリーンショット整理** -- 日本語/英語のスクリーンショットファイルや CleanShot の出力を、年月別サブフォルダに整理します。

**年月別サブフォルダ整理** -- すべてのファイルを年月別サブフォルダに振り分けるシンプルなプリセットです。

---

### オフィスワーク（Office）

**書類整理** -- PDF、Word、Excel/CSV、テキストファイルをそれぞれの専用フォルダに分類します。

**プレゼン資料整理** -- PowerPoint や Keynote ファイルを年月別サブフォルダに移動し、50MB を超える PDF には「大容量プレゼン」タグを付けます。

**メール添付整理** -- 添付ファイルを画像、文書、その他に分けて Attachments 以下のフォルダに整理します。

**請求書・領収書管理** -- ファイル名に「請求」を含むファイルに青の「請求書」タグ、「領収」を含むファイルに緑の「領収書」タグを付け、年月別サブフォルダに移動します。

**仕事用タグ付け** -- 直近3日以内に更新されたファイルに赤の「作業中」タグ、今週更新のファイルに青の「今週」タグ、100MB 超のファイルに橙の「要圧縮」タグを付けます。

---

### クリエイティブ（Creative）

**写真・画像整理** -- RAW 画像は Pictures/RAW、PSD 等の編集ファイルは Pictures/Edits、SVG/WebP は Pictures/Web、一般画像は年月別サブフォルダに整理します。

**動画整理** -- 500MB 超の動画は Movies/Footage に移動して「大容量動画」タグを付け、fcpbundle/prproj/aep は Movies/Projects、50MB 未満は Movies/Clips に移動します。

**音楽・音声整理** -- flac/wav/aiff は Music/Lossless、mp3/aac/m4a は Music/General、ボイスメモは Music/Recordings に整理します。

**フォント管理** -- ttf/otf/woff ファイルに紫の「フォント」タグ、font を含む ZIP に紫の「フォントZIP」タグを付けます。

**デザインアセット整理** -- Figma/Sketch は Design/Projects、icns/ico は Design/Icons、@2x/@3x 画像は Design/Retina に整理します。

---

### 開発者（Developer）

**ソースコード整理** -- Swift、Python、Web（JS/TS/HTML/CSS）、その他の言語ファイルを拡張子別サブフォルダに分類します。

**データ・設定ファイル整理** -- JSON/YAML/XML 等を Development/Config、SQLite/DB を Development/Data、SQL を年月別サブフォルダに整理します。

**ログファイル整理** -- ログを年月別サブフォルダに整理し、crash/ips ファイルに赤の「クラッシュ」タグを付けて CrashReports に移動します。30日経過したログはゴミ箱に移動します。

**ビルド成果物管理** -- ipa/apk/aab を年月日サブフォルダに移動して青の「ビルド」タグを付け、framework/dylib は Development/Libraries に整理します。

**シェルスクリプト整理** -- sh/bash/zsh を Development/Scripts、Makefile/Dockerfile を Development/BuildFiles に整理します。

**ビルド成果物のアーカイブ** -- .o/.dylib/.dSYM/.build ファイルをアーカイブに移動します。

---

### メンテナンス（Maintenance）

**大容量ファイル検出** -- 500MB 超に赤の「超大容量」、100-500MB に橙の「大容量」、50-100MB に黄の「中容量」タグを付けます。

**古いファイル警告** -- 30日経過に黄の「30日経過」、90日に橙の「90日経過」、180日に赤の「180日経過」タグを付けます。

**一時ファイル自動削除** -- 7日経過した .tmp ファイル、ダウンロード中断ファイル（crdownload/part/download）、.DS_Store をゴミ箱に移動します。

**ディスク使用量アラート** -- 1GB 超の動画に赤の「巨大動画」タグ、30日経過した DMG に橙の「削除候補」タグを付けます。

**Finder タグ整理** -- 「重要」タグのファイルを Documents/Important に移動、「確認」タグに「確認済み」を追加、「完了」タグ＋30日経過のファイルを Archive に移動します。

**古いログファイルのアーカイブ** -- 30日経過した .log と .txt ファイルをアーカイブに移動します。

---

### アーカイブ（Archive）

**未使用ファイルのアーカイブ** -- 最終アクセスから30日以上経過したファイルをアーカイブに移動します。

**大容量ファイルのアーカイブ** -- 100MB 超のファイルをアーカイブに移動します。

**一時ファイルのアーカイブ** -- tmp/temp/cache/bak ファイルをアーカイブに移動します。

---

### カスタマイズ

プリセットを適用した後は、ノードエディタで自由にカスタマイズできます。移動先パスの変更、条件の追加や削除、タグ名や色の変更、リネームなどのアクション追加、AND/OR ロジックの切り替えなど、プリセットをベースに自分の使い方に合わせて調整してください。

---

## English

Presets are ready-made rule templates for common file organization patterns. Instead of building rules from scratch, pick a preset, customize what you need, and start organizing.

### Using a preset

1. In the Rules tab, click "New Rule" then "Choose from Presets"
2. Select a template from the list
3. The template opens in the node editor
4. Adjust destination paths and tag names for your setup, then save

Use the search bar to find presets by keyword in Japanese or English.

---

### General

**Download Organization** -- Sorts Downloads by type: images to kind subfolders, PDFs to monthly subfolders, archives to Archives, installers to Installers, videos to Videos. Tags files older than 30 days with "Needs Organization."

**Desktop Organization** -- Screenshots go to Pictures/Screenshots, documents to Documents. Files over 100MB get a "Large" tag; files older than 14 days get a "Needs Organization" tag.

**Old File Archive** -- 90-day files to Archive, 180-day files get "Long Unused" tag, 365-day files to Trash.

**Duplicate & Temp Management** -- tmp/temp/bak files to Trash; copy-duplicates get a "Possible Duplicate" tag.

**Screenshot Organization** -- Japanese/English screenshots and CleanShot output to monthly subfolders.

**Monthly Subfolder Organization** -- All files to yyyy/MM subfolders.

---

### Office

**Document Organization** -- PDF, Word, Excel/CSV, and text files to type-specific folders.

**Presentation Organization** -- PowerPoint and Keynote to monthly subfolders. PDFs over 50MB tagged "Large Presentation."

**Email Attachment Organization** -- Attachments sorted into Images, Documents, and Others under Attachments.

**Invoice & Receipt Management** -- Files with "invoice" in the name get a blue "Invoice" tag; "receipt" files get a green "Receipt" tag. Both go to monthly subfolders.

**Work File Tagging** -- Recently updated files tagged "In Progress" (red), this week's files tagged "This Week" (blue), files over 100MB tagged "Needs Compression" (orange).

---

### Creative

**Photo & Image Organization** -- RAW to Pictures/RAW, PSD edits to Pictures/Edits, SVG/WebP to Pictures/Web, general images to monthly subfolders.

**Video Organization** -- Footage over 500MB to Movies/Footage with a "Large Video" tag, editing projects to Movies/Projects, clips under 50MB to Movies/Clips.

**Music & Audio Organization** -- Lossless (flac/wav/aiff) to Music/Lossless, general (mp3/aac/m4a) to Music/General, voice memos to Music/Recordings.

**Font Management** -- Font files (ttf/otf/woff) tagged purple "Font"; font-related ZIPs tagged purple "Font ZIP."

**Design Asset Organization** -- Figma/Sketch to Design/Projects, icons to Design/Icons, @2x/@3x images to Design/Retina.

---

### Developer

**Source Code Organization** -- Swift, Python, Web (JS/TS/HTML/CSS), and other languages to extension-based subfolders.

**Data & Config File Organization** -- JSON/YAML/XML to Development/Config, SQLite/DB to Development/Data, SQL to monthly subfolders.

**Log File Organization** -- Logs to monthly subfolders, crash reports tagged red "Crash" and moved to CrashReports. Logs older than 30 days go to Trash.

**Build Artifact Management** -- Mobile artifacts (ipa/apk/aab) to daily subfolders with blue "Build" tag; libraries to Development/Libraries.

**Shell Script Organization** -- Shell scripts to Development/Scripts, build files (Makefile/Dockerfile) to Development/BuildFiles.

**Build Artifact Archive** -- .o/.dylib/.dSYM/.build files to archive.

---

### Maintenance

**Large File Detection** -- Color-coded tags: red for 500MB+, orange for 100-500MB, yellow for 50-100MB.

**Old File Warning** -- Yellow tag at 30 days, orange at 90 days, red at 180 days.

**Auto-delete Temp Files** -- 7-day old .tmp files, incomplete downloads (crdownload/part/download), and .DS_Store to Trash.

**Disk Usage Alert** -- Videos over 1GB tagged red "Huge Video"; DMGs older than 30 days tagged orange "Delete Candidate."

**Finder Tag Organization** -- "Important" tagged files to Documents/Important; "Review" tagged files get "Reviewed" added; "Done" tagged files older than 30 days to Archive.

**Old Log File Archive** -- .log and .txt files older than 30 days to archive.

---

### Archive

**Unused File Archive** -- Files not accessed for 30+ days to archive.

**Large File Archive** -- Files over 100MB to archive.

**Temp File Archive** -- tmp/temp/cache/bak files to archive.

---

### Customizing

After applying a preset, you can freely modify it in the node editor: change destination paths, add or remove conditions, adjust tag names and colors, add actions like rename, or switch between AND/OR logic. Use presets as a starting point and tailor them to your workflow.
