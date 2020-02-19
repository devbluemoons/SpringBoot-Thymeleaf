###### RESTFul
```java
@GetMapping // get 
@PostMapping // post
@PutMapping // update[All]
@DeletMapping // delete
```
  
###### @RequestBody, @ResponseBody
```java
@RequestBody // 요청을 http body 에 받아 올 때
@ResponseBody // 응답을 http body 에 담아 보낼 때
```

###### @Controller, @RestController
```java
@Controller // return을 view로 한다 data를 포함할 수 있다 
@RestController // data만 return 한다
```
