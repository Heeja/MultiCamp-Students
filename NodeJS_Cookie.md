### Parse는 경직된 객체...

```
var cookies = {};
if(request.headers.cookie !== undefined){
	cookies = cookie.parse(request.headers.cookie);
}
```

* Parse할 값이 undefind이면 Parse 객체는 처리하지 않고 내려 놓는다. => Error 발생하게 된다!
  그래서 Parse할 값이 undefind인지 아닌지 구분해 줄 필요가 있다.