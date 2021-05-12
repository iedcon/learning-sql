## Q. 5-1
> 아래 결과를 낼 수 있는 쿼리
```sql
MariaDB [sakila]> SELECT c.first_name, c.last_name, a.address, ct.city
    -> FROM customer c
    ->   INNER JOIN address a
    ->   ON c.address_id = a.address_id
    ->   INNER JOIN city ct
    ->   ON a.city_id = ct.city_id
    -> WHERE a.district = 'California';
+------------+-----------+------------------------+----------------+
| first_name | last_name | address                | city           |
+------------+-----------+------------------------+----------------+
| PATRICIA   | JOHNSON   | 1121 Loja Avenue       | San Bernardino |
| BETTY      | WHITE     | 770 Bydgoszcz Avenue   | Citrus Heights |
| ALICE      | STEWART   | 1135 Izumisano Parkway | Fontana        |
| ROSA       | REYNOLDS  | 793 Cam Ranh Avenue    | Lancaster      |
| RENEE      | LANE      | 533 al-Ayn Boulevard   | Compton        |
| KRISTIN    | JOHNSTON  | 226 Brest Manor        | Sunnyvale      |
| CASSANDRA  | WALTERS   | 920 Kumbakonam Loop    | Salinas        |
| JACOB      | LANCE     | 1866 al-Qatif Avenue   | El Monte       |
| RENE       | MCALISTER | 1895 Zhezqazghan Drive | Garden Grove   |
+------------+-----------+------------------------+----------------+
9 rows in set (0.002 sec)
```

## Q. 5-2
>JOHN 이라는 이름의 배우가 출연한 모든 영화의 제목을 반환하는 쿼리
```sql
MariaDB [sakila]> SELECT f.title FROM film f
    -> INNER JOIN film_actor fa
    -> ON fa.film_id = f.film_id
    -> INNER JOIN actor a
    -> ON fa.actor_id = a.actor_id
    -> WHERE a.first_name = 'JOHN';
+---------------------------+
| title                     |
+---------------------------+
| ALLEY EVOLUTION           |
| BEVERLY OUTLAW            |
| CANDLES GRAPES            |
| CLEOPATRA DEVIL           |
| COLOR PHILADELPHIA        |
| CONQUERER NUTS            |
| DAUGHTER MADIGAN          |
| GLEAMING JAWBREAKER       |
| GOLDMINE TYCOON           |
| HOME PITY                 |
| INTERVIEW LIAISONS        |
| ISHTAR ROCKETEER          |
| JAPANESE RUN              |
| JERSEY SASSY              |
| LUKE MUMMY                |
| MILLION ACE               |
| MONSTER SPARTACUS         |
| NAME DETECTIVE            |
| NECKLACE OUTBREAK         |
| NEWSIES STORY             |
| PET HAUNTING              |
| PIANIST OUTFIELD          |
| PINOCCHIO SIMON           |
| PITTSBURGH HUNCHBACK      |
| QUILLS BULL               |
| RAGING AIRPLANE           |
| ROXANNE REBEL             |
| SATISFACTION CONFIDENTIAL |
| SONG HEDWIG               |
+---------------------------+
29 rows in set (0.001 sec)
```

## Q. 5-3
> 같은 도시에 있으면서 서로 다른 주소를 반환하는 쿼리
```sql
MariaDB [sakila]> SELECT a1.address, a2.address
    -> FROM address a1
    ->   INNER JOIN address a2
    ->   ON a1.city_id = a2.city_id
    -> WHERE a1.address_id != a2.address_id;
+----------------------+----------------------+
| address              | address              |
+----------------------+----------------------+
| 47 MySakila Drive    | 23 Workhaven Lane    |
| 28 MySQL Boulevard   | 1411 Lillydale Drive |
| 23 Workhaven Lane    | 47 MySakila Drive    |
| 1411 Lillydale Drive | 28 MySQL Boulevard   |
| 1497 Yuzhou Drive    | 548 Uruapan Street   |
| 587 Benguela Manor   | 43 Vilnius Manor     |
| 548 Uruapan Street   | 1497 Yuzhou Drive    |
| 43 Vilnius Manor     | 587 Benguela Manor   |
+----------------------+----------------------+
8 rows in set (0.002 sec)
```