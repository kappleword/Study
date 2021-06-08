# 21/06/08
### JavaScript
* 객체 종류 3가지
  - 내장 객체 : 사용자 객체도 포함된다
  - 브라우저 객체모델 BOM : 브라우저 관련 객체로 브라우저와 관련된 정보를 얻거나 제어할 수 있게 해줌
  - 문서 객체 DOM : HTML 태그들을 객체화 한 것이며, 주로 HTML 페이지의 내용과 속성 등을 제어하기 위해 사용
* html
  - head : meta tag(검색엔진,포털사이트 정부 수집 용) ,view port, 인코딩타입, 호이스팅(hoisting)이 일어나는곳
  - body : 화면 출력 포지션
* 템플릿 리터럴 (내장된 표현식을 허용하는 문자열 리터럴)
  - 참고 : https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals
* 배열은 [], Object는 {}사용 할 것
* 일반 함수 정의방식과 익명 함수 선언 참조 방식의 차이점
  - 일반 함수 정의는 함수 호출 시 호이스팅(hoisting) 기술을 지원한다, but 익명 함수 선언 참조 방식은 호이스팅을 지원하지 않는다
  - 호이스팅을 적용하면 호출문이 함수 정의문 보다 먼저 나와도 호이스팅이 함수 정의문을 끌어올려서(head로) 함수를 호출한다
* 프로토타입(prototype) : 자바 static과 비슷한 기능으로 사용에 따라 메모리 할당을 줄일 수 있음
```javascript
function Person() {
  this.eyes = 2;
  this.nose = 1;
}
let kim  = new Person();
let park = new Person();
console.log(kim.eyes);  // => 2
```
↓이런식으로 변경 가능
```javascript
function Person() {}
Person.prototype.eyes = 2;
Person.prototype.nose = 1;
let kim  = new Person();
let park = new Person():
console.log(kim.eyes); // => 2
```

* function(함수) : 코드를 잘 정리정돈하기 위한 도구
  - function 사용의 장점
    + 코드의 유지보수가 쉬워진다, 하나의 함수를 여러곳에서 사용할 때 다 바꿀 필요없이 함수만 바꾸면 됨
    + 코드의 길이가 짧아진다, 같은 코드의 반복을 없애고 웹페이지의 크기가 작아져서 전송에 유리해짐
    + 함수를 사용하면 두 코드가 논리적으로 같다는 것을 알 수 있고, 적절한 이름을 붙여주면 이 코드가 어떤 일을 하는지 한 눈에 알 수 있다
  -  return : 함수내부에서 처리한 결과값을 밖으로 내보내는 역할을 하는 일종의 출력값
  -  retrun을 이용하여 값을 돌려줄 수 있고, 함수 탈출(종료) 용도로 사용 가능
  -  함수를 사용할 때 this로 태그를 전달해주고, 이를 함수는 매개변수로 받아 사용 가능
  -  매개변수(Parameter) : i,j 인자(Argument) : 2,3
```javascript
function hello(i, j) {
  document.write(i + j);
}
hello(2, 3);
```
### Spring
```
INSERT INTO board_master(bm_no,bm_title,bm_writer,bm_content,bm_date,bm_hit,bm_group,bm_pos,bm_step,bm_pw,bm_email)
VALUES(#{bm_no},#{bm_title},#{bm_writer},#{bm_content},#{bm_date},#{bm_hit,#{bm_group},#{bm_pos},#{bm_step},#{bm_pw},#{bm_email})
VALUES(SELECT 문.......)
```
`localhost:9001/board/boardInsert.sp4?bm_no=100&bm_title=제목&bs_file=a.txt&bm_writer=김철수&bm_email=test@hot.com&bm_content=글내용&bm_pw=123`

