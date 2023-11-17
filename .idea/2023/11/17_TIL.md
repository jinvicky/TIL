# SQL Programmers

---
## MYSQL NULL 처리

NULL일 경우 기본값 설정
```SQL
# 컬럼명이 NULL일 경우 'No name'으로 설정
IFNULL(컬럼명, 'No name') 
```

NULL이거나 아닌 경우만 조회
```SQL 
SELECT COUNT(USER_ID) FROM USER_INFO
WHERE AGE IS NULL 
# WHERE AGE IS NOT NULL (NULL이 아닐 경우)
```

## JOIN 문제 풀이
자동차 관련 문제에 난항을 겪고 있다. 뒤로 미룸. 
몇 문제는 IS NULL 등의 쉬운 문제라서 스킵. 

#### 오랜 기간 보호한 동물
```SQL
SELECT INS.NAME, INS.DATETIME FROM ANIMAL_INS INS
LEFT OUTER JOIN ANIMAL_OUTS OUTS
ON INS.ANIMAL_ID = OUTS.ANIMAL_ID
WHERE OUTS.ANIMAL_ID IS NULL
ORDER BY INS.DATETIME LIMIT 3
```
* MYSQL에는 TOP(N) 같이 상위 N건만 추출하는 함수가 없다. 그래서 대신 LIMIT N 구문을 사용했다. 


#### 보호소에서 중성화한 동물

```SQL
SELECT INS.ANIMAL_ID, INS.ANIMAL_TYPE, INS.NAME
FROM ANIMAL_INS INS
INNER JOIN ANIMAL_OUTS OUTS
ON INS.ANIMAL_ID = OUTS.ANIMAL_ID
WHERE INS.SEX_UPON_INTAKE REGEXP 'Intact' 
AND OUTS.SEX_UPON_OUTCOME REGEXP 'Neutered|Spayed'
```
* LIKE를 여러번 쓰는 것 말고 다른 방법이 없을까 찾아보다가 REGEXP를 사용해보았다. Intact 조건의 경우 LIKE로 하나 별 다를 바 없지만. 

#### 상품별 오프라인 매출 구하기
```SQL
SELECT P.PRODUCT_CODE,  P.PRICE * SUM(SALES_AMOUNT) AS SALES FROM PRODUCT P
RIGHT OUTER JOIN OFFLINE_SALE OS
ON P.PRODUCT_ID = OS.PRODUCT_ID
GROUP BY P.PRODUCT_CODE
ORDER BY SALES DESC, P.PRODUCT_CODE ;
```
* SUM()을 써야 하는데 COUNT()를 써서 오답을 냈었다. 왜 SUM()을 써야 하냐면 판매기록 ROW가 5줄이어도 건당 판매량이 2 이상이면 값이 바뀌기 때문이다. 

