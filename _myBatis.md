###### ${}, #{}
  
- ${} : 값 자체로 넘긴다 / 따옴표, 쌍따옴표 등의 기호를 제거한 type이 없는 값 자체가 된다
- #{} : 타입을 포함한 값을 넘긴다, 문자열 또는 숫자값
  
###### foreach
```xml
<if test="hostnames != null and hostnames != ''">
    AND HOSTNAME IN 
    <foreach collection="hostnames" item="item" open="(" separator="," close=")">
        #{item}
    </foreach>
</if>
```
