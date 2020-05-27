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
  
###### check map property
- `map`에서 특정 프로퍼티의 존재 유무는 `?. 연산자`로 확인할 수 없다. 대신 `maps 유틸리티` 사용  
- `maps.isEmpty(obj)`: `obj`가 `null`이거나 `null`이 아니어도 비어있으면 `true`
- `maps.containsKey(obj, name)`: `obj`에 `name`으로 지정된 요소가 있으면 `true`  
  
```html
<!-- ex) th:if="${#maps.containsKey(object,'property_name')}" -->

<td th:if="${#maps.containsKey(row,'DEPARTMENT')}" th:text="${row.DEPARTMENT}"></td>
<td th:if="${not #maps.containsKey(row,'DEPARTMENT')}"></td>

<td th:if="${#maps.containsKey(row,'PHONE')}" th:text="${row.PHONE}"></td>
<td th:if="${not #maps.containsKey(row,'PHONE')}"></td>
```
[참조] https://noritersand.github.io/java/2019/01/24/java-%ED%83%80%EC%9E%84%EB%A6%AC%ED%94%84-thymeleaf-%EA%B8%B0%EB%B3%B8/
  
###### check empty (List / Map)
```html
<!-- List -->
${not #string.isEmpty(list-data)}

<!-- Map -->
${map-data.isEmpty()}
```
  
###### date format
```html
<th:block th:text="${#dates.format(base-date, 'yyyy-MM-dd HH:mm:ss')}"></th:block>
```
###### concat or mixed string
```html
<th:block th:text="|${group.CODE} / ${group.CODE_NAME}|"></th:block>
<td th:text="${#maps.containsKey(row,'COUNT')} ? |${row.COUNT} 건| : ''"></td>
```
###### substring
```html
"${#strings.substring(data,startPoint,howMany)}"

<!-- example -->
<td th:text="${#strings.substring(row.DTIME,0,10)}"></td>
<td th:text="${#maps.containsKey(row,'DTIME')} ? ${#strings.substring(row.DTIME,0,16)} : ''"></td>
```
  
###### th:width / `DYNAMIC TABLE`
```html
<thead>
  <tr th:if="${!column.isEmpty()}">
    <th:block th:each="item, status : ${column}">
      <th th:width="|${100 / status.size}%|" onclick="sort(event)">
        <div class="th-text sorting">
          <input type="hidden" th:value="${item.COLUMN_NAME}"/>
          <th:block th:text="${item.COLUMN_NAME}"></th:block>
        </div>
      </th>
    </th:block>
  </tr>
</thead>
```
  
###### map.get("key") / `DYNAMIC TABLE`
```html
<tbody>
  <th:block th:if="${!list.isEmpty()}">
    <tr th:each="row, status : ${list}">
      <td th:text="${status.count + (page.curPage - 1) * page.pageSize}"></td>
      <th:block th:each="item : ${column}">
        <td th:text="${row.get(item.COLUMN_NAME)}"></td>
      </th:block>
    </tr>
  </th:block>
  <th:block th:if="${list.isEmpty()}">
    <tr><td th:colspan="${column.size()}">데이터가 존재하지 않습니다.</td></tr>
  </th:block>
</tbody>
```
[Ref.] https://stackoverflow.com/questions/28621301/how-to-use-map-getkey-in-thymeleaf-broadleaf-ecom  
  
###### sticky thead
```html
<thead class="sticky-thead"></thead>
```
```css
.sticky-thead th {
	z-index: 100;
	background:#ddebf5;
	font-weight:bold;
	position: sticky;
	top: 0;
}

.sticky-thead th:before {
	content:'';
	position:absolute;
	left: 0;
	top: 0;
	width:100%;
	border-top:1px solid #7d9aae;
}

.sticky-thead th:after {
	content:'';
	position:absolute;
	left: 0;
	bottom: 0;
	width:100%;
	border-bottom:1px solid #C2D2DF;
}
```
  
###### how to check null for list
```html
<th:block th:if="${not #lists.isEmpty(list-Object)}"></th:block>
<th:block th:if="${#lists.isEmpty(list-Object)}"></th:block>
```
