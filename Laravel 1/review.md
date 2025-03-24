# Laravel Lesson レビュー①

## Todo一覧機能

### Todoモデルのallメソッドで実行しているSQLは何か

- SELECT * FROM todos ~~WHERE deleted_at IS NULL~~;

### Todoモデルのallメソッドの返り値は何か

>Illuminate\Database\Eloquent\Collection {#261 ▼
  #items: array:2 [▼
    0 => App\Todo {#262 ▶}
    1 => App\Todo {#263 ▶}
  ]
}

### 配列の代わりにCollectionクラスを使用するメリットは

- 可読性、保守性の向上
- 豊富なメソッドの提供による簡単、効率的なデータ操作

### view関数の第1・第2引数の指定と何をしているか

- 第一引数に画面に表示したいbladeファイル
- 第二引数に渡したいデータを連想配列の形で

### index.blade.phpの$todos・$todoに代入されているものは何か

- $todos...$todo->all();の返り値、2つのTodoインスタンスを格納したIlluminate\Database\Eloquent\Collectionクラスのインスタンス
- $todo...Todoインスタンス、todosテーブルから取得したレコード

## Todo作成機能

### Requestクラスのallメソッドは何をしているか

- フォームから送信された値を一括で取得

### fillメソッドは何をしているか

- Todoインスタンスの各プロパティに一括で代入

### $fillableは何のために設定しているか

- fillメソッドで更新されるカラムを制限し、意図しないカラムを更新されないようにする。

### saveメソッドで実行しているSQLは何か

- `UPDATE todos SET content = $todo['content'] WHERE id = $todo['id'];`
>content部分を変更してTodoクラスの項目分の処理

### redirect()->route()は何をしているか

- routeで指定した場所にリダイレクトする処理

## その他

### テーブル構成をマイグレーションファイルで管理するメリット

- マイグレーションファイルを開発者同士でgitなどで共有しておけば
マイグレーションを実行するだけで、開発者同士のテーブル構成を統一させることができる。

### マイグレーションファイルのup()、down()は何のコマンドを実行した時に呼び出されるのか

- up
`php artisan migrate`
- down
`php artisan migrate:rollback`

### Seederクラスの役割は何か

- DBにテストデータを作成する

### route関数の引数・返り値・使用するメリット

- 引数...第一引数がURI、第二引数にそのURIとHTTPメソッドの組み合わせで実行したい処理
- 返り値...そのアドレスにアクセスした時に表示される内容
- メリット...可読性と保守性

### @extends・@section・@yieldの関係性とbladeを分割するメリット

- `@extends`で継承する親Bladeを指定
- `@section` ~ `@endsection`で囲われた部分を、親Bladeの`@yield`の箇所に挿入
##### メリット
- 重複するコードを共通化して再利用できるようになるため、保守性が向上する。
### @csrfは何のための記述か

- CSRF対策、フォーム内に`@csrf`を追記するだけでトークンの発行、検証も行ってくれる。

### {{ }}とは何の省略系か

`<?php と ?>`、また、エスケープ処理
