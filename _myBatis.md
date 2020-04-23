###### ${}, #{}
  
- ${} : 값 자체로 넘긴다 / 따옴표, 쌍따옴표 등의 기호를 제거한 type이 없는 값 자체가 된다
- #{} : 타입을 포함한 값을 넘긴다, 문자열 또는 숫자값
  
###### foreach
- 자료구조 List<String> 은 문자열이 아니기 때문에 `""` 공백과 비교될 수 없어 참조할 경우 에러가 발생한다
```xml
<if test="hostnames != null">
    AND HOSTNAME IN 
    <foreach collection="hostnames" item="item" open="(" separator="," close=")">
        #{item}
    </foreach>
</if>
```
