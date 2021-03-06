<!-- omit in toc -->
# 独房改善備忘録

<!-- omit in toc -->
# 独房改善備忘録 | yaru.belza.ga

──*きったないワンルームをあらゆる工夫でまともな環境にしたかった一部始終（建設中）*

<!-- omit in toc -->
## 概要

漢[**ベルザ**が](https://belza.ga)ボロアパートの一室（汚部屋）改善を[**やる**](https://yaru.belza.ga)ブログ。  
投稿する記事などをこのリポジトリで管理している。

<!-- omit in toc -->
## 説明書きの構成

- [一連のシステムの構成](#一連のシステムの構成)
- [ディレクトリ構造とファイルの説明](#ディレクトリ構造とファイルの説明)
- [Markdown記法の記事の構造](#markdown記法の記事の構造)
  - [記事全体の構造](#記事全体の構造)
  - [記事内メタデータ](#記事内メタデータ)
  - [冒頭部分](#冒頭部分)
  - [冒頭終了コメント](#冒頭終了コメント)
  - [もくじ](#もくじ)
  - [主部分](#主部分)
  - [記事終了コメント](#記事終了コメント)
- [コミット時メッセージのきまり](#コミット時メッセージのきまり)
  - [基本の体裁と文字列の意味](#基本の体裁と文字列の意味)
  - [特殊な文字列とその意味](#特殊な文字列とその意味)
  - [コミット時コメントの例](#コミット時コメントの例)
- [著者](#著者)
- [バージョン](#バージョン)
- [更新履歴](#更新履歴)

## 一連のシステムの構成

- ブログサービス: Seesaaブログ
  - 無料で利用
  - freenomの無料ドメインで独自ドメイン化している
- テキストエディタ: VSCode
- 画像ストレージ: Amazon Photos
  - 予定
- 記事管理: git
- 記事のバックアップ的な: GitHub
- HTML化や記事の投稿など: 手作業…
  - Github Actions + XML-RPCを用いてCI/CD環境を構築したい
- そのほかAmazonアソシエイトや楽天アフィリエイトなど小手先のやつ

## ディレクトリ構造とファイルの説明

```リポジトリのディレクトリ構造
yaru
├── .markdownlint.json
├── README.md
├── .backup
│   └── .stylesheet*.css
└── articles
    └── *.md
```

- `.markdownlint.json`: VSCodeで利用している拡張機能の設定ファイル
- `README.md`: この説明書き
- `.backup/.stylesheet*.css`: Seesaaブログて適用しているブログテーマのCSSファイル
- `articles/*.md`: `yyyyMMdd-a-summary-of-this-article.md`な命名方式のMarkdownファイル
  - HTMLファイルに変換されてからブログに投稿される記事
  - ファイル名のうち拡張子より前の部分は記事のURLとなる

## Markdown記法の記事の構造

SeesaaブログがMarkdown記法に対応していないため、HTML形式に変換し投稿する。

<p>
<details>
<summary><strong>記事のデータ構造</strong>（クリックで開く）</summary>
<div>

```記事のデータ構造
<!--! metadata
    id: 4444
    url: @ITSELF!
    idea: "トースタ改造電子化アプリ制御考察"
    title: "Catolixトースターを改造してスマホから操作したりできるか検討【激安IoTシリーズ】"
    author: "ルター"
    category: @DEFAULT
    label: @NULL!
    hashtag: @NULL!
    keyword: @NULL!
    description: @NULL!
    genre: @DEFAULT
    posted_at: 20210404164440
    updated_at: 20210414041604
    country: @JA!
    note: @WIP!
!-->

IoT家電には憧れがあるがAPIが非公開でプロプライエタリなアプリを用いた操作を強いられるのが嫌だ。日本メーカーだとベンダロックインをカマされて金もかかりそうな気がする。  
このシリーズは既製品の激安家電を電子改造し、なんとかしてIoT化できないか試みる。
今回は、ご存知Catolixブランドの激安トースターについて考察。

<!--! readmore !-->
<!-- omit-in-toc -->
#### もくじ  

---

- [Catolixトースターの全貌](#Catolixトースターの全貌)  
  - [メーカーの説明](#メーカーの説明)
  - [トースターの内部構造](#トースターの内部構造)
- [まとめ](#まとめ)  

---

#### Catolixトースターの全貌

なんちゃらかんちゃらうんぬんかんぬん

##### メーカーの説明

Catolixはすごいぜ！

##### トースターの内部構造

汎用的だなあ

#### まとめ

余裕でIoTできそう！

<!--! end-of-article !-->

```

</div>
</details>
</p>

### 記事全体の構造

記事は、:

- 記事内メタデータ
- 冒頭部分
- 冒頭終了コメント
- もくじ
- 主部分
  - 段落部分の集合
  - まとめ
- 記事終了コメント

の構造を持つ。

### 記事内メタデータ

記事内メタデータは、記事固有の情報をHTMLのコメントアウトを用いて冒頭に記述したものである。  
`<!--! metadata !-->`と記述し、一般のHTMLコメントアウトと区別する。  
いまのところ14のプロパティを持っている。

<p>
<details>
<summary><strong>記事内メタデータのプロパティ</strong>（クリックで開く）</summary>
<div>

- `id`: 1以上の固有の整数・記事のID
- `url`: 固有の文字列・ドメイン以下の記事のURL
  - `@ITSELF!`はファイルの名前を示す
- `idea`: 固有の文字列・内容の要約
- `title`: 固有の文字列・タイトル
- `author`: 文字列・著者
  - ベルザのブログなので原則`"ベルザ"`を指定する
- `category`: 文字列・Seesaaブログ内のカテゴリ
  - `@DEFAULT`はブログ既定のカテゴリを示す
- `label`: 文字列・Seesaaブログ内のラベル（？）
  - `@NULL!`は値がないことを示す
- `hashtag`: 文字列・記事の投稿と同時にTwitterに投稿するさいに自動的に付加されるハッシュタグ
- `keyword`: 文字列・Seesaaブログ内のキーワード（？）
- `description`: 文字列・記事の説明（？）
- `genre`: 文字列・Seesaaブログ内のジャンル（？）
- `posted_at`: `yyyyMMddHHmmss`形式の日付・投稿日時
- `updated_at`: `yyyyMMddHHmmss`形式の日付・更新日時
- `country`: 文字列・投稿元の国
  - `@JA!`を指定すると日本になる
  - `posted_at`と`updated_at`とのUTCからの時差を求めたりするのに使うかも
  - 記事の言語設定とかにも使うと複雑になりそう
- `note`: 文字列・そのほかの項目
  - いまのところ`@WIP!`は記事の製作中、`@TRIAL!`はいろいろ試験中であることを示す

</div>
</details>
</p>

### 冒頭部分

冒頭部分の文章は、Seesaaブログの「本文」に相当する。「続きを読む」の前に表示される部分である。

### 冒頭終了コメント

冒頭終了コメントは、記事の冒頭部分と「もくじ」の境界をHTMLのコメントアウトを用いて記述したものである。  
`<!--! readmore !-->`と記述し、一般のHTMLコメントと区別する。
これより下は「続きを読む」以降に表示される。

### もくじ

もくじは、Seesaaブログの「追記」に相当する部分の冒頭に配置する、記事内の段落構成を記述したものである。  
Seesaaブログの「もくじ」機能は使用せず、Markdownで記述する。

### 主部分

主部分は、記事の本題を段落に分けて記述したものである。
記事を記事たらしめる最も重要な要素で、意味論的な記事の内容そのもの。

### 記事終了コメント

記事終了コメントは、記事の終わりをHTMLのコメントアウトを用いて記述したものである。  
`<!--! end-of-article !-->`と記述し、一般のHTMLコメントと区別する。

## コミット時メッセージのきまり

### 基本の体裁と文字列の意味

（いまのところ）ファイルをひとつずつコミットするシステム  
`git commit -m "N ??? WRITESOMETHING [--ATTRIBUTES]"`…スペースに分けて記述する

<p>
<details>
<summary><strong>コミット時メッセージの文字列の意味</strong>（クリックで開く）</summary>
<div>

- `N`: 1以上の整数・そのファイルをコミットした回数
- `???`: 3文字の文字列・そのファイルへ行った操作
  - `JOT`: 記事ファイルのみ・内容を書き留めた
    - いわゆる「下書き」
  - `PUB`: 記事ファイルのみ・完成させ、投稿した
  - `EDI`: 記事ファイルのみ・投稿後の内容を編集した
  - ~~`REN`: 記事ファイルのみ・ファイル名を変更した~~
    - ファイル名の変更は面倒なことになるのでなるべくやらない
  - `DEF`: 記事以外のファイル・定義した
  - `MOD`: 記事以外のファイル・内容を変更した
  - `MOV`: すべてのファイル・ディレクトリを移動した
  - `DEL`: すべてのファイル・削除した
- `WRITESOMETHING`: （主に）ファイルのわかりやすい表現
  - 記事ファイルの場合は`metadata`内の`idea`
  - 記事以外のファイルの場合はルートディレクトリからのパス
- `[--ATTRIBUTES]`: `JOT`, `PUB`, `EDI`のいずれかの操作を行った際の変更内容の列挙
  - `all`: `[--ATTRIBUTES]`オプションのすべて
  - `content`: 内容
  - `essential`: `content`, `html`, `md`, `metadata`のすべて
  - `formal`: `html`, `md`, `metadata`のすべて
  - `html`: HTMLタグ
  - `md`: Markdown書式
  - `natural`: `content`, `typo`のすべて
  - `metadata`: 記事内メタデータ
  - `typo`: 内容の誤字脱字

<div>
</details>
</p>

### 特殊な文字列とその意味

- `INITIAL COMMIT`: リポジトリの最初のコミット
- `SPECIAL`: リポジトリのメタ的な操作
  - ディレクトリの生成のみをコミットする場合（？）
  - ほか、破壊的な変更

### コミット時コメントの例

- `git commit -m "1 PUB 1日で納豆1万回かき混ぜ essential"`…最初のコミットで記事を投稿する
- `git commit -m "1 JOT シーシャフレーバー保管時温度管理 essential !html"`…`html`以外の`essential`を書き留める
  - たぶんこういう書き方もできるようにする
- `git commit -m "4 EDI 電気不使用ウォシュレット考察 natural"`…投稿済みの記事の内容を編集し内容の誤字脱字を修正
- `git commit -m "1 DEF .backup/.markup.html"`…Seesaaブログで適用しているブログテーマのHTMLファイルをデフォルトから新しく定義
- `git commit -m "2 DEF .backup/.markup.html"`…Seesaaブログで適用しているブログテーマの定義済みHTMLファイルを変更
- `git commit -m "SPECIAL"`…なんらかの破壊的な変更を適用

## 著者

[ベルザ](https://belza.ga): 伝統的な京の範疇からすこ〜し離れたところにある格安ボロアパートの汚部屋住人

## バージョン

- 命名規則など: 0.1.1
- リポジトリのディレクトリ構造: 0.1.2
- CI/CDまわり: 0.1.1
- この説明書き: 0.1.2

## 更新履歴

2021/05/17 12:54:40 JST リポジトリのディレクトリ構造を一部変更
2021/05/17 12:45:00 JST この説明書きの一部URLが無効だったため修正  
2021/05/17 12:34:56 JST リポジトリのディレクトリ構造を一部変更・記事内メタデータの一部のプロパティに固有値を指定・ほか書き足りなかったところを追記  
2021/05/17 11:43:28 JST 記事内メタデータとcommit時コメントに用いる整数の最小値を指定  
2021/05/17 00:52:59 JST とりあえず作成、骨が折れる…
