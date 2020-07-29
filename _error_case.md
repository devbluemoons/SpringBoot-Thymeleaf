###### must use e.printStackTrace();
- this gives infomation that is caused almost ploblems
- when developing you must use this!!!

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
  
###### systemctl VS java -jar
- `systemctl` 명령어를 사용하여 `jar파일`을 실행할 경우 편리함에 이점이 있지만  
- 에러가 발생할 경우 직관적으로 확인하기 어렵다는 단점이 있다.
- 이와 같은 경우에는 직접 `java -jar` 명령어를 사용하여 어플리케이션을 실행해보자   
- `에러로그`를 직관적으로 확인할 수 있다.
  
###### cannot find symbol (Compile Time error)
- 클래스명이나 변수명이 잘못되었을 때 발생하는 에러
