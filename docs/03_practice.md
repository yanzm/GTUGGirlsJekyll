# markdown の変換を体験しよう

* [Mastering Markdown](https://guides.github.com/features/mastering-markdown/)
* [Markdown tutorial](http://www.markdowntutorial.com/)

## markdown ファイルを作成する

about.md と同じ階層に practice.md を作成します。

practice.md
```markdown
---
layout: page
title: Practice
permalink: /practice/
---

```

保存すると、http://localhost:4000/ の右上 About の隣に Practice が追加されているので、クリックしてこのページを表示します。


## markdown 記法が html タグに変換されるのを確認する

practice.md に markdown 記法を追加して、つどリロードしてみましょう。

### Headers

```markdown
---
layout: page
title: Practice
permalink: /practice/
---

# h1

## h2

### h3

#### h4

##### h5

```

デベロッパーツールを開いて、markdown 部分がどのような html タグに変換されたか確認しましょう。




### Emphasis

```markdown
---
layout: page
title: Practice
permalink: /practice/
---

...

*This text will be italic*
_This will also be italic_

**This text will be bold**
__This will also be bold__

_You **can** combine them_

```



### Lists

```markdown
---
layout: page
title: Practice
permalink: /practice/
---

...

* Item 1
* Item 2
  * Item 2a
  * Item 2b

1. Item 1
2. Item 2
3. Item 3
   * Item 3a
   * Item 3b

```


### Images

```markdown
---
layout: page
title: Practice
permalink: /practice/
---

...

![Image of Yaktocat](https://octodex.github.com/images/yaktocat.png)

```


### Links

```markdown
---
layout: page
title: Practice
permalink: /practice/
---

...

[GitHub](http://github.com)

```



### Blockquotes

```markdown
---
layout: page
title: Practice
permalink: /practice/
---

...

As Kanye West said:

> We're living the future so
> the present is our past.

```



### Inline code

```markdown
---
layout: page
title: Practice
permalink: /practice/
---

...

I think you should use an
`<addr>` element here instead.

```



### Block code

```markdown
---
layout: page
title: Practice
permalink: /practice/
---

...


```java
public class MainActivity {

  private String name;

  public void setName(String name) {
    this.name = name;
  }

  public String getName() {
    return name;
  }
}
```

```html
<!DOCTYPE html>
<html>
 <head></head>
 <body>
   <div class="main">
   </div>
 </body>
</html>
```

```javascript
function fancyAlert(arg) {
  if(arg) {
    $.facebox({div:'#foo'})
  }
}
```

```


### Tables

```markdown
---
layout: page
title: Practice
permalink: /practice/
---

...

First Header | Second Header
------------ | -------------
Content from cell 1 | Content from cell 2
Content in the first column | Content in the second column

```


### Strikethrough

```markdown
---
layout: page
title: Practice
permalink: /practice/
---

...

~~this~~

```



