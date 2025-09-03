# MySQL に関するセルフハンズオンの流れ

1. MySQL に接続する
  - connect: `mysql -h 127.0.0.1 --port PPPP -p -u UUUU`
    - PPPP はポート番号、UUUU はユーザー名
    - このあとパスワードを要求される
2. データベースを洗い出し、選択する
  - list: `show databases;`
  - set: `use DDD;`
  - get: `select database();`
3. テーブルを洗い出す
  - list: `show tables;`
4. スキーマを確認する
  - get: `show create table TTT;`
    - create 文が出力される。index や foreign key の情報も出る。
  - get: `desc TTT;` `describe TTT;`
  - get: `show columns from TTT;`
    - desc と同じ
  - get: `show index from TTT;`
    - cardinality なども出力される。
5. クエリーの効率性を確認する
  - get: `explain QQQQ;`
    - QQQQ はクエリーがそのまま入る

# 注意事項
## mysql_native_password plugin
MySQL 8.4 から MySQL 9.0 にアップグレードする過程で除去された。これの影響で、MySQL 9.0 だとパスワードでログインできないはず。 <https://dev.mysql.com/doc/refman/9.0/en/mysql-nutshell.html>
