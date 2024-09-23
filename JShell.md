# JShell

## 説明

- Java9 から導入された。一行一行の即時対応。
- 指導を簡素化するためのツール。
- コードを入力して Return キーを押すと実行されます。
- また、最初にメソッド全体を記述してから実行することもできます。
- Java を一度に 1 行ずつ教えるのに最適です。

## 起動と終了

- Windows ユーザはコマンドプロンプト、Mac/Linux ユーザはターミナルで開いてください。

### 起動

```
$ jshell
```

### 終了

```
jshell > /exit
```

## JShell で HelloWorld

```
jshell> System.out.println("Hello World");
Hello World

jshell> "HelloWorld";
$2 ==> "HelloWorld"
```

## JShell のショートカット

- Windows の場合(mac も基本的に変わらないです。control の下にある上向きの矢印、control の上のある左向きの矢印を駆使してください。)
  - クラスのインポート
    - インポートしたいクラスを入力し、`Shift` を押しながら `tab` を押した後、`i` 　を入力。
  - 変数の宣言
    - 変数の値を入力し`Shift`を押しながら `tab` を押した後、`v` を入力。
  - メソッドの宣言
    - 変数の値を入力し `Shift` を押しながら `tab` を押した後、`m` を入力。
  - 履歴の検索
    - `Ctrl` + `r`
