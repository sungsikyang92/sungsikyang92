# **오류 해결 과정**

# 20220719

*   에러발생

사진업로드 후 불러오는 과정에서 에러가 발생했다.

경로상의 문제인데, 로컬저장소에 저장을 하고 웹에 불러오니 작업이 이루어지지 않았다.

이에 방법은

1.   그냥 워크스페이스에 저장하고 불러온다.
2.   s3를 사용한다.

워크스페이스에 저장하고 불러오는것은 이미 하고있었고, 이것은 그냥 연습으로 하기에는 좋았다.

그래서 s3를 사용하기로 결심했고, 현재 네이버 아이디가 있기에 네이버 s3인 object storage를 무료로 사용할 수 있었다.

그런데 네이버에 들어가야할 값이 명확히 명시되지않아 너무 모호했다. 결국 하루종일 시도했지만 성공하지못하였고, 네이버 s3를 사용하지 못했다. 사람들이 사용하지 않아서 자료조차 찾을 수 없엇다.



# 20220713

*   에러발생

    ![스크린샷 2022-07-13 오전 9.43.40](/Users/ssiky/Library/Application Support/typora-user-images/스크린샷 2022-07-13 오전 9.43.40.png)

*   해결방법

    

# 20220712

*   에러발생

    jsp에서 c:forEach하여 리스트값을 불러오는데 값을 불러오지못하는 현상

    ![스크린샷 2022-07-12 오전 10.57.33](/Users/ssiky/Library/Application Support/typora-user-images/스크린샷 2022-07-12 오전 10.57.33.png)

*   해결하기 위하여 한 행동

    1.   Controller에서부터 ServiceImpl, Service, Mapper, Dto 모두 확인하였다. 입력된 값없이 데이터를 불러오는것이기에 따로 값이 잘 전달되는지 확인해야할 필요는 없었다. 

    2.   전달되는것 말고 값을 잘 불러오는지 확인해보았다.

         `System.out.println(communityMapper.getComBoardList().get(0));`

         service, controller에서 정상적으로 잘 받아온다

         `CommunityDto(cBoardNo=1, cTitle=test1, cContent=test중입니다, cCreateDate=Tue Jul 12 00:00:00 KST 2022, cIsModified=false, cLocation=testLoc, cCategory=testCat, userNo=1, hashNo=1, picNo=1)`

    3.   dto 변수명과 db의 변수명이 같은지 확인해보았으나, 다른점을 찾을 수 없었다.

*   해결

    getter와 setter를 적용시키며 변수명이 조금씩 변했다.

    Community게시판의 변수들이라 앞에 c를 붙이고 fk로 받아오는 값들은 c가 없이 들어가있었다.

    그런데 getter와 setter가 적용되며 c값들은 대문자로 인식이되었고, c가 붙지않은 값들은 그대로 적용이되었다.

    결국 jsp 화면에서 c가 붙은 변수명들을 C로 바꾸어주었고, 나머지는 소문자 그대로 유지하니 해결되었다.

    



# 20220627 ![스크린샷 2022-06-27 오전 8.15.01](/Users/ssiky/Library/Application Support/typora-user-images/스크린샷 2022-06-27 오전 8.15.01.png)

드디어 위의 에러를 해결했다.

1.   경로가 \img02.jpg가 아닌 /img02.jpg가 되게 수정해주었다. 윈도우와 다르기때문에 \\이 아닌 /을 사용해준다.
2.   그리고나서도 같지만 조금 다른 문제가 지속되었는데. 300에러로써 권한이 없다는 에러였다. 모든 이미지의 권한은 chmod777로 바꿔주었다.
3.   그리고나서도 문제가 발생하였는데. 같은 300에러였다. 모든 경로에 이미지가 제대로있는지 확인해주었다. resources/static과 target폴더안의 static 그리고 FINDER내의 경로에도 이미지가 제대로 있는지 확인하였다. 그 결과 누락이 되어있음을 확인했고, 누락을 확인한 후에는 파일명이 다르다는것을 찾아냈다.

위의 세가지를 모두 해서일지.. 마지막 3번째 방법덕분에 되었을지는 잘 몰르겠지만, 해결했다. 드디어.,.!



# 20220624

