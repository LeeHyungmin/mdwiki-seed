#Jquery HTML DOM 접근방법
---
##1. DOM
1. HTML 트리 구조를 통해 클라이언트 영역에서 재조합 기능을 제공하여 사용자와 상호 작용을 하는 구조적인 모델로 HTML 트리 구조 내에서 개별 객체에 접근이 제공되는 방법을 말합니다.
2. 간단하게 각 요소에 접근이 가능한 HTML의 트리구조  
##
	<html>
        <head>
            <title>DOM Tree</title>
        </head>
        <body>
            <div>Hello jQuery</div> 
                <p>안녕하세요?</p>
        </body>
    </html>
##
![](http://www.sqler.com/files/attach/images/368179/192/386/0c1cae25491bfc1156614c1084125b0a.jpg)
---
##2.셀렉터(Selecter)
1. 원하는 개체를 쉽게 선택하는 방법
2. ###기본 셀렉터
	> 예제는 **[유니비전](http://211.238.176.44:8020/univision/)**홈에서 확인 가능
	1. $("*")
		- **모든 요소**를 배열형식의 JQuery 개체로 반환
		- **예** : 모든 요소에 빨간 테두리 부여
			- $("*").css("border", "1px solid #ff0000");
	2. $("#id")
		- 요소 중 **특정 ID의 엘리먼트**를 반환
		- **예** : 로그인 폼에 빨간 테두리 부여
			- $("#loginForm").css("border", "1px solid #ff0000");
	3. $("elementName")
		- 특정하는 요소 즉 **특정 태그와 동일한 개체**를 찾아 배열형식의 JQuery 개체로 반환
		- **예** : input 태그에 초록 테두리 부여
			- $("input").css("border", "1px solid #00ff00");
	4. $(".className")
		- 요소 중 **특정 class의 엘리먼트**를 반환
		- **예** : login_box라는 class를 사용하는 개체에 시안색의 테두리 부여
			- $(".login_box").css("border", "1px solid #00ffff")
	5. $("selector1, selector2, selectorN)
		- 여러 셀렉터를 통하여 **여러 요소에 접근 가능**
		- **예** : 위의 예제 2,3,4번의 엘리먼트에 파란색 테두리 부여
			- $("#loginForm, input, .login_box").css("border", "1px solid #0000ff")
<br><br>
3. ###속성값을 통한 셀렉터
	> 예제는 **[유니비전](http://211.238.176.44:8020/univision/)**홈에서 확인 가능
	1. $(Selector[attr])
		- attr값을 가지는 셀렉터를 반환
		- **예** : form 태그에 action 속성이 있는 엘리먼트에 자주색 테두리 부여
			- $("form[action]").css("border", "1px solid #ff00ff");
	2. $(Selector[attr='value'])
		- attr의 값이 value인 셀렉터 반환
		- **예** : form 태그에 action 속성의 값이 *'/univision/security/login2'*인 엘리먼트에 자주색 테두리 부여
			- $("form[action='/univision/security/login2']").css("border", "1px solid #ff00ff");
	3. $(Selector[attr!='value'])
		- attr의 값이 value가 아닌 셀렉터 반환
		- **예** : form 태그에 action 속성의 값이 *'/univision/security/login2'*이 아닌 엘리먼트에  자주색 테두리 부여
			- $("form[action!='/univision/security/login2']").css("border", "1px solid #ff00ff");
	4. $(Selector[attr^='value'])
		- attr의 값이 value로 시작하는 셀렉터 반환
		- **예** : form 태그에 action 속성의 값이 *'/u'*로 시작하는 엘리먼트에 자주색 테두리 부여
			- $("form[action^='/u']").css("border", "1px solid #ff00ff");
	5. $(Selector[attr$='value'])
		- attr의 값이 value로 끝나는 셀렉터 반환
		- **예** : form 태그에 action 속성의 값이 *'n2'*로 끝나는 엘리먼트에 자주색 테두리 부여
			- $("form[action$='n2']").css("border", "1px solid #ff00ff");
	6. $(Selector[attr*='value'])
		- attr의 값이 value를 포함하는 셀렉터 반환
		- **예** : form 태그에 action 속성의 값이 *'/s'*를 포함하는 엘리먼트에 자주색 테두리 부여
			- $("form[action*='/s']").css("border", "1px solid #ff00ff");
	7. $(Selector[attr~='value'])
		- attr의 값이 정확한 value를 포함하는 셀렉터 반환
		- ~='man'이라면 'iron man'은 포함되지만 'superman'은 포함되지 않습니다.
		- 즉 공백 + value라고 생각하시는 게 쉽습니다.
		- **예** : form 태그에 method 속성의 값이 완전한 *'/s'*를 포함하는 엘리먼트에 자주색 테두리 부여
			- $("form[action~='/s']").css("border", "1px solid #ff00ff");
<br><br>
4. ###DOM 계층을 이용한 요소 접근
    > 예제는 **[유니비전](http://211.238.176.44:8020/univision/)**홈에서 확인 가능  
	>IE6버전 포함 그 이전 버전의 브라우저에서는 사용되지 않습니다.
	1. $("parent > child")
		- Child Selector라고 하며 부모(parent)요소 바로 아래 자식(child)인 엘리먼트 반환
		- **예** : div 태그 하위의 article 태그에 빨간색 테두리 부여
			- $("div > article").css("border", "1px solid #ff0000");
	2. $(“ancestor descendant”)
		- Descendant Selector라고 하며 조상(ancestor)과 일치하는 후손(descendant)인 엘리먼트 반환
		- **예** : div 태그 하위의 img 태그에 노란색 테두리 부여
			- $("div img").css("border", "1px solid #ffff00");
	3. $(“prev + next”)
		- Next Adjacent Selector라고 하며 Prev요소 바로 다음 형제(adjacent) 요소인 next요소 반환
		- **예** : p 태그의 형제인 form 태그에 초록색 테두리 부여
			- $("p + form").css("border", "1px solid #00ff00");
	4. $(“prev ~ siblings”)
		- Next Siblings Selector라고 하며 Prev요소 다음 형제들(sibling)인 엘리먼트 모두 반환
		- **예** : p 태그의 형제인 form 태그에 시안색 테두리 부여
			- $("p ~ form").css("border", "1px solid #00ffff");  

---

##3. 참조
><http://www.sqler.com/>