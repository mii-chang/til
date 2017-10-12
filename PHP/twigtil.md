## PHP

### twig
- PHPのテンプレートエンジン

``` twig
{% block [blockName] %} 　<!--- HTMLのタグの名前を[blockName]に入れる -->
ブロックに入れる内容
{% endblock %} 
```
例えば

baseとなるtwigを作る

``` twig:base.twig
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{% block title %}twig base{% endblock %} twig! </title>
</head>
<body>
  <div id="header"> 
    {% block header %}
    <!-- ヘッダーに入れたいHTML -->
    {% endblock header %}
   </div>
  <div id="content">
    {% block content %}
    <!-- ページの中に入れたいHTML -->
    {% endblock %}
  </div>
  <div id="footer">
    {% block footer %}
    <!-- フッターに入れたいHTML -->
    {% endblock footer %}
  </div>
</body>
</html>
```

baseを元にして作りたい他ページのtwigをbaseを継承して作る

``` twig:testpage.twig
{% extends "base.html" %} <!-- baseを継承 -->

  {% block title %}
    テストページ！
  {% endblock %}
  {% block content %}
    <h1>test page!</h1>
    <p class="message">
      hello world!
   </p>
  {% endblock %}
```

継承先で変更を加えなかったものは、継承元の内容がそのまま表示される

twigを元にして出力されたHTML

``` html:testpage.html
<html>
<head>
    <title>テストページ！ twig!</title> <!-- baseで{% %}外に書いてた内容はそのまま残る -->
</head>
<body>
  <div id="header">
    <!-- ヘッダーに入れたいHTML -->
  </div>
  <div id="content">
    <h1>test page!</h1>
    <p class="message">
      hello world!
    </p>
  </div>
  <div id="footer">
    <!-- フッターに入れたいHTML -->
  </div>
</body>
</html>
```