패스 안잡아진다...진짜..화난다... 이거 무조건 해결한다...20220627해결완료



# 20220619

지금 몇일째 첫페이지 불러오는것과 DB연결에 대하여 오류가 지속적으로 발생하고 있다..

Exception during pool initialization 오류이다.

`java.sql.SQLException: Access denied for user 'ssiky'@'localhost' (using password: YES)`

인데.. 

내가 설정한 mysql의 유저는 ssy였다. 그런데 계속 ssiky를 찾는다.

그래서 ssiky를 만들어서 연결했더니 해결되었다. 왜그럴까?

# 20220615

## No editor descriptor for id org.eclipse.jst.jsp.core.jspsource.source // No editor descriptor for id com.springsource.sts.config.ui.editors.SpringConfigEditor

맥북의 네트워크가 잘 되지않아서 TUVA가서 검사를 받고왔다.. 그런데 검사만 받았을 뿐인데.. 정상적으로 종료되었던 이클립스가 되지 않아서 삭제했다가 다시 설칠했다.

그랬더니 제목의 두 에러가 떳다.

첫번째 오류는 `Help`->`Install New Software`-> `Work with`->`All Availablt Sites`에서 `Web,XML,JavaEE AND OSGI Enterprise Development`설치해주면 해결된다.

두번째 오류는 `Help`->`Install New Software`->스프링 관련 검색으로 `Spring IDE Boot Support`를 설치해주면 오류가 해결된다.







# 20220611

## Controller에서 JSP로 값을 넘기지 못하는 경우

*   문제발생

게시판 제목을 클릭하며 상세보기페이지로 넘어갔을때, controller에서 jsp로 값을 넘기지 못하는 오류가 발생하였다.

*   해결과정

1.   우선 게시물을 클릭하였을때 PathVariable을 통하여 해당 게시물의 번호가 잘 전달되는지 확인하였다. 결과 이상없음
2.   컨트롤러로 부터 시작하여, service와 repository 그리고 sql문까지 게시물의 번호가 잘 전달되고 그걸 통해서 원하는 값들이 순차적으로 잘 return되는지 확인하였다. 결과 이상없음

*   해결

모든 값은 list로 return되었고, list그대로 jsp로 넘겨 반복문이 존재하지않아 값을 뽑아올수 없었던 문제였다.

controller에서 return받은 list를 반복문을 통해 model에 필요한 값을 각각 add해줌으로써 문제를 해결할 수 있었다.



# 20220610

## Spring MVC with jdbc - Board Config 404 and 500 Error

*   해결과정

1.   우선 모든 기본 path들을 "/"으로 설정해주었다. 그럼에도 문제가 지속되었다.
2.   설정한 config들이 백엔드 WebApi 제작할때의 config로써 페이지를 불러오지 못한다는것을 알았고, SpringConfigClass를 따로 만들었다.
     1.   이를통해 web.xml설정이 아닌 java config 클래스 사용법을 알 수 있었다. 
3.   이 과정에서 문제는 500에러와 Bean을 찾지 못하는 문제가 생겼었다.
     1.   SpringConfigClass를 만들면서 하나의 클래스를 만들어주고 그것으로 Bean을 정의해주었는데, 이미 내가 만들어놓은 Bean을 정의하는 클래스가 있었음으로 충돌이 생긴것이었다.
4.   그 후의 404에러로 돌아와서 Config의 경로설정을 잘못한것을 찾아내어 고쳤다.

*   해결

결국 마지막에는 테이블과 dto의 변수명을 제대로 입력하지 않아서 발생한 문제로 마무리 지으며 오류가 마무리되었다.







# 20220602

## SQL에서 특정 문자열이 출력되지 않을때 혹은 null값으로 출력이 될 때

*   해결과정

우선적으로 콘솔의 오류를 찾아보았다. sql에러라는것을 알 수 있었음.

1.   sql문 실행해보니 문제없이 원하는 답이 출력이 되는것을 확인, 그러나 동일한 문제가 발생함
2.   쿼리문중 하나를 직접 대입하지않고, static final로 만들어서 코드에서 실행, 그러나 동일한 문제가 발생함

*   해결

