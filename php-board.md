### 基本表示 SQL
```sql
select * from board where dflg is null order by row_no desc
```
- ## 表示順は登校が新しい順
  - 自動採番の主キーを逆順にソートする

- ## 表示データの条件
  - dflg が null
- ## 削除されたデータの条件
  - dflg が "D"
