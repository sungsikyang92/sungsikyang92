# TODAY I LEARNED - 20220513

### 1. JS  노드 생성/삽입/삭제하기

##### 1.1 노드생성

새로운 요소 노드 객체를 생성할 때는 createElement() 메서드를 사용한다.

```javascript
const element = document.createElement(요소의 이름);
const element = document.createElement("li");
```

새로운 텍스트 노드 객체를 생성할 때는 ceateTextNode() 메서드를 사용한다.

```javascript
const textnode = document.createTextNode(텍스트);
const textnode = document.createTextNode("TEXT");
```

##### 1.2 노드삽입

*   appendChild() 메서드

    요소 객체에 인수로 넘긴 노드 객체를 해당 요소의 마지막 자식 노드로 삽입한다.

    ```javascript
    요소 노드.appendChild(삽입할노드);
    li.appendChild(span);
    ```

*   insertBefore() 메서드

    지정한 자식 노드 바로 앞에 노드 객체를 삽입할 때 사용한다.

    ```javascript
    요소 노드.insertBefore(삽입할 노드, 자식 노드)
    <ul id="phoneList">
        <li>iPhone</li>
    	<li>Galaxy</li>
    </ul>
    <script>
        const phoneList = document.getElementById("phoneList");
    	const element = document.createElement("li");
    	const text = document.createTextNode("BlackBerry");
    	phoneList.insertBefore(element, phoneList.children[1]);
    	element.appendChilde(text);
    </script>
    ```

    <img width="125" alt="스크린샷 2022-05-13 오후 2 45 50" src="https://user-images.githubusercontent.com/71358285/168219008-5c330374-7190-4eb9-a198-69d4a08696a0.png" align="left">

***



# TODAY I LEARNED - 20220512

### 1.   마크다운에서 빈 체크박스와 체크된 체크박스 만들기

```
- [ ] //빈 체크박스
- [x] //체크된 체크박스
- [X] //체크된 체크박스
```
***

### 2.   spring project 초기 설정 (간편하게 stgart.spring.io에서 만들자)
     1.    spring initializr에서 projectg GENERATE

<img width="666" alt="image" src="https://user-images.githubusercontent.com/71358285/168215315-1222d0e0-13c4-4041-8d65-f20bb56574a7.png">

우선 Dependecies는

*   Spring Web
*   Lombok

을 추가해주었다.
***

### 3. ID 선택자와 CLASS 선택자

선택자의 종류는 많지만, 그 중 id선택자와와 class선택자를 비교해보자.

|          | ID선택자 | CLASS선택자 |
|----------| -------------------- | -------------------- |
|설명| 특정 id 속성이 있는 태그를 선택 | 특정 클래스가 있는 태그를 선택 |
|| 웹 표준에 id 속성은 웹 페이지 내부에서 중복되면 안된다는 규정이 있으므로 아이디 선택자는 특정 태그 하나를 선택할 때 사용한다. | 문서 안 복수의 요소에 스타일을 적용하는 경우에 사용한다. |
|형태|#아이디|.클래스|

태그선택자 < 클래스선택자 < 아이디선택자 < 인라인스타일 < !important 순서로 우선순위를 가진다.

```html
 <h2>선택자 우선순위 테스트</h2>
    <div id="test1" class="test1" style="background-color: purple;">우선순위 테스트</div>
    <p id="test2" class="test2" style="background-color: blue;">우선순위 테스트2</p>
```

***

### 4. AUTOFOCUS

input태그의 autofocus 속성은 페이지가 로드될 때 자동으로 포커스가 input으로 이동됨을 명시해주는 것이다.

***

### 5. JavaScript 시간 가져와서 나타내기

1.   Date객체를 생성한다.

```javascript
const date = new Date();
```

2.   객체 생성 후 가져오고 싶은 정보를 가져온다

```javascript
const getYear = String(date.getFullYear());
```

3.   월과 일의 경우 1자리 숫자일때 보기좋게 두 자리로 표현하기 위해서 padStart()함수를 사용한다.

```javascript
const getMonth = String(date.getMonth()).padStart(2,"0");
```

padStart는 매개변수로 두개를 받을 수 있는데, 앞은 몇자리수까지 나타낼것인지 그리고 뒤는 해당 자리수에 도달하기 위해 어떠한 문자를 채워넣을지 써주면 된다.

***

### 6. TDD(Test-Driven Development, TDD)

TDD란 "프로그램을 작성하기 전에 테스트를 먼저 작성하는 것"이라고 TDD를 주도한 켄트 벡이 정의했다.

TDD의 정의는 "업무 코드를 작성하기 전에 테스트 코드를 먼저 만드는 것" 이라고 정의된다.

