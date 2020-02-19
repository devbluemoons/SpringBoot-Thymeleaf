###### BeanUtils.copyProperties(vo, target);

객체를 복사할 때 사용  
특히 vo, dto 등의 data 모델을 복사할 때 사용됨  
setter를 통해 모든 필드를 복사할 수 없을 경우 사용    
target이 되는 객체에 특정 필드값만 대입할 경우 사용  

```java
import org.springframework.beans.BeanUtils;

BeanUtils.copyProperties(source, target);

// example
@Transactional
	public Long updateTestDev(TestDevVo vo) throws Exception {
		
		TestDevVo target = testMapper.findOneTestDev(vo.getSeq());
		BeanUtils.copyProperties(vo, target);
		
		return testMapper.updateTestDev(target);
	}
```
