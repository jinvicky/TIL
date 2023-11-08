# SQL을 작성하는 방법 

---


### 부정 조건을 사용하지 않는다.
인덱스가 있는 컬럼이라도 부정 조건을 사용하면 FULL SCAN이 발생한다.

안 좋은 예시
```jsx 
WHERE N_COL1 != 30;
```

개선한 예시
```jsx
WHERE N_COL1 < 30 OR N_COL1 >30;
```

```jsX
NOT_EXISTS (SELECT~);
```
```jsx
LEFT JOIN (SELECT~) B ON ~ WHERE B.N_COL1 IS NULL;
```

### IN과 EXISTS 

---
데이터 집합의 처리 범위가 넓고 부분범위 처리가 필요한 경우는 EXISTS를, 
데이터 집합의 처리 범위가 좁고 데이터 집합이 작다면 IN을 사용한다.(더 유리)

### 여러 ROW의 그룹함수 사용

---
로우별 처리 후 집계를 하지 말고, 로우수를 줄인 후 가공처리 작업을 수행한다. 

로우별 처리 후 집계
```
SUM(SALE*10) * SUM(ACCOUNT)
...
```
```
SUM(SALE) * SUM(ACCOUNT) * 10
...
```

### 서브쿼리보다 조인을 가급적 사용한다.

---

### OR 대신 UNION ALL, IN을 사용한다. 