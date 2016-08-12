# JQuery on / off
##1. on / off
1. 하나 또는 그 이상의 요소에 **이벤트 헨들러를 부여 / 해제**한다.
2. 형식
	- .on( events [, selector] [, data], handler( eventObject ) )
	- events -> 해당 요소의 이벤트 종류
		- click, keydown 등의 이벤트가 존재한다.
	- selector -> 이벤트가 발생할 요소의 후손을 찾는 선택자
	- data -> 이벤트 발생시 헨들러에 전송할 데이터
	- handler( eventObject ) -> 이벤트 발생 시의 기능
3. 동적처리 시의 주의점
	- 위의 selector를 추가해서 하위 요소에서 발생한 이벤트도 반응하도록 유도해야 한다.
	- **예1** : BAD 하위 요소에서 이벤트 발생 불가
    >$("#buttonId li").on("click", function() {
    >>alert($(this).text());
    >
    >});
    >
    >$("button").on("click", function() {
    >>$("ul").append("<\li>added</li\>");
    >
    }
    - **예** : GOOD 하위 요소에서도 이벤트 발생
    >$("#buttonId").on("click", "li", function() {
    >>alert($(this).text());
    >
    });

    >$("button").on("click", function() {
    >>$("ul").append("<li\>added</li\>");
    >
    });

4. Events-map
	- 문자열, JSON 등이 올 수 있다.
	- **예** : 문자열의 Events-map
	  >$("button").on("click mouseout", function() {  
      >>alert("이벤트 발생!");  
      >});
    - **예** : SJON의 Events-map  
	  >$("#demo9 button").on({  
      >>  click: function() {  
      >>>    $("button").html("<span style='color: red;'>click event</span>")
      >  
      >>  },  
        mouseover: function() {  
      >>>    $("button").html("<span style='color: blue;'>mouseover event</span>")
      >  
      >> }
      >  
      }); 
5. Events namespace
  	- 하나의 요소에 다수의 헨들러가 포함되어 있을 경우 이를 제어하기 위한 기능
  	- **예** : 
  	>jQuery(document).ready(function() {
    >>$("#divId #buttonId").on("click.first", function() {
    >>>alert("first action");
    >
    >>});

    >>$("#divId #buttonId").on({
    >>>"click.second": function() {
    >>>>alert("second action");
    >
    >>>},  
    >>>"click.third": function() {
    >>>>alert("third action");
    >
    >>>}
    >
    >>});
    >
    });

    >function fn_del() {
    >>$("#divId #button2Id").off("click.second");
    >
    >}
6. data 
	- hendler에 보내어지는 data
	- **예** : 
	>function foo(event) {
    >>    alert(event.data.txt1 + event.data.txt2);
    >
    }

    >$("#demo13 #do").on("click", {txt1: "hello", txt2: " world!"}, foo);

---

##2.참조
><http://noritersand.tistory.com/218>