# MySQL に関するセルフハンズオンの流れ

1. MySQL に接続する
  - connect: `mysql -h 127.0.0.1 --port PPPP -p -u UUUU`
    - PPPP はポート番号（例: 3306）、UUUU はログインするユーザー名
    - このあとパスワードを要求される。接続後に `status;` で接続先と認証方式を確認できる
2. データベースを洗い出し、選択する
  - list: `show databases;`
  - set: `use DDD;`
    - DDD は利用したいデータベース名
  - get: `select database();`
3. テーブルを洗い出す
  - list: `show tables;`
4. スキーマを確認する
  - get: `show create table TTT;`
    - create 文が出力される。index や foreign key の情報も出る。
    - TTT は確認したいテーブル名
  - get: `desc TTT;` / `describe TTT;`
  - get: `show columns from TTT;`
    - `desc`/`describe` は `show columns` のエイリアス。NULL 許可やデフォルト値など列ごとの定義がまとまって分かる
  - get: `show index from TTT;`
    - 主キー/セカンダリキーや `Cardinality`（統計的な行数推定）、`Visible` など index に関する詳細が出力される
5. クエリーの効率性を確認する
  - get: `explain QQQQ;`
    - QQQQ は解析したい SELECT/INSERT/UPDATE などのクエリー。`EXPLAIN ANALYZE` で実行計画と実測時間を両方確認できる（MySQL 8.0+）

# 注意事項
## mysql_native_password plugin
MySQL 8.4 から MySQL 9.0 にアップグレードする過程で除去された。これの影響で、MySQL 9.0 だとパスワードでログインできないはず。
- 代替として `caching_sha2_password` や `sha256_password` などサポートされている認証方式でユーザーを再作成する (by GPT-5-Codex, 2025-09-17)
- 詳細: <https://dev.mysql.com/doc/refman/9.0/en/mysql-nutshell.html>
