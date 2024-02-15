# AIDT_오늘의 TIL

--- 

Vue를 사용했는데 팝업이 새창 열림이다. 이 때 아파치 또는 nginx 쪽에서 index.html을 라우팅하는 부분이 없어서
404 not Found 에러가 발생했다. 

따라서 아파치 또는 nginx 쪽에 가서 처리를 해야 한다.

참고 링크

```xml








```








# ALG_오늘의 TIL

---
## 후위 표기식 

https://www.acmicpc.net/problem/1918

### 후기 
우선순위가 더 높으면 stack에 쌓는다만 생각했는데, 우선순위가 같은 경우도 고려를 했어야 했다. 
<br />
게다가 중첩 if문을 너무 많이 사용했다. 3개 이상이면 잘못 짠 코드라는데 => 따라서 if 걸고 continue 떡칠을 하느니 switch를 하는 게 낫다고 생각함. 