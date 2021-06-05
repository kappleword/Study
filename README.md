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
```
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
```
	<servlet-mapping>
		<servlet-name>appServlet</servlet-name>
		<url-pattern>*.sp4</url-pattern>
	</servlet-mapping>
```
4. 또 분류에 따라 board-controller로 이동  
WebContent/WEB-INF/spring-servlet.xml
```
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
```
	<bean id="board-controller" class="web.mvc.Board41Controller">
		<property name="methodNameResolver" ref="board-resolver"/>
		<property name="boardLogic" ref="board-logic"/>
	</bean>
```
6.board-mdao & board-sdao 참고, 클래스 web.mvc.Board41Logic.java 참고  
WebContent/WEB-INF/spring-service.xml
```
	<bean id="board-logic" class="web.mvc.Board41Logic">
		<property name="boardMDao" ref="board-mdao"/>
		<property name="boardSDao" ref="board-sdao"/>
	</bean>
```
7. 계속 경로 참조해서 오라클 접속  
WebContent/WEB-INF/spring-data.xml
```
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
```
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
```
	<bean id="board-controller" class="web.mvc.Board41Controller">
		<property name="methodNameResolver" ref="board-resolver"/>
	</bean>
```
12. board-resolver로 와서  
WebContent/WEB-INF/spring-servlet.xml
```
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
```
	<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
		<property name="prefix" value="/WEB-INF/views/"/>
		<property name="suffix" value=".jsp"/>
	</bean>
```
