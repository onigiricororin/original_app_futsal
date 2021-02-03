# README
## アプリケーション名	
誰でもチームを強くできるアプリ
## アプリケーション概要	このアプリケーションでできることを記述しましょう。
スポーツチームが目標達成に必要な活動を管理できる
## URL	デプロイ済みのURL
## テスト用アカウント	
## 利用方法
アマチュアスポーツチームの活動管理に活用する
## 目指した課題解決	

## 洗い出した要件	
* トップページ
- 表示
「誰でもチームを強くできるアプリ・DTTA」と表示されている
- ボタン
サインイン、ログインページへ遷移できるボタンがある
新規登録画面へ遷移できるボタンがある

* サインイン/ログインページ
- 表示
ユーザID入力画面がある
パスワード入力画面がある
エラー時にメッセージが表示される
- ボタン
ログインボタンがある

* 新規登録ページ
- 表示
チーム名入力画面がある
代表者氏名入力画面がある
- ボタン
登録ボタンがある

* ログインページ後、共通ヘッダー
- ボタン
サインイン/ログインページに遷移できるボタンがある
ログイン時は、ログアウトできるボタンがある
- 表示
チームビジョンが表示されている
チームコンセプトが表示されている
チーム目標が表示されている

* チームページ（カレンダーをベースとしてた情報表示）
- 表示
ヘッダーが表示されている
カレンダーが表示されている
未入力の出欠一覧が表示される
次回の活動詳細が表示されている
次回の活動における活動目標が記載されている
マイルストーンの活動予定が表示されている
マイルストーンまでの残りの活動日数が表示されている
直近の活動記録が一覧で表示されている
チーム全体での決定事項が表示されている
- ボタン
カレンダーから活動詳細へ遷移できるボタンがある
出欠の登録ができるボタンがある
活動目標の編集ボタンがある

* 記録された活動の詳細ページ
- 表示
活動詳細（日付・時刻・件名・本文）が閲覧できる。
前回活動記録に定めた次回アクションが表示されている
出席ユーザーの情報が閲覧できる
動画リンクが貼れる
チームページへのリンクがある
- ボタン
出欠を編集できる
活動の結果が記入ができる
振り返りを記載できる
次回アクションが記載できる

## 実装した機能についてのGIFと説明	
今後実装予定

## ローカルでの動作方法


This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version
ruby 2.6.5p114 (2019-10-01 revision 67812) [x86_64-darwin18]

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...

# テーブル設計

## users テーブル

| Column   | Type   | Options     |
| -------- | ------ | ----------- |
| last_name  | string | null: false |
| first_name | string | null: false |
| last_read_name  | string | null: false |
| first_read_name | string | null: false |
| nickname | string | null: false, unique: true |
| birthday | date   | null: false |
| email    | string | null: false, unique: true |
| encrypted_password| string | null: false |


### Association

- has_many :items
- has_many :orders

## items テーブル

| Column      | Type        | Options     |
| ------      | ------      | ----------- |
| user        | references  | null: false, foreign_key: true |
| name        | string      | null: false |
| summary     | text        | null: false |
| price       | integer     | null: false |
| category_id  | integer    | null: false |
| condition_id | integer    | null: false |
| burden_id    | integer    | null: false |
| prefecture_id| integer    | null: false |
| days_to_ship_id | integer | null: false |

### Association

- belongs_to :user
- has_one :order

## orders テーブル

| Column | Type       | Options                        |
| ------ | ---------- | ------------------------------ |
| user   | references | null: false, foreign_key: true |
| item   | references | null: false, foreign_key: true |

### Association

- belongs_to :user
- belongs_to :item
- has_one :address

## addresses テーブル

| Column      | Type       | Options                        |
| -------     | ---------- | ------------------------------ |
| order       | references | null: false, foreign_key: true |
| postal_code | string     | null: false      |
| prefecture_id | integer  | null: false      |
| city        | string     | null: false      |
| house_number| string     | null: false      |
| building_name| string    |                  |
| phone_number | string    | null: false      |


### Association

- belongs_to :order
