### Search Button 추가

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

4. 버튼 추가 끝!

### jQuery에서 Form Tag 활용하기

1. Javascript로 그냥 하는것이 더 편할 수도 있지만.. 시도해보았다.

2. 먼저 Form tag에 Name을 'loginReq'라고 지정하였고, 각 Input tag의 name도 지정해 주었다
   (Login_email, login_paswdd, RemeID)

3. 이제 js파일에 값을 받아노느 코드를 적어보도록 한다.

   ```
   $('form').submit( function () {
   // 해당 페이지에서 form tag의 submit 처리가 발생하면 다음 function을 수행한다.
   
           const loginEmail = $("input[name=login_email]", document.loginReq).val();
           const loginPaswdd = $("input[name=login_paswdd]", document.loginReq).val();
           const RememID = $("input[name=RememID]", document.loginReq).val();
   
           const send_params = {
               loginEmail,
               loginPaswdd,
               RememID,
           };
   // 정보를 보내는 form의 name을 document.뒤에 써주고, form의 input tag의 name을 위와 같이 지정해주면 그곳을 찾는다. 뒤에 .val()은 입력값 받기.
   // 출처: https://hivery.tistory.com/20 [하이베리의 소소한 일상])
   ```

4. Form tag submit처리를 수행 할 때.. 해당 페이지의 모든 submit처리에 대해 작업을 수행한다고 하였다.
   이 것에 대해 효율적이지 못하다는 생각이 들어 아래와 같이 수정하였다.

   ```
   $('#loginReqID').submit( function () {
   ```

   tag ID가 loginReqID인 submit작업에 반응 하도록 하였다.
   이렇게 되면 해당 웹페이지에 여러 form tag를 작성했을때 조금더 효율적이지 않을까 생각이 든다.

5. 



