# Record

# 説明
（Java14~Preview ,Java16~正式リリース）  
これまでの値を受け渡すBeanの考え方が変わった話。  
- 可変Bean → 不変Bean
- セッター、ゲッター、hashCode、equals、toStringメソッド →　コンストラクタで初期化され、ゲッター、hashCode、equals、toStringのみ。（セッターが削除）

不変データオブジェクトをアプリケーションの基本として考えていく。

## メリット
- コードの記述量が減る
- コードの可読性が上がる


### 以下、スライドの説明文を翻訳した内容
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
var marika = new Person("marika",34,"Tokyo");
```
```java
marika.setName("Shiotsuki");
```
これが出たらOK！

```java
|  エラー:
|  シンボルを見つけられません
|    シンボル:   メソッド setName(java.lang.String)
|    場所: タイプPersonの変数 marika
|  marika.setName("Shiotsuki");
|  ^------------^
```
```java
marika.age();
これが出たらOK！
```
```java
$3 ==> 34
```