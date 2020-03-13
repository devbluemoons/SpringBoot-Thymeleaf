###### HashMap<String, Object> cast error  
- 맵으로 받은 데이터를 `int number = (int) param.get("data001")` 이런식으로 바로 캐스팅하면 에러 발생
- 이러한 형태로 파싱을 해줘야 정상작동한다 int curPage =  Integer.parseInt(String.valueOf(param.get("data001")));
  
```java
@PostMapping("/findData")
public String findData(@RequestParam Map<String, Object> param) throws Exception{

    if(param.get("data001").equals("")) {
        param.put("data001", 1);
    }

    int curPage = Integer.parseInt(String.valueOf(param.get("data001")));

    return "redirect:/main";
}
```
