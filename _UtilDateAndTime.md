###### utilities Date and Time
```java
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Calendar;
import java.util.Date;
import java.util.GregorianCalendar;
import java.util.HashMap;
import java.util.Map;

import org.springframework.stereotype.Component;

@Component
public class DateAndTime {
	
	public String getCurrentDateTypeString() {
		
		SimpleDateFormat formatter= new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
		Date date = new Date(System.currentTimeMillis());
		
		return formatter.format(date);
	}
	
	public String getYyyyMMddHHmmss(String time) throws ParseException {
		
		SimpleDateFormat originalString = new SimpleDateFormat("yyyyMMddHHmmss");
		SimpleDateFormat formatter= new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
		Date date = originalString.parse(time);
		
		return formatter.format(date);
	}
	
	public Date getCurrentDateTypeDate() {
		return new Date(System.currentTimeMillis());
	}
	
	public String getYyyyMMdd() throws ParseException {
		
		SimpleDateFormat formatter = new SimpleDateFormat("yyyy-MM-dd");
		return formatter.format(new Date());
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
	
	public int getCurrentHour() {
		
		Date date = new Date();
		Calendar calendar = GregorianCalendar.getInstance();
		calendar.setTime(date); 
		
		return calendar.get(Calendar.HOUR_OF_DAY);
	}
	
	public int getMonth() {
		
		Date date = new Date();
		Calendar calendar = GregorianCalendar.getInstance();
		calendar.setTime(date); 
		
		return calendar.get(Calendar.MONTH);
	}

	public Map<String, String> getDateTimeToStringInMap() {
		Map<String, String> map = new HashMap<String, String>();
		SimpleDateFormat sdf = new SimpleDateFormat("yyyyMMddHHmmss");
		
		String str = sdf.format(new Date());
		map.put("yyyy", str.substring(0,  4));
		map.put("MM", str.substring(4,  6));
		map.put("dd", str.substring(6,  8));
		map.put("HH", str.substring(8,  10));
		map.put("mm", str.substring(10,  12));
		map.put("ss", str.substring(12,  14));
		
		return map;
	}
}
```
