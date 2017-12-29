---
title: knex의 Array 컨트롤
date: 2017-11-22 19:28:10
categories:
    - Node.js
---

- 데이터 삽입

````sql
INSERT INTO bglam_services ("possibleLanguages")
VALUES ('{5, 2, 6}');
-- VALUES(ARRAY[5, 2, 6])
````

- 업데이트

````sql
UPDATE bglam_services
SET "possibleLanguages" = '{1, 2, 3}'
-- set "possibleLanguages" = ARRAY[1, 1, 1]
-- set "possibleLanguages"[1] = 3
WHERE ID = 875;
````

- 데이터 조회

````sql
SELECT   "possibleLanguages"[1],
		"possibleLanguages"[1:2] -- 시작인덱스:끝인덱스
FROM     bglam_services;

SELECT *
FROM services
WHERE types && '{1,2,3}';
-- WHERE 1 = ANY("possibleLanguages")
````

&& 연산자는 두 배열 사이에서 겹치는게 하나라도 있으면 true를 반환

## Reference

https://stackoverflow.com/questions/33335338/inserting-array-values

배열 비교 연산자 : https://www.postgresql.org/docs/9.1/static/functions-array.html