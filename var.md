# var

## 説明

- Java は型付き言語です。
  すべての変数は、型で宣言する必要があります。
  プリミティブは、 'int x;' のように一度表示されるタイプが必要です。
  参照では、型が 2 回表示されている必要があります。
  新しい var キーワードを使用すると、この繰り返しがなくなります。
  冗長性や過剰なコーディングに関する別の苦情は削除されました。
  ローカルの NullPointerException の最も一般的な理由の 1 つは、参照のインスタンス化を怠ることです。var では、インスタンス化する必要があります。

## var の使いどころ

- Java 10 から使えるようになった。

  - 型名が長いことがあるので、コード自体が長くなっていたものが短くて済むようになった。

- 何が入っているかぱっと見わからないから、テストコードには利用可能であっても本体では推奨しないところも？
  - ぱっと見てわからないのは困る？！？

## var の注意

- 初期化が必要

  ```
  var obj; // コンパイルエラー
  ```

- null は代入できない

  ```
  var obj = null; // コンパイルエラー
  ```

- `ローカル変数`でのみ使用可能
  ```
  public class Sample {
      // ここでは使えない
      String hoge = "hoge";
      void sample() {
          // ここではvarが使える
          var fuga = "fuga";
      }
  }
  ```

## Sample

- final 変数にしたい場合は var の左側に final を付ける。

```
final var f1 = 123;
var final f2 = 123; // コンパイルエラー
```

- 配列(配列の初期化構文では var は使用できない。配列の型を明示すれば可。)

```
var array1 = { 1, 2, 3 }; // コンパイルエラー
var array2 = new int[]{ 1, 2, 3 };
```

- var は for 文や try 文でも使用できる。

```
var list = List.of("a", "b", "c");
for (var s : list) {
  System.out.println(s);
}
```

```
try (var is = Files.newInputStream(path)) {
  ～
}
```

## 参考

- [Java var](https://www.ne.jp/asahi/hishidama/home/tech/java/var.html)
- [JEP 286](https://openjdk.org/jeps/286)
