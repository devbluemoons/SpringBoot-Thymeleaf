###### utilities Date and Time
```java
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Calendar;
import java.util.Date;

import org.springframework.stereotype.Component;

@Component
public class UtilDateAndTime {
	
	public String getCurrentTimeTypeString() {
		
		SimpleDateFormat formatter= new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
		Date date = new Date(System.currentTimeMillis());
		
		return formatter.format(date);
	}
	
	public Date getCurrentTimeTypeDate() {
		
		return new Date(System.currentTimeMillis());
	}
	
	public Date stringToDate(String date) throws ParseException {
		
		SimpleDateFormat formatter = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
		return formatter.parse(date);
	}
	
	public String dateToString(Date date) {
		
		SimpleDateFormat formatter = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
		return formatter.format(date);
	}
	
	public Date minusMinuteFromNow(int minute) {
		
		Calendar cal = Calendar.getInstance();
		cal.add(Calendar.MINUTE, - minute);
		
		return cal.getTime();
	}
}
```
