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
