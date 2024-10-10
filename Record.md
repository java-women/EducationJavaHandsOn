# Record

# 説明
（Java14~Preview ,Java16~正式リリース）  
これまでの値を受け渡すBeanに新しい書き方が増えた話。  
現代のプログラミングモデルは、可変クラスではなく、不変のBeanに移行しているので、簡単に対応できるようになった。
- JavaBeans:可変Beanを取り扱う。  Record:不変Beanを取り扱う。
- セッター、ゲッター、hashCode、equals、toStringメソッド →　Recordは、コンストラクタ、ゲッター、hashCode、equals、toStringのみ。（セッターが削除）

不変データオブジェクトをアプリケーションの基本として考えていく。

## メリット
- コードの記述量が減る
- コードの可読性が上がる

## 制約
- Recordのインスタンスフィールド(Recordヘッダに記述されたコンポーネントに対応)は暗黙的にfinalである
- 他のインスタンスフィールドを持つことはできない
- 他のクラスをextend（継承）することはできない
- Recordクラスは暗黙的にfinalである。   
- Recordはabstractとして宣言できない

## Recordの使用ポイント
- データ転送オブジェクト（DTO）: APIレスポンスやデータベース結果のマッピングに最適
- 複数の戻り値: メソッドから複数の値を返す際に、アドホックなタプルの代わりに使用可能
- イミュータブルな値オブジェクト: 日付範囲や座標など、変更不可能な値を表現するのに最適
- パターンマッチング: Java 16以降で導入されたパターンマッチング機能と組み合わせて使用　（これが一番のモチベ）


### 以下、スライドの説明文を翻訳した内容（スライド時には削除）
JavaBeanスタイルのクラスは、データを保持するための設計として広く使われてきました。  
多くのフレームワークは、セッター、ゲッター、hashCode、equals、toStringメソッドを備えたクラスに依存しています。  
しかし、現代のプログラミングモデルは、可変クラスではなく、不変のBeanに移行しています。  
不変のデータオブジェクトはコンストラクタで初期化され、ゲッターだけを持ちます。
新しいrecordクラスは、コードの記述量を減らし、不変性を奨励します。不変のデータオブジェクトがアプリケーションの中心となるでしょう。

インスタンス変数はクラス宣言の後ではなく、クラスのシグネチャ内にリストされます。これらのインスタンス変数は自動的にprivateです。
注目すべき点として、セッターが存在せず、これによりオブジェクトが不変になります。また、ゲッターはありませんが、変数名を使用してインスタンス変数の値を読み取ることができます。
hashCode、equals、toStringはデフォルトで用意されています。新しいコンパクトコンストラクタでは、必要に応じてバリデーションも行えます。


# personクラスを作ってみよう
名前と年齢と住所を持った人を表すオブジェクトを書いてみよう！
## これまで

```java
public class Person {
    private final String name;
    private final int age;
    private final String address;

    public Person(String name, int age, String address) {
        this.name = name;
        this.age = age;
        this.address = address;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public String getAddress() {
        return address;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Person person = (Person) o;
        return age == person.age &&
               Objects.equals(name, person.name) &&
               Objects.equals(address, person.address);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, age, address);
    }

    @Override
    public String toString() {
        return "Person{" +
               "name='" + name + '\'' +
               ", age=" + age +
               ", address='" + address + '\'' +
               '}';
    }
}
```

## これから
```java
public record Person(String name, int age, String address) {
    // コンストラクタ、getter、equals、hashCode、toStringが自動生成される
}
```

##　　JShellでやってみよう
```java
public record Person(String name, int age, String address) {}
```
```java
// インスタンスの自動生成 
var marika = new Person("marika",34,"Tokyo");
```
```java
// フィールドへのsetter禁止
marika.setName("Shiotsuki");
// error
|  エラー:
|  シンボルを見つけられません
|    シンボル:   メソッド setName(java.lang.String)
|    場所: タイプPersonの変数 marika
|  marika.setName("Shiotsuki");
|  ^------------^
```
```java
// フィールドのgetter生成
marika.age();
// result
$3 ==> 34
```
```java
// toString()メソッドの自動実装
System.out.println(marika); 
// result
$4 ==> Person[name=marika, age=34, address=Tokyo]
```
```java
// レコード型かの確認
System.out.println(Person.class.isRecord()); 
// result
$5 ==> true
```
```java
// レコード型の場合のクラスの形取得
var components = Person.class.getRecordComponents();
for (var component : components) {
    System.out.println(component.getName() + ": " + component.getType().getSimpleName());
}
// result
$6 ==> name: String
$7 ==> age: int
$8 ==> address: String
```

## 参考
https://www.infoq.com/jp/articles/java-14-feature-spotlight/