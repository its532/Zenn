---
title: "sql基本の基本"
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
| 2    | tarou | female |

このようなテーブルを作りたいとして、以下のようなsqlを書く。

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
INSERT INTO user(name, gender)
VALUES(its, male);
```


| id   | name | gender |
| ---- | ---- | ---- |
| 1    | yamada | male |
| 2    | tarou | female |
| 3    | its | male |

# SELECT

テーブルを取得するためにカラムを指定する。`*`を用いることでテーブル全体を指定することも可能。

# FROM
どのテーブルからデータをとってくるか指定する。

## テーブルのデータを丸々とってくる

```sql
SELECT *
FROM user;
```

| id   | name | gender |
| ---- | ---- | ---- |
| 1    | yamada | male |
| 2    | tarou | female |
| 3    | its | male |

## テーブルのカラムで指定

```sql
SELECT name
FROM user;
```

| name |
| ---- |
| yamada |
| tarou |
| its |

## テーブルの複数カラムで指定

```sql
SELECT name,gender
FROM user;
```

| name | gender |
| ---- | ---- |
| yamada | male |
| tarou | female |
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
| 2    | tarou | female |


# UPDATE
テーブルの内容を更新するときに使う。
DELETE同様にWhereを用いて条件をつけることができる。

```sql
UPDATE user
SET gender = 'female'
WHERE name = 'yamada';
```

| id   | name | gender |
| ---- | ---- | ---- |
| 1    | yamada | female |
| 2    | tarou | female |

# ORDER BY
データを並び替える時に使う。
列ごとに昇順 (ASC) 降順 (DESC) を指定することができる。デフォルトは昇順となっている。

```sql
SELECT *
FROM user
ORDER BY　id DESC;
```
| id   | name | gender |
| ---- | ---- | ---- |
| 2    | tarou | female |
| 1    | yamada | female |
