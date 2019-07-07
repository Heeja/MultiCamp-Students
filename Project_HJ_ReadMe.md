## Express Module 설치

⚙︎⚙︎ **node가 설치 되어 있는 상황이어야 한다.**

1. Express Generator Module 설치
   **npm i -g express-generator**

2. 프로젝트 생성
   **express [생성할 디렉토리 이름] —view=ejs**

3. **cd [생성한 디렉토리 이름**]

4. 사용할 session 모듈을 추가로 설치해준다.
   **npm i express-session**

5. 개발 편의를 위해 nodemon을 설치한다. (코드를 수정하고 저장할 때 마다 서버를 재시작한다.)
   **npm i -save-dev nodemon**

6. 마지막으로 처음에 생성한 Express module을 설치한다.
   **npm i**

7. 설치한 모듈 서비스 시작.

   **npm start**

8. 브라우저를 통해 정상적으로 접속 되는지 확인한다.
   서비스 하는 IP에 3000포트로 접속한다. (Service IP : 3000)
   [express module이 설치된 폴더] \ bin \ **www** 파일 안에 포트번호를 지정할 수 있다.



## 기초 설정

출처: https://html5up.net/txt

1. 기본으로 사용할 홈페이지를 적용시킨다.
   html 파일을 복사하여 붙여 넣거나, html 코드를 index.ejs에 복사한다.

2. html파일을 사용하려면 app.js에 아래 코드를 추가해야한다.

   ```
   app.engine('html',require('ejs').renderFile);
   ```

3. 또한 html 파일 명에 맞도록 route 기능도 추가해야한다.
   Ex) 주소 뒤에 /index로 접속하면 ./routes/index.js를 통해 index.ejs를 호출한다.

   ```
   app.use('/index', require('./routes/index'));
   ```

4. 기본적으로 ejs 확장명은 생략되지만 html 확장명은 적어주어야 한다.

   ```
   res.render('index.html',);
   ```

5. Html 코드

   ```
   <!DOCTYPE HTML>
   <html>
   <head>
   	<title>Project HJ</title>
   	<meta charset="utf-8" />
   	<meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no" />
   
   	<!-- CSS Link -->
   	<link rel="stylesheet" href="stylesheets/main.css" />
   	<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
   
   	<!-- Script -->
   	<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
     	<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.0/js/bootstrap.min.js"></script>
   	<script src="javascripts/basic.js"></script>
   	
   </head>
   
   <body class="homepage is-preload">
   	<div id="page-wrapper">
   
   		<!-- Header -->
   		<header id="header">
   			<div class="logo container">
   				<div>
   					<p>Project. </p>
   					<h1><a href="/" id="logo">HJ</a></h1> <br>
   					<p class="header_p">Music Copyright fusion in BlockChain </p>
   				</div>
   			</div>
   		</header>
   
   		<!-- Nav -->
   		<nav id="nav">
   			<ul>
   				<li class="current"><a href="/">Home</a></li>
   				<li><a href="#">Product</a></li>
   				<li><a href="/search">Search Music</a></li>
   				<li><a href="#">Support</a></li>
   			</ul>
   
   		</nav>
   
   		<!-- Banner -->
   		<section id="banner">
   			<div class="content">
   				<h2>Welcome to Project HJ</h2>
   				<a href="#main" class="button scrolly">Contact</a>
   			</div>
   		</section>
   
   		<!-- Footer -->
   		<footer id="footer">
   			<div class="container">
   				<div class="row gtr-200">
   					<div class="col-12">
   
   						<!-- About -->
   						<section>
   							<h2 class="major"><span>What's this about?</span></h2>
   							<p>
   								This is <strong>TXT</strong>, yet another free responsive site template designed by
   								<a href="http://twitter.com/ajlkn">AJ</a> for <a href="http://html5up.net">HTML5 UP</a>.
   								It's released under the
   								<a href="http://html5up.net/license/">Creative Commons Attribution</a> license so feel
   								free to use it for
   								whatever you're working on (personal or commercial), just be sure to give us credit for
   								the design.
   								That's basically it :)
   							</p>
   						</section>
   
   					</div>
   					<div class="col-12">
   
   						<!-- Contact -->
   						<section>
   							<h2 class="major"><span>Get in touch</span></h2>
   							<ul class="contact">
   								<li><a class="icon brands fa-facebook-f" href="#">
   									<span class="label">Facebook</span></a></li>
   								<li><a class="icon brands fa-twitter" href="#">
   									<span class="label">Twitter</span></a>
   								</li>
   								<li><a class="icon brands fa-instagram" href="#">
   									<span class="label">Instagram</span></a></li>
   								<li><a class="icon brands fa-dribbble" href="#">
   									<span class="label">Dribbble</span></a>
   								</li>
   								<li><a class="icon brands fa-linkedin-in" href="#">
   									<span class="label">LinkedIn</span></a></li>
   							</ul>
   						</section>
   					</div>
   				</div>
   
   				<!-- Copyright -->
   				<div id="copyright">
   					<ul class="menu">
   						<li>&copy; Untitled. All rights reserved</li>
   						<li>Design: <a href="http://html5up.net">HTML5 UP</a></li>
   					</ul>
   				</div>
   			</div>
   		</footer>
   	</div>
   </body>
   </html>
   ```



