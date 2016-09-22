# saori
## 概要
[saori](https://github.com/hrgruri/saori)はgithub.ioでブログをするための静的サイトジェネレータです. PHPで作られていてターミナル上で動作をさせます. MarkdownとJSONでブログの記事や設定を記述していきます.  

## 始め方
### インストール
インストールはComposerからできます
```sh
composer create-project hrgruri/saori-skeleton blog
```
### 初期化
インストールが終わったら初期化をしましょう. 初期化をすることで,必要最低限の設定ファイルが生成されます.
```sh
php saori init
```
そうするとcontents/config.jsonができていると思うので, 必要なところを編集してください. <font color='red'>idはGitHubのアカウント名</font>です.

## 使い方
### 記事を投稿する
```php
php saori draft :article_title
```
これでdraft/:article_titleディレクトリが生成されます. 中にはarticle.mdとconfig.jsonがあるので,記事の設定(タグやタイトル)と記事(Markdown形式)を書いていきましょう.  

書き終えれば次のコマンドを実行します.
```php
php saori post :article_title
```
こうすると先に書いた記事がcontents/yyyy/mm/:article_titleに移動されます.  

### サイトを生成する
いよいよサイトを生成します.
```php
php saori build
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
cd username.github.io
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
これは,saoriというテーマを使用した際に使用する色を変えるためのものです. 変更できる箇所と名前はテーマによって異なるので注意してください. saoriテーマは[ここ](https://github.com/hrgruri/saori/blob/v2.1/src/theme/saori/config.json)で確認することができます.
