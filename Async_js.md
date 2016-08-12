#Async.js
---
##1. 콜백헬(CallBack - Hell)
1. 콜백헬이란
	- 함수들을 순차적으로 실행하고자 할때 콜백 함수들의 중첩이 생겨서 코드가 복잡해지는 문제가 발생하는데 이를 콜백헬이라합니다.
	- 코드가 복잡해지고, 코드의 가독성이 떨어져서 유지 보수가 매우 힘들어지게 됩니다.
2. **예** : confirm 창이 여러번 발생하게 한 함수
    
    >callback3rd('three',
    >>callback2nd('222',
    >>>callback1st('111','one')
    >
    >>)
    >
    >);
  
    >function callback1st(arg1, arg2) {
    >>document.write("func1 = " + arg1 + ", " + arg2 + "<br\>");
    >
    >}

    >function callback2nd(arg3, func3) {
    >>document.write("func2 = " + arg3 + "<br\>");
    >
    >}

    >function callback3rd(arg4,func2) {
    >>document.write("func3 = " + arg4 + "<br\>");
    >
    >}

---

##2. Async.js란
1. 콜백헬을 해결할 수 있는 package
2. 종류
	> Async.js 내에는 많은 함수(약 20개)가 있지만 그 중 대표적으로 사용되는 4개의 예제만 소개하겠습니다.
	1. Waterfall(폭포)
		- 기본적으로는 task가 순서대로 실행
		- Result가 마지막 callback에 모이는 게 아니라 실행되는 각 작업(함수) 사이로 전달
		- 함수 실행 중 err가 있으면 그 이후로는 실행 중단
		- **예** : 위의 콜백헬이 발생한 코드를 waterfall 방식으로 처리했습니다.
	

    	>var async = require('async');

		>async.waterfall([
    	>>function(callback){
		>>>callback(null, '111', 'one');
		>>
  		>>},
    	>>function(arg1, arg2, callback){
    	>>>document.write("func1 = " + arg1 + ", " + arg2 + "<br\>");
    	>>>callback(null, '222');
    	>>
    	>>},
    	>>function(arg, callback){
    	>>>document.write("func2 = " + arg3 + "<br\>");
    	>>>callback(null, 'three');
    	>>
    	>>}  
    	>
    	>],   
    	>function(err, result){  
    	>>document.write("func3 = " + result + "<br\>");
    	>
    	>});

    2. Series(직렬)
	    - 주어진 함수 배열(혹은 object)을 순서대로 실행
	    - 모든 함수 실행이 끝나면 callback이 호출
	    - 함수 실행 중 err가 있으면 그 이후로는 실행 중단
	    - **예** : 위의 콜백헬이 발생한 코드를 Series 방식으로 처리했습니다.

		>var async = require('async');

		>async.series([
  		>>function(callback){
        >>>callback(null, '111', 'one');
        >>
  		>>},  
  		>>function(callback){
    	>>>callback(null, '222');
    	>
  		>>},  
  		>>function(callback){
	    >>>callback(null, 'three');
	    >
        >>}
        >
        >],  
		>function(err, results){
		>>document.write("func1 = " + result[0][0] + ", " + result[0][1] + "<br\>");  
  		>>document.write("func2 = " + result[1] + "<br\>");  
  		>>document.write("func3 = " + result[2] + "<br\>");
  		>  
		>});  
	3. Parallel(병렬)
		- 주어진 함수 배열(혹은 object)을 동시에 실행
		- 모든 함수 실행이 끝나면 callback이 호출
		- 함수 실행 중 err가 있으면 그 이후로는 실행 중단
		- **예** : 위의 콜백헬이 발생한 코드를 Parallel 방식으로 처리했습니다.
		>var async = require('async');
		>var tasks;
		>var i = 0;

		>var func = function(callback){
		>>if(i===0){
	    >>>++i;  
	    >>>callback(null,'111','one');  
	  	>>>return;
	  	>>
		>>}else if(i===1){
	  	>>>++i;  
	  	>>>callback(null,'222');  
	  	>>>return;
	  	>
		>>}else{
		>>>++i;  
	  	>>>callback(null,'three');  
	  	>>>return;
	  	>
		>>}
		>
		>}
<br><br>
		>var tasks = {};
		>for(var j = 0; j < 3; j++){
		>>tasks['func'+j] = func;
		>
		>}
<br><br>
		>async.parallel(tasks,
  		>>function(err, results){
		>>>document.write("func1 = " + result.func0 + "<br\>");  
    	>>>document.write("func2 = " + result.func2 + "<br\>");  
    	>>>document.write("func3 = " + result.func3 + "<br\>");  
    	>
  		>>}
  		>
		);
	4. Auto(자동)
		- Ascync를 자동으로 구현
		- 병렬, 직렬 처리를 맘대로 할 수 있다.(series와 parellel의 기능을 모두 가지고 있다.)
		- **예** : 위의 콜백헬이 발생한 코드를 Auto 방식으로 처리했습니다.
		
		>var async = require("async");
		>async.auto ({
		>>func1: function(callback){
		>>>callback(null,'111','one');
		>
		>>},
		>>func2: function(callback){
		>>>callback(null,'222');
		>
		>>},
		>>func3: function(callback){
		>>>callback(null,'three');
		>
		>>}
		>
		>},  
		>function (err, results) {
		>>if (err) {
		>>>console.log(err);
		>
		>>} else {
		>>>document.write("func1 = " + result[0][0] + ", " + result[0][1] + "<br\>");  
        >>>document.write("func2 = " + result[1] + "<br\>");  
        >>>document.write("func3 = " + result[2] + "<br\>");     
		>
		>>}
		>
		>});

---

##3. 참조
>bloodguy블로그  
>><http://bloodguy.tistory.com/entry/nodejs-async-%EB%AA%A8%EB%93%88%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EB%B9%84%EB%8F%99%EA%B8%B0-%EC%B2%98%EB%A6%AC-%ED%8C%A8%ED%84%B4>

>dakoo's tech 블로그  
>><http://dakoostech.blogspot.kr/2015/03/asyncjs-flow-asyncwaterfall-asyncseries.html>