## Login, 회원가입(Join) Button

1. 페이지 상단 메뉴바에 버튼을 추가하여 본다.

   ```
   <!-- Nav -->
   		<nav id="nav">
   			<ul>
   				<li class="current"><a href="/">Home</a></li>
   				<li><a href="#">Product</a></li>
   				<li><a href="/search">Search Music</a></li>
   				<li><a href="#">Support</a></li>
   			
           <li class="signin">
             <a href="#modalLayer_Login" class="modalLoginLink">LOG IN</a></li>
           <li class="signup">
             <a href="#modalLayer_Join" class="modalJoinLink">Join</a></li>
             
   	</ul>
   ```

   ul태그 안에 li태그를 그대로 사용하여 버튼을 만든다
   button태그를 사용하지 않고 a태그를 통해 동작하도록 하였다.



## Login, 회원가입(Join) 창

1. Login과 Join 버튼을 눌렀을때, 페이지 중앙에 팝업으로 나오도록 index.ejs(html)에 코드를 작성한다.

   ```
   <!-- Modal_LogIn -->
   <div id="modalLayer_Login">
    <div class="modalLoginContent">
     <div id="close">x</div>
    <div>
     <div class="LogIn">Login IN</div>
     <form name="loginReq" method="post" id="loginReqID">
      <div>
       <input class="inputType" type="text" name="login_email" placeholder="Email">
      </div>
      <div>
   		<input class="inputType" type="password" name="login_paswdd" placeholder="Password">  
      </div>
      <div>
       <div>
        <div class="checkBoxText" name="RememID" >Remember ID</div>
        <input type="checkbox" />
       </div>
       <div><input class="inputsumbit" type="submit" value="LOG IN"></div>
      </div>
     </form>
     <div class="divcoment" >u... want.. together us..
     <span class="spantype" role="button">
     <strong id="Loing_Join">Join</strong>
     </span>
   </div>
   </div>
   </div>
   </div>
   
   <!-- Modal_Join -->
   <div id="modalLayer_Join">
    <div class="modalJoinContent">
     <div id="close">x</div>
     <div>
      <div class="Join">Join</div>
      <form name="joinReq" method="post" id="joinReqID">
       <div>
        <input class="inputType" type="text" name="joinEmail" placeholder="Email">
       </div>
       <div>
        <input class="inputType" type="text" name="joinName" placeholder="Name">
       </div>
       <div>
        <input class="inputType" type="password" name="userPaswdd" placeholder="Password">
       </div>
       <div>
        <input class="inputType" type="password" name="confirmPaswdd" placeholder="Comfirm Password">
       </div>
      <div>
       <div>
        <div>
         <input class="checkBox" type="checkbox" name="ShareInfo" />
         <div class="checkBoxText" >Agree, Share your Info.</div>
        </div>
        <div><input class="inputsumbit" type="submit" value="JOIN"></div>
       </div>
      </form>
     </div>
    </div>
   </div>
   ```

