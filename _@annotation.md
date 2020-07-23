###### RESTFul
```java
@GetMapping // get 
@PostMapping // post
@PutMapping // update[All]
@DeleteMapping // delete
```
  
###### @RequestBody / @ResponseBody
```java
@RequestBody // 요청을 http body 에 받아 올 때
@ResponseBody // 응답을 http body 에 담아 보낼 때 / return 값이 없어도 적용하는 것이 좋다
```

###### @Controller / @RestController
```java
@Controller // return을 view로 한다 data를 포함할 수 있다 
@RestController // data만 return 한다
```
  
###### @PostMapping + return Type String
호출한 결과를 다른 뷰로 넘길 때 사용하는 조합
```java
@PostMapping("/findAllTestDev")
public String findAllTestDev(TestDevVo vo, Model model) throws Exception{
		
		model.addAttribute("testData", testService.findAllTestDev(vo));
		return "test/tableContents";
}
```
  
###### @PostMapping + @ResponseBody
요청한 곳으로 응답을 반환할 때 사용하는 조합  
`post메서드`는 `body`에 `요청`할 내용을 담아서 전달하고 `응답`받을 내용도 `body`로 받는다
```java
@PostMapping("/registerTestDev")
@ResponseBody public Long registerTestDev(TestDevVo vo) throws Exception{
		
		return testService.registerTestDev(vo);
}
```
  
###### @NotBlank / @NotNull / @NotEmpty
