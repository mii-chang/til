Kotlinは関数型言語。 
この場合の関数は数学と同じような意味合いの関数 
大原則、入力値と出力値が1対1。  
👉出力値は入力力しか決まらない。 
  👉関数の中で値・状態を持たない。（Stateless）  
  ⇔メソッドはメソッド内で他のところからデータとか持ってきてる  
    
関数型 
変数に代入できる👉引数に渡せる、別の関数の戻り値にできる 


- イミュータビリティー
  原則、変数値は不要（初期化したら変わらない）  
  不変じゃない👉可変だと値を持ってしまう。👉マルチスレッドでロックが必要になってくる
  
  
# 変数の宣言
- val 
JavaのFinalに匹敵。  

- var 
変更可能な変数。   

**基本的にvalを使おう！**


# 関数呼び出しをかんたんにする

```Kotlin
fun main(args: Array<String>) {
    fun <T> join(
    collection: Collection <T>,
    separator: String,
    prefix: String,
    postfix: String
    ): String {
        val result = StringBuilder(prefix)
        for ((index, element) in collection.withIndex()){
            if (index > 0) result.append(separator)
            result.append(element)
        }
        result.append(postfix)
        return result.toString()
    }
    
   val list = listOf(1,2,3)
    println(join(list, ".", "(", ")"))
}
```

- join関数を呼び出すためには、`collection`,`separator`,`prefix`,`postfix`の4つの引数が必要！



retrnしかしない関数なら更に省略可能
例えば
```
fun hoge(x: Int, y: Int) {
  return x + y
}

```
が
```
fun hoge(x: Int, y: Int) = return x + y
```
になる！！

## withIndex
- コレクションの中身をIndex番号と一緒に引っ張れる  
  - この例では、`index`にIndex番号、`element`にコレクションの中身が入ってくる
  
  
これめんどくさいな！？
> join関数を呼び出すためには、`collection`,`separator`,`prefix`,`postfix`の4つの引数が必要！

🎉省略できます🎊

```Kotlin
fun main(args: Array<String>) {
    fun <T> join(
    collection: Collection <T>,
    separator: String = ",",
    prefix: String = "(",
    postfix: String = ")"
    ): String {
        val result = StringBuilder(prefix)
        for ((index, element) in collection.withIndex()){
            if (index > 0) result.append(separator)
            result.append(element)
        }
        result.append(postfix)
        return result.toString()
    }
    
   val list = listOf(1,2,3)
    println(join(list))
}
```


` println(join(list))`でこれ以降の引数は省略されたことになる。（ただし**デフォルト引数**が必要）

## デフォルト引数

```Kotlin
fun <T> join(
    collection: Collection <T>,
    separator: String = ",",
    prefix: String = "(",
    postfix: String = ")"
    ): String {~~~~~~~~~
```

引数の中に型の他にデフォルトの引数を設定できる。これが設定されている関数であれば、呼び出しのときにすべての引数を書かなくてもOK！


- でもデフォルトの引数じゃ嫌な時があるかも。。。。。
 
 **🎉名前付き引数で指定できるぞ！🎊**
 
 ```Kotlin
fun <T> join(
    collection: Collection <T>,
    separator: String = ",",
    prefix: String = "(",
    postfix: String = ")"
    ): String {~~~~~~~~~
    
    ~~~~~~~
    
    val list = listOf(1,2,3)
    println(join(list, postfix = "}"))
    
```

変えたいものだけ名前付き引数で指定することが可能！便利！
