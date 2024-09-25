# Launch Multi-File Source-Code Programs

## 説明

- コード実行のオーバーヘッドに対処

  - これまでのやり方
    - 実行するには 2 ステップ必要
      - コンパイル：`javac`
      - 実行：`java -jar`

- 複数ファイルのソースコードスタイル

  - ワンステップで実行できるようになる
    - `java`
      - ファイルに main を持つ public クラスがある場合、コンパイルして実行。
      - これで、同じフォルダまたはサブフォルダに複数のクラスファイルを持つことができる。
      - jar ファイルを含めることもできる。
    - IDE をマスターしなくてもよくなる。

- Java 学習と IDE
  - 言語学習の焦点
    - 新しい言語を学ぶ際には、その言語自体に集中することが重要です。IDE は学習の妨げになる可能性がある。
  - シングルファイル実行
    - Python のように、Java もシングルファイルでプログラムを実行できるようになった。これにより、複数のクラスファイルを使う必要がなくなった。
  - テキストエディタの使用
    - シングルファイル実行には、テキストエディタ（Notepad や Vim など）だけで十分。IDE を使わずに、コマンドラインでコンパイルと実行が可能。
  - Linux/Mac 環境
    - Linux や Mac では、シェバン（Shebang）構文を使ってシングルファイルプログラムを簡単に実行できる。
  - デモンストレーション
    - シングルファイルプログラムとマルチファイルプログラムのデモを行う手順が説明されています。具体的には、[JavaCalculations03.java](https://github.com/omniprof/JCP_EC_Education_WG_Presentation/blob/main/JavaCalculator03.java) というファイルを使って、コマンドラインでプログラムを実行する方法が示されています。

## 参考

- Java11 [JEP330](https://openjdk.org/jeps/330)
- Java22 [JEP458](https://openjdk.org/jeps/458)
