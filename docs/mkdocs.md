# mkdocsに関するまとめ

mkdocsはいわゆる静的サイトジェネレータの一つ。Python製で、コンテンツをmarkdownで記述する。
For full documentation visit [mkdocs.org](http://mkdocs.org).

## インストール

1. install python and pip
2. install mkdocs with pip

        pip install mkdocs

## ディレクトリ構成

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.

## 設定ファイル`mkdocs.yml`

* トップページのファイル名は常にindexでないといけない。
* 対応する拡張子は`markdown`、`mdown`、`mkdn`、`mkd`、`md`。

```
pages:
- Home: 'index.md'
- User Guide:
    - 'Writing your docs': 'user-guide/writing-your-docs.md'
    - 'Styling your docs': 'user-guide/styling-your-docs.md'
- About:
    - 'License': 'about/license.md'
    - 'Release Notes': 'about/release-notes.md'
theme: readthedocs
```

### カスタムCSS

`extra_css`で外部CSSを設定できる。

    extra_css:
        - "css/extra.css"

### コードハイライト

`markdown_extensions`でコードブロックに色付けできる。行番号をつけたい場合は`linenums`を`true`に。

    markdown_extensions:
      - codehilite:
          linenums: true

## テーマ

`readthedocs`と`material`が2大テーマっぽい。
`readthedocs`は標準で導入されているため即時で利用可能だが、`material`はインストールする必要あり。


### `material`テーマ
公式サイトは[Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)。インストールはpipで。

    pip install mkdocs-material



## PDF出力

mkdocsにはmarkdownをPDF形式で出力する機能はない。そのため、PDF出力するためにはmkdocsのコンテンツを何らかの方法で変換する必要がある。ここでは次の方法について記載する。

* `mkdocs-pandoc`と`pandoc`
* `wkhtmltopdf`

### wkhtmltopdf

`wkhtmltopdf`はhtmlをPDFに変換するコマンドラインツール。インストールは[公式サイト](https://wkhtmltopdf.org/)から、Windowsはインストーラ、Linuxはパッケージを入手できる。

まずはmkdocsでHTMLを出力し、出力された各index.htmlをPDFに変換する。

    mkdocs build
    wkhtmltopdf site/your_page/index.html youe_page.pdf

私の思うこの方法のメリット／デメリットは以下の通り。

* メリット
    * mkdocsのテーマをそのまま出力するため、きれいなPDFファイルにできること
    * フォントなど日本語周りの設定も考慮不要で手軽であること
* デメリット
    * 単一のhtmlしか変換できないため、すべてのコンテンツを一つのPDF化ファイルに出力したい場合は各htmlをPDF化→PDFの結合作業が必要になること
    * `material`テーマ使用時は、検索やナビゲーションバーなどPDFには不要な要素も含めて出力されること

## 章番号を表示する

`material`テーマのデフォルト見出しは、`h1`と`h2`を区別しづらかったり、パッと見たときのレベルが分かりづらいため章番号をつける。
章番号はCSSで自動裁判するのが便利。

CSSで章番号をつけるには、counterを利用する。詳しくは以下のサイトで。
[CSSで見出し要素(h1, h2...)の前に自動で採番する方法](https://qiita.com/itagakishintaro/items/437418f917cc31de10cd)

`material`テーマに適用するため、次の記述を追加している。

* `h1`要素の指定に`.md-typeset`を追加
* 疑似要素`::before`の指定に`[id]`を追加
* 疑似要素`::before`に`display: inline;`を追加（デフォルトで指定されている`display: block;`を上書きするため）

```css
html {
    counter-reset: chapter;
}

.md-typeset h2 {
    counter-reset: sub-chapter;
}

.md-typeset h3 {
    counter-reset: section;
}

.md-typeset h2[id]::before {
    display: inline;
    counter-increment: chapter;
    content: counter(chapter) ". ";
}

.md-typeset h3[id]::before {
    display: inline;
    counter-increment: sub-chapter;
    content: counter(chapter) "." counter(sub-chapter) ". ";
}

.md-typeset h4[id]::before {
    display: inline;
    counter-increment: section;
    content: counter(chapter) "." counter(sub-chapter) "." counter(section) ". ";
}
```

## 拡張機能: admonition

警告文やメモを目立つスタイルで表示するプラグイン。materialテーマをインストールしていれば、`mkdocs.yml`に以下を追記するのみで利用できる。

```
markdown_extensions:
    - admonition
```

!!! Note
    materialテーマをインストールしていれば`mkdocs.yml`での設定のみで利用可能。

標準で利用できるパターンは[公式サイト](https://squidfunk.github.io/mkdocs-material/extensions/admonition/)を参照。




