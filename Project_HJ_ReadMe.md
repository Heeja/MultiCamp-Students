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