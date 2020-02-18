## Thymeleaf

###### first set-up
```html
<html xmlns:th="http://www.thymeleaf.org" xmlns:layout="http://www.ultraq.net.nz/thymeleaf/layout">

</html>
```
###### check this rule!!
  
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
<td th:text="${row.update_dt}"></td> <!-- 변수 타입이 date이고 값이 없을 경우 에러 발생 -->
```
  
###### loop, variable status
  
반복문 사용시 index 또는 count 정보가 필요할 때가 있다 thymeleaf는 이 정보를 status 속성을 통해 제공한다
반복문에서 지정한 변수 뒤에 stat을 붙여서 사용할 수도 있고 직접 이름을 정하여 사용할 수도 있다  
```html
<tr th:each="row, status : ${Data}">
  <td th:text="${status.index}"></td>
  <td th:text="${status.count}"></td>
  <td th:text="${row.name}"></td>
</tr>
<!-- OR -->
<tr th:each="row : ${Data}">
  <td th:text="${rowStat.index}"></td>
  <td th:text="${rowStat.count}"></td>
  <td th:text="${row.name}"></td>
</tr>
```
