###### spring-boot-starter-security
```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-security</artifactId>
</dependency>

<dependency>
  <groupId>org.thymeleaf.extras</groupId>
  <artifactId>thymeleaf-extras-springsecurity5</artifactId>
</dependency>
```
  
###### Login Controller
```java
@Controller
@RequestMapping("/login")
public class LoginController {
	
	@GetMapping({"","/"})
	public String login() throws Exception {
		return "login";
	}
	
	@GetMapping("/error")
	public String loginError(Model model) throws Exception {
		model.addAttribute("errorMessage", "아이디 또는 비밀번호를 다시 확인해 주세요.");
		return "login";
	}
}
```
  
###### Login Service
```java
@Service
@AllArgsConstructor
public class LoginService implements UserDetailsService {
	
	@Autowired UserService userService;
	
	@Override
	@Transactional
	public UserDetails loadUserByUsername(String userId) throws UsernameNotFoundException {
		
		Set<GrantedAuthority> authorities = new HashSet<>();
		Map<String, Object> item = new HashMap<>();
		Map<String, Object> param = new HashMap<>();
		param.put("USER_ID", userId);
		
		try {
			item = userService.findOneDiUserByUserId(param);
			if(item != null) {
				authorities.add(new SimpleGrantedAuthority(item.get("AUTH").toString()));
			}
		} catch (Exception e) {
			e.printStackTrace();
		}
		return new User(item.get("USER_NAME").toString(), item.get("PASS_WORD").toString(), authorities);
	}
}
```
  
###### SecurityConfig
```java
@Configuration
@EnableWebSecurity
@AllArgsConstructor
public class SecurityConfig extends WebSecurityConfigurerAdapter {
	
	@Autowired LoginService loginService;
	
	@Override
	public void configure(WebSecurity web) throws Exception {
		// static & templates 디렉터리의 하위 파일 목록은 인증 무시 ( = 항상통과 )
		web.ignoring().antMatchers("/static/**").antMatchers("/templates/**");
	}
	
	@Override
	protected void configure(HttpSecurity http) throws Exception {
		
		http.authorizeRequests()
			// 페이지 권한 설정
			.antMatchers("/register").hasRole("ENG") // 엔지니어 권한을 가진 사용자만 접근가능
			.anyRequest().authenticated() // 모든 요청에 대해 인증된 사용자만 접근가능
		// 로그인 설정
		.and()
			.formLogin()
			.loginPage("/login")
			.usernameParameter("userId")
			.defaultSuccessUrl("/login/success")
			.failureUrl("/login/error")
			.permitAll()
		// 로그아웃 설정
		.and()
			.logout()
			.logoutRequestMatcher(new AntPathRequestMatcher("/logout"))
			.logoutSuccessUrl("/")
			.invalidateHttpSession(true)
		// 예외처리 핸들링
		.and()
			.exceptionHandling()
			.accessDeniedPage("/")
		// csrf 필터링 해제
		.and()
			.csrf().disable();
	}
	
	@Override
	public void configure(AuthenticationManagerBuilder auth) throws Exception {
		auth.userDetailsService(loginService).passwordEncoder(passwordEncoder());
	}
	
	public PasswordEncoder passwordEncoder() {
		return new BCryptPasswordEncoder();
	}
}
```
  
###### Index Controller
```java
@Controller
public class IndexController {
	
	@Autowired UserService userService;
	
	@GetMapping({"","/"})
	public String index() throws Exception {
		
		User user = (User) SecurityContextHolder.getContext().getAuthentication().getPrincipal();
		
		if(user != null) {
			return "redirect:/main"; // 지정된 메인화면 (사이트에 따라 메인화면이 달라질 수 있다!)
		}else {
			return "redirect:/login";
		}
	}
}
```
  
###### Password / Insert / Update
- Spring Security required BcryptPassword
- We must use this API
```java
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;

public PasswordEncoder passwordEncoder() {
	return new BCryptPasswordEncoder();
}

String password = param.get("PASS_WORD").toString();
param.replace("PASS_WORD", passwordEncoder().encode(password));
```
  
###### Thymeleaf Authority
```html
<div sec:authorize="hasRole('ROLE_ENG')">contents</div> 
<div sec:authorize="hasAnyRole('ROLE_ENG','ROLE_ADMIN')">contents</div>
```
  
###### csrf / `post` issue
[Ref.] https://www.slipp.net/questions/480
