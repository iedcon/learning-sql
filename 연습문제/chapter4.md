## 4-1, 4-2를 위한 서브셋

```sql
MariaDB [sakila]> (SELECT payment_id, customer_id, amount, date(payment_date) FROM payment WHERE payment_id BETWEEN 101 AND 120);
+------------+-------------+--------+--------------------+
| payment_id | customer_id | amount | date(payment_date) |
+------------+-------------+--------+--------------------+
|        101 |           4 |   8.99 | 2005-08-18         |
|        102 |           4 |   1.99 | 2005-08-19         |
|        103 |           4 |   2.99 | 2005-08-20         |
|        104 |           4 |   6.99 | 2005-08-20         |
|        105 |           4 |   4.99 | 2005-08-21         |
|        106 |           4 |   2.99 | 2005-08-22         |
|        107 |           4 |   1.99 | 2005-08-23         |
|        108 |           5 |   0.99 | 2005-05-29         |
|        109 |           5 |   6.99 | 2005-05-31         |
|        110 |           5 |   1.99 | 2005-05-31         |
|        111 |           5 |   3.99 | 2005-06-15         |
|        112 |           5 |   2.99 | 2005-06-16         |
|        113 |           5 |   4.99 | 2005-06-17         |
|        114 |           5 |   2.99 | 2005-06-19         |
|        115 |           5 |   4.99 | 2005-06-20         |
|        116 |           5 |   4.99 | 2005-07-06         |
|        117 |           5 |   2.99 | 2005-07-08         |
|        118 |           5 |   4.99 | 2005-07-09         |
|        119 |           5 |   5.99 | 2005-07-09         |
|        120 |           5 |   1.99 | 2005-07-09         |
+------------+-------------+--------+--------------------+
20 rows in set (0.001 sec)
```

## Q. 4-1
>customer_id <> 5 AND (amount > 8 OR date(payment_date) = '2005-08-23')을 만족하는 payment ID는?
```sql
MariaDB [sakila]> SELECT pay.payment_id FROM (SELECT payment_id, customer_id, amount, date(payment_date) AS payment_date FROM payment WHERE payment_id BETWEEN 101 AND 120) pay WHERE pay.customer_id <> 5 AND (pay.amount > 8 OR pay.payment_date = '2005-08-23');
+------------+
| payment_id |
+------------+
|        101 |
|        107 |
+------------+
2 rows in set (0.001 sec)
```

## Q. 4-2
>customer_id = 5 AND NOT (amount > 6 OR date(payment_date) = '2005-06-19')를 만족하는 payment ID는?
```sql
MariaDB [sakila]> SELECT pay.payment_id FROM (SELECT payment_id, customer_id, amount, date(payment_date) AS payment_date FROM payment WHERE payment_id BETWEEN 101 AND 120) pay WHERE pay.customer_id = 5 AND NOT (pay.amount > 6 OR pay.payment_date = '2005-06-19');
+------------+
| payment_id |
+------------+
|        108 |
|        110 |
|        111 |
|        112 |
|        113 |
|        115 |
|        116 |
|        117 |
|        118 |
|        119 |
|        120 |
+------------+
11 rows in set (0.001 sec)
```

## Q. 4-3
>payment 테이블에서 금액이 1.98, 7.98 또는 9.98인 모든 행을 검색하는 쿼리
```sql
MariaDB [sakila]> SELECT * FROM payment WHERE amount IN (1.98, 7.98, 9.98);
+------------+-------------+----------+-----------+--------+---------------------+---------------------+
| payment_id | customer_id | staff_id | rental_id | amount | payment_date        | last_update         |
+------------+-------------+----------+-----------+--------+---------------------+---------------------+
|       1482 |          53 |        2 |     11657 |   7.98 | 2006-02-14 15:16:03 | 2006-02-15 22:12:42 |
|       1670 |          60 |        2 |     12489 |   9.98 | 2006-02-14 15:16:03 | 2006-02-15 22:12:45 |
|       2901 |         107 |        1 |     13079 |   1.98 | 2006-02-14 15:16:03 | 2006-02-15 22:13:03 |
|       4234 |         155 |        2 |     11496 |   7.98 | 2006-02-14 15:16:03 | 2006-02-15 22:13:33 |
|       4449 |         163 |        2 |     11754 |   7.98 | 2006-02-14 15:16:03 | 2006-02-15 22:13:38 |
|       7243 |         267 |        2 |     12066 |   7.98 | 2006-02-14 15:16:03 | 2006-02-15 22:15:06 |
|       9585 |         354 |        1 |     12759 |   7.98 | 2006-02-14 15:16:03 | 2006-02-15 22:16:47 |
+------------+-------------+----------+-----------+--------+---------------------+---------------------+
7 rows in set (0.011 sec)
```

## Q. 4-4
> last_name의 두 번째 위치에 A가 있고 A 다음에 W가 있는(위치 무관) 모든 고객을 찾는 쿼리
```sql
MariaDB [sakila]> SELECT * FROM customer WHERE last_name LIKE '_A%W%';
+-------------+----------+------------+------------+------------------------------------+------------+--------+---------------------+---------------------+
| customer_id | store_id | first_name | last_name  | email                              | address_id | active | create_date         | last_update         |
+-------------+----------+------------+------------+------------------------------------+------------+--------+---------------------+---------------------+
|         159 |        1 | JILL       | HAWKINS    | JILL.HAWKINS@sakilacustomer.org    |        163 |      1 | 2006-02-14 22:04:36 | 2006-02-15 04:57:20 |
|         169 |        2 | ERICA      | MATTHEWS   | ERICA.MATTHEWS@sakilacustomer.org  |        173 |      0 | 2006-02-14 22:04:36 | 2006-02-15 04:57:20 |
|         192 |        1 | LAURIE     | LAWRENCE   | LAURIE.LAWRENCE@sakilacustomer.org |        196 |      1 | 2006-02-14 22:04:36 | 2006-02-15 04:57:20 |
|         200 |        2 | JEANNE     | LAWSON     | JEANNE.LAWSON@sakilacustomer.org   |        204 |      1 | 2006-02-14 22:04:36 | 2006-02-15 04:57:20 |
|         272 |        1 | KAY        | CALDWELL   | KAY.CALDWELL@sakilacustomer.org    |        277 |      1 | 2006-02-14 22:04:37 | 2006-02-15 04:57:20 |
|         300 |        1 | JOHN       | FARNSWORTH | JOHN.FARNSWORTH@sakilacustomer.org |        305 |      1 | 2006-02-14 22:04:37 | 2006-02-15 04:57:20 |
|         358 |        2 | SAMUEL     | MARLOW     | SAMUEL.MARLOW@sakilacustomer.org   |        363 |      1 | 2006-02-14 22:04:37 | 2006-02-15 04:57:20 |
|         361 |        2 | LAWRENCE   | LAWTON     | LAWRENCE.LAWTON@sakilacustomer.org |        366 |      1 | 2006-02-14 22:04:37 | 2006-02-15 04:57:20 |
|         421 |        1 | LEE        | HAWKS      | LEE.HAWKS@sakilacustomer.org       |        426 |      1 | 2006-02-14 22:04:37 | 2006-02-15 04:57:20 |
+-------------+----------+------------+------------+------------------------------------+------------+--------+---------------------+---------------------+
9 rows in set (0.002 sec)
```