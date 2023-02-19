# 내장 함수
- `lower(str)`: 소문자 변환
- `upper(str)`: 대문자 변환
- `year(date)`: 년도 추출
- `round(숫자, 반올림할 자릿수)`: 반올림할 자리 + 1 에서 반올림, `반올림할 자릿수`를 안쓸경우 소수점 첫번째 자리에서 반올림, -1과 같이 음수를 사용할 경우 정수부 |-1 + 1| 번째 자리에서 반올림
```sql
SELECT ROUND(3456.1234567) FROM DUAL
-- 3456

SELECT ROUND(3456.1234567 ,1) FROM DUAL
-- 3456.1

SELECT ROUND(3456.1234567 ,4) FROM DUAL
-- 3456.1235

SELECT ROUND(3456.1234567 ,-1) FROM DUAL
-- 3460

SELECT ROUND(3456.1234567 ,-2) FROM DUAL
-- 3500
```
- `truncate(숫자, 자릿수)`:  숫자를 자릿수 + 1에서 버림
- `date_format(datetime, '%Y-%m-%d')`: 데이트 포맷 함수로 `202-03-01`과 같이 출력된다.
- MySQL 문자열 검색
	- `LIKE`: LIKE 문자열패턴
		- 부정형은 NOT LIKE
		- 대소문자를 구분하지 않음 -> `LIKE BINARY` 를 사용하면 대소문자 구분
		- 문자열패턴은 `%` 는 와일드카드로 (어떠한 문자 {0, }개), `_`는 임의의 문자1개
	- `LOCATE`: LOCATE(substr, str)
	- `INSTR`: INSTR(str, substr);
- `time(datetime)`: 시간 추출, 대소비교 가능
- `cast(형변환할 expr as 자료형(SIGNED))` : 정수형변환시 SIGNED를 사용하고 `truncate(실수, 0)`과 같이 소수부를 버릴때 사용됨
- `datediff(expr1, expr2)`: expr1, expr2에는 날짜 포맷을 `YYYY-MM-DD` 또는 `YYYY-MM-DD HH:MM:SS`형태로 지정, 두 표현식 사이의 일수를 계산
- `timediff(expr1, expr2)`: 두 표현식 간의 시간을 계산함
- `timestampdiff(unit, datetime_expr1, datetime_expr2)`: `unit`은 `MONTH, YEAR, DAY, WEEK, HOUR, MINUTE`등 다양한 단위값으로 차이를 계산함


# 기본 문법
- `case` 사용법
```sql
CASE
	WHEN 조건
	THEN '반환 값'
	WHEN 조건
	THEN '반환 값'
	ELSE 'WHEN 조건에 해당 안되는 경우 반환 값'
END (AS alias명)
```

- `if`문
```sql
if(조건문, 참일때 값, 거짓일때 값)
```
- `ifnull`문
```sql
ifnull(null일 수도 있는 필드값, null일때 대체할 값)
```
- `with recursive, set` 구문
	- select 구문에서 사용하는 `:=` 연산자는 sql문 안에서는 `=` 이 동등비교연산자로 사용되기때문에 `set`을 통해 변수를 선언하고 sql구문안에서는 `:=` 연산자를 사용

```sql
# -- 사용자 정의 변수 사용
# SET @HOUR = -1;

# SELECT (@HOUR := @HOUR +1) AS `HOUR`, (SELECT COUNT(*) FROM ANIMAL_OUTS WHERE @HOUR = HOUR(`DATETIME`))
# FROM ANIMAL_OUTS
# WHERE @HOUR < 23
# ORDER BY `HOUR`;

-- WITH RECURSIVE 사용
WITH RECURSIVE `TIME` AS (
    SELECT 0 AS H
    UNION ALL
    SELECT H + 1 AS H FROM `TIME` WHERE H < 23
)

SELECT H AS `HOUR`, COUNT(ANIMAL_ID) AS `COUNT`
FROM `TIME` LEFT JOIN ANIMAL_OUTS ON H = HOUR(DATETIME) 
GROUP BY `HOUR`
ORDER BY `HOUR`;
```

- `group by` 와 `order by` 절을 함께 사용할 때 `order by` 절에 집계함수를 사용할 수 있다. ([프로그래머스 SQL 고득점 kit 문제 참고](https://school.programmers.co.kr/learn/courses/30/lessons/131124))
```sql
select MEMBER_NAME, REVIEW_TEXT, date_format(REVIEW_DATE, '%Y-%m-%d') as REVIEW_DATE
from MEMBER_PROFILE natural join REST_REVIEW
where MEMBER_PROFILE.MEMBER_ID = ( 
    select MEMBER_ID
    from REST_REVIEW
    group by MEMBER_ID
    order by count(*) desc
    LIMIT 1)
order by REVIEW_DATE, REVIEW_TEXT;
```