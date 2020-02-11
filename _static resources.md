## static resources (html, css, js)
  
###### path
```
/src/main/resources/static/css
/src/main/resources/static/js
```
  
###### application.properties
```sh
spring.mvc.static-path-pattern=/static/**
spring.resources.static-locations=classpath:/static/
spring.resources.add-mappings=true
```
  
###### 
