---
title: "sql基本"
emoji: "🐈"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [sql, datebase]
published: false
---

# CREATE TABLE
テーブルの作成をする際に`create table`を実行。

| id   | name | gender |
| ---- | ---- | ---- |
| 1    | yamada | male |
| 2    | hanako | female |

このようなテーブルを作りたいとして、以下のsqlを書く。

```sql
CREATE TABLE user(
    id VARCHAR(4) NOT NULL,
    name VARCHAR(20) NOT NULL,
    gender VARCHAR(20) NOT NULL,
    PRIMARY KEY (id);
)
```

# INSERT
テーブルにレコードを追加するときに使う。

```sql
INSERT INTO users(name, gender)
VALUES(its, male);
```


| id   | name | gender |
| ---- | ---- | ---- |
| 1    | yamada | male |
| 2    | hanako | female |
| 3    | its | male |

# SELECT

テーブルを取得するためにカラムを指定する。`*`を用いることでテーブル全体を指定することも可能。

# FROM
どのテーブルからデータをとってくるか指定する。

## テーブルのデータを丸々とってくる

```sql
SELECT *
FROM users;
```

| id   | name | gender |
| ---- | ---- | ---- |
| 1    | yamada | male |
| 2    | hanako | female |
| 3    | its | male |

## テーブルのカラムで指定

```sql
SELECT name
FROM users;
```

| name |
| ---- |
| yamada |
| hanako |
| its |

## テーブルの複数カラムで指定

```sql
SELECT name,gender
FROM users;
```

| name | gender |
| ---- | ---- |
| yamada | male |
| hanako | female |
| its | male |

# DELETE
指定のデータを削除することができる。
`Where`を用いることで条件をつけることができる。

## テーブル削除
```sql
DELETE FROM users;
```

## テーブルの指定したものを削除
```sql
DELETE FROM users
WHERE name = its;
```

| id   | name | gender |
| ---- | ---- | ---- |
| 1    | yamada | male |
| 2    | hanako | female |


# UPDATE
テーブルの内容を更新するときに使う。
DELETE同様にWhereを用いて条件をつけることができる。

```sql
UPDATE users
SET gender = 'female'
WHERE name = 'yamada';
```

| id   | name | gender |
| ---- | ---- | ---- |
| 1    | yamada | female |
| 2    | hanako | female |

# AS
データを取得する際に、カラム名(テーブル名も)を別名をつけることができる。
```sql
SELECT name as　`名前`, gender as　`性別`,
FROM users
```

| 名前 | 性別 |
| ---- | ---- |
| yamada | male |
| hanako | female |

# EXISTS
`EXISTS`はサブクエリが返す値をbooleanで返し、trueの時にメインクエリを実行する。
ここではuserテーブルのnameにyamadaが存在していたらuserテーブルを返すという処理をしている。
```sql
SELECT * FROM users
WHERE EXISTS
(SELECT * FROM users
WHERE name = 'yamada');
```

| id   | name | gender |
| ---- | ---- | ---- |
| 1    | yamada | male |
| 2    | hanako | female |

# DISTINCT
重複したデータを取り除いて、データを取得することができる。
同じ名前の人が二人いるとして
| id   | name | gender |
| ---- | ---- | ---- |
| 1    | yamada | male |
| 2    | hanako | female |
| 3    | hanako | female |

```sql
SELECT distinct name
FROM users
```

| name |
| ---- |
| yamada |
| hanako |

# ORDER BY
データを並び替える時に使う。
列ごとに昇順 (ASC) 降順 (DESC) を指定することができる。デフォルトは昇順となっている。

```sql
SELECT *
FROM users
ORDER BY　id DESC;
```
| id   | name | gender |
| ---- | ---- | ---- |
| 2    | hanako | female |
| 1    | yamada | female |

# COUNT
`COUNT`はレコード数を取得する。

```sql
SELECT COUNT(*)
FROM users
-- 2
```

| id   | name | gender |
| ---- | ---- | ---- |
| 1    | yamada | male |
| 2    | hanako | female |


# GROUP BY
指定したカラムの値を基準にデータをグループ化し、集計関数を用いて複数のデータをまとめて計算することができる。

| id   | name | gender |
| ---- | ---- | ---- |
| 1    | yamada | male |
| 2    | hanako | female |
| 3    | its | male |


```sql
SELECT COUNT(*) as count
FROM users GROUP BY gender
```
| gender | count |
| ---- | ---- |
| male |  2  |
| female |  1  |
