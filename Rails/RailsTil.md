## はじめに
### Rubyのアップデート

```
rbenv -version

//インストールされてるrubyのバージョン確認
rbenv versions

//今のRubyのバージョンを一覧表示
rbenv --list

//インストール
rbenv install -v [version]

//バージョンアップ
rbenv global [version]

```

### 基本の構造を作る

```
//gemのインストール
gem install -v [version]

//workspaceディレクトリをつくる
mkdir workspace

//workspaceディレクトリに移動
cd workspace

//rails new
rails -[version] -new [appname]

```

### ディレクトリ構造
https://railstutorial.jp/chapters/beginning?version=5.0#table-rails_directory_structure

|Directory|Work|
|:--|:--|
|app/|モデル、ビュー、コントローラ、ヘルパーなどを含む主要なアプリケーションコード|
|app/assets|アプリケーションで使うCSS (Cascading Style Sheet)、JavaScriptファイル、画像などのアセット|
|bin/|バイナリ実行可能ファイル|
|config/|アプリケーションの設定|
|db/|データベース関連のファイル|
|doc/|マニュアルなど、アプリケーションのドキュメント|
|lib/|ライブラリモジュール|
|lib/assets|ライブラリで使うCSS (Cascading Style Sheet)、JavaScriptファイル、画像などのアセット|
|log/|アプリケーションのログファイル|
|public/|エラーページなど、一般(Webブラウザなど)に直接公開するデータ|
|bin/rails|コード生成、コンソールの起動、ローカルのWebサーバの立ち上げなどで使うRailsスクリプト|
|test/|アプリケーションのテスト|
|tmp/|一時ファイル|
|vendor/|サードパーティのプラグインやgemなど|
|vendor/assets|サードパーティのプラグインやgemで使うCSS (Cascading Style Sheet)、JavaScriptファイル、画像などのアセット|
|README.md|アプリケーションの簡単な説明 (訳注: 近年は .rdocよりも .md ファイルの方がよく使われているようです)|
|Rakefile|rakeコマンドで使えるタスク|
|Gemfile|このアプリケーションに必要なGemの定義ファイル|
|Gemfile.lock|アプリケーションで使われるgemのバージョンを確認するためのリスト|
|config.ru|Rackミドルウェア用の設定ファイル|
