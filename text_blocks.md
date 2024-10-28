# text blocks

## 説明

- ソースコードに入力されたものが、そのままソースコードに反映される
- HTML、XML、JSONを含む文字列には特に便利
- 引用符を3つ並べて書くのが嫌いな人はいるだろうか？


## 昔の書き方

```
String htmlStr = "<html><head><link rel='stylesheet' "
   + "href='styles/main.css' "
   + "type='text/css'/><title>The Learning Servlet</title></head>"
   + "<body><h1>GET method</h1>"
   + "<form id='form:index' action='index.html'>"
   + "<br/><input type='submit' value='Return to Home page'/></form>"
   + "</body></html>";
```


## JDK 15からのText Blockを使った新しい書き方

```
String htmlStr = """
  <html>
     <head>
        <link rel='stylesheet'href='styles/main.css' type='text/css’/>
        <title>The Learning Servlet</title>
     </head>
     <body>
        <h1>GET method</h1>
        <form id='form:index' action = 'index.html'>
           <br/>
           <input type= 'submit' value='Return to Home page' />
        </form>
     </body>
  </html>""";
```


## String formatted
- Stringテキスト ブロック機能の一部として、クラスにいくつかの新しいメソッドが追加された

```
out.println("""
  <html>
    <head>
      <title>Just Servlet Output</title>
      <link rel='stylesheet' href='styles/main.css' type= 'text/css'/>
      </head>
    <body>
      <h1>Thanks for joining our email list</h1>
      <p>Here is the information that you entered:</p>
      <label>Email:</label>
      <span>%s</span>
    </body>
  </html>""".formatted(user.getEmailAddress()));
```


## 参考

- https://openjdk.org/jeps/378
    - 例が長すぎてスライドに入らなかった場合、JEPに載ってる例を使った方が良さそう
- https://www.ne.jp/asahi/hishidama/home/tech/java/textblock.html#h_overview

