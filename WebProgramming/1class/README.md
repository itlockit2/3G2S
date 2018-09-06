# HTML, CSS, Javascript로 분리된 웹 페이지 만들기
## 1. HTML 태그로 문서의 구조와 내용 만들기
```{.html}
<!DOCTYPE html>
<html>
<head>
<title>웹 페이지의 구성 요소</title>
</head>
<body>
<h3>Elvis Presley</h3>
<hr>
He was an American singer and actor. In November
1956, he made his film debut in <span>Love Me 
Tender</span>. He is often referred to as 
"<span>the King of Rock and Roll</span>".
</body>
</html>
```
## 2. CSS 코드로 문서 모양 만들기
```{.html}
<style>
	body { background-color : linen; 
	color : green;
	margin-left : 40px; 
	margin-right : 40px;
	}
	h3 { text-align : center; 
	color : darkred;
	}
	hr { height : 5px;
	border : solid grey; 
	background-color : grey 
	}
	span { color: blue; 
	font-size: 20px; 
	}
</style>
```
## 3. Javascript 코드로 사용자 인터페이스 처리
```{.html}
<script>
	function show() { // <img>에 이미지 달기
		document.getElementById("fig").src = "ElvisPresley.png"
	}
	function hide() { // <img>에 이미지 제거
		document.getElementById("fig").src= "";
	}
</script>
```
##4. h3에 이벤트 추가, img출력부분 설정
```{.html}
<h3 onmouseover="show()" onmouseout="hide()"> Elvis Presley</h3>
<div><img id="fig" src=""></div>
```

