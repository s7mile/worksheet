# Front-end Web developer Worksheet
사내 프로젝트 진행 시 인터넷이 연결되어 있지 않은 환경(혹은 로컬환경)에서, 코딩 단의 작업 결과물 공유와 기타 업무 공유를 위해 HTML 문서 형태의 파일을 공유하여 사용하도록 합니다.

현재 일부 개별적으로 사용 중인 워크시트 파일이 특정 프로젝트에서 사용하도록 작성된 Dummy 형식의 파일로 코드 관리가 되지 않으며, 주 사용자들의 사용성을 높이고, 효율적인 코드 관리를 위해 사내 공식 워크시트를 공유합니다.

- [워크시트 미리보기](http://cidow.com/worksheet/worksheet.html)
- 파일 내려받기(다른 이름으로 대상 저장): [HTML](http://cidow.com/worksheet/worksheet.html), [CSS](http://cidow.com/worksheet/worksheet.min.css), [JS](http://cidow.com/worksheet/worksheet.min.js)

## How to use
사용 시 배포되는 HTML, CSS, JS 파일을 내려받아 HTML 파일만 해당 프로젝트에 맞게 수정하여 사용하며, 코드 관리를 위해 수정이 필요한 부분은 해당 내용을 공유하여 수정/배포가 될 수 있도록 합니다.

워크시트의 기본 기능은 아래와 같습니다.

- 워크시트는 __최신 버전의 브라우저에서만 사용함을 기본__으로 합니다.
- &lt;nav&gt;, &lt;footer&gt;, &lt;tfoot&gt; 영역 자동 생성
- &lt;aside&gt;, 테마기능 사용 시 인터넷 연결 환경 필요
- Task 목록 일괄 관리
- Task 필터
- 이전 메뉴 Depth명 자동 복사
- Number 셀 자동 생성
- File Name 링크 자동 연결
- Due Date 날짜 비교 후 class 할당

각 부분별 상세 내용은 아래와 같으며, 기본 지정된 class를 기준으로 설명 하였습니다.

### Add Task
필요한 단계만큼 아래의 예시와 같이 &lt;label&gt; ~ &lt;/label&gt;을 생성하여, &lt;b&gt;, &lt;i&gt;태그를 해당 프로젝트에 맞게 변경하여 사용합니다.

변경된 Task 목록은 워크시트 전체에 일괄적으로 반영 되며, 기본적으로 5단계 색상을 제공합니다. (5단계 이상 생성은 가능하지만, 특정 색상을 지정하기 위해선 사용자가 색상을 추가해야 합니다.)

```html
<!-- filterWrap -->
<section class="filterWrap">
	<h2>Task Key/Filter</h2>
	<form action="/">
		<fieldset>
			<legend>Filter option(It'll be automatically applied)</legend>
			<label><input type="checkbox" value="all">All</label>
			<label><input type="checkbox"><b class='default'>0</b><i>Undone</i></label>
			<label><input type="checkbox"><b>1</b><i>Done</i></label>
			<label><input type="checkbox"><b>2</b><i>Modify</i></label>
			<label><input type="checkbox"><b>3</b><i>Dev</i></label>
			<label><input type="checkbox"><b>4</b><i>SampleTask</i></label>
		</fieldset>
	</form>
</section>
<!-- //filterWrap -->
```

&lt;b&gt;태그에 지정된 __.default__는 워크시트의 Task 셀이 공백이거나 지정된 Task의 목록과 다른 값일때 해당 Task를 할당 합니다.

```html
<label><input type="checkbox"><b class='default'>0</b><i>Undone</i></label>
```

전체 선택에 사용되는 __value="all"__은 변경하지 않습니다.
```html
<label><input type="checkbox" value="all">All</label>
```

### File Name
워크시트의 .fileName 셀에 파일명 입력 시, __&lt;caption&gt; 에 작성된 폴더명(경로)과 .filePath 셀에 작성된 폴더명(경로)__을 기준으로 앵커 태그가 자동으로 생성됩니다. (자동으로 생성되는 링크가 아닌, 특정 위치로 링크를 원하는 경우 직접 앵커 태그를 연결해 주시면 됩니다.)


```html
<caption>gnb1forlder</caption>
<td class="filePath">dummy</td>
<td class="fileName">SampleSubMain2.php</td>
```

```html
<td class="fileName"><a target="_blank" href="/gnb1forlder/dummy/SampleSubMain2.php">SampleSubMain2.php</td>
```

### Turn-Off Theme, Aside, Delay info
기본 플러그인 옵션 변경 방식과 같으며, 기본 테마만을 사용하거나 도움말, 딜레이 정보 기능이 불필요하다고 판단될 경우 아래와 같이 사용하지 않도록 설정할 수 있습니다.

```html
<script>
	/* User script(setting) */
	$(function() {
		$('body').feWorksheet({
			themesOption: false,
		    asideOption: false,
		    delayInfo: false
		});
	});
</script>
```

### More info
파일은 Github의 Public Repository와 사내 서버 링크를 통해 __Compressed__ 버전을 공유하며, 사내 SVN(/SVN/library)을 통해 __Development__ 버전을 공유합니다. (차후 Github Private Repository로 변경하여 일괄 관리예정)

워크시트는 아래와 같은 옵션을 제공하지만, _원활한 스타일 적용을 위해 기본 옵션 사용을 추천_하며, 각 옵션의 value는 __Development__ 버전 코드 확인을 통해 유효한 value를 확인하실 수 있습니다.

```javascript
$.fn.feWorksheet.defaultOptions = {
	// Default elements
	workseetEl: 'table:not(footer table)', // Worksheet table el
	filterSectionClass: 'filterWrap', // Filter section class
	// Default worksheet cell class
	numCellClass: 'pageNumber', // Number cell class
	depthCellClass: 'menuDepth', // Depth
	pathCellClass: 'filePath', // File path
	nameCellClass: 'fileName', // File name
	dueCellClass: 'dueDate', // Due date
	delayBefore: 'delayBefore', // Delay: Before
	delayAfter: 'delayAfter', // Delay: After
	delayToday: 'delayToday', // Delay: Today
	delayError: 'delayError', // Delay: Error
	taskCellClass: 'checkTask', // Task
	// Options
	naviTitle: 'Navigation', // Navigation title
	naviPrefix: 'menuIdx', // Navigation prefix
	totalCountTitle: 'Total Count', // Total count title
	totalCountCaption: 'Task total count', // Total count caption
	numCellText: 'Number', // Number cell title
	themesOption: true, // Themes
	asideOption: true, // Aside
	delayInfo: true // Delay info
};
```
## Todo
- [ ] 도움말/사용방법(aside) 업데이트 / 인터넷 사용 가능 환경
- [ ] 테마기능 업데이트 / 인터넷 사용 가능 환경
- [ ] 사용자 테마 추가
- [ ] 도움말, 테마 스타일링
- [x] 도움말, 테마, 스타일 파일 사내 서버로 이전
- [x] 미리보기(샘플) 페이지

## History
- 사내 내부 테스트를 위한 1차 버전 공개 (V1.0)