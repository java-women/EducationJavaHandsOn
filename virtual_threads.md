# Virtuous Virtual Threads

## 説明

- OSスレッドではなくJavaスレッド
- JDK 21

```
 public class VirtualThreadClass extends Thread { . . }

 public void perform() {
      for (int i = 0; i < 5; ++i) {
         Thread.ofVirtual().name("Thread # " + i).
            start(new VirtualThreadClass());
}
```


## 簡単にいうと

- Java プラットフォームに導入された仮想スレッドのこと
- この仮想スレッド（Virtual Threads）は軽量スレッドであり、高スループットの同時実行アプリケーションの作成、保守、監視の労力を大幅に削減する
- JDK 21から


## 今までの書き方、プラットフォーム・スレッドとは

- OSスレッドの薄いラッパー
- 基盤となるOSスレッド上でJavaコードを実行する
- プラットフォーム・スレッドの存続期間中ずっとOSスレッドを保持する
- このため、使用可能なプラットフォーム・スレッドの数はOSスレッドの数に制限される


## 新しい書き方、仮想スレッド（Virtual Threads）とは

- プラットフォーム・スレッドと同様に、仮想スレッドもjava.lang.Threadのインスタンス
- 仮想スレッドは特定のOSスレッドに関連付けられないにもかかわらず、仮想スレッドはOSスレッド上でコードを実行する
- 仮想スレッドで実行されているコードがブロッキングI/O操作をコールすると、Javaランタイムは、再開できるまで仮想スレッドを一時停止する
- 一時停止された仮想スレッドに関連付けられていたOSスレッドは解放され、他の仮想スレッドの操作を実行できる


## 参考
- https://b.chiroito.dev/entry/virtualthreads1
- https://openjdk.org/jeps/444
- https://docs.oracle.com/javase/jp/21/core/virtual-threads.html#GUID-2BCFC2DD-7D84-4B0C-9222-97F9C7C6C521
- https://iikanji.hatenablog.jp/entry/2024/02/26/171731
    - これわかりやすかった

