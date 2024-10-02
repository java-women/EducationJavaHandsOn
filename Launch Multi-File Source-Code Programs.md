# Launch Multi-File Source-Code Programs

## 説明

- コード実行のオーバーヘッドに対処

  - これまでのやり方
    - 実行するには 2 ステップ必要
      - コンパイル：`javac`
      - 実行：`java -jar`

- Java の実行に関する JEP

  - Java11 にて、[JEP 330 Launch Single-File Source-Code Programs](https://openjdk.org/jeps/330) がリリースされ、明示的なコンパイル操作を省略し、.java ファイルを java コマンドで直接実行できるようになった。

    - `Prog.java`　(JEP330 では 1 つのファイルに収める必要がある。)

    ```java
      class Prog {
          public static void main(String[] args) { Helper.run(); }
      }
      class Helper {
      static void run() { System.out.println("Hello!"); }
      }

    ```

    ```
    $ java Prog.java
    Hello!
    ```

  - Java22 にて、[JEP 458 Launch Multi-File Source-Code Programs](https://openjdk.org/jeps/458) がリリースされ、複数のソースコードから構成される Java プログラムのすべてのファイルを事前にコンパイルしなくとも、java コマンドで直接実行すると実行時に必要に応じてコンパイルし、実行できるようになった。

  - `Prog.java`

  ```java
  class Prog {
    public static void main(String[] args) { Helper.run(); }
  }
  ```

  - `Helper.java`

  ```java
  class Helper {
    static void run() { System.out.println("Hello!"); }
  }
  ```

  ```
  $ java Prog.java
  Hello!
  ```

  > Prog クラスがメモリ上でコンパイルされ、main メソッドが呼ばれる。  
  > このクラスのコードは Helper クラスを参照しているので、ランチャーはファイルシステム内の Helper.java ファイルを見つけて、そのクラスをメモリ内でコンパイルして実行。

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

## Sample

- シングルファイル実行
  - [JavaCalculations03.java](https://github.com/omniprof/JCP_EC_Education_WG_Presentation/blob/main/JavaCalculator03.java)
- マルチファイル実行
  - Java の実行に関する JEP の、JEP458 のサンプル参照
- jar を含めた実行

  - フォルダの構成

    - JunitSample.java
    - apiguardian-api-1.1.2.jar
    - junit-jupiter-api-5.11.0.jar
    - junit-jupiter-engine-5.11.0.jar
    - junit-platform-engine-1.11.0.jar
    - opentest4j-1.3.0.jar

  - `JunitSample.java`

    ```java
    import static org.junit.jupiter.api.Assertions.*;

    import org.junit.jupiter.api.Test;

    public class JunitSample {
        // java コマンドで実行なので、main メソッドがないとエラーになる
        void main() {
            // 2が4なわけない
            assertEquals(2, 4);
        }
    }
    ```

    - 実行

    ```
    java --enable-preview --class-path "*" JunitSample.java
    ```

    - 結果

    ```
    Exception in thread "main" org.opentest4j.AssertionFailedError: expected: <2> but was: <4>
        at org.junit.jupiter.api.AssertionFailureBuilder.build(AssertionFailureBuilder.java:151)
        at org.junit.jupiter.api.AssertionFailureBuilder.buildAndThrow(AssertionFailureBuilder.java:132)
        at org.junit.jupiter.api.AssertEquals.failNotEqual(AssertEquals.java:197)
        at org.junit.jupiter.api.AssertEquals.assertEquals(AssertEquals.java:150)
        at org.junit.jupiter.api.AssertEquals.assertEquals(AssertEquals.java:145)
        at org.junit.jupiter.api.Assertions.assertEquals(Assertions.java:531)
        at JunitSample.main(JunitSample.java:8)
    ```
