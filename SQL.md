# 내장 함수
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