# Random-Color
Javascript를 사용해 랜덤 컬러 프로그램 만들기

![image](https://github.com/leeyongha2006/Random-Color/assets/126844590/f344730f-cb3d-4dbf-b649-8a39c15459eb)
### 박스를 클릭하면 해당 색이 클립보드에 복사되고 새로고침 박스를 누르면 랜덤 색들로 변하는 프로그램이다

## js
```javascript
window.onload = function () {
    addColor(); // 페이지 로딩 완료 시 색상 추가 함수 실행 (Call addColor function on page load)
  };
  
  for (let i = 1; i <= 9; i++) {
    const box = document.createElement('div');
    box.classList.add('box'); // 클래스 'box' 추가 (Add class 'box')
    document.querySelector('.container').appendChild(box); // 컨테이너 요소에 박스 추가 (Append box to container element)
    box.style.cursor = 'pointer'; // 커서 모양을 포인터로 설정 (Set cursor style to pointer)
  
    box.addEventListener('click', () => {
      console.log(box.innerHTML); // 박스 내용 로그 출력 (Log box content)
      navigator.clipboard.writeText(box.innerHTML); // 클립보드에 박스 내용 복사 (Copy box content to clipboard)
      console.log("copied"); // "copied" 메시지 로그 출력 (Log "copied" message)
      toastr.success('이제 사용할 수 있습니다!', '클립보드에 복사됨', { timeOut: 3000 }); // toastr 라이브러리 사용하여 성공 메시지 표시 (Use toastr library to display success message)
    });
  }
  
  const btn = document.querySelector('.btn'); // 버튼 요소 찾기 (Find button element)
  const randomColorBlock = document.querySelectorAll('.box'); // 모든 .box 클래스 요소 찾기 (Find all elements with class .box)
  
  function RandomHexColorCode () {
    var chars = '0123456789abcdef';
    var colorLength = 6;
    var color = '';
  
    for (var i = 0; i < colorLength; i++) {
      var randomColor = Math.floor(Math.random() * chars.length);
      color += chars.substring(randomColor, randomColor + 1);
    }
    return '#' + color;
  }
  
  function addColor () {
    randomColorBlock.forEach(e => {
      var newColor = RandomHexColorCode();
      e.style.backgroundColor = newColor; // 배경 색상 설정 (Set background color)
      e.innerHTML = newColor; // 박스 내용 설정 (Set box content)
    });
  }
```

## css
```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  
  body {
    font-family: "sans";
    color: black;
    background-color: #19172e;
  }
  
  @font-face {
    src: url("font/sans.ttf");
    font-family: "sans";
  }
  
  .heading {
    color: white;
    padding-top: 10px;
    justify-content: center;
    text-align: center;
    font-size: 2rem;
  }
  
  .btn {
    background: #333;
    color: white;
    padding: 15px 60px;
    font-size: 1.5rem;
    margin: 20px auto;
    display: block;
    cursor: pointer;
    border-radius: 5px;
    border: none;
  }
  
  .btn:hover {
    background-color: #1e8e3e;
    color: white;
  }
  
  .item {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
  }
  
  .copy {
    color: white;
    padding: 15px 20px;
    font-size: 1.5rem;
    margin: 20px auto;
    background: #333;
    cursor: not-allowed ;
    border-radius: 5px;
    border: none;
    user-select: none;
  }
  
  
  .container {
    display: flex;
    flex-wrap: wrap;
  }
  
  .box {
    width: 33.3%;
    height: 150px;
    display: flex;
    justify-content: center;
    align-items: center;
    background: #19172e;
    border: 2px solid #19172e;
    border-radius: 8px;
    font-size: 1.5rem;
  }
  
  .body {
    display: flex;
    flex-direction: column;
  }
  @media (max-width: 500px) {
    .box {
      font-size: 0.8rem;
    }
  }
  @media (max-width: 450px) {
    .item {
      flex-direction: column;
    }
    .copy {
      margin-left: 0px;
      width: 100%;
    }
  }
  
  @media (max-width: 450px) {
    .copy {
      width: 100%;
    }
  }
  
  @media (max-width: 300px) {
    .copy {
      padding: 5px;
      width: fit-content;
      text-align: center;
    }
    .btn {
      padding: 5px;
    }
  }
```
## index.html
```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta http-equiv="X-UA-Compatible" content="IE=edge" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<title>Random Color Generator</title>
		<link rel="stylesheet" href="css/style.css" />
		<link rel="shortcut icon" href="assets/wheel.png" type="image/x-icon" />
		<link
			rel="stylesheet"
			href="https://cdnjs.cloudflare.com/ajax/libs/toastr.js/latest/css/toastr.min.css"
		/>
		<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
		<script src="https://cdnjs.cloudflare.com/ajax/libs/toastr.js/latest/js/toastr.min.js"></script>
	</head>
	<body>
		<h2 class="heading">Random Color Generator</h2>

		<div class="body">
			<div class="item">
				<button class="btn" onclick="addColor();">Refresh</button>
				<div class="copy">Click on any box below to copy the code.</div>
			</div>
			<div class="cont">
				<section class="container"></section>
			</div>
		</div>
		<br /><br />


		<script src="script/main.js"></script>
	</body>
</html>
```
