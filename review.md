# PHP App ① レビュー

## 全般

### 以下のaタグのリンクを押下した際にedit.phpの$_GETにどんな値が格納されるか説明してください。

```html
<a href="edit.php?todo_id=123&todo_content=焼肉">更新</a>
```
「array(2) { ["todo_id"]=> string(3) "123" ["todo_content"]=> string(6) "焼肉" }」の値が格納されます。

### 以下のフォームの送信ボタンを押下した際にstore.phpの$_POSTにどんな値が格納されるか説明してください。

```html
<form action="store.php" method="post">
    <input type="text" name="id" value="123">
		<textarea　name="content">焼肉</textarea>
    <button type="submit">送信</button>
</form>
```
「array(2) { ["id"]=> string(3) "123" ["content"]=> string(6) "焼肉" }」の値が格納されます。

### `require_once()` は何のために記述しているか説明してください。
（）の中のファイルを読み込み、そのファイルを使用できるようにするためです。

### `savePostedData($post)`は何をしているか説明してください。
こちら未定義かと思われますので、現時点ではわかりません。

### `header('location: ./index.php')`は何をしているか説明してください。
index.htmlファイルへ画面を遷移させています。

### `getRefererPath()`は何をしているか説明してください。
こちら未定義かと思われますので、現時点ではわかりません。

### `connectPdo()` の返り値は何か、またこの記述は何をするための記述か説明してください。
PHPに定義済みのPDOクラスをインスタンス化して、DBから取得した値が返り値として返ってきます。
PHPとDBを接続して値を取得するため、または取得できなかった時のエラーメッセージを表示させるための記述です。

### `try catch`とは何か説明してください。
プログラム実行中にエラーや例外が発生した時に例外処理が行われるように定義してある処理。
try{}の中にエラーが起こりうるコードを定義して、catch内に実際にエラーが起きた時の処理を定義します。

### Pdoクラスをインスタンス化する際に`try catch`が必要な理由を説明してください。
エラーが出たときにクラッシュを起こさずに処理を終えるためです。

## 新規作成

### `createTodoData($post)`は何をしているか説明してください。
結論としては、connetion.phpで定義されたcreateTodoData関数を呼び出したときに、
DBのカラム「content」に$todoTextの値を登録させる処理をしています。
一連の流れは以下の通りです。

1.フォームから送られてきたデータを、キーが「content」、バリューが入力値のデータをpost形式で、store.phpに送る。

2．createData関数を呼び出し、$_POSTを引数としている。

3．$_POSTによってにキーが「content」、バリューが入力値のデータが取得される。

4．createData関数の定義元を確認すると、createTodoData関数を呼び出し、
引数$postも渡している。

5．createTodoData関数の定義元を確認すると、PDO接続の上、
DBのカラム「content」に引数$todoTextの値が登録されるSQL文がを準備し、
Queryメソッドで発行するようになっている。

6．引数$todoTextに引数$postの値が渡され、引数$postには$_POSTの値が渡される。

7．createTodoData($post)の実行された箇所で上記1～6までの一連の流れが実行される。→完了

###　※追加課題※PDOクラスもっと調べていつthrowされているか回答。
connectPdo関数が実行されて、PDOインスタンスが作成されたときです。
（マニュアルに「__construct() は、 指定されたデータベースへの接続に失敗した場合、 PDO::ATTR_ERRMODE が設定されているかどうかに関わらず、 PDOException をスローします。」とあるため。）

## 一覧

### `getTodoList()`の返り値について説明してください。
getAllRecords関数の処理結果が返り値として呼びだされています。
getAllRecords関数はPDO接続をしたDB上のdeleted_atがNULLのレコードを取得するSQL文が含まれており、取得した値をfetchAllで抽出してgetAllRecords()に返して、その返った値が配列のデータ型でgetTodoList()の返り値として返って来ます。

### `<?= ?>`は何の省略形か説明してください。
echoの省略系です。

## 更新

### `getSelectedTodo($_GET['id'])`の返り値は何か、またなぜ`$_GET['id']` を引数に渡すのか説明してください。

### `updateTodoData($post)`は何をしているか説明してください。

## 削除

### `deleteTodoData($id)`は何をしているか説明してください。

### `deleted_at`を現在時刻で更新すると一覧画面からToDoが非表示になる理由を説明してください。

### 今回のように実際のデータを削除せずに非表示にすることで削除されたように扱うことを〇〇削除というか。

### 実際にデータを削除することを〇〇削除というか。

### 前問のそれぞれの削除のメリット・デメリットについて説明してください。
