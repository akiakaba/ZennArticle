---
title: "SQLめも" 
emoji: "🏘"
type: "tech" 
topics: ["SQL"]
published: false
---
# コマンド
## データベースの確認
```
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| innodb             |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.16 sec)
```

このように初期では5つのデータベースが作成されている。このデータベースはMySQLが動作するためのデータベースとして必要だから、決して削除しない。

## データベースを作成
基本構文　
`$ CREATE DATABASE データベース名;`

例：

```
mysql> CREATE DATABASE Test;
Query OK, 1 row affected (0.18 sec)
```

```
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| Test     |
| innodb             |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
6 rows in set (0.16 sec)
```

## 使うデータベースを指定
基本構文
`$ USE データベース名`

例:

```
mysql> USE WebCampProTest;
Database changed

```

##テーブルの作成
基本構文

```
$ CREATE TABLE テーブル名 (カラム名1 カラム型,
    カラム名2, カラム型,
    ...,
    カラム名n, カラム型,);

```

例：

```
mysql> CREATE TABLE meibo (id INT, name VARCHAR(100), name_kana VARCHAR(200), prefecture VARCHAR(50), address TEXT, age INT);
Query OK, 0 rows affected (0.78 sec)
```

## テーブルの確認

基本構文
　`$ SHOW TABLES;`

```
mysql> SHOW TABLES;
+--------------------------+
| Test                     |
+--------------------------+
| meibo                    |
+--------------------------+
1 row in set (0.18 sec)
```

## テーブル内の確認
基本構文
`$ DESK テーブル名`

```
mysql> DESC meibo;
+------------+--------------+------+-----+---------+-------+
| Field      | Type         | Null | Key | Default | Extra |
+------------+--------------+------+-----+---------+-------+
| id         | int(11)      | YES  |     | NULL    |       |
| name       | varchar(100) | YES  |     | NULL    |       |
| name_kana  | varchar(200) | YES  |     | NULL    |       |
| prefecture | varchar(50)  | YES  |     | NULL    |       |
| address    | text         | YES  |     | NULL    |       |
| age        | int(11)      | YES  |     | NULL    |       |
+------------+--------------+------+-----+---------+-------+
6 rows in set (0.17 sec)
```

## テーブル内にデータを挿入
基本構文
`$ INSERT INTO テーブル名 (カラム名1, カラム名2, ...) VALUES (値1, 値2, ...);`

例：

```
mysql> INSERT INTO meibo (id, name, name_kana, prefecture, address, age) VALUES (1, '青山 和久', 'あおやま かずひさ', '東京都', '東京都千代田区丸の内１丁目', 25);
Query OK, 1 row affected (0.20 sec)
```

##テーブルないのデータを検索
基本構文
`$ SELECT * FROM テーブル名;`

例：

```
mysql> SELECT * FROM meibo;
+------+---------------+---------------------------+------------+-----------------------------------------+------+
| id   | name          | name_kana                 | prefecture | address                                 | age  |
+------+---------------+---------------------------+------------+-----------------------------------------+------+
|    1 | 青山 和久      | あおやま かずひさ             | 東京都      | 東京都千代田区丸の内１丁目                   |   25 |
+------+---------------+---------------------------+------------+-----------------------------------------+------+
1 row in set (0.17 sec)
```

カラムを指定して取り出す場合

```
mysql> SELECT id, name FROM meibo;
+------+---------------+
| id   | name          |
+------+---------------+
|    1 | 青山 和久      |
+------+---------------+
1 row in set (0.18 sec)

```

データの条件を指定して取り出す場合

```
mysql> SELECT * FROM meibo WHERE prefecture = '東京都';
+------+---------------+---------------------------+------------+---------------------------------------------------------------+------+
| id   | name          | name_kana                 | prefecture | address                                                       | age  |
+------+---------------+---------------------------+------------+---------------------------------------------------------------+------+
|    1 | 青山 和久      | あおやま かずひさ              | 東京都     | 東京都千代田区丸の内１丁目                                          |   25 |
|    3 | 白鳥 蒼甫      | しらとり そうすけ               | 東京都     | 東京都練馬区豊玉南4-11                                            |   22 |
|    5 | 尾上 菊生      | おがみ きくお                 | 東京都     | 東京都小平市回田町2-12-17フォレスト回田町202                          |   41 |
+------+---------------+---------------------------+------------+---------------------------------------------------------------+------+
3 rows in set (0.16 sec)
```

```
mysql> SELECT * FROM meibo WHERE prefecture='東京都' AND age >= 35;
+------+---------------+---------------------+------------+---------------------------------------------------------------+------+
| id   | name          | name_kana           | prefecture | address                                                       | age  |
+------+---------------+---------------------+------------+---------------------------------------------------------------+------+
|    5 | 尾上 菊生      | おがみ きくお           | 東京都     | 東京都小平市回田町2-12-17フォレスト回田町202                           |   41 |
+------+---------------+---------------------+------------+---------------------------------------------------------------+------+
1 row in set (0.17 sec)
```

## データを更新
基本構文
`$ UPDATE テーブル名 SET カラム名1 = 値1, カラム名2 = 値2, ..., カラム名n = 値n WHERE 条件文;`

例：

```
mysql> UPDATE meibo SET age = 25 WHERE id = 3;
Query OK, 1 row affected (0.17 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

##テータの削除
基本構文
`$ DELETE FROM テーブル名 WHERE 条件文;`

```
mysql> DELETE FROM meibo WHERE id > 7;
Query OK, 4 rows affected (0.19 sec)
```



# テーブルを作成(例を使用して)
## テーブル設計
Testデータベースにテーブルを作成していきます。今回は名簿をイメージした構成のテーブルを作成していきます。
テーブルの項目内容とカラム名、型は下記の表のようにすることとします。

| 項目内容 | カラム名 | カラム型 |
|:--|:--|:--|
| ID | id | INT |
| 名前 | name | VARCHAR(100) |
| ふりがな | name_kana | VARCHAR(200) |
| 県名 | prefecture | VARCHAR(50) |
| 住所 | address | TEXT |
| 年齢 | age | INT |

カラム型に記述しているものは下記の内容を意味しています。

| カラム型 | 内容 |
|:--|:--|
| INT | 整数値 |
| VARCHAR(n) | n文字までの文字列 |
| TEXT | 最大文字列を指定しない文字列型 |

##テーブルを作成する
テーブル名はmeiboとしてテーブルを作成します。テーブル作成にはCREATE TABLEというSQLを使用します。

```
mysql> CREATE TABLE meibo (id INT, name VARCHAR(100), name_kana VARCHAR(200), prefecture VARCHAR(50), address TEXT, age INT);
Query OK, 0 rows affected (0.78 sec)
```
##テーブルを確認する
```
mysql> SHOW TABLES;
+--------------------------+
| Tables_in_WebCampProTest |
+--------------------------+
| meibo                    |
+--------------------------+
1 row in set (0.18 sec)
```

```
mysql> DESC meibo;
+------------+--------------+------+-----+---------+-------+
| Field      | Type         | Null | Key | Default | Extra |
+------------+--------------+------+-----+---------+-------+
| id         | int(11)      | YES  |     | NULL    |       |
| name       | varchar(100) | YES  |     | NULL    |       |
| name_kana  | varchar(200) | YES  |     | NULL    |       |
| prefecture | varchar(50)  | YES  |     | NULL    |       |
| address    | text         | YES  |     | NULL    |       |
| age        | int(11)      | YES  |     | NULL    |       |
+------------+--------------+------+-----+---------+-------+
6 rows in set (0.17 sec)
```

