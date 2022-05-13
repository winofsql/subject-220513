### CTRL + SPACE でスニペットを表示して SQL を作成 

### VSCode の 拡張をインストールしていると、拡張子 .sql のファイル上のSQL の上に実行リンクが表示される
( SQL と SQL の切れ目は、; (セミコロン)　だが、SQL の特殊な記述によってはバグが散見される( RUN が表示されない )

### 1) 日付関数のバリエーション
### 2) NULL 値を含む計算方法 : IFNULL 関数を使用
### 3) SELECT ～ INTO OUTFILE ファイルパス オプション で、SQL の結果をテキストファイルに出力可能

### フォーットを適用 : SHIFT + ALT + F

```sql
SELECT
    CURDATE() AS 今日,
    NOW() AS 日付と時間,
    DATE_FORMAT(CURDATE(), '%Y/%m/%d') AS フォーマット,
    CURDATE() + INTERVAL 1 DAY AS 日数加算1,
    DATE_ADD(CURDATE(), INTERVAL 1 DAY) AS 日数加算2,
    DATE_ADD(CURDATE(), INTERVAL -1 MONTH) AS 月数加算,
    DATE_ADD(CURDATE(), INTERVAL 1 YEAR) AS 年数加算,
    TO_DAYS(CURDATE()) - TO_DAYS(CAST('2021/01/01' AS DATETIME)) AS 経過日数,
    DATE_FORMAT(CURDATE(), '%d') AS 日,
    DATE_FORMAT(CURDATE(), '%j') AS 年間通算日,
    DAYOFYEAR(CURDATE()) AS 年間通算日,
    DATE_FORMAT(NOW(), '%H') AS 時,
    DATE_FORMAT(NOW(), '%i') AS 分,
    DATE_FORMAT(NOW(), '%S') AS 秒,
    DATE_FORMAT(CURDATE(), '%m') AS 月,
    DATE_FORMAT(CURDATE(), '%w') AS 曜日,
    DATE_FORMAT(CURDATE(), '%U') AS 週,
    DATE_FORMAT(CURDATE(), '%Y') AS 年;

SELECT
    IFNULL(NULL, 0) + 1 AS 計算結果;

SELECT
    氏名,
    給与 + IFNULL(手当, 0) AS 支給額
FROM
    社員マスタ;

SELECT
    氏名,
    給与 + COALESCE(手当, 0) AS 支給額
FROM
    社員マスタ;

SELECT
    *
FROM
    得意先マスタ
    LEFT OUTER JOIN 社員マスタ ON 得意先マスタ.担当者 = 社員マスタ.社員コード;

SELECT
    * INTO OUTFILE '/xampp/tmp/test.csv' FIELDS TERMINATED BY ',' OPTIONALLY ENCLOSED BY '"' LINES TERMINATED BY '\n'
FROM
    社員マスタ;
```

- ### スニペットの作成時にパラメータを投すると、実行時に入力モードとなる
    - TAB キーで次の入力に進む事ができる

```json
    "select-left-outer": {
        "scope": "sql",
        "prefix": "select-left-outer-join",
        "body": [
            "SELECT * FROM $1",
            "    LEFT OUTER JOIN $2",
            "    ON $1.$3 = $2.$4",
            ";",
        ],
        "description": ""
    }
```
