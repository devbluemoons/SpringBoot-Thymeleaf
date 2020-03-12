 ###### create Pagination
```java
import lombok.Data;

@Data
public class Pagination {
	
	/** 한 페이지당 게시글 수 **/
	private int pageSize = 15;
	
	/** 한 블럭(range)당 페이지 수 **/
	private int rangeSize = 10;
	
	/** 현재 페이지 **/
	private int curPage = 1;
	
	/** 현재 블럭(range) **/
	private int curRange = 1;
	
	/** 총 게시글 수 **/
	private int listCnt;
	
	/** 총 페이지 수 **/
	private int pageCnt;
	
	/** 총 블럭(range) 수 **/
	private int rangeCnt;
	
	/** 블럭(range)내에서 시작 페이지 **/
	private int startPage = 1;
	
	/** 블럭(range)내에서 끝 페이지 **/
	private int endPage = 1;
	
	/** 시작 index **/
	private int startIndex = 0;
	
	/** 이전 페이지 **/
	private int prevPage;
	
	/** 다음 페이지 **/
	private int nextPage;
	
	// class를 상속받을 경우 오류 방지를 위한 "기본 생성자" 정의
	public Pagination() {}
	
	// 생성자 파라미터를 통하여 "총 게시물 수"와 "현재 페이지"를 받는다
	public Pagination(int listCnt, int curPage) {
		
		/**
		 * 페이징 처리 순서
		 * 1. 총 페이지수
		 * 2. 총 블럭(range)수
		 * 3. range setting
		 */
		
		/** 현재페이지 **/
		setCurPage(curPage);
		/** 총 게시물 수 **/
		setListCnt(listCnt);
		
		/** 1. 총 페이지 수 **/
		setPageCnt(listCnt);
		/** 2. 총 블럭(range)수 **/
		setRangeCnt(pageCnt);
		/** 3. 블럭(range) setting **/
		rangeSetting(curPage);
		
		/** DB 질의를 위한 startIndex 설정 **/
		setStartIndex(curPage);
	}
	// ("총 페이지 수") "총 게시물 수"를 "한 페이지당 게시글 수"로 나눈다
	public void setPageCnt(int listCnt) {
		
		this.pageCnt = (int) Math.ceil(listCnt*1.0 / pageSize);
	}
	// ("총 블럭[range]수") "총 페이지 수"를 "한 블럭(range)당 페이지 수"로 나눈다
	public void setRangeCnt(int pageCnt) {
		
		this.rangeCnt = (int) Math.ceil(pageCnt*1.0 / rangeSize);
	}
	// ("현재 블럭[range]") "현재 페이지"에서 "한 블럭(range)당 페이지 수"로 나눈다
	public void setCurRange(int curPage) {
		
		this.curRange = (int)((curPage - 1) / rangeSize) + 1;
	}
	
	// 블럭(range)내에서 필요한 값들을 구한다
	public void rangeSetting(int curPage){
		
		setCurRange(curPage);
		
		// 블럭(range)내에서 "시작 페이지","끝 페이지" 값을 구한다
		this.startPage = (curRange - 1) * rangeSize + 1;
		this.endPage = startPage + rangeSize - 1;
		
		// "끝 페이지 값"이 "총 페이지 수"를 넘지 않도록 한다
		if(endPage > pageCnt){
			this.endPage = pageCnt;
		}
		
		// "현재 페이지"를 기준으로 "이전 페이지","다음 페이지" 값을 구한다
		this.prevPage = curPage - 1;
		this.nextPage = curPage + 1;
	}
	
	// DB에서 data를 가져올 때 "현재 페이지"를 기준으로 "시작점"을 구한다
	public void setStartIndex(int curPage) {
		
		this.startIndex = (curPage - 1) * pageSize;
	}
}
```
  
참조 : https://gangnam-americano.tistory.com
