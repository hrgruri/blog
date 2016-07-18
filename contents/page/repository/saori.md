# saori
## 概要
[saori](https://github.com/hrgruri/saori)はgithub.ioでブログをするための静的サイトジェネレータです. PHPで作られていてターミナル上で動作をさせます. MarkdownとJSONでブログの記事や設定を記述していきます.  

## 始め方
### インストール
インストールはComposerからできます
```sh
mkdir blog
cd blog
composer require hrgruri/saori
```
### 初期化
まずは動かすためのコードを記述します. main.phpにでも以下のコードを書いてください.
```php
<?php
require ('vendor/autoload.php');
$saori = new hrgruri\saori\Saori(__DIR__);
$saori->run($argv);
```
次の初期化をしましょう. 初期化をすることで,必要最低限の設定ファイルが生成されます.
```sh
php main.php init
```
そうするとcontents/config.jsonができていると思うので, 必要なところを編集してください. <font color='red'>idはGitHubのアカウント名</font>です.

## 使い方
### 記事を投稿する
```php
php main.php post (:article_title)
```
これで contents/yyyy/mm/:article_title にarticle.mdとconfig.jsonが生成されます. ちなみにarticle_titleを設定しなければ contents/yyyy/mm/ddhhmm (日時分)に生成されます.  
config.jsonで記事のタイトルとタグを設定します.
いよいよ記事の作成です. article.mdにMarkdown形式で記述していきます.
### サイトを生成する
いよいよサイトを生成します.
```php
php main.php make
```
これでlocalとusername.github.io (username部分はcontents/config.jsonのid)が作られます.  
公開する前にどのようなサイトが生成されたのかを確認してみたいと思います. 確認にはPHPのビルトイン･サーバを使いましょう.
```php
php -S localhost:8000 -t local
```
ブラウザで[http://localhost:8000](http://localhost:8000)にアクセスしてみましょう.

### GitHubにPush
まずはGitHubに｢username.github.io｣というリポジトリを作成しましょう. username部分はGitHubのアカウント名です.  
```sh
cd hrgruri.github.io
git init
git remote add origin git@github.com:username/username.github.io.git
git add --all
git commit -m 'Initial commit'
git push origin master
```

## その他
config.jsonを編集することでブログの設定を変えることができます. それ以外にもtheme.jsonでテーマごとの設定を上書きすることができます. (できない部分もあり)
```json
{
    "saori": {
        "color": {
            "header" : "#A9EEE6",
            "title" :"#F7FBFC",
            "body":"#FEFAEC",
            "page-contents": "#FFF1CF"
        }
    }
}
```
これは,saoriというテーマを使用した際に使用する色を変えるためのものです. 変更できる箇所と名前はテーマによって異なるので注意してください. saoriテーマは[ここ](https://github.com/hrgruri/saori/blob/v1.0/src/theme/saori/config.json)で確認することができます.

(2016-07-15: 内部的な話は現在書いています)
