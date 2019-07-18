---

theme: "Simple"
transition: "default"

---

## 1章 Laravelの概要

---

## はじめに

- 今村昌平と申します。
- Web業務システム受託の会社で勤務(1年半)
- 自分で Webアプリ作成中(マニュアル共有アプリ)
- Web業界入る前は、動物のお医者さん

--

## 本日の概要

### 前半

- laravel の特徴(1-1-1)と開発情報(1-1-2)
- Laravel のディレクトリ構成(1-3-1)
- 処理の流れ(1-3-2)
- 簡単なアプリケーション作成(1-3-3 ~ 1-3-7)

### 後半

- Homestead による環境構築
- Laradock による環境構築

---

## 1-1 Laravelとは

- PHP のフレームワーク

![php-flamework](https://www.nethues.com/blog/wp-content/uploads/2019/03/Laravel-Trends.png)

---

### 1-1-1 Laravel の特徴

- 学習コストが低い
- Symfony ベース(信頼性がある)
- 多機能
- 積極的なバージョンアップ
- ディレクトリ構成は開発者が自由に定める

--

#### バージョンアップ

![laravel service](https://user-images.githubusercontent.com/39234750/61394254-af22da80-a8fd-11e9-921a-46d11420f269.png)

---

### 1-1-2 開発情報

--

### 開発情報 1

| サイト               | URL                           |
|----------------------|-------------------------------|
| 公式サイト           | https://laravel.com           |
| 公式ドキュメント     | https://laravel.com/docs      |
| 日本語訳ドキュメント | https://readouble.com/laravel |
| GitHubリポジトリ     | https://github.com/laravel    |

--

### 開発情報 2

| サイト                | URL                                        |
|-----------------------|--------------------------------------------|
| PHPユーザーズ(日本語) | https://phpusers-ja.slack.com              |
| Larachat-jp           | https://larachat-jp.slack.com              |
| Laravel.jp(FaceBook)  | https://www.facebook.com/groups/laravel.jp |
| teratail              | https://teratail.com                       |
| stackoverflow         | https://ja.stackoverflow.com/              |

---

## 1-3 最初のアプリケーション

- ※今村は Homestead が動かせなかったため
- 以降の節では、Laradock を用いています

---

### 1-3-1 Laravel のディレクトリ構成

https://github.com/ShoheiImamura/laravel-chapter1/tree/master/sampleapp

--

#### ディレクトリ構成1

| ディレクトリ | 説明                                                      |
|--------------|-----------------------------------------------------------|
| app/         | アプリケーションの主要な処理クラスを配置                  |
| bootstrap/   | アプリケーションで最初に実行される                        |
| config/      | アプリケーションの設定値を記載したファイル等              |
| database/    | データベース関連のファイル                                |
| public/      | Webアプリケーションとして公開する場合のドキュメントルート |

--

#### ディレクトリ構成2

| ディレクトリ | 説明                                             |
|--------------|--------------------------------------------------|
| resources/   | View のテンプレートやSASS などのメタ言語ファイル |
| routes/      | アプリケーションのルート定義ファイル             |
| storage/     | Laravelが出力するファイルの出力先                |
| tests/       | テストコードを記載したファイルを置く             |
| vendor/      | Composer でダウンロードされるパッケージ          |

---

### 1-3-2 Welcomeページの処理

--

#### イメージ

![ページの表示フロー](https://laravel10.files.wordpress.com/2015/02/laravel_mvc1.png?w=620)

参考:[ララ帳](https://laravel10.wordpress.com/2015/02/15/%E5%88%9D%E3%82%81%E3%81%A6%E3%81%AElaravel-5-1-%E3%83%9A%E3%83%BC%E3%82%B8%E3%81%AE%E8%A1%A8%E7%A4%BA%E3%83%95%E3%83%AD%E3%83%BC/)

--

#### エントリポイント

- http://homestead.test/ へのアクセスはまず、 public ディレクトリを参照する

--

#### ルーティング

- ルーティングは、URLと処理の関連付け
  - ○○にアクセスがあったら、☓☓を呼び出す
- routes/web.php に定義する

    [routes/](https://github.com/ShoheiImamura/laravel-chapter1/tree/master/sampleapp/routes)  
    [routes/web.php](https://github.com/ShoheiImamura/laravel-chapter1/blob/master/sampleapp/routes/web.php)

--

#### ビュー

- resources/views/ ディレクトリの中に配置される
- 拡張子は、 xxx.blade.php
  - ほぼ HTML
  - テンプレートエンジン「Blade」
  - {{...}}や, @ で始まる構文などを使う

    [resources/views/](https://github.com/ShoheiImamura/laravel-chapter1/tree/master/sampleapp/resources/views)
    [resourcex/views/welcome.blade.php](https://github.com/ShoheiImamura/laravel-chapter1/blob/master/sampleapp/resources/views/welcome.blade.php)

---

#### 以降のスライドの流れ

1. ルーティングとビューの設定
2. テストコードの作成と実行
3. データベースの設定と準備、マイグレーション
4. 認証・登録機能の確認
5. 登録画面、動線の作成
6. ユーザ認証機能の実装
7. イベント機能の利用、準備
8. メール送信機能の実装

--

#### 完成したアプリケーション

[http://localhost:10080/home](http://localhost:10080/home)※  
[http://localhost:8025](http://localhost:8025)

---

### 1-3-3 はじめてのページ

- http://homestead.test/home にアクセスすると、TOP画面が表示されるようにします

--

#### ルーティング定義を追加

- routes/web.php に記述
- `Route::get({URL}, {テンプレートを返す関数})`

[sampleapp/routes/web.php](https://github.com/ShoheiImamura/laravel-chapter1/blob/master/sampleapp/routes/web.php#L18-L20)

--

#### TOP画面のテンプレートファイルを用意

- resouces/views に配置
- ファイル名 home.blade.php として保存

[sampleapp/resources/views/home.blade.php](https://github.com/ShoheiImamura/laravel-chapter1/blob/master/sampleapp/resources/views/home.blade.php)

---

### 1-3-4 はじめてのテストコード

- PHPUnit を利用する
  - トップ画面のHTTPステータスコード200が返却されること
  - トップ画面のレスポンスに"こんにちは!"の文字が含まれていること

[tests/Fearure/HomeTest.php](https://github.com/ShoheiImamura/laravel-chapter1/blob/master/sampleapp/tests/Feature/HomeTest.php#L16-L28)

--

#### php artisan コマンド

- Laravel のコマンドラインインターフェイス
- laravel のアプリケーションのルートディレクトリで実行する
  - php artisan xxx

[https://readouble.com/laravel/5.5/](https://readouble.com/laravel/5.5/ja/artisan.html)

--

#### テスト実行

- コマンドラインから PHPUnit を実行する
  - vendor/bin/phpunit

---

### 1-3-5 ユーザ登録の実装

- データベース準備
- 認証・登録機能確認
- 登録画面作成

--

#### データベース準備

- マイグレーション機能を用いる
  - データベースのスキーマ作成、データ投入をプログラムによる処理で実施できる
  - ファイルは database/migrations に配置される
  - コマンドは php artisan migrate

[マイグレーションファイル](https://github.com/ShoheiImamura/laravel-chapter1/blob/master/sampleapp/database/migrations/2014_10_12_000000_create_users_table.php)

--

#### Userテーブル定義

![userテーブル定義](https://user-images.githubusercontent.com/39234750/61405730-7b53af00-a915-11e9-9200-d6a379fab22a.png)

--

#### 認証・登録機能

- 登録はコントローラで処理

| 処理     | クラス名           | メソッド名           |
|----------|--------------------|----------------------|
| 画面表示 | RegisterController | showRegistrationForm |
| 登録     | RegisterController | register             |

[app/Http/Controller/Auth/RegisterController.php](https://github.com/ShoheiImamura/laravel-chapter1/blob/master/sampleapp/app/Http/Controllers/Auth/RegisterController.php#L23)  
[routes/web.php](https://github.com/ShoheiImamura/laravel-chapter1/blob/master/sampleapp/routes/web.php#L21-L22)

--

#### 登録画面作成

- ファイル名 register.blade.php で作成
- CSRF トークンを挿入するために{{ csrf_field() }}を記述

[resource/views/auth/register.blade.php8](https://github.com/ShoheiImamura/laravel-chapter1/blob/master/sampleapp/resources/views/auth/register.blade.php)

- トップ画面をログイン有無で出し分ける

[resources/views/home.blade.php](https://github.com/ShoheiImamura/laravel-chapter1/blob/master/sampleapp/resources/views/home.blade.php)

---

### 1-3-6 ユーザ認証

[ルーティング](https://github.com/ShoheiImamura/laravel-chapter1/blob/master/sampleapp/routes/web.php#L24-L25)
[ログインフォーム](https://github.com/ShoheiImamura/laravel-chapter1/blob/master/sampleapp/resources/views/auth/login.blade.php)

---

### 1-3-7 イベント

- プログラムで発生する事象(イベント)から、その事象に対応した処理(リスナー)を実行する機能
- イベントをフックすることで、任意の処理を差し込める

1. メール送信設定
2. イベントとリスナーのファイル作成
3. リスナークラスの実装

--

#### メール送信設定

- MailHog というSMTPサーバを用いる

[.envファイルの設定](https://github.com/ShoheiImamura/laravel-chapter1/blob/master/sampleapp/.env.example#L25-L30)※.exapmle.env

--

#### イベントとリスナーのファイル作成

- app/Providers/EventServiceProvider.php にリスナーを定義する
- コマンドライン`php artisan event:generate`からリスナーを作成する

[EventServiceProvider.php](https://github.com/ShoheiImamura/laravel-chapter1/blob/master/sampleapp/app/Providers/EventServiceProvider.php#L19-L21)

--

#### リスナークラスの実装

- イベント発生時に、リスナークラスの handle メソッドが実行される
- Mailer クラスでメールを送信する

[RegisteredListener.php](https://github.com/ShoheiImamura/laravel-chapter1/blob/master/sampleapp/app/Listeners/RegisteredListener.php)

[]

---
