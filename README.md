# [Railsコードメモ]

## サービス概要

記載したコードを消さずに取っておきたい人向けに
コードを保存できる
メモ形式のサービスです。

# Railsに絞った理由
Rails on Ruby を現在進行形で学習しているためエラーの内容やコードを保存する際に必要な事項をイメージがしやすいこと。
rubyではなくrailsなのはファイル数やファイル名など複数あり、コードを保存する際に予めファイル名などが付いていれば自分で命名する手間が減るなどコード保存アプリとしてメリットがrubyよりもあるため。
まずは現在進行形で学習しているRailsでメモアプリを展開し、その後のレビューや評価などでその他の言語も増やしていこうと考えているため。

##　想定されるユーザー層

記載したコードを消さずに取っておきたい人、メモに保存してもメモの量が多くなりコードをどこに記載したか分からなくなってしまう人

## サービスコンセプト

デフォルトのメモ帳アプリにもコードを保存することは出来ますが、
メモの量が多くなりどこにどのコードを記載したか分からなくなってしまうため
カテゴライズされたメモでコードをどこに保存したか、またコードを見返したい時などに
分かりやすいメモを考案しました。
私自身、デフォルトのメモ帳アプリなどにコードを記載したりしますが
コードだけではなく様々なことをメモに記載するためどこにコードを保存したか
探すことがありました。
そこで、エラーが出た時のコードの保存やメソッドの変更などカテゴライズごとにメモが分別されるなど
いつどんなコードを記載したかわかるメモがあればと思い、このサービスを考えました。
コードで躓いた時でも簡単にどんなコードを書いたか見返せるメモアプリにしていきたいと思います。

### 実装を予定している機能
## MVPリリース時に実装予定の機能
* トップページ
* 新規投稿フォーム
* 編集フォーム
* 投稿一覧
* カテゴライズ機能
* 選択機能(controller‥など記載しなくても選択でcontrollerやmodelなど記載したいファイル名を選べる)
* マルチ検索機能（ 使用技術とライブラリ：　Stimulus Autocomplete（Rails7 ）& JQuery）

### 本リリース時に実装する予定の機能
* トップページ
* 新規投稿フォーム
* 編集フォーム
* 投稿一覧
* カテゴライズ機能
* 選択機能(controller‥など記載しなくても選択でcontrollerやmodelなど記載したいファイル名を選べる)
* マルチ検索機能（ 使用技術とライブラリ：　Stimulus Autocomplete（Rails7 ）& JQuery）
* * 以下追加機能
* ソート機能（投稿は作成日時順に並べる）
* キーとバックグラウンド処理（キー：Sidekiq バックエンド：Active Job）
* ロボらんてくんのようなチャットサービス
  → 高度な技術を扱うライブラリ(予定）：keras （初心者でも扱いやすいこと、チャットボットの作成が可能な事、
  様々なプラットフォームにデプロイが可能なため）

## 以下メモアプリの具体的な機能　##

### メモの主な機能の流れ：
* まずメモアプリを開いた時に以下のどちらかのカテゴライズを選択する
  ・カテゴライズ
  ＊主に2つに分けて保存（とりあえず大まかなカテゴライズなのでアドバイスがあれば追加）
  エラー用または保存用
* カテゴライズの選択が終わった後でメモの記入欄が表示される
* 記入し送信ボタンを押すと、メモ一覧にメモが投稿される
   ※メモは日付毎にまとめて掲載する

### メモの構成内容：

* 日付欄　（デフォルトで今日の日付が入るようにする）
* カテゴライズ欄
* カテゴライズでエラーを選んだ場合は、カテゴライズの後にどんな種類のエラーなのかをタイトル記入欄を追加する。
* タイトル欄（エラーを選ばなかった場合）
* ファイル名欄（選択肢の欄でフォルダ名の記載など）
* コード欄
* 備考欄（タイトル以外で何か記載したい時の欄）
* 文章を追加ボタン
（※検索機能はメモ投稿一覧のところに設置など）

### エラー用(カテゴライズ)
（エラーを選んだ場合、タイトルを記入する際に選択肢で選べる。選ばなかった場合は自分で記載）
* Name Error
* No Method Error
* Template is missing
* LoadError
* Actioncontroller::UnknownFormat
* ArgumentError
* Syntax errorなど

例：カテゴライズ欄：　エラー
　　エラー名：　No Method Error
	ファイル名：　app/controllers/(ここから自分の作成したファイル名）
　　　コード： def event_params
              params.require(:event).permit(:title, :content, :held_at, :prefecture_id, :thumbnail, :followed_id)
              end
    備考欄：　paramsが値を受け取れない（何も記載することがなければ空欄など）

### 保存用(カテゴライズ)

例：カテゴライズ欄：　保存用
	タイトル名：　前のコードと比較（用途などを記載する）
	ファイル名：　app/controllers/(ここから自分の作成したファイル名を記入)_controller.rb　　　
	コード： def event_params
            params.require(:event).permit(:title, :content, :held_at, :prefecture_id, :thumbnail, :followed_id)
          end
      備考欄：　（何も記載することがなければ空欄など）

### タイトル記入の選択機能

* 選択肢機能：フォルダ
（以下はメモでタイトルを記入する際に選択肢で選べる。選ばなかった場合は自分で記載）

* app/
* app/assets/
* app/controllers/_controller.rb
* app/models/.rb
* app/view/.html
* app/helper/
* bin/
* config/
* config/routes.rb
* config/locales/ja.yml
* db/
* db/migrate/.rb
* lib/
* log/
* public/
* spec/
* storage/
* tmp/
* vendor/
* .browserslistrc
* .gitattributes
* .gitignore
* Gemfile
* Rakefile
* Read.me

### 画面遷移図
Figma：https://www.figma.com/file/udCxen2U09uuFFj4CNkgAJ/%E7%84%A1%E9%A1%8C?type=design&node-id=0%3A1&mode=design&t=1sD2upAdrS2gplve-1
### READMEに記載した機能
- [ ] トップページ
- [ ] メモ新規投稿機能
- [ ] メモ編集機能
- [ ] メモ削除機能
- [ ] メモ閲覧機能
- [ ] カテゴライズ機能
- [ ] 選択（チェックボックスなど）機能
- [ ] ソート機能（投稿は基本的に作成日時順に並べる）
- [ ] マルチ検索機能
- [ ] チャットサービス機能(現時点だと技術力がないため作成可能であれば）
- [ ] キーとバックグラウンド処理機能

### 未ログインでも閲覧or利用できるページ
以下の項目はちゃんと未ログインでも閲覧or利用できる画面遷移になっているか？
- [ ] ログイン機能を付けないためログインで全て閲覧可能

### ER図
[![Image from Gyazo](https://i.gyazo.com/c00a827dafe220f582e627d1c95338d5.png)](https://gyazo.com/c00a827dafe220f582e627d1c95338d5)
