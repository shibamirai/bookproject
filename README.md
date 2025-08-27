# Django のツボとコツがゼッタイにわかる本 第３版 正誤表

## 第３章　Djange の基本的な機能を理解しよう！

### 3-9 class-based view で実装する

- p.84 リスト 5

  **誤**：
  ```python
  from pathlib import Path
  print(Path(__file__))
  ```

  **正**：
  ```python
  from pathlib import Path
  print(Path(__file__).name)
  ```

## 第４章　本棚アプリケーションの作成①（CRUD の理解）

### 4-13 レイアウト等の調整

- p.166 リスト 1　コード追加部分

  **正**：
  ```html
  <nav class="navbar navbar-dark bg-success sticky-top">
    <div class="navbar-nav d-flex flex-row">
      <a href="{% url 'list-book' %}" class="nav-link mx-3">書籍一覧</a>
      <a href="{% url 'create-book' %}" class="nav-link mx-3">書籍登録</a>
    </div>
  </nav>
  <div class="m-4">
    <h1>{% block h1 %}{% endblock%}</h1>
  </div>
  ```

## 第５章　本棚アプリケーションの作成②（Django の機能のさらなる理解）

### 5-5 ログアウト機能の追加

- p.194 リスト 3

  LogoutView に GET メソッドでリクエストを送るとエラーになるので、下記のように変更する

  **誤**：
  ```html
  <a href="{% url 'accounts:logout' %}" class="nav-link mx-3">ログアウト</a>
  ```

  **正**：
  ```html
  <form method="post" action="{% url 'accounts:logout' %}">
      {% csrf_token %}
      <button class="nav-link mx-3">ログアウト</button>
  </form>
  ```

### 5-8 画像の表示

- p.239 Column

  「デプロイ編で紹介している動画」とは本書第2版の話（AWSで公開する方法）でこの第3版にはない。
（本番環境では MEDIA_ROOT の設定を変える）

## 第６章　サイトを公開しよう！

### 6-2 GitHub のアカウント作成

- p.288 git init コマンドの出力内容が異なる

  **誤**：
  ```cmd
  $ git init
  Initialized empty Git repository in /name of your directory/project3/.git/
  ```
  **正**：
  ```cmd
  $ git init
  Initialized empty Git repository in /name of your directory/project3/bookproject/.git/
  ```

### 6-4 デプロイのための設定

- p.297 リスト 1

  dj_database_url.config() 内の下記パラメータ
  ```
  default='postgresql://postgres:postgres@localhost:5432/bookproject',
  ```
  は、環境変数 DATABASE_URL が設定されていなかった場合のデフォルト値を設定するものなので、本来はローカル環境で使用しているデータベースの接続先 URL を設定する。
  ここでは設定しないか、代わりに下記のようにローカルで使用しているSQLiteの設定をする
  ```
  default='sqlite:///{}db.sqlite3'.format(BASE_DIR),
  ```

- p.300 リスト 3

  `if not DEBUG:` からの 4 行には「コード追加」と書かれていないが、これらも追加する必要がある  
  また、それとともにファイル先頭に以下を追加する

  ```python
  import os
  ```

- p.302 スクリプトファイルの作成

  Windows でビルドスクリプトを作った場合は、実行権限の変更は不要

- p.303 リスト 5

  `your_name`, `your_password` の部分はこの後書き換えるので、ここではでたらめな値で構わない(ただし何か値をセットしておくこと)
