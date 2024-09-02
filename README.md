<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>08-26 인터랙션 애니메이션 종류 실습</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
        }

        .container {
            width: 100%;
            height: 100%;
            display: flex;
            justify-content: space-around;
            align-items: center;
            background-color: skyblue;
            flex-wrap: wrap;
        }

        .item {
            width: 200px;
            height: 200px;
            background-color: gray;
            color: white;
            font-size: 72px;
            text-align: center;
            line-height: 200px;
            cursor: pointer;
        }

        .desc {
            border-radius: 10px;
            padding: 10px 20px;
            width: 300px;
            height: 150px;
            background-color: lightgray;
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: Noto Sans KR;
            font-size: 20px;
        }
    </style>
</head>
<body>
    <!--오브젝트-->
    <div class="container top">
        <div class="item item1">1</div>
        <div class="item item2">2</div>
        <div class="item item3">3</div>
        <div class="item item4">4</div>
    </div>

    <!--오브젝트 설명글-->
    <div class="container description">
        <div class="desc item1">스타일 속성을이용해 속성을 이용한 애니메이션</div>
        <div class="desc item2">requestAnimationFrame메서드</div>
        <div class="desc item3">addEventlistener를 이용한 mouseevent</div>
        <div class="desc item4">requestanimationframe메서드와 addeventlistener메서드를 사용</div>
    </div>

    <!--애니메이션 설정-->
    <script>
        "use strict"; // 엄격 모드; 자바 스크립트에서 오류가 났을 때 콘솔에 띄워줌

        const item1 = document.querySelector('.item1');
        const item2 = document.querySelector('.item2');
        const item3 = document.querySelector('.item3');
        const item4 = document.querySelector('.item4');

        // :::::::::::첫 번째 사각형:::::::::::
        // 스타일 속성값 변경 => 엘리먼트의 인라인스타일을 변경
        window.addEventListener('load', function() {
            item1.style.rotate = '360deg'; //deg 반드시 붙여써야함
            item1.style.transition = '10s';
            // => 자바스크립트를 통해 style을 바꿀 경우
            // 스타일 속성이 body의 <>내부에 인라인 형태로 들어가게 된다
        });

        // :::::::::::두 번째 사각형:::::::::::
        // requestAnimationFrame 이용
        let rotate = 0; // 변수는 바깥쪽에서 선언해둔다
        function item2Rotate() {
            item2.style.transform = `rotate(${rotate}deg)`;
            rotate += 1; // 반복 실행할 때마다 rotate값이 커진다
            requestAnimationFrame(item2Rotate); // 인수를 함수명으로 넣어주면 순환한다(반복실행)
        }
        item2Rotate() // 함수 만들고 이렇게 호출까지 해야 실행이 된다

        // :::::::::::세 번째 사각형:::::::::::
        // addEventListener메서드 사용, click 이벤트
        // 1번 클릭할 때마다 90도씩 회전하는 함수를 만들어 회전시키는 방식
        // 회전하는 각도 숫자, 회전하는 속도(초) 조절 가능하다!
        let rotate3 = 0; // 변수 선언
        item3.addEventListener('click', function() {
            rotate3 += 90; // 클릭을 인식했을 때 회전값을 90만큼 추가한다
            item3.style.transform = `rotate(${rotate3}deg)`;
            item3.style.transition = '5s';
        });

        // MDN Event에 가면 이벤트 리스너에서 사용할 수 있는 이벤트 리스트들이 나온다.


        //:::::::::::네 번째 사각형:::::::::::
        // requestAnimationFrame과 addEventListner 메서드 사용
        // 마우스오버시 회전시키는 함수를 실행시키고(함수 내에서 requestAnimationFrame 호출)
        // 마우스가 떠나면 requestAnimationFrame 실행을 멈춘다.
        let rotate4 = 0;
        let item4Req; // requestAnimationFrame을 이용해 회전시키다 멈추기 위해 변수선언
        
        // 마우스오버 인식해서 회전 함수 호출하는 함수
        item4.addEventListener('mouseover', function() {
            item4Rotate();
        });
        // 마우스 떠나면 회전 멈추게 하는 함수
        item4.addEventListener('mouseleave', function() {
            cancelAnimationFrame(item4Req)
        });

        // box 회전시키는 함수
        function item4Rotate() {
            rotate4 += 1;
            item4.style.transform = `rotate(${rotate4}deg)`;
            item4Req = requestAnimationFrame(item4Rotate)
        }

    </script>
</body>
</html>