1.   특정 문자열이 출력되지 않을때의 경우, 애초에 dto에서 누락되어있었다.. 왜 누락되었을까. 앞으로는 문제 발생 시 dto까지 꼭 체크하자.
2.   null값으로 출력될때, 이는 dto의 네이밍과 쿼리문의 네이밍이 맞지 않아서 생긴 문제였다. ALIAS를 사용하여 네이밍규격을 맞춰주니 해결되었다.

***

## CoponentScan의 basePackages 설정 문제

*   문제

본래 service패키지에 service와 serviceImpl이 그리고 dao패키지에 dao와 daosql이 같이 있었다. 그 후, 웹 어플리케이션을 실행하고나니 적어도 1개 이상의 빈을 찾을수가 없다는 오류가 발생했다.

*   해결과정

1.   Controller, Service, Repository 어노테이션들이 잘 설정되어있는지 확인하였다.
2.   Service를 serviceImpl과 서로 다른 패키지로 옮기면서 문제가 발생하지 않았을까 해서
     1.   본래 경로인 dao와 service까지의 경로에서 dao.sqls 그리고 serviceImpl로 경로를 바꿔주었으나 같은 오류가 발생했다.
     2.   dao.* 그리고 service.*로 경로를 바꿔보았으나 같은 오류가 발생하였다.

*   해결

dao와 dao.sqls 그리고 service와 serviceImpl 모두를 등록하였다. 



# 20220531

## WebAppInitializer.config로 web.xml을 대체할때 404 에러

*   해결과정

1.   pom.xml과 web.xml의 설정을 조금씩 바꿔가며 실행했을때 뜨는 콘솔에러를 보고 수정해봄
2.   위와 같은 과정에서 Problems에 뜨는 오류를 수정해봄
3.   config들에 잘못작성된 코드가 없는지 다시 확인해봄
4.   build Path와 contextPath를 '/'으로 수정해봄

*   해결

콘솔창에서 web.xml에 관련된 오류인것을 다시한번 확인하였다. 읽어보니 실행에대하여 두가지가 있어서 충돌이 발생해서 404에러가 뜬것 같았다. 생각해보니 WebAppInitializer.config가 web.xml을 대신하기 위해 만든것이니 주석처리가 아닌 그냥 삭제해서 없애버리면 충돌이 사라지지않을까? 하는 생각에 그냥 지워버리고 실행시켜봤다.

정상 작동한다...이것으로 몇시간을 쓴것일까..



# 20220527

## 방명록 웹어플리케이션에서 한글 입력시 DB의 한글이 깨진다.

*   해결과정

우선 이클립스와 프로젝트의 설정에서 UTF-8로의 인코딩이 잘 되어있는가 확인하였다.

그 후 데이터가 이동하는 flow에 대하여 생각

1.   config들에서 UTF-8로 설정해야하는 파일들에서 잘 되어있는지 확인
2.   Servlet단계에서  response.setContentType("text/html; charset=UTF-8")로 인코딩했던거 기억해서 controller 찾아봄. 근데 컨트롤러 레이어에서는 없어도됨. controller Test에서 문제없이 한글 잘 입출력 출력 되는거 확인.
3. service 레이어확인 여기도 그런거 없어서 관계 무, service test에서 문제없이 한글 잘 입출력되는거 확인
4. dao 확인, dao 테스트에서 문제없이 한글 입출력 되는거 확인

5.   다 잘 되는데 왜? 뒤늦게 pom.xml이랑 web.xml확인함. 근데 여기서 문제있었으면 애초에 안될거라 생각. 보니까 web.xml 필터에서도 UTF-8 해놈

이미 몇시간이 지나있었다. 인터넷 검색해도 이미 내가 적용해보았거나, 나한테 해당안되는것들만나옴.(이미 다 해봄)

*   해결

다시한번 마지막으로 해보고 안되면 나중에 해보자는 마음으로 모두 천천히 살펴봄.

그러던 중 web.xml의 filter-mapping의 url-pattern이 '/'인것을 발견, '/*'으로 적용해보니....

#### 해결이되어버렸다

'/'만 해놓으면 그 위치만 적용이되고 '/*'의  '\*'가 붙어있어야 그 하위 링크들도 UTF-8이 적용이 되는가보다.

