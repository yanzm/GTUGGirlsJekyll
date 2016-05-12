# Boostrap4 と組み合わせて GTUG Girls のサイトを作ろう

## 1. プロジェクト作成

```
$ jekyll new gtug_girls_site
$ cd gtug_girls_site
```

## 2. Bootstrap の設定

* http://v4-alpha.getbootstrap.com/getting-started/introduction/

_includes/head.html の head タグ内の /css/main.css の前に bootstrap の stylesheet と google fonts を追加します。

```html
<head>
  <meta charset="utf-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

  <title>{% if page.title %}{{ page.title | escape }}{% else %}{{ site.title | escape }}{% endif %}</title>
  <meta name="description" content="{% if page.excerpt %}{{ page.excerpt | strip_html | strip_newlines | truncate: 160 }}{% else %}{{ site.description }}{% endif %}">

  <!-- google font -->
  <link href="//fonts.googleapis.com/css?family=RobotoDraft:regular,bold,italic,thin,light,bolditalic,black,medium&amp;lang=en" rel="stylesheet" type="text/css">

  <!-- Bootstrap CSS -->
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-alpha.2/css/bootstrap.min.css" integrity="sha384-y3tfxAZXuh4HwSYylfB+J125MxIs6mR5FOHamPBG064zB+AFeWH94NdvaCBm8qnd" crossorigin="anonymous">

  <link rel="stylesheet" href="{{ "/css/main.css" | prepend: site.baseurl }}">
  <link rel="canonical" href="{{ page.url | replace:'index.html','' | prepend: site.baseurl | prepend: site.url }}">

</head>
```

_layout/default.html の body タグ内の最後に bootstrap の script タグを追加します。

```html
<!DOCTYPE html>
<html>

  {% include head.html %}

  <body>

    ...

    <!-- jQuery first, then Bootstrap JS. -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.4/jquery.min.js"></script>
	<script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-alpha.2/js/bootstrap.min.js" integrity="sha384-vZ2WRJMwsjRMW/8U7i6PWi6AlO1L79snBrmgiDpgIWJ82z8eA5lenwvxbMV1PAh7" crossorigin="anonymous"></script>
  </body>

</html>
```

## 3. テンプレートの変更

footer をつけないので削除します。

_layouts/default.html
```html
<!DOCTYPE html>
<html>

  {% include head.html %}

  <body>

    {% include header.html %}

    {{ content }}

    <script src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.4/jquery.min.js"></script>
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-alpha.2/js/bootstrap.min.js" integrity="sha384-vZ2WRJMwsjRMW/8U7i6PWi6AlO1L79snBrmgiDpgIWJ82z8eA5lenwvxbMV1PAh7" crossorigin="anonymous"></script>
  </body>

</html>
```

## 4. ヘッダー部分の変更

Bootstrap の Navbar を使うように変更します。

_includes/header.html
```
<nav class="navbar navbar-light bg-faded">
  <div class="container">
    <a class="navbar-brand" href="/">{{ site.title }}</a>
    <ul class="nav navbar-nav pull-xs-right">
      {% for my_page in site.pages %}
        {% if my_page.title %}
        <li class="nav-item">
          <a class="nav-link" href="{{ my_page.url | prepend: site.baseurl }}">{{ my_page.title }}</a>
        </li>
        {% endif %}
      {% endfor %}
    </ul>
  </div>
</nav>
```

## 5. meetup log ページの作成

about.md を削除して meetups.md を用意します。

```
---
layout: page
title: Meetup Log
permalink: /meetups/
---

<div class="main-content">
  <h3>第26回 GTUG Girls+PyLadiesTokyo Meetup 「初めての機械学習」</h3>
  <ul>
    <li>内容：機械学習</li>
    <li>開催日：2016年2月23日（火）19:00〜22:00（受付18:30〜）</li>
    <li>講師：<a href="https://twitter.com/a_macbee" target="_blank">@a_macbee</a> さん</li>
    <li>チューター：TBA</li>
    <li>会場：VOYAGE GROUP<br>東京都渋谷区神泉町8-16 渋谷ファーストプレイス8F<br><a href="http://voyagegroup.com/company/access/" target="_blank">http://voyagegroup.com/company/access/</a></li>
  </ul>
  <ul>
    <li>資料 : <a href="https://github.com/PyLadiesTokyo/intro_neural_network" target="_blank">PyLadiesTokyo/intro_neural_network</a></li>
    <li><a href="http://gtuggirls.connpass.com/event/26066/" target="_blank">第26回 GTUG Girls+PyLadiesTokyo Meetup 「初めての機械学習」 - connpass</a></li>
    <li><a href="https://groups.google.com/forum/#!topic/gtug-girls/pqdgjp4k2rE">Google Group : GTUG Girls</a></li>
  </ul>
</div>
```


