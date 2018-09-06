# HTML, CSS, Javascript�� �и��� �� ������ �����
## 1. HTML �±׷� ������ ������ ���� �����
```{.html}
<!DOCTYPE html>
<html>
<head>
<title>�� �������� ���� ���</title>
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
## 2. CSS �ڵ�� ���� ��� �����
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
## 3. Javascript �ڵ�� ����� �������̽� ó��
```{.html}
<script>
	function show() { // <img>�� �̹��� �ޱ�
		document.getElementById("fig").src = "ElvisPresley.png"
	}
	function hide() { // <img>�� �̹��� ����
		document.getElementById("fig").src= "";
	}
</script>
```
##4. h3�� �̺�Ʈ �߰�, img��ºκ� ����
```{.html}
<h3 onmouseover="show()" onmouseout="hide()"> Elvis Presley</h3>
<div><img id="fig" src=""></div>
```

