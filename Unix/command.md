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

