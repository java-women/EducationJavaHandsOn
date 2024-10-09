# Preview Features

- Java 言語の新機能はすぐに使うことはできない。

  - 追加された新機能はプレビュー機能として利用可能となる。
  - プレビュー機能を利用する場合はオプションの付与が必要。

- プレビュー機能を利用する

  - コマンドライン、または IDE でオプションを指定する必要がある。

    - コマンドライン関連

      - 従来のコマンドライン

        - コンパイル

          - `javac --source 23 --enable-preview Main.java`

        - 実行

          - `java --enable-preview Main`

        - JShell の起動

          - `jshell --enable-preview`

        - コンパイルと実行(JEP330 と JEJEP458)

          - `java --enable-preview Main.java`

    - IDE
      - eclipse
        - MarketPlace から Java 23 Support for Eclipse をダウンロード
        - コンパイラのレベルを JDK23 で設定
        - Installed JRE を JDK23 で設定
        - 実行環境に JDK23 を設定
      - IntelJ
        - プロジェクトで JDK23 を使うように設定
        - File>Project Structure>Project Settings>Modules を開いて、プレビュー機能を ON にする。

# 備考

- IDE については時間次第では省略。（話すようであれば画面のハードコピー等があったほうがよいかもだけれども、小さすぎて見えないかもしれない。）