# 21/06/07
### HTML
* index.html파일 안에 `<link rel="stylesheet" href="파일이름.css">`으로 스타일.css와 연결해줘야 적용됨
* grid를 이용해 화면 영역 나누기
1. 화면 영역을 나눠주고
```css
.main-container {
  width: 1080px;
  margin: auto;
  display: grid;
  grid-template-columns: repeat(3, 1fr); /* 균일한 크기로 3등분 */
  grid-template-rows: repeat(24, 40px); /* 40px로 24등분 */
  gap: 10px;
}
```
2. 클래스별 속성 생성 후
```
.box-one {
  grid-column: 1 / 3; /* 나눈 영역을 지정해줘서 영역 크기 설정 */
  grid-row: 1 / 3;
}
.temp-box {
  background: skyblue;
  text-align: center;
  font-size: 30px;
  border: 1px solid #010102;
}
```
3. `<div class="temp-box box-one">1</div>` 이런식으로 적용해주면 끝

### JavaScript
* 구조
  - <head> CSS, JavaScript, Jquery, 공통코드들(include)
  - <body> DOM Tree
  - `$(document).ready(function {     });`    >>> $:Jquery 기반 	
* `document.write("내용");` >>> document = html문서, write = 함수
* if문
```javascript
function test() {
          if (true && true) {
            document.write("같다.","<br>");
          }
          else {
            document.write("다르다.");
          }
        }
```
* 배열 : 3가지 방법으로 선언 가능
	- `document.write(d3.length);` : 배열 길이 출력도 가능, 3 출력됨
	- d3.push("coconut");` :  배열의 맨 뒤에 coconut 값 추가
```javascript
function test() {
	const d1 = new Array();
	d1[0] = 30;
	d1[1] = "닌텐도";
	d1[2] = true;
	const d2 = new Array(50, "태블릿",false);
	const d3 = [90,"핸드폰",true];
```
* 비교연산자
	- === : 동등, html에서는 `&lt;`는 < 를 의미하는 것이고, `&gt;`는 > 를 의미한다
* 리팩토링 : Javascript에는 자기 자신을 가리키기 위한 this를 사용 가능하다



# 21/06/06
### JavaScript
* Javascript의 가장 중요한 역할는 사용자와 상호작용 하는 것, 이러한 Javascript의 특성을 이용해서 우리는 웹페이지를 더 동적으로 만듬
* HTML의 script 태그 안에는 Javascript 코드 사용, 동적으로 다양하게 출력가능 <-> HTML 코드 정적 문자 그대로를 출력
* alert('경고내용') : Javascript 경고창 띄워주는 명령어 (이벤트 조건 만족 시 '경고내용' 경고창이 뜸)
  - 구조 : alert('hi')
* 콘솔 창으로 Javascript 코드를 실행가능, alert를 예시로 들면 현재 페이지에서 바로 경고창으로 출력가능
* 스타일으로 색 변경 가능 ex) style="background-color: black; color: white;"
* div와 span : CSS나 Javascript 코드를 삽입하기 위해서 존재하는 태그
  - div 태그는 화면 전체를 사용하기 때문에 줄바꿈이 되고, span은 줄바꿈이 되지 않음
* js 클래스를 만든 후 안에 속성 넣고, html코드에 적용 가능
```css
 .js {
        font-weight: bold;
 }
```
```javascript
<span class="js">Javascript</span> is wonderful!
```
* 클래스 대신 id도 사용 가능한데 id는 한 페이지에서 딱 한번밖에 못 씀
```css
 #first {
    color: green;
 }
