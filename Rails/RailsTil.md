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
rbenv grobal [version]

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
