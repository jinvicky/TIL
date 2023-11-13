# SQL Programmers - Group By

---

### LIKE와 REGEXP
LIKE문을 여러개 쓸 수도 있지만, 와일드 카드를 쓰지 않는다면 
REGEXP로 한번에 처리 가능하다. 

LIKE를 사용한 경우
```SQL
... WHERE OPTIONS LIKE ('%통풍시트%')
OR OPTIONS LIKE ('%열선시트%')
OR OPTIONS LIKE ('%가죽시트%')
```
REGEXP를 사용한 경우
```SQL
WHERE OPTIONS REGEXP '통풍시트|열선시트|가죽시트'
```

### INNER JOIN 조건절
ON 조건도 좋지만 USING()으로 간단하게 할 수도 있다. 

ON 조건절
```SQL
SELECT B.CATEGORY, SUM(BS.SALES) AS TOTAL_SALES
FROM BOOK B
INNER JOIN BOOK_SALES BS
ON B.BOOK_ID = BS.BOOK_ID
```
USING()
```SQL
SELECT CATEGORY, SUM(SALES) AS TOTAL_SALES FROM BOOK_SALES
INNER JOIN BOOK USING(BOOK_ID)
```


# SQLD 

---

any (=some)
- 서브쿼리의 결과에 존재하는 어느 하나의 값이라도 만족하는 조건을 의미.