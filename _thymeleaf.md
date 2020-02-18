## Thymeleaf

###### first set-up
```html
<html xmlns:th="http://www.thymeleaf.org" xmlns:layout="http://www.ultraq.net.nz/thymeleaf/layout">

</html>
```
###### must check this
  
변수 타입이 string, int 일 경우 변수에 값이 없어도 그냥 넘어간다  
그러나 타입이 date 일 경우 에러를 발생시킨다  
이 부분을 잘 처리해주어야 한다
  
```html
<td th:text="${row.seq}"></td>
<td th:text="${row.name}"></td> 
<td th:text="${row.phone}"></td>
<td th:text="${row.address}"></td>
<td th:text="${row.email}"></td>
<td th:text="${row.register_dt}"></td>
<td th:text="${row.update_dt}">view</td> <!-- 변수 타입이 date이고 값이 없을 경우 에러 발생 -->
```
