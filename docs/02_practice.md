# Jekyllの使い方

## Jekyllプロジェクトを作成する

jekyll new [project name] でプロジェクトディレクトリを作成します。

```
$ jekyll new myblog
```

作成されたディレクトリに移動して中身を見てみましょう。
いくつかのファイルが自動で作成されています。

```
$ cd myblog
$ ls
_config.yml	_layouts	_sass		css		index.html
_includes	_posts		about.md	feed.xml
```

ローカルサーバーで現在のディレクトリのプロジェクトを表示できます。表示先は http://localhost:4000 です。

```
$ jekyll serve
```

jekyll serve 中にファイルを変更すると、自動でサイト用のファイルも更新されます。ただし、_config.ymlだけは別で、jekyll serve をやり直す必要があります。

Ctrl + c で jekyll serve を止めて、再度ディレクトリの中身を確認してみましょう。

```
$ ls
_config.yml	_layouts	_sass		about.md	feed.xml
_includes	_posts		_site		css		index.html
```

新しく _site というディレクトリが作成されています。ここはサイト用に生成されたファイルが格納される場所です。最終的にはこの中身をサーバーにデプロイしてサイトを公開します。



## プロジェクト構成

```
.
├── _config.yml # 設定ファイル
├── _includes   # 複数のページで利用するページの一部
|   ├── footer.html
|   ├── head.html
|   ├── header.html
|   ├── icon-github.html
|   ├── icon-github.svg
|   ├── icon-twitter.html
|   └── icon-twitter.svg
├── _layouts    # markdownのデータを流し込むテンプレート
|   ├── default.html
|   ├── page.html
|   └── post.html
├── _posts      # ブログ記事のような動的コンテンツデータ
|   └── 2016-05-10-welcome-to-jekyll.markdown
├── _sass       # テンプレートなどで利用するSASS
|   ├── _base.scss
|   ├── _layout.scss
|   └── _syntax-highlighting.scss
├── _site       # 生成された静的サイトの配置場所
├── about.md    # Aboutページのデータ
├── css         # css に変換されて _site に配置される
|   └── main.scss
├── feed.xml    # RSS登録用のXML
└── index.html  # トップページ
```

### YAML Front Matter

Jekyll では、ファイルの先頭にハイフン3つで囲まれた正しいYAML形式のブロックがあると、それを特別なファイルと認識して処理します。このブロック部分をFront Matterと呼びます。

例えば index.html を見ると、先頭に次のような Front Matter があります。ここではあらかじめ用意されている変数（以下だと layout）に値をセットして、このページの設定を行います。用意されている変数は https://jekyllrb.com/docs/frontmatter/ の Predefined Global Variables の表にあります。

```
---
layout: default
---
```

ここでは layout に default を指定しているので、この index.html では _layout/default.html が利用されます。


### Liquid template language

index.html 全体を見てみましょう。

```
---
layout: default
---

<div class="home">

  <h1 class="page-heading">Posts</h1>

  <ul class="post-list">
    {% for post in site.posts %}
      <li>
        <span class="post-meta">{{ post.date | date: "%b %-d, %Y" }}</span>

        <h2>
          <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
        </h2>
      </li>
    {% endfor %}
  </ul>

  <p class="rss-subscribe">subscribe <a href="{{ "/feed.xml" | prepend: site.baseurl }}">via RSS</a></p>

</div>
```

YAML Front Matter に続いてコンテンツ部分である <div> タグがあります。
この中に ```{% for post in site.posts %}``` や ```{{ post.date | date: "%b %-d, %Y" }}``` という {} を使った記述があります。
この部分は Liquid template language です。

* https://github.com/Shopify/liquid/wiki
* [Liquid template language](https://help.shopify.com/themes/liquid/basics)

```{% for post in site.posts %}...{% endfor %}``` は Liquid template language の Tag、```{{ post.title }}``` は Object、```{{ post.date | date: "%b %-d, %Y" }}``` は Filter です。

ここの処理では、site.posts の数だけ <li> タグを作るようになっています。




### Templates

テンプレートファイルは _layout ディレクトリに置きます。テンプレートファイルの中の ```{{ content }}``` 部分が、そのテンプレートを利用するコンテンツに置き換わります。

例えば、index.html では _layout/default.html がテンプレートとして指定されています。

_layout/default.html を見ると次のようになっており、```{{ content }}``` 部分が ```<div class="home">...</div>``` に置き換えられた index.html が _site ディレクトリに生成されます。

```
<!DOCTYPE html>
<html>

  {% include head.html %}

  <body>

    {% include header.html %}

    <div class="page-content">
      <div class="wrapper">
        {{ content }}
      </div>
    </div>

    {% include footer.html %}

  </body>

</html>
```

```{% include head.html %}``` と記述すると、この部分が _includes/head.html に置き換わります。


### SASS

Jekyll では YAML Front Matter がついたSASSファイル（.scss ファイル）をCSSに変換してくれます。

css/main.scss を見ると、以下のような YAML Front Matter がついています（# の行はコメントです）。

```
---
# Only the main Sass file needs front matter (the dashes are enough)
---
...

// Import partials from `sass_dir` (defaults to `_sass`)
@import
        "base",
        "layout",
        "syntax-highlighting"
;
```

このため、この SASS ファイルが変換されて _site/css/main.css が生成されます。

css/main.scss の最後には @import で外部の SASS ファイルが指定されています。import 対象の SASS ファイルは _sass ディレクトリに配置します。実際、_sass ディレクトリには _base.scss, _layout.scss, _syntax-highlighting.scss が配置されています。



### Post

* [The Posts Folder](https://jekyllrb.com/docs/posts/)

_post にはブログのエントリーのような動的なページコンテンツを配置します。
ファイルの名前は
```
YYY-MM-DD-name-of-post.ext
```
にする必要があります。
例えば
```
2016-05-10-welcome-to-jekyll.markdown
```
のようになります。


以下のファイルを _posts に作成してみましょう。

ファイル名: 2016-05-12-my-first-jekyll.markdown
中身:
```
---
layout: post
title:  "My First Jekyll!"
date:   2016-05-12 19:00:00 +0900
---

Hello Jekyll
```

jekyll serve すると（すでに他のターミナルでしている場合は再起動する必要はありません、単にブラウザのページをリロードしてください）、トップページに My First Jekyll! というリンクが増えます。

_site を確認すると、_site/2016/05/12/my-first-jekyll.html というファイルが生成されています。


### Config

_config.yml は設定ファイルです。
あらかじめ用意されている設定項目は https://jekyllrb.com/docs/configuration/ に記載されています。

あらかじめ用意されている項目以外に site.XX として他のページで Liquid Object として参照できる変数を定義できます。

例えば _config.yml に以下のように設定されていると、
```
twitter_username: jekyllrb
```
テンプレートやコンテンツで
```
{{ site.github_username }}
```
のように使うことができ、この部分が jekyllrb に置き換えられます。






