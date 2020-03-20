## Spring Security
  
###### add maven dependency in pom.xml
```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```
###### PasswordEncoder
```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;

public class PasswordEncoding implements PasswordEncoder {
	
	@Autowired PasswordEncoder passwordEncoder;

	public PasswordEncoding() {
		this.passwordEncoder = new BCryptPasswordEncoder();
	}

	public PasswordEncoding(PasswordEncoder passwordEncoder) {
		this.passwordEncoder = passwordEncoder;
	}
	
	@Override
	public String encode(CharSequence rawPassword) {
		return passwordEncoder.encode(rawPassword);
	}

	@Override
	public boolean matches(CharSequence rawPassword, String encodedPassword) {
		return passwordEncoder.matches(rawPassword, encodedPassword);
	}
}
```
###### how to use
```java
public class testPassword {
   public void test(){
      PasswordEncoding passwordEncoding = new PasswordEncoding();

         String rawPassword1 = "12345678";
         String rawPassword2 = "12345678";

         String newPassword1 = passwordEncoding.encode(rawPassword1);
         String newPassword2 = passwordEncoding.encode(rawPassword2);

         System.out.println("newPassword1 : "+newPassword1);
         System.out.println("newPassword2 : "+newPassword2);

         System.out.println("\nmatches : "+passwordEncoding.matches(rawPassword1,newPassword1));
         System.out.println("matches : "+passwordEncoding.matches(rawPassword2,newPassword1));
   }
}
```
[Ref.] https://youngjinmo.github.io/2019/11/springsecurity-passwordencoder/