코드를 검증하는 테스트 코드를 먼저 만든 다음에 실제 작성해야 하는 프로그램 코드 작성에 들어가라는 뜻이다.

이는 메소드나 함수같은 프로그램 모듈을 작성할 때 '작성 종료조건을 먼저 정해놓고 코딩을 시작한다'라는 의미로 받아들이면 편하다.

```java
public class Calculator{
  public int sum(int a, int b){
    return 0;
  }
  
  public static void main(String[] args){
 		Calculator calc = new Calculator();
    System.out.println(calc.sum(10, 20) == 30);
    System.out.println(calc.sum(1, 2) == 3);
    System.out.println(calc.sum(-10, 20) ==10);
    System.out.println(calc.sum(0,0) == 0);
  }
}
------실행결과------
  false
  false
  false
  true
```

위의 코드를 살펴보면, main메소드를 텟흐트 메소드처럼 사용하였다. sum 메소드는 구현하지 않고 비어있는 상태이고, 검증코드를 먼저 만들어 놓았다. 검증코드에 해당하는 테스트 케이스를 모두 만족하면, 즉 실행 결과가 모두 true로 나오면 sum 메소드가 정상적으로 작성됐다고 판단하기로 한다. 다시말해, 명시적인 코드로 개발 종료조건을 정해놓은 것, 이런 식의 개발 접근 방식이 Test-Driven Development이다.  

<p style="text-align:right;"><sub>출처 - TDD 실천법과 도구(채수원 저자)</sub></p>

***

### 7. gitignore가 작동하지 않을때 해결방법

git의 캐시 문제이므로 터미널을 열어서 캐시 삭제 후 다시 커밋하면 된다.

```bash
git rm -r --cached
git add .
git commit -m "leave a message"
```

![스크린샷 2022-05-12 오후 3.17.07](/Users/ssiky/Library/Application Support/typora-user-images/스크린샷 2022-05-12 오후 3.17.07.png)

이런식으로 gitignore에 적었지만, 업로드 되었던 파일들이 삭제가 된다.

***

### 8. querySelector()와 querySelectAll 그리고 getElementById()

| 이름             | 설명                                                         |
| ---------------- | ------------------------------------------------------------ |
| querySelector()  | selector의 구체적인 그룹과 일치하는 document안의 첫번째 엘리먼트를 반환한다. 일치하는게 없으면 null을 반환한다. |
|                  | css 엘리먼트 선택자로 많이 쓰인다. 좀 더 구체적으로 원하는 것을 선택하여 정보를 가져올 수 있다. |
| getElementById() | id를 통해 엘리먼트를 반환한다. document에 해당하는 ID의 엘리먼트가 없으면 null을 반환한다. |
|                  | dom방식이다.                                                 |

아래의 예시코드로 알아보자.

```javascript
<!DOCTYPE html>
<html>
<head>
  <title>getElementByIdExample</title>
	<script>
  	onload = function(){
  		const header = document.getElementById('header');
  		header.style.color='orange';
  		header.style.background='red';
  		header.innerHTML = 'From JavaScript';
		};
  </script>
</head>
<body>
	<h1 id="header">Header</h1>
</body>
</html>
```


```javascript
<!DOCTYPE html>
<html>
<head>
  <title>querySelectorExample</title>
	<script>
  	onload = function(){
  		const header = document.querySelector('h1');
  		header.style.color='orange';
  		header.style.background='red';
  		header.innerHTML = 'From JavaScript';
		};
  </script>
</head>
<body>
	<h1>Header</h1>
	<h1>Header</h1>
	<h1>Header</h1>
</body>
</html>
```
```javascript
<!DOCTYPE html>
<html>
<head>
  <title>querySelectorAllExample</title>
	<script>
  	onload = function(){
  		const headers = document.querySelectorAll('h1');
    	for (const i = 0; i < headers.length; i++){
            const header = headers[i];
              	header.style.color='orange';
		  		header.style.background='red';
  				header.innerHTML = 'From JavaScript';
        }
	};
  </script>
</head>
<body>
	<h1>Header</h1>
	<h1>Header</h1>
	<h1>Header</h1>
</body>
</html>
```



***

### 9. script의 defer

/html을 만나야 script가 실행되기 시작하게 한다. 페이지를 먼저 로드하고 scriptr가 실행됨으로, 페이지를 불러 올 때 빠르게 불러온다는 착각을 주게 할 수 있다.

***

### 10. innerText와 innerHTML의 차이점

element.innerText는 element안의 text값들만 가져온다. 그러나 element.innerHTML은 element안의 HTML이나 XML을 가져온다.

***