2. Modal을 사용하여 아래와 같이 style 태그를 추가한다.

   ```
   <style>
   		/* Modal_LogIn */
   
   		#modalLayer_Login {
   			display: none;
   			position: relative;
   		}
   
   		#modalLayer_Login .modalLoginContent {
   			position: fixed;
   			z-index: 11;
   			bottom: 38%;
   			left: 40%;
   			border-radius: 8px;
   			box-sizing: border-box;
   			box-shadow: 0 6px 10px 0 rgba(0,0,0,.1);
   			background: #fff;
   			font-size: 1.5rem;
   			color: #262626;
   			overflow: hidden;
   			padding: 45px;
   		}
   
   		#modalLayer_Login .LogIn {
   			width: 100%;
   			text-align: center;
   			font-family: MaisonNeue,sans-serif;
   			font-weight: 900;
   			font-size: 18px;
   			letter-spacing: 1px;
   			color: #262626;
   			padding-bottom: 6px;
   			border-bottom: 1px solid #d8d8d8;
   		}
   
   		#modalLayer_Login .inputType {
   			font-family: MaisonNeue,sans-serif;
   			width: 100%;
   			position: relative;
   			margin-top: 18px;
   			font-size: 14px;
   		}
   
   		#modalLayer_Login .inputsumbit {
   			background: #ef3e28;
   			cursor: pointer;
   			letter-spacing: .4pt;
   			color: #fff;
   			text-align: center;
   			padding: 10px 24px 9px 24px;
   			border: 1px solid #ef3e28;
   			font-family: MaisonNeue,sans-serif;
   			font-weight: 900;
   			font-size: 14px;
   			-webkit-transition: .3s background linear;
   			-moz-transition: .3s background linear;
   			-ms-transition: .3s background linear;
   			-o-transition: .3s background linear;
   			transition: .3s background linear;
   			border-radius: 4px;
   		}
   
   		#modalLayer_Login .divcoment {
   			font-family: Georgia,sans-serif;
   			font-style: italic;
   			text-align: center;
   			margin-top: 24px;
   			margin-left: -2px;
   			width: calc(100% + 4px);
   			font-size: 13px;
   			color: #262626;
   			float: left;
   		}
   
   		#modalLayer_Login .spantype {
   			font-family: Georgia,sans-serif;
   			font-style: italic;
   			text-align: center;
   			margin-top: 24px;
   			margin-left: -2px;
   			width: calc(100% + 4px);
   			font-size: 13px;
   			color: #262626;
   			float: left;
   			cursor: pointer;
   		}
   
   		#modalLayer_Login .checkBoxText {
   			float: left;
   			position: relative;
   			font-size: 12px;
   			font-weight: 900;
   			font-familY: MaisonNeue,sans-serif;
   		}
   
   		#modalLayer_Login .modalLoginContent #close {
   			position: absolute;
   			margin: 6px;
   			right: 0;
   			top: 0;
   			cursor: pointer;
   		}
    
   		/* Modal_Join */
   
   		#modalLayer_Join {
   			display: none;
   			position: relative;
   		}
   
   		#modalLayer_Join .modalJoinContent {
   			position: fixed;
   			z-index: 11;
   			bottom: 38%;
   			left: 42%;
   			border-radius: 8px;
   			box-sizing: border-box;
   			box-shadow: 0 6px 10px 0 rgba(0,0,0,.1);
   			background: #fff;
   			font-size: 1.5rem;
   			color: #262626;
   			overflow: hidden;
   			padding: 45px;
   		}
   
   		#modalLayer_Join .Join {
   			width: 100%;
   			text-align: center;
   			font-family: MaisonNeue,sans-serif;
   			font-weight: 900;
   			font-size: 18px;
   			letter-spacing: 1px;
   			color: #262626;
   			padding-bottom: 6px;
   			border-bottom: 1px solid #d8d8d8;
   		}
   
   		#modalLayer_Join .inputType {
   			font-family: MaisonNeue,sans-serif;
   			width: 100%;
   			position: relative;
   			margin-top: 18px;
   			font-size: 14px;
   		}
   
   		#modalLayer_Join .inputsumbit {
   			background: #ef3e28;
   			cursor: pointer;
   			letter-spacing: .4pt;
   			color: #fff;
   			text-align: center;
   			padding: 10px 24px 9px 24px;
   			border: 1px solid #ef3e28;
   			font-family: MaisonNeue,sans-serif;
   			font-weight: 900;
   			font-size: 14px;
   			-webkit-transition: .3s background linear;
   			-moz-transition: .3s background linear;
   			-ms-transition: .3s background linear;
   			-o-transition: .3s background linear;
   			transition: .3s background linear;
   			border-radius: 4px;
   		}
   
   		#modalLayer_Join .divcoment {
   			font-family: Georgia,sans-serif;
   			font-style: italic;
   			text-align: center;
   			margin-top: 24px;
   			margin-left: -2px;
   			width: calc(100% + 4px);
   			font-size: 13px;
   			color: #262626;
   			float: left;
   		}
   
   		#modalLayer_Join .spantype {
   			font-family: Georgia,sans-serif;
   			font-style: italic;
   			text-align: center;
   			margin-top: 24px;
   			margin-left: -2px;
   			width: calc(100% + 4px);
   			font-size: 13px;
   			color: #262626;
   			float: left;
   			cursor: pointer;
   		}
   
   		#modalLayer_Join .checkBoxText {
   			float: left;
   			position: relative;
   			font-size: 12px;
   			font-weight: 900;
   			font-familY: MaisonNeue,sans-serif;
   		}
   
   		#modalLayer_Join .modalJoinContent #close {
   			position: absolute;
   			margin: 6px;
   			right: 0;
   			top: 0;
   			cursor: pointer;
   		}
   		
   	</style>
   ```

   (UI는 https://www.emusic.com/ 을 참조하였다.)

3. Js파일을 생성하여 버튼에 대한 동작을 지정한다.
   **js파일은 반드시 ejs(html) 코드 상단에 Script로 지정하여 주어야 한다.**

   ```
   /* Login Page  */
       const modalLayer_Login = $("#modalLayer_Login");
       const modalLoginLink = $(".modalLoginLink");
       const modalLoginCont = $(".modalLoginContent");
       const marginLoginLeft = modalLoginCont.outerWidth() / 2;
       const marginLoginTop = modalLoginCont.outerHeight() / 2;
   
       modalLoginLink.click(function () {
           modalLayer_Login.fadeIn("slow");
           modalLoginCont.css({ "margin-top": -marginLoginTop, "margin-left": -marginLoginLeft });
           $(this).blur();
           $(".modalLoginContent > a").focus();
           return false;
       });
   
       $(".modalLoginContent #close").click(function () {
           modalLayer_Login.fadeOut("slow");
           modalLoginLink.focus();
       });
   
   /* Login Page Join Button Event */
       $('#Loing_Join').click(function(){
           modalLayer_Login.fadeOut("slow");
           modalLayer_Join.fadeIn("slow");
       });
       
   /* Join Page */
       const modalLayer_Join = $("#modalLayer_Join");
       const modalJoinLink = $(".modalJoinLink");
       const modalJoinCont = $(".modalJoinContent");
       const marginJoinLeft = modalJoinCont.outerWidth() / 2;
       const marginJoinTop = modalJoinCont.outerHeight() / 2;
   
       modalJoinLink.click(function () {
           modalLayer_Join.fadeIn("slow");
           modalJoinCont.css({ "margin-top": -marginJoinTop, "margin-left": -marginJoinLeft });
           $(this).blur();
           $(".modalJoinContent > a").focus();
           return false;
       });
   
       $(".modalJoinContent #close").click(function () {
           modalLayer_Join.fadeOut("slow");
           modalJoinLink.focus();
       });
   ```

   

## 회원가입(Join) 동작

1. Js에 아래와 같이 동작을 지정한다.

   ```
   /* Join insert */
   
       $('#joinReqID').submit( function(){
           //$('form').submit(function(){
           const email = $("input[name=joinEmail]", document.joinReq).val();
           const name = $("input[name=joinName]", document.joinReq).val();
           const userPaswdd = $("input[name=userPaswdd]", document.joinReq).val();
           const confirmPaswdd = $("input[name=confirmPaswdd]", document.joinReq).val();
   
           const modalLayer_Join = $("#modalLayer_Join");
   
           const contact_params = {
               email,
               name,
               userPaswdd,
           };
   
           if (userPaswdd === confirmPaswdd) {
               $.post('/JoinReq', contact_params, function (data, status) {
                   const data_parse = JSON.parse(data);
                   alert(data_parse.msg);
   
                   $("input[name=joinEmail]", document.joinReq).val("");
                   $("input[name=joinName]", document.joinReq).val("");
                   $("input[name=userPaswdd]", document.joinReq).val("");
                   $("input[name=confirmPaswdd]", document.joinReq).val("");
                                       
               });
               modalLayer_Join.fadeOut("slow");
   
               // 리플레시 없이 form 완료하기 // Prevents the default action of the event
               event.preventDefault();
   
           } else if (userPaswdd != confirmPaswdd) {
               alert("입력하신 비밀번호가 일치하지 않습니다. 다시 입력 바랍니다.");
           }
       });
   ```



## jQuery에서 Form Tag 활용

1. Javascript로 하면.. 더 편할 수도 있지만.. 시도해보았다.

2. 먼저 Form tag에 Name을 'loginReq'라고 지정하였고, 각 Input tag의 name도 지정해 주었다
   (Login_email, login_paswdd)

3. 이제 js파일에 값을 받아노느 코드를 적어보도록 한다.

   ```
   $('form').submit( function () {
   // 해당 페이지에서 form tag의 submit 처리가 발생하면 다음 function을 수행한다.
   
           const loginEmail = $("input[name=login_email]", document.loginReq).val();
           const loginPaswdd = $("input[name=login_paswdd]", document.loginReq).val();
           // Input tag에 지정한 name을 $('input[name=지정한 name]',)으로 작성하고
   				// ',' 뒤에는 document.formID)를 작성한다. 맨 뒤에는 .val()으로 입력값을 받는다!
   
           const send_params = {
               loginEmail,
               loginPaswdd,
           };
   // 출처: https://hivery.tistory.com/20 [하이베리의 소소한 일상])
   ```

4. Form tag submit처리를 수행 할 때.. 해당 페이지의 모든 submit처리에 대해 작업을 수행한다고 하였다.
   이 것에 대해 효율적이지 못하다는 생각이 들어 아래와 같이 수정하였다.

   ```
   $('#loginReqID').submit( function () {
   ```

   tag ID가 loginReqID인 submit작업에 반응 하도록 하였다.
   이렇게 되면 해당 웹페이지에 여러 form tag를 작성했을때 조금더 효율적이지 않을까 생각이 든다.



## Login 동작



```
/* login Try */

    $('#loginReqID').submit( function () {
        const loginEmail = $("input[name=login_email]", document.loginReq).val();
        const loginPaswdd = $("input[name=login_paswdd]", document.loginReq).val();
        // 정보를 보내는 form의 name을 document.뒤에 써주고,
        // form의 input tag의 name을 위와 같이 지정해주면 그곳을 찾는다. 뒤에 .val()은 입력값 받기.

				// 출처: https://hivery.tistory.com/20 [하이베리의 소소한 일상])

        const send_params = {
            loginEmail,
            loginPaswdd,
        };

        $.post("/loginReq", send_params, function(data, status) {
            const data_parse = JSON.parse(data);
            alert(data_parse.msg);
        });
        event.preventDefault();
        window.location.reload(true);
        });
        
        
/* Logout */
        $('#logout_btn').click(function () {
            $.get("/logout", function (data, status) {
                alert("로그아웃 되었습니다.");
                location.reload();
            });
        });
```



## Login, Join CSS 수정

1. Login, Join 팝업 창을 위해 modal을 사용했었다.
   class를 설정해준 김에 사용하여 css를 수정하도록 하였다.

2. nav - li tag안의 'modalLoginLink'과 'modalJoinLink' class명을 설정한 tag의 배경색과 글자색을 변경! 

   ```
   #nav li .modalLoginLink, #nav li .modalJoinLink {
   			background-color: rgba(255, 0, 0, 0.541);
   			color: black;
   		}
   ```

3. hover 기능 또한 주어서 다른 버튼과 다르게 보이도록 해본다.
   위에서 설정한 tag에 :hover를 추가하여 마우스 오버상태 일 때 변경될 배경색상과 글자색을 지정한다.
   (2,3번 두 개 다 추가하는 것!)

   ```
   #nav li .modalLoginLink:hover, #nav li .modalJoinLink:hover {
   			background-color: rgb(96, 192, 139);
   			color: #3C5A98;
   		}
   ```



## Search Button 추가

1. Button을 먼저 추가!

   ```
   <button class="SearchButton" type="submit">
   	<i class="fa fa-search"></i>
   </button>
   ```

   - Button Tag를 추가하고 Class, type 입력
   - Button Tag안에 i Tag 추가. (icon을 가져오기 위함)
     i Tag의 class를 위와 같이 준다.

   *당장은 설정한 class의 css가 적용되지 않으니 아래 내용을 수행하도록 한다.

2. 해당 버튼이 생성되는 html(또는 ejs)에 Link주소를 입력한다.

   ```
   <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
   ```

   - 위 링크는 icon을 가져오기 위한 링크.

3. 이번엔 버튼의 크기와 색상, icon의 크기와 색상을 입힌다.

   ```
   #Search .SearchButton {
   			background-color: #c0cadf;
   			border: none;
   			color: black;
   			padding: 10px 10px;
   			font-size: 8px;
   			cursor: pointer;
   			float: right;
   	}
   ```

   - Style이나 css파일에 추가하도록 한다.
     필자는 Search id를 가진 tag안에 SearchButton이라는 class명을 가진 버튼이다.

   


