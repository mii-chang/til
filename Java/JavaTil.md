# クラス変数・インスタンス変数（メソッド）
```Java
class hoge {
public static int x;//クラス変数
public int a;//インスタンス変数
public int b;//インスタンス変数

public static void test(){//クラスメソッド
int a;//ローカル変数
int b;//ローカル変数
~~~
}

public void test2(){//インスタンスメソッド
~~~~~
}

```

## デフォルトコンストラクタ
- コンストラクタの中でも、引数を持たないコンストラクタのことを**デフォルトコンストラクタ**という。
- クラスの中でコンストラクタを何も定義しなければ、自動的に作られている。
- 明示的に引数のあるコンストラクタを１つでも作っていれば、デフォルトコンストラクタが効かなくなる。  
  - なので必要なときはデフォルトコンストラクタをちゃんと作らないと✗

## superクラス
- superクラスは**継承元**のこと。

### superキーワード
- コードによくついてる`super(hoge)`の意味  
  - 普通はコンストラクタを作るときにデフォルトコンストラクタが実行されるが、コンストラクタを作りたいクラスが他のクラスを継承していた場合、かつデフォルトコンストラクタがない場合、superを使ってコンストラクタの指定をしないといけない。
 
 
 ex　すべてデフォルトコンストラクタは無い  
 ```Java
 class X {
  int x;
  
  //コンストラクタ
  X(int a) {
    x =a
  }
}

class Y extends X {
  int y;
  
  //コンストラクタ
  Y(int a, int b){
    super(a); //Xにはデフォルトコンストラクタがないので、superで1つ引数を渡してあげないといけない
    y = b;
  }

class Z extends Y {
  int z;
  
  //コンストラクタ
  Z(int a, int b, int c) {
    super(a, b); //Yにはデフォルトコンストラクタがないので、superで2つ引数を渡してあげないといけない
    z = c;
  }
}
  
 ```

## 例外
### try-catch
- tryの内容を試みた結果、Errorをcatchした場合、catch以降の処理をして終わってね  
  - この文が呼ばれているメソッド内でエラーの後始末をしている。
   
### throws
- throwsが書かれているメソッドの中でErrorが発生した場合、thowsが書かれているメソッドはエラーの責任を放棄しますよ  
  - このメソッドの呼び出し元にエラーが有ると主張するためのもの。
  
  
# 文字列クラス
オブジェクトの運用で

- 値が不変(immutable) 例:Stringクラス  
  - 不変→スレッド間でロック**不要**⇛排他的制御しなくて良い  
    ↕  
- 値が可変(mutable) 例:StringBufferクラス

**関数型言語ではimmutableが大事！**  
  ⇛コレクションクラス
  
- 文字列の連結  
```Java
String s = "abc";
s = Ss+ "def";
```
文字列を連結すると、連結した時点で新たに連結後の内容のインスタンスが作られる！

```Java
String s1 = "abc";
String s2 = "abc";

if(s1 == s2){
~~~~~~
}
```
これの場合、`s1`と`s2`は**等しく**なる。  

```Java
String s1 = "abc";
String s2 = "abc";

s1 = s1 + "def";
s2 = s2 + "def";

if(s1 == s2){
~~~~~~
}
```

これの場合、`s1`と`s2`は等しくない。(文字列を連結した時点で新たしいインスタンスが作られたから(newされたのと同じ的なふうに考えたらOK))  

コンストラクタを作る時、いつもなら  
`String s = new String("abc");`  
ていう感じにしてるが、Stringはnewしなくてもインスタンスを作れる例外的なオブジェクト。  
なので、いつもみたいに  
`String s = "abc";`  
としてOK。
でも、内容的には`String s = new String("abc");`みたいなことをしたいので、`""`の中を見て、内容(文字列リテラル)が同じだったら節約の意味で同じ領域を使ってる。
なので連結してないときは`==`で比較可能

**要するにString比較するときは`.equals`を使おうって話**


# Generics  
## メソッドに対するGenerics
- 任意の仮置きクラスを引数として受けるメソッドを定義できる。

```Java
public class Main {
	public static void main(String[] args) {
		int a = 10;
		double b = 11.2;
		swap(a,b);
	}
	
	static <T> void swap(T a, T b) {//このTが仮置きの型
		T c = null;
		c = a;
		a = b;
		b = c;
		System.out.println(a);
		System.out.println(b);
		System.out.println(c);
	}
}
```

実行結果
```
11.2
10
10
```
## Classに対するGenerics
- Classに対しても同様に仮置きの型を引数にできる
```Java

public class Sub<T> {//このTが仮置きの型
	T a;
	T b;

	Sub(T x, T y) {
		a = x;
		b = y;
	}

	void print() {
		System.out.println(a);
		System.out.println(b);
	}

	void swap() {
		T c = null;

		c = a;
		a = b;
		b = c;
	}
}

```

```Java

public class Main {
	public static void main(String[] args) {
		Sub<Integer> sub1 = new Sub<Integer>(10, 20);
		sub1.swap();
		sub1.print();

		Sub<Double> sub2 = new Sub<Double>(2.3, 4.56);
		sub2.swap();
		sub2.print();

		Sub<String> sub3 = new Sub<String>("abc", "hello");
		sub3.swap();
		sub3.print();
	}

}

```

実行結果
```
20
10
4.56
2.3
hello
abc
```