## 6. index.html を変更

```html
---
layout: default
---

<div>

<div class="jumbotron jumbotron-fluid">
  <div class="container">
  	<img src="{{ "/img/gtug-girls.png" | prepend: site.baseurl }}">
  </div>
</div>

<div class="container main-content">
  <h1 class="m-b-2">Welcome to GTUG Girls</h1>
  <p>
      GTUG Girls は女性のテクノロジーコミュニティです。<br>
      実際に手を動かすことをモットーに、2ヶ月に1回程度初心者向けのハンズオンイベントを開催しています。<br>
      Canvas、WebGLなどHTML5系のものからAndroid、Go言語までさまざまな内容で行っています。<br>
      常に初心者向けのイベントなので、はじめての方でも大丈夫です。参加お待ちしています。<br><br>
      一緒にわいわい、がやがや、テクノロジーを楽しみましょう！
  </p>

  <h3 class="m-t-3">GTUG Girlsって何？</h3>
  <ul>
      <li>モノ・コトのしくみが気になる？</li>
      <li>ニューテクノロジーってクールだと思う？</li>
      <li>作ること好き？</li>
  </ul>
  <p>
    １つでもあてはまったあなたは GTUG Girl!<br>
    ガールズパワーでテクノロジーを乗りこなし、いままでにない何かを一緒につくろう！
  </p>
  </p>
    GTUG Girls への参加をご希望の方は、こちらのメーリングリストにご登録ください。<br>
    ＊女性のみです<br>
    <a href="https://groups.google.com/forum/#!forum/gtug-girls" target="new">Google Group : GTUG Girls<core-icon icon="launch"></core-icon></a>
  </p>

  <h3 class="m-t-3">次回のMeetup</h3>
  <p>
    次回のミートアップは『Jekyll』です！<br>
    Jekyllは静的Webページを生成するためのツールです。GitHubでWebページをホスティングできるGitHub Pagesと相性がよく、作ったページを簡単に公開することができます。
  </p>
  <h4 class="m-t-2">第27回 GTUG Girls Meetup 「Jekyllを使ってみよう」</h4>
  <ul>
    <li>内容：Jekyll</li>
    <li>開催日：2016年5月12日（木）19:00〜22:00（受付18:30〜）</li>
    <li>講師：<a href="https://twitter.com/yanzm" target="_blank">あんざいゆき</a> さん</li>
    <li>チューター：TBA</li>
    <li>会場：株式会社FiNC<br>東京都千代田区有楽町1-12-1 新有楽町ビル5F<br><a href="https://finc.com/contact/" target="_blank">https://finc.com/contact/</a></li>
    <li>詳細・お申し込み：<a href="http://gtuggirls.connpass.com/event/30374/" target="_blank">http://gtuggirls.connpass.com/event/30374/</a></li>
  </ul>

  <h3 class="m-t-3">最近のMeetup</h3>
  <p>
    2月23日（火）に26回目のMeetup 「初めての機械学習」を開催しました。
  </p>
  <ul>
    <li><a href="http://gtuggirls.connpass.com/event/26066/" target="_blank">第26回 GTUG Girls+PyLadiesTokyo Meetup 「初めての機械学習」 - connpass</a></li>
  </ul>
  <p>
    <a href="/meetups/">過去のMeetup一覧</a>
  </p>

  <h3 class="m-t-3">Staff募集</h3>
  <p>
    GTUG Girls の運営を手伝っていただけるスタッフを募集しています。<br>
    <a href="mailto:gtug-girls-staff@googlegroups.com">gtug-girls-staff@googlegroups.com</a> までメールいただくか、イベントでスタッフにお問い合わせください。
  </p>

</div>
```

## 7. 画像を用意

img フォルダを作成し、gtug-girls.png を配置する


## 8. main.css を用意

css/main.scss を削除して css/main.css を用意します。

```css
body {
  font-family: RobotoDraft, 'Helvetica Neue', Helvetica, Arial, "ヒラギノ角ゴ ProN","Hiragino Kaku Gothic ProN", "游ゴシック","Yu Gothic", "メイリオ","Meiryo", sans-serif;
  margin: 0;
  background-color: #f1f1f1;
}

.jumbotron {
  background-color: #ffffff;
}

h1 {
  font-weight: 100;
}

a {
  color: #1F8A99;
}

.main-content li {
  color: #666;
  padding: 5px 0;  
}

.post-header {
  padding: 20px 0;
}
```