```
* 우선 순위는 id > class > 태그
  - 이를 이용해 class 위에 id를 얹어서 구현가능 (class로 광범위한 효과를 주고, id를 이용해 그것 만 예외적으로 디자인 변경 가능 )
* querySelector("찾을내용") : 원하는 태그를 선택해줌
  - 구조 : documnet.querySelector("body").style.backgroundColor = 'black';

### 넥사크로
* 프로젝트 생성 후 작업 환경 세팅, 톰캣 서버 연동 복습
* 간단하게 ui화면 그리기
![ui](./img/0606_ui.png)

# 21/06/05
### 넥사크로
![nexacro0605](./img/nexacro_0605.png)
+ Tools-options-Generate
  - 경로 D:\nexacro\nexa_test\WebContent 지정 (이클립스 작업폴더)
  - select browser 설정은 크롬만 체크
+ ctrl+F1 넥사크로 매뉴얼
+ nexacro 교재 4. 화면 개발 실습 중요
  - 55p 화면 생성 레이아웃 - 신규 화면 생성시 OOO.xfdl
+ Select바 Grid - 그리드(화면) 하나 그려줌
+ Select바 Dataset - Dataset 생성 ex)de_emp
  - Dataset Editor - colurms - add로 컬럼 추가
  - 드래그앤 드롭 방식으로 추가
  - Dataset Editor - row - add로 테이블 내용 추가 가능(로우 추가)
+ 자바 > 넥사크로 (구조)
  - table tag > grid
  - json > dataset
  - DataSet ds_emp = new DataSet(); > binddataset="de_emp"

### eclipse 오류
import로 복사한 프로젝트 등록할때 already Exist뜨면  
복사한프로젝트폴더/.project로가서 <name>기존프로젝트이름</name>을 <name>작업할 프로젝트이름</name>으로 수정

# 21/06/04
### 넥사크로
![nexacro0604](./img/nexacro_0604.PNG)
+ 넥사크로 도입
  * pojo, spring 같이 o boot는 x
  * Libraries 빌드패스잡아줘야함
  * xml 화면 : Grid 
  * DataSet 실제 데이터를 가지고있는 구조체(데이터집합) > nexacro.jar~ 제공
+ 자바 프로젝트와 연결
  * WebContent-nexa17 : 
  * App-Desktop.xadl.js >> 메인파일  
  * nexacro/17/project/kosmo80안 파일을 dev_nexa/WebContent/nexa에 배포함
+ design-화면, source-xml, script-event 역할
+ 넥사크로 메뉴
  * Tools 물리적인 경로 등록
  * Generate - Application 배포(배치)작업
+ 퀵 뷰바(돋보기라인)
  * 돋보기버튼 - 실행(설정바꿔서 톰캣으로 실행가능)
  * file 아래아래 바 넥사크로 제공 컴포넌트
+ 작업영역  
  * TOP - 도구창들
  * LEFT - 파일목록
  * RIGHT - 작업화면
  * 오른쪽 창 - 이벤트 설정
+ WebContent-deptManager.jsp, empManager.jsp, 툼캣서버포트, 넥사크로-TypeDefinition-service 전부 포트를 똑같이 설정해줘야 연결됨
  * 9000포트는 거르자 (다 똑같게 세팅해둬도 안되는 사람들이 많았음)

# 21/06/03
### Spring
![spring](./img/spring_flow_chart.PNG)
1. 요청이 올 때 (예시는 http://localhost:9001/board/getBoardList.sp4)
2. 프론트 컨트롤러인 Dispatcher 서블릿이 처리 후 적절한 세부 컨트롤러한테 작업을 뿌려준다  
WebContent/WEB-INF/web.xml
```html
	<servlet>
		<servlet-name>appServlet</servlet-name>
		<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
		<init-param>
			<param-name>contextConfigLocation</param-name>
			<param-value>/WEB-INF/spring-servlet.xml</param-value>
		</init-param>
		<load-on-startup>1</load-on-startup>
	</servlet>
  ```
3. xxx.sp4니 spring-servlet.xml로 보내서  
WebContent/WEB-INF/web.xml
```html
	<servlet-mapping>
		<servlet-name>appServlet</servlet-name>
		<url-pattern>*.sp4</url-pattern>
	</servlet-mapping>
