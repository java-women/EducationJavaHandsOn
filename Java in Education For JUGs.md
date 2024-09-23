# 概要
https://github.com/jcp-org/Java-in-Education/blob/main/Java%20in%20Education%20For%20JUGs%202.3.1.pptx の内容をざっくり和訳して読む

# Myths & Benefits of Learning Java
p.2〜7 Javaがイケてないと言われる理由（神話）と、それに対する反論
- Javaは初心者にとって学習曲線が急であることがあります
  - ただし、それは講師自身が言語を学ぶ際に急な学習曲線を経験した場合のみです。
- Java は軽量で素早いタスクには適していません
  - より大規模で複雑なアプリケーションに適しています
  - マルチファイルソースコードを見たことや、LinuxでShebang（`#!/bin/bash`みたいなやつ）を実行したことはありますか？
  - Javaの学習を簡単にするために、今まさに改善が行われています
- Oracle Java Development Kit (JDK) はオープンソースではありません
  - OpenJDK は JDK の完全なオープンソース実装です
  - Java の継続的な開発は、Oracle Java 開発者による OpenJDK プロジェクトで行われています
- Java は「古い」言語です (Java 1996、Python 1991)
  - つまり枯れていて広く使用されており、ドキュメントが豊富ということです
- Java プログラマーは世界中の他のどの技術のプログラマーよりもたくさんいます
  - あなたを助け、指導してくれる人を見つけるのは簡単です
- Java（およびJVM言語のKotlin）はAndroid開発の基盤です

# Java Language Enhancements
p.8〜28 Java8以降のエンハンスメントの紹介
- このプレゼンテーションでは、Java言語のエンハンスメントについて説明します
- これらのエンハンスメントは、Java を取り巻く誤解の一部を払拭するのに役立ちます
- それはなぜJavaが現在の全レベルの学校で教えられるべき言語であるかについてです

## JShell
* 起動の仕方と簡単な説明くらいにとどめておく
    - なんか書きました。
        - https://github.com/mumian1014/MyFirstJava/blob/main/20230702_javajo.md 
## Launch Multi-File Source-Code Programs（JEP 458）
## Preview Features
## Implicitly Declared Classes and Instance Main Methods
## var
* JShellを使ったサンプル
## text blocks
* テキストのサンプルのみでよいのでは？（before, afterの比較）
## switch
* JShellのハンズオンとbefore,afterの比較
### an expression & without a break
### The pattern matching switch
## records
## Virtuous Virtual Threads

# What’s Pushing Java Aside?
p.29〜32 教育においてJavaが押し除けられている理由（教育現場でよく使われるJavaScript、Pythonとの比較）
- JavaScript
  - ダウンロードはわずか
  - 学校のすべてのPCのブラウザで利用可能
- Python
  - 2つの大きなトレンド（ビッグデータ、AI/ML）に関係する
  - Online Jupyter notepadが人気（有名）

## Machine Learning and Big Data VisiRec JSR 381
- Javaは機械学習の領域に進出しています
- AmazonのDeep Java Library（DJL）はJSR381の実装の一つです
- Javaツールの奥深さと幅広さにより、MLに最適なプラットフォームとなっています

## Why is Python widely used for AI/ML?
- Python は C で書かれているため、C ライブラリと簡単にやり取りできます
- 多くの AI/ML ライブラリは C で書かれているため、Python はより簡単にやり取りできます
- Java の弱点は他の言語とやり取りすることです
- Java 22 では、C ライブラリへのアクセスを大幅に簡素化する Foreign Function & Memory API があります

## The Java Virtual Machine – Home to More Than Java
- JVMはJava以外の言語にも使われています
- Kotlin、Scala、Groovy、Clojure など
- JVM 上で実行され、Java と Python 間の相互運用性をサポートする Jython と呼ばれる Python もあります

# Why teach Java to  students?
p.33 なぜ学生にJavaを教えるのか？
- 多くの金融機関はバックエンドの実行に Java を利用しています
- Twitter、LinkedIn、Amazon などが Java を使用しています
- あなたの将来は、あなたがどれだけ上手にコーディングできるかによって決まります
- キャリアの中でどんな言語でも扱えるように準備するために学ぶのに最適な言語です
- プログラミングの意味を学生に明確に理解させるのに最適な言語です

# Conclusion
p.34
学生や教師/教授に働きかけよう
- 学生に JUG に参加するよう勧める
- コンピュータ サイエンス プログラムの教員に JUG に参加するよう勧める
- コンピュータ サイエンスの学生協会に働きかける
- キャンパスで会議を開く
- 教師向けのリソースを宣伝する
- 教師/教授専用のセミナーや JUG 会議を開催する
- 教育に携わる
- 学生向けの Java ハッカソンを実施する
- なぜなら、学生はすぐにあなたの同僚になるからです
