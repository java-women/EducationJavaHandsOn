# Implicitly Declared Classes and Instance Main Methods

# 説明

- Java に関する最も一般的な不満

  - 他の言語と比較して、初心者には適していない。
      - 文法やルールを習得するのに時間がかかる。
      - オブジェクト指向への理解と記述の多さに初心者はつまづきやすい。

  - 従来の Hello World

    - `HelloWorld.java`

    ```java
    public class HelloWorld {
        public static void main(String[] args) {
            System.out.println("HelloWorld");
        }
    }
    ```

- 初心者が大規模プログラム向けに設計された言語機能を理解しなくても最初のプログラムを作成できるようになった。

  - 究極の簡素化
    - クラス宣言は不要
    - アクセス制御の宣言は不要

- main メソッドはインスタンスメソッドとして表現できる。
- 暗黙的なクラスだけでなく、任意の Java プログラムで使用できる。

  - `HelloWorld.java`

  ```java
  void main() {
      System.out.println("HelloWorld");
  }
  ```

- コンソールの操作

  - 従来の書き方

  ```java
  try {
    BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
    String line = reader.readLine();
    ...
  } catch (IOException ioe) {
    ...
  }
  ```

  - すべての暗黙化されたクラスで利用可能となった。

    - `public static void println(Object obj);`
    - `public static void print(Object obj);`
    - `public static String readln(String prompt);`

  - HelloWorld がもっと簡単に。

    - `HelloWorld.java`

    ```java
    void main() {
        println("HelloWorld");
    }
    ```

  - コンソールとの対話も簡単に。

    - `Greetings.java`

    ```java
    void main() {
        String name = readln("Name: ");
        print("Pleased to meet you, ");
        println(name);
    }
    ```

# 参考

- Java21
  - [JEP 445](https://openjdk.org/jeps/445)
- Java22
  - [JEP 463](https://openjdk.org/jeps/463)
- Java 23
  - [JEP 477](https://openjdk.org/jeps/477)
