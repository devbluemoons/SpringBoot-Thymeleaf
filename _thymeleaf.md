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
###### th:block tag
  
`th:block` 태그는 타임리프의 문법을 적용할 수 있는 태그이다
```html
<th:block></th:block>
<!-- Example -->
<th:block th:text="${user.name}"></th:block>
```
  
###### import dynamic js file path
```html
<script th:src="|/static/js/${javascript_File_name}.js|"></script>
<!-- Example -->
<script th:src="|/static/js/${routerPath}.js|"></script> <!--routerPath javaScript file-->
```
  
###### table multiple loot example
```html
<table class="tbList">
  <colgroup><col style=""></colgroup>
  <thead>
    <tr>
      <th>no</th>
      <th>column01</th>
      <th>column02</th>
      <th>column03</th>
      <th>column04</th>
      <th>column05</th>
    </tr>
  </thead>
  <tbody>
    <th:block th:each="group, gStat : ${equipGroupList}">
      <tr th:each="equip, eStat : ${group.diAgentList}">
        <td th:if="${eStat.index == 0 && eStat.size == 1}" th:text="${gStat.count}"></td>
        <td th:if="${eStat.index == 0 && eStat.size > 1}" th:rowspan="${eStat.size}" th:text="${gStat.count}"></td>
        <td th:if="${eStat.index == 0 && eStat.size == 1}">
          <input type="checkbox" th:value="${group.CODE}" onclick="checkBox(this)">
        </td>
        <td th:if="${eStat.index == 0 && eStat.size > 1}" th:rowspan="${eStat.size}">
          <input type="checkbox" th:value="${group.CODE}" onclick="checkBox(this)">
        </td>
        <td th:if="${eStat.index == 0 && eStat.size == 1}" th:text="${group.CODE_NAME}"></td>
        <td th:if="${eStat.index == 0 && eStat.size > 1}" th:rowspan="${eStat.size}" th:text="${group.CODE_NAME}"></td>
        <td th:text="${equip.HOSTNAME}"></td>
        <td th:text="${equip.MODEL}"></td>
        <td th:text="${equip.AGENT_IP}"></td>
      </tr>
    </th:block>
  </tbody>
</table>
```