```
4. 또 분류에 따라 board-controller로 이동  
WebContent/WEB-INF/spring-servlet.xml
```html
	<bean id="url-mapping" 
	class="org.springframework.web.servlet.handler.SimpleUrlHandlerMapping">
		<property name="mappings">
			<props>
				<prop key="/board/getBoardList.sp4">board-controller</prop>
				<prop key="/board/jsonGetBoardList.sp4">board-controller</prop>
			</props>
		</property>
	</bean>
```
5. board-controller로 와서 코드가 시킨 board-logic을 참고, 클래스 web.mvc.Board41Controller.java 참고  
WebContent/WEB-INF/spring-servlet.xml
```html
	<bean id="board-controller" class="web.mvc.Board41Controller">
		<property name="methodNameResolver" ref="board-resolver"/>
		<property name="boardLogic" ref="board-logic"/>
	</bean>
```
6.board-mdao & board-sdao 참고, 클래스 web.mvc.Board41Logic.java 참고  
WebContent/WEB-INF/spring-service.xml
```html
	<bean id="board-logic" class="web.mvc.Board41Logic">
		<property name="boardMDao" ref="board-mdao"/>
		<property name="boardSDao" ref="board-sdao"/>
	</bean>
```
7. 계속 경로 참조해서 오라클 접속  
WebContent/WEB-INF/spring-data.xml
```html
	<bean id="data-source-target" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
		<property name="driverClassName">
			<value>oracle.jdbc.driver.OracleDriver</value>
		</property>
		<property name="url">
			<value>jdbc:oracle:thin:@***.0.0.1:1521:orcl11</value>
		</property>
		<property name="username">
			<value>*****</value>
		</property>
		<property name="password">
			<value>*****</value>
		</property>
	</bean>
	<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
		<property name="configLocation" value="WEB-INF/mybatis-config.xml"/>
		<property name="dataSource" ref="data-source-target"/>		
	</bean>
	<bean id="sqlSessionTemplate" class="org.mybatis.spring.SqlSessionTemplate">
		<constructor-arg index="0" ref="sqlSessionFactory"/>
	</bean>
	<bean id="board-mdao" class="web.mvc.Board41MDao">
		<property name="sqlSessionTemplate" ref="sqlSessionTemplate"/>
	</bean>
	<bean id="board-sdao" class="web.mvc.Board41SDao">
		<property name="sqlSessionTemplate" ref="sqlSessionTemplate"/>
	</bean>
```
8. 오라클에서 값 받아오고 돌아와서  
WebContent/WEB-INF/mybatis-config.xml
```html
 <typeAliases>
 	<typeAlias alias="bmVO" type="com.vo.BoardMVO"/>
 	<typeAlias alias="bsVO" type="com.vo.BoardSVO"/>
 </typeAliases>
 <mappers>
 	<mapper resource="com/mybatis/mapper/board.xml"/>
 </mappers>
```
9. board-logic로 오고
10. board-controller 와서
11. 컨트롤러에서 다시 Dispatcher 서블릿으로  
WebContent/WEB-INF/spring-servlet.xml  
```html
	<bean id="board-controller" class="web.mvc.Board41Controller">
		<property name="methodNameResolver" ref="board-resolver"/>
	</bean>
```
12. board-resolver로 와서  
WebContent/WEB-INF/spring-servlet.xml
```html
	<bean id="board-resolver" class="org.springframework.web.servlet.mvc.multiaction.PropertiesMethodNameResolver">
		<property name="mappings">
			<props>
				<prop key="/board/getBoardList.sp4">getBoardList</prop>
				<prop key="/board/jsonGetBoardList.sp4">jsonGetBoardList</prop>
			</props>
		</property>
	</bean>
```
13. 경로 지정해주고 뒤에 jsp붙여줘서 숨어있는? WEB-INF/views/board/getBoardList.jsp를 불러왔다  
WebContent/WEB-INF/spring-servlet.xml
```html
	<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
		<property name="prefix" value="/WEB-INF/views/"/>
		<property name="suffix" value=".jsp"/>
	</bean>
```
