# saori v1.1の開発
現在saori v1.1の開発を行っています.  
- 下書き機能
- 記事のキャッシュ

に関することを行いました.  

## 下書き機能
下書き機能は`php main.php draft :name`とするとcontents/draft/:name/article.mdが作成されてここで記事の下書きができるよになるものです. 投稿したい場合は`php main.php post :name`とするとcontents/article/yyyy/mm/:nameにコピーされます. 記事のconfigファイルは`post`した時に作成されます.

## 記事のキャッシュ
今まではarticle.mdの画像パスを書き換えたものをcache/に作成しておき, `article.html()`でarticle.mdを読み込んでパースをしていました.  
これを予めパースしておきarticle.htmlをcache/に作成しておき, `article.html()`でarticle.htmlを読み込むというものに変更しました.
### 時間計測
500回ループさせて時間を計測しました. 変更前後で2回計測.

||変更前|変更後|
|---|---|---|
|1回目|60.15|53.39|
|2回目|59.77|54.78|
|平均|59.96|54.085|

記事の数やブログのテンプレートによって前後するとは思いますが, 方式を変えたことで5.875秒削減できました. 現在のところブログを生成する際には誤差かもしれませんが, 記事数が増えれば差が大きくなっていくかもしれません.