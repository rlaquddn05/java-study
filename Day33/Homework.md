### MySQL숙제
#### 숙제1

```MySQL
-- 초기 데이터 입력 
MariaDB [testdb]> select * from pokemon;
+----+----------+-------+------+------+---------------------+
| no | name     | level | hp   | ap   | regdate             |
+----+----------+-------+------+------+---------------------+
|  1 | 피카츄   |    10 |  100 |    5 | 2020-12-09 15:41:11 |
|  2 | 푸린     |     5 |  300 |   50 | 2020-12-09 15:41:11 |
|  3 | 라이츄   |     3 |  100 |    5 | 2020-12-09 15:41:11 |
|  4 | 망나뇽   |     7 |  100 |    6 | 2020-12-09 15:41:11 |
|  5 | 치코리타 |     8 |  100 |    9 | 2020-12-09 15:41:11 |
|  6 | 잠만보   |    90 |  100 |   10 | 2020-12-09 15:41:11 |
|  7 | 뚜벅초   |    15 |  100 |    2 | 2020-12-09 15:41:11 |
|  8 | 닥트리오 |   100 | NULL | NULL | 2020-12-09 15:41:13 |
|  9 | 뮤       |    30 | NULL | NULL | 2019-11-28 22:10:03 |
| 10 | 피츄     |    30 | NULL | NULL | 2019-02-28 12:14:23 |
+----+----------+-------+------+------+---------------------+
10 rows in set (0.000 sec)

--등록일자가 2020/01/01 이전인 포켓몬들의 번호, 이름, 등록일자 알려줘
MariaDB [testdb]> SELECT name, regdate FROM pokemon WHERE regdate < 2020/01/01;
Empty set, 1 warning (0.007 sec)

-- 레벨이 5 이상 10 이하인 포켓몬들의 모든 정보 알려줘 
MariaDB [testdb]> SELECT * FROM pokemon WHERE level >= 5 AND level <=10;
+----+----------+-------+------+------+---------------------+
| no | name     | level | hp   | ap   | regdate             |
+----+----------+-------+------+------+---------------------+
|  1 | 피카츄   |    10 |  100 |    5 | 2020-12-09 15:41:11 |
|  2 | 푸린     |     5 |  300 |   50 | 2020-12-09 15:41:11 |
|  4 | 망나뇽   |     7 |  100 |    6 | 2020-12-09 15:41:11 |
|  5 | 치코리타 |     8 |  100 |    9 | 2020-12-09 15:41:11 |
+----+----------+-------+------+------+---------------------+
4 rows in set (0.001 sec)

-- 모든 포켓몬들의 레벨 보여줘
MariaDB [testdb]> SELECT level  FROM pokemon;
+-------+
| level |
+-------+
|    10 |
|     5 |
|     3 |
|     7 |
|     8 |
|    90 |
|    15 |
|   100 |
|    30 |
|    30 |
+-------+
10 rows in set (0.000 sec)

-- 모든 포켓몬들의 레벨 보여줘. 중복 제거 해줘. (DISTINCT)
MariaDB [testdb]> SELECT DISTINCT level FROM pokemon;
+-------+
| level |
+-------+
|    10 |
|     5 |
|     3 |
|     7 |
|     8 |
|    90 |
|    15 |
|   100 |
|    30 |
+-------+
9 rows in set (0.007 sec)

--모든 포켓몬들의 이름, 레벨 보여줘. 이름 오름차순으로 보여줘  (ORDER BY) (순서상 제일 마지막에 실행해서 결과창 숫자가 이상함)
MariaDB [testdb]> SELECT name, level FROM pokemon ORDER BY name ASC;
+----------+-------+
| name     | level |
+----------+-------+
| 닥트리오 |    49 |
| 뚜벅초   |    32 |
| 라이츄   |     8 |
| 망나뇽   |    16 |
| 뮤       |    31 |
| 잠만보   |    88 |
| 치코리타 |     9 |
| 푸린     |    12 |
| 피츄     |    31 |
| 피카츄   |    11 |
+----------+-------+
10 rows in set (0.000 sec)

모든 포켓몬들의 이름, 레벨 보여줘. 레벨 많은 순으로 보여줘  (ORDER BY) 
MariaDB [testdb]> SELECT name, level FROM pokemon ORDER BY level DESC;
+----------+-------+
| name     | level |
+----------+-------+
| 잠만보   |    88 |
| 닥트리오 |    49 |
| 뚜벅초   |    32 |
| 뮤       |    31 |
| 피츄     |    31 |
| 망나뇽   |    16 |
| 푸린     |    12 |
| 피카츄   |    11 |
| 치코리타 |     9 |
| 라이츄   |     8 |
+----------+-------+
10 rows in set (0.000 sec)


--레벨이 3이상인 모든 포켓몬들의 이름, 레벨 보여줘. 레벨 많은 순으로, 같은 레벨이면 이름 오름차순으로 보여줘  (ORDER BY)
MariaDB [testdb]> SELECT name, level FROM pokemon WHERE level >=3 ORDER BY level DESC, name ASC;
+----------+-------+
| name     | level |
+----------+-------+
| 닥트리오 |   100 |
| 잠만보   |    90 |
| 뮤       |    30 |
| 피츄     |    30 |
| 뚜벅초   |    15 |
| 피카츄   |    10 |
| 치코리타 |     8 |
| 망나뇽   |     7 |
| 푸린     |     5 |
| 라이츄   |     3 |
+----------+-------+
10 rows in set (0.001 sec)

-- 모든 포켓몬들의 이름, 레벨 보여줘. 등록일자 최신순으로 보여줘.
MariaDB [testdb]> SELECT name, level FROM pokemon ORDER BY regdate DESC;
+----------+-------+
| name     | level |
+----------+-------+
| 닥트리오 |   100 |
| 피카츄   |    10 |
| 뚜벅초   |    15 |
| 잠만보   |    90 |
| 치코리타 |     8 |
| 망나뇽   |     7 |
| 라이츄   |     3 |
| 푸린     |     5 |
| 뮤       |    30 |
| 피츄     |    30 |
+----------+-------+
10 rows in set (0.000 sec)

-- 레벨이 100 미만인 포켓몬들의 레벨을 1씩 증가해줘
MariaDB [testdb]> UPDATE pokemon SET level= level +1 WHERE level <= 50;
Query OK, 8 rows affected (0.008 sec)
Rows matched: 8  Changed: 8  Warnings: 0

MariaDB [testdb]> SELECT * FROM pokemon;
+----+----------+-------+------+------+---------------------+
| no | name     | level | hp   | ap   | regdate             |
+----+----------+-------+------+------+---------------------+
|  1 | 피카츄   |    11 |  100 |    5 | 2020-12-09 15:41:11 |
|  2 | 푸린     |     6 |  300 |   50 | 2020-12-09 15:41:11 |
|  3 | 라이츄   |     4 |  100 |    5 | 2020-12-09 15:41:11 |
|  4 | 망나뇽   |     8 |  100 |    6 | 2020-12-09 15:41:11 |
|  5 | 치코리타 |     9 |  100 |    9 | 2020-12-09 15:41:11 |
|  6 | 잠만보   |    90 |  100 |   10 | 2020-12-09 15:41:11 |
|  7 | 뚜벅초   |    16 |  100 |    2 | 2020-12-09 15:41:11 |
|  8 | 닥트리오 |   100 | NULL | NULL | 2020-12-09 15:41:13 |
|  9 | 뮤       |    31 | NULL | NULL | 2019-11-28 22:10:03 |
| 10 | 피츄     |    31 | NULL | NULL | 2019-02-28 12:14:23 |
+----+----------+-------+------+------+---------------------+
10 rows in set (0.000 sec)

-- 포켓몬 중 레벨이 100 인 포켓몬들을 삭제해줘(순서상 뒤에서 실행하여 변경사항 없음)
MariaDB [testdb]> DELETE FROM pokemon WHERE level = 100;
Query OK, 0 rows affected (0.000 sec)

-- 레벨이 짝수인 포켓몬들의 레벨을 두배로 변경해줘
MariaDB [testdb]> UPDATE pokemon SET level = level *2 WHERE level%2=0 ;
Query OK, 5 rows affected (0.009 sec)
Rows matched: 5  Changed: 5  Warnings: 0

MariaDB [testdb]> SELECT * FROM pokemon;
+----+----------+-------+------+------+---------------------+
| no | name     | level | hp   | ap   | regdate             |
+----+----------+-------+------+------+---------------------+
|  1 | 피카츄   |    11 |  100 |    5 | 2020-12-09 15:41:11 |
|  2 | 푸린     |    12 |  300 |   50 | 2020-12-09 15:41:11 |
|  3 | 라이츄   |     8 |  100 |    5 | 2020-12-09 15:41:11 |
|  4 | 망나뇽   |    16 |  100 |    6 | 2020-12-09 15:41:11 |
|  5 | 치코리타 |     9 |  100 |    9 | 2020-12-09 15:41:11 |
|  6 | 잠만보   |    88 |  100 |   10 | 2020-12-09 15:41:11 |
|  7 | 뚜벅초   |    32 |  100 |    2 | 2020-12-09 15:41:11 |
|  8 | 닥트리오 |    49 | NULL | NULL | 2020-12-09 15:41:13 |
|  9 | 뮤       |    31 | NULL | NULL | 2019-11-28 22:10:03 |
| 10 | 피츄     |    31 | NULL | NULL | 2019-02-28 12:14:23 |
+----+----------+-------+------+------+---------------------+
10 rows in set (0.001 sec)

체력이 레벨의 100배보다 큰 포켓몬들의 레벨을 체력의 1/100로 수정해줘
MariaDB [testdb]> UPDATE pokemon SET level = hp * 0.01 WHERE hp > level*100;
Query OK, 0 rows affected (0.000 sec)
Rows matched: 0  Changed: 0  Warnings: 0

MariaDB [testdb]> SELECT * FROM pokemon;
+----+----------+-------+------+------+---------------------+
| no | name     | level | hp   | ap   | regdate             |
+----+----------+-------+------+------+---------------------+
|  1 | 피카츄   |    11 |  100 |    5 | 2020-12-09 15:41:11 |
|  2 | 푸린     |    12 |  300 |   50 | 2020-12-09 15:41:11 |
|  3 | 라이츄   |     8 |  100 |    5 | 2020-12-09 15:41:11 |
|  4 | 망나뇽   |    16 |  100 |    6 | 2020-12-09 15:41:11 |
|  5 | 치코리타 |     9 |  100 |    9 | 2020-12-09 15:41:11 |
|  6 | 잠만보   |    88 |  100 |   10 | 2020-12-09 15:41:11 |
|  7 | 뚜벅초   |    32 |  100 |    2 | 2020-12-09 15:41:11 |
|  8 | 닥트리오 |    49 | NULL | NULL | 2020-12-09 15:41:13 |
|  9 | 뮤       |    31 | NULL | NULL | 2019-11-28 22:10:03 |
| 10 | 피츄     |    31 | NULL | NULL | 2019-02-28 12:14:23 |
+----+----------+-------+------+------+---------------------+
10 rows in set (0.000 sec)
```
#### 숙제2
```MySQL
MariaDB [testdb]> CREATE TABLE member(
    ->     `no` INT PRIMARY KEY AUTO_INCREMENT,
    ->     `id` VARCHAR(20) NOT NULL UNIQUE,
    ->     `password` VARCHAR(21),
    ->     `email` VARCHAR(40) UNIQUE,
    ->     `type` INT(1) CHECK (type >=1 AND type <=4),
    ->     `point` INT(7) DEFAULT 1000 CHECK (point >0));
Query OK, 0 rows affected (0.022 sec)

MariaDB [testdb]> DESC member;
+----------+-------------+------+-----+---------+----------------+
| Field    | Type        | Null | Key | Default | Extra          |
+----------+-------------+------+-----+---------+----------------+
| no       | int(11)     | NO   | PRI | NULL    | auto_increment |
| id       | varchar(20) | NO   | UNI | NULL    |                |
| password | varchar(21) | YES  |     | NULL    |                |
| email    | varchar(40) | YES  | UNI | NULL    |                |
| type     | int(1)      | YES  |     | NULL    |                |
| point    | int(7)      | YES  |     | 1000    |                |
+----------+-------------+------+-----+---------+----------------+
6 rows in set (0.046 sec)

MariaDB [testdb]> CREATE TABLE QNA (
    ->    no INT PRIMARY KEY AUTO_INCREMENT,
    ->    writer_no INT(9),
    ->    content VARCHAR(100) NOT NULL,
    ->     regdate DATETIME DEFAULT CURRENT_TIMESTAMP,
    ->    FOREIGN KEY(writer_no) REFERENCES member(no) ON DELETE CASCADE
    ->    );
Query OK, 0 rows affected (0.018 sec)

MariaDB [testdb]> DESC QNA;
+-----------+--------------+------+-----+---------------------+----------------+
| Field     | Type         | Null | Key | Default             | Extra          |
+-----------+--------------+------+-----+---------------------+----------------+
| no        | int(11)      | NO   | PRI | NULL                | auto_increment |
| writer_no | int(9)       | YES  | MUL | NULL                |                |
| content   | varchar(100) | NO   |     | NULL                |                |
| regdate   | datetime     | YES  |     | current_timestamp() |                |
+-----------+--------------+------+-----+---------------------+----------------+
4 rows in set (0.027 sec)
