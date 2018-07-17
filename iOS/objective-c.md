## `@property　` とはなんぞ  

同名のインスタンス変数へのアクセサ(setter/getter)が作られる。  
`@property NSString *hoge;`  
を宣言すると、同時に `@property NSString *_hoge;`が宣言される。  
そしたら
```
NSLog(@"%@", self.hoge);
NSLog(@"%@", _hoge);
```
どちらでもアクセス可能になる

## アンスコの意味は何じゃ  
インスタンス変数にはアンスコつけようぜっていうお約束みたいなもの。
