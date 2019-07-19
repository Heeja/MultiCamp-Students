#### each문(forEach)

* 이렇게

  ```
  var array = [
          {name: 'hanbit', link: 'http://hanb.co.kr'},
          {name: 'daum', link: 'http://daum.net'},
          {name: 'naver', link: 'http://naver.com'}      
          ]
  
          $.each(array, function(index, item){
          var output = '';
          output += '<a href="' + item.link +'">';
          output += '     <h1>' + item.name +'</h1>';
          output += '</a>';
          document.body.innerHTML += output;
          });
  ```

  출처: https://gakari.tistory.com/entry/Jquery-each-메소드-사용법 [가카리의 공부방]

