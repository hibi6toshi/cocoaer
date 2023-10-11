# Cocoaer
![サービスロゴ](/resources/Cocoaer_logo.jpeg)

孝行をもっと身近に、手軽に。  
孝行に特化したCGMです。

▼**サービス URL**

https://web.cocoaer.net/

(※Chromeのみ対応しております。)

## 主な機能
### 孝行の表示・投稿

| 表示  | 投稿/編集 |
| --- | --- |
| ![article_show](/resources/article_show.gif) | ![article_create](/resources/article_create.gif)  |
| 投稿された孝行を表示できます。 <br> コメント・お気に入り登録できます。  | 孝行を投稿できます。 <br>サムネイル画像を指定できます。<br>ターゲット・カテゴリ・日数・費用を設定できます。  |

### プロジェクトの表示・投稿

| 表示  | 投稿/編集 |
| --- | --- |
| ![project_show](/resources/project_show.gif) | ![project_create](/resources/project_create.gif)  |
| 投稿されたプロジェクトを表示できます。 <br> お気に入り登録できます。  | プロジェクトを投稿できます。<br>ターゲット・カテゴリ・目標日・費用を設定できます。<br>タスク・アクションを複数登録できます。 |

### フォーラムの表示・投稿

| 表示  | 投稿/編集 |
| --- | --- |
| ![forum_show](/resources/forum_show.gif) | ![forum_create](/resources/forum_create.gif)  |
| 投稿されたフォーラムを表示できます。 <br> コメント・お気に入り登録できます。  | フォーラムを投稿できます。<br>ターゲット・カテゴリ・日数・費用を設定できます。 |

### お気に入り一覧

| 表示  | 投稿/編集 |
![favorite](/resources/favorite.gif)



■　画面遷移図
https://www.figma.com/file/fsUtM0ocbfR2CHklVjkkZC/Untitled?node-id=0%3A1&t=rIkv44a6duu7mhQc-1

■　ER図：上段はマスタ系、それ以外はトランザクション系です。
![ER図](/resources/er.drawio.png)
[Users]ユーザ情報マスタ
  - name: ユーザの名前
  - sub: auth0から払い出されるuserIdを格納する
  - avatar: アバター画像
  - introduction: 自己紹介
  
[Piety_Targets]ターゲット情報マスタ(例: 父・母・兄弟,etc...)
  - name: ターゲット情報

[Piety_Categorys]カテゴリマスタ(例： 食事・贈り物・旅行, etc...)
  - name: カテゴリ情報

[Articles]孝行の記録情報
  - user_id: 投稿者のユーザーID
  - target_id: ターゲット情報のID
  - category_id: カテゴリ情報のID
  - days: 孝行の実施日数
  - cost: 費用
  - title: タイトル
  - body: 詳細
  - picture: 画像用

[Forums]フォーラム機能
  - user_id: 投稿者のユーザID
  - target_id: ターゲット情報のID
  - category_id: カテゴリ情報のID
  - days: 孝行の実施日数
  - cost: 予算
  - title: タイトル
  - body: 詳細

[Projects]プロジェクト機能
  - user_id: 投稿者のユーザID
  - target_id: ターゲット情報のID
  - category_id: カテゴリ情報のID
  - limit_date: 締切日
  - cost: 予算
  - title: タイトル
  - body: 詳細

[Comments]Article/Forumに対するコメント
  - commentable_type: Article or Forum
  - commentable_id: Article or ForumのID
  - user_id: コメントをしたユーザのID
  - body: コメント内容


[Favorites]Article/Forum/Projectに対するお気に入り
  - favoritable_type: Article or Forum or Project
  - favoritable_id: Article or Forum or ProjectのID
  - user_id: お気に入りをしたユーザのID

[Tasks]プロジェクトのタスク
  - user_id: タスクを作成したユーザのID
  - project_id: タスク対象のプロジェクトID
  - value: タスク内容

[Actions]プロジェクトでの行動記録
  - user_id: アクションを作成したユーザのID
  - project_id: アクション対象のプロジェクトID
  - value: アクション内容

■　インフラ構成図：ECR + ECSは省略。

![インフラ構成図](/resources/infra.drawio.png)

## 主な使用技術
### バックエンド
- Ruby on Rails(APIモード)
- MySQL
- Rspec

### フロントエンド
- React
- TypeScript
- Tailwind
- Jest
- React Testing Library 

### 認証
- Auth0

### インフラ
- フロントエンド：S3 + CloudFront
- バックエンド: ECR + ECS + AWS Fragate
- 画像ストレージ: S3
