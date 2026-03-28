# はじめに / Getting Started

## 日本語

TidyBox は、Mac のメニューバーに常駐するファイル自動整理アプリです。Dock にアイコンを表示せず、メニューバーからすべての操作を行えます。macOS の FSEvents を使ってファイルの追加をリアルタイムに検知し、ルールに従って整理します。インターネット接続は不要で、ファイルが外部に送信されることはありません。M1/M2/M3/M4 Mac でネイティブ動作します。

### インストール

Mac App Store から TidyBox をダウンロードしてインストールしてください。macOS 15.0（Sequoia）以降が必要です。

### 初回起動

TidyBox を起動すると、メニューバーにアイコンが表示されます（Dock にはアイコンが表示されません。これは設定で変更できます）。初回はオンボーディング画面が表示されるので、フォルダアクセスの許可を求められた場合は「許可」を選択し、画面の手順に沿って最初の監視フォルダとルールを設定してください。

メインウィンドウを開くには、メニューバーの TidyBox アイコンをクリックしてポップオーバーを表示し、「メインウィンドウを開く」を選択します。

### クイックスタート

#### 1. 監視フォルダを登録する

メインウィンドウの「設定」>「監視ディレクトリ」を開き、「追加」ボタンをクリックして整理したいフォルダ（例: `~/Downloads`）を選択します。

#### 2. ルールを作成する

「ルール」タブを開き、「新規ルール」>「プリセットから選択」の順にクリックします。たとえば「ダウンロード整理」プリセットを選択すると、ノードエディタにテンプレートが展開されます。移動先パスなどを自分の環境に合わせて調整し、保存してください。

#### 3. 整理が始まる

監視フォルダにファイルが追加されると、ルールに従って整理されます。整理の状況はダッシュボードで確認でき、間違った操作は履歴画面から元に戻せます。

初めは「ドライランモード」を有効にしておくと安心です。ルールの評価は行いますが実際のファイル操作は行わないため、ルールの動作を安全に確認できます。設定 > 一般 > 「ドライランモード」で切り替えてください。

---

## English

TidyBox is a file organization app that lives in your Mac's menu bar. It uses macOS FSEvents to detect new files in real time and organizes them according to your rules. No internet connection is needed -- your files never leave your Mac. TidyBox runs natively on M1/M2/M3/M4 Macs and requires macOS 15.0 (Sequoia) or later.

### Installation

Download and install TidyBox from the Mac App Store.

### First Launch

When you open TidyBox, its icon appears in the menu bar (not in the Dock, though you can change this in settings). An onboarding screen walks you through granting folder access and setting up your first watched folder and rules.

To open the main window, click the TidyBox icon in the menu bar, then select "Open Main Window" from the popover.

### Quick Start

#### 1. Add a watched folder

Go to Settings > Watched Directories in the main window and click "Add." Select the folder you want to organize, such as `~/Downloads`.

#### 2. Create a rule

Open the Rules tab and click "New Rule," then "Choose from Presets." Select a preset like "Download Organization" -- it opens in the node editor as a ready-made template. Adjust the destination paths for your setup and save.

#### 3. Organization begins

When files are added to the watched folder, TidyBox organizes them according to your rules. Check the Dashboard to see activity, and use the History screen to undo any mistakes.

Consider enabling Dry Run Mode when you first set up TidyBox. It evaluates rules without actually moving files, so you can verify everything works as expected. Toggle it under Settings > General.
