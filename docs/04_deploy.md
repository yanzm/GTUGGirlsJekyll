# Github pages で公開する

github pages では、 User や Organization 用のサイトと、プロジェクト用のサイトを作ることができます。

* https://help.github.com/articles/user-organization-and-project-pages/

## User や Organization 用のサイト

User や Organization 用のサイトを作るには、決まった名前のリポジトリ `[name].github.io` を作り、master ブランチにサイト用のコンテンツを置きます。

例えば github の GTUGGirls Organization (https://github.com/GTUGGirls) 用のサイトは GTUGGirls.github.io リポジトリに作ります。


## プロジェクト用のサイト

ライブラリなど、プロジェクト用のサイトを作るには、プロジェクトのリポジトリに `gh-pages` ブランチを作り、そこにサイト用のコンテンツを置きます。


## GitHub Pages with Jekyll 3.0

Github では Issue などで markdown を使っていますが、同じような記述方法で Jekyll でWebページを作ることができます。

* https://github.com/blog/2100-github-pages-jekyll-3
* https://help.github.com/articles/using-jekyll-as-a-static-site-generator-with-github-pages/








### サンプルリポジトリを用意する

https://github.com/new からサンプル用のリポジトリを用意します。リポジトリ名はなんでも良いです。jekyllsample とか。Public を選択し、Initialize this repository with a README にチェックして Create repository をクリックします。

作成したら `git clone` します。

```
$ git clone git@github.com:[username]/jekyllsample.git
$ cd jekyllsample
```

jekyll プロジェクトを現在のディレクトリに作ります。

```
$ jekyll new .
```

.gitignoreファイルを用意します。ローカルで見た目をチェックするために jekyll serve すると _site/ が作られますが、これは github pages 用のリポジトリに入れる必要はないので .gitignore で無視する対象に指定しておきます。

.gitignore
```
_site/
.sass-cache/
```

gh-pages ブランチを作成し、commit して push します。

```
$ git checkout -b gh-pages
$ git add -A
$ git commit -m 'first commit'
$ git push origin gh-pages
```

http://[username].github.io/jekyllsample/

を確認すると、Jekyll から生成されたページが表示されます。
しかし、css がうまく当たっておらずレイアウトが崩れています。
これはプロジェクト用の github pages でURLと階層構造が一致しないからです。

これを解決するために、_includes/head.html の /css/main.css への prepend を site.baseurl から site.github.url に変更します。

```
  <link rel="stylesheet" href="{{ "/css/main.css" | prepend: site.baseurl }}">
を
  <link rel="stylesheet" href="{{ "/css/main.css" | prepend: site.github.url }}">
に変更
```

変更を commit して push します。

```
$ git add -A
$ git commit -m 'fix css path'
$ git push origin gh-pages
```

http://[username].github.io/jekyllsample/

をリロードすると、css が正しく参照されてレイアウトが直ります。


まだ問題があります。About や Post へのリンクをタップしても 404 になります。これも css と同じ問題です。

* _includes/head.html
* _includes/header.html
* index.html
* feed.xml

内の site.baseurl も site.github.url に変更しましょう。



