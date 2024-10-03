# switch

## 説明

- 式とbreakなしのJDK 14のスイッチ
    - 感覚的に説明できるスイッチ
    - 値を設定する際に使用するコードの重複を減らす
    - スイッチ式またはスイッチルール
    - breakの終わりで、すべてのケースが終了する！


## 元の英文の訳が分かりにくかったので、簡単に書くと以下

- 式とbreakなしのJDK 14のswitch
    - 感覚的に書ける
    - コード量を減らせる
    - スイッチ式またはswitchルール
        - https://openjdk.org/jeps/441 でswitch ruleって言葉出てるけどどれを指しているのかわからない・・・
    - 前まではbreakがないと次のcaseに行っていたが、新しい書き方の場合はbreakがなくても次のcaseに行かない


## どっちを教えたい/学びたい？
- 古い書き方と新しい書き方の比較

```
double value = 0;
switch (point) {
    case NORTH:
        value = 12.12;
        break;
    case SOUTH:
        value = 14.14;
        break;
    case EAST:
        value = 16.16;
        break;
    case WEST:
        value = 18.18;
        break;
}
```

↓

```
double value = switch (point) {
    case NORTH -> 12.12;
    case SOUTH -> 14.14;
    case EAST -> 16.16;
    case WEST -> 18.18;
    default -> 0.0;    
};
```


## 古い書き方

- 古い書き方だと、break文が多いため不必要に冗長になる
- それにより視覚的なノイズになってしまうため、break文の欠落が起こり、予想外に失敗に終わることがある
- 結果デバッグしにくいエラーを覆い隠してしまうことがある

例

```
switch (day) {
    case MONDAY:
    case FRIDAY:
    case SUNDAY:
        System.out.println(6);
        break;
    case TUESDAY:
        System.out.println(7);
        break;
    case THURSDAY:
    case SATURDAY:
        System.out.println(8);
        break;
    case WEDNESDAY:
        System.out.println(9);
        break;
}
```


## 新しい書き方

- スイッチのラベルが一致した場合にラベルの右側のコードのみが実行される
- 新しい形式のスイッチのラベルは"case L ->"
- カンマで区切られた複数の定数をケースごとに許可する

例

```
switch (day) {
    case MONDAY, FRIDAY, SUNDAY -> System.out.println(6);
    case TUESDAY                -> System.out.println(7);
    case THURSDAY, SATURDAY     -> System.out.println(8);
    case WEDNESDAY              -> System.out.println(9);
}
```


## switch式で値を返す

今までの書き方

```
int numLetters;
switch (day) {
    case MONDAY:
    case FRIDAY:
    case SUNDAY:
        numLetters = 6;
        break;
    case TUESDAY:
        numLetters = 7;
        break;
    case THURSDAY:
    case SATURDAY:
        numLetters = 8;
        break;
    case WEDNESDAY:
        numLetters = 9;
        break;
    default:
        throw new IllegalStateException("Wat: " + day);
}
```

- 今までの書き方だと
    - 表現が回りくどい
    - 繰り返しが多い
    - 間違いが起こりやすい
- 新しい書き方だと
    - 直接表現できるから明確で安全

新しい書き方

```
int numLetters = switch (day) {
    case MONDAY, FRIDAY, SUNDAY -> 6;
    case TUESDAY                -> 7;
    case THURSDAY, SATURDAY     -> 8;
    case WEDNESDAY              -> 9;
};
```


## yield（説明いらないかも）

- ほとんどのswitch式では、switchラベルの右側には1つの式が存在する
- 式ではなくブロックが必要な場合は、yieldが必要

```
int j = switch (day) {
    case MONDAY  -> 0;
    case TUESDAY -> 1;
    default      -> {
        int k = day.toString().length();
        int result = f(k);
        yield result;
    }
};
```


## 手を動かすのに使えそうな簡単な例

```
static void howMany(int k) {
    switch (k) {
        case 1  -> System.out.println("one");
        case 2  -> System.out.println("two");
        default -> System.out.println("many");
    }
}

howMany(1);
howMany(2);
howMany(3);
```

```
static void howMany(int k) {
    System.out.println(
        switch (k) {
            case  1 -> "one";
            case  2 -> "two";
            default -> "many";
        }
    );
}
```


## Java 21でのパターンマッチングのswitch

```
Object x = "4";
String designation = switch (x) {
    // case Integer i when i > 4 && i < 12 -> "child";
    case Integer i when i < 12 -> "child";
    case Integer i when i < 18 -> "teenager";
    case Integer i when i < 25 -> "young adult";
    case Integer i when i < 65 -> "adult";
    case Integer i when i >= 65 -> "senior";
    default -> "Not an Integer";
};
System.out.printf("Designation is %s%n", designation);
```


## 今までの書き方

- Java 16（JEP394）で登場したinstanceof演算子を拡張し、型パターンを受け取ってパターンマッチングを実行する必要があった
- 過度に一般的な制御構造（プログラムの構造）を使用しているため、コーディングエラーが隠れたままになる

```
static String formatter(Object obj) {
    String formatted = "unknown";
    if (obj instanceof Integer i) {
        formatted = String.format("int %d", i);
    } else if (obj instanceof Long l) {
        formatted = String.format("long %d", l);
    } else if (obj instanceof Double d) {
        formatted = String.format("double %f", d);
    } else if (obj instanceof String s) {
        formatted = String.format("String %s", s);
    }
    return formatted;
}
```


## 新しい書き方

- 最適な書き方ができる
- switch文やswitch式を拡張して任意の型で動作するようになり、case定数だけでなくパターンを含むラベルを許可するようになる

```
static String formatterPatternSwitch(Object obj) {
    return switch (obj) {
        case Integer i -> String.format("int %d", i);
        case Long l    -> String.format("long %d", l);
        case Double d  -> String.format("double %f", d);
        case String s  -> String.format("String %s", s);
        default        -> obj.toString();
    };
}
```


## switchとnull

今までの書き方

```
static void testFooBarOld(String s) {
    if (s == null) {
        System.out.println("Oops!");
        return;
    }
    switch (s) {
        case "Foo", "Bar" -> System.out.println("Great");
        default           -> System.out.println("Ok");
    }
}
```

新しい書き方

```
static void testFooBarNew(String s) {
    switch (s) {
        case null         -> System.out.println("Oops");
        case "Foo", "Bar" -> System.out.println("Great");
        default           -> System.out.println("Ok");
    }
}
```


## 参考
- https://openjdk.org/jeps/361
- https://openjdk.org/jeps/441
- 必要であればよこなさんの資料の絵での説明みたいなのも導入する
    - https://speakerdeck.com/ihcomega56/jep-455

