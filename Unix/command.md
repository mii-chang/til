## ファイル操作
- touchコマンド  
コピーのときとかに使うこと多  
`touch`
1. 空のファイルを作る
2. （指定ファイルが存在しているなら）タイムスタンプを最新にしUpdate

- tarコマンドp111  
`tar`  
1. 複数ファイルをまとめる（アーカイブ）
2. アーカイブを展開する
最近のtarコマンドは
3. 圧縮解凍も一緒にできる(gzip or bzip2)(option z or j)

**Unixでzipで圧縮したいときは、1ファイルしか圧縮できない→ここでtarの出番。複数ファイルを一旦tarでまとめて、それをgzipで圧縮！→無事にファイルサイズが小さくなる。**


### 例
```
[vagrant@localhost ~]$ mkdir 04  
[vagrant@localhost ~]$ cd 04
[vagrant@localhost 04]$ mkdir 10
[vagrant@localhost 04]$ mkdir 11
[vagrant@localhost 04]$ ls
10  11
[vagrant@localhost 04]$ cd 10
[vagrant@localhost 10]$ vi memo.text
[vagrant@localhost 10]$ cd ..
[vagrant@localhost 04]$ cd 11
[vagrant@localhost 11]$ vi memo.text
[vagrant@localhost 11]$ cd ..
[vagrant@localhost 04]$ cd ..
[vagrant@localhost ~]$ ls
04
[vagrant@localhost ~]$ tar cfj a.tar.bz2 04
[vagrant@localhost ~]$ ls
04  a.tar.bz2
[vagrant@localhost ~]$ tar tfv a.tar.bz2 
drwxrwxr-x vagrant/vagrant   0 2018-04-10 06:21 04/
drwxrwxr-x vagrant/vagrant   0 2018-04-10 06:22 04/10/
-rw-rw-r-- vagrant/vagrant  21 2018-04-10 06:22 04/10/memo.text
drwxrwxr-x vagrant/vagrant   0 2018-04-10 06:22 04/11/
-rw-rw-r-- vagrant/vagrant   7 2018-04-10 06:22 04/11/memo.text
```


## 標準入出力
- コマンドの実行結果の出力をファイルに纏める
1. もしすでにファイルがあったら上書きする  
`[コマンド] > [ファイル名]`
ex:`ls > 0411/list.txt`
2. すでにファイルがあったら末尾に追記  
`[コマンド] >> [ファイル名]`
ex:`ls >> 0411/list.txt`
- 標準入力もとに文字数カウント
`wc`  
`wc < [カウントしたいテキストファイル名]`  
ex 
```
[0411] wc                                                                                                                   12:20:52
123
456

7
       4       3      11
       
```
出力結果` 4       3      11`は、行数・単語数・文字数の結果

- 複数のコマンドをつなげるには`｜`パイプを使う
```
$ cat [ファイル名] > [別ファイル名]
$ cat [ファイル名] | wc
$ cat wc | wc
```
- echoコマンド  
print的なもの  
**使い所！**  
エディタ使わなくてもかんたんにダミーファイルができる  
ex  
`$ echo "hogehoge" > hoge.txt"`

- findコマンド  
- mp3を移動させる  
`find <dir> -type f | grep -P "\.mp3$" | wargs -I{} mv {}  <mp3-dir>`
       
- .git をのぞいて表示する  
`find <dir> -name .git -prune -o -print`
参考：http://www.roshi.tv/2011/02/find-prune.html 
       
- 深さ<depth>階層目までのディレクトリを表示させる  
`find <dir> -type d -maxdepth <depth>`
       
- 空のディレクトリを消す  
`find -empty -delete`
       
