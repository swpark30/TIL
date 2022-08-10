### Canvas 태그

> html5가 발표되고 canvas기능이 추가되면서 자바스크립트만으로 이러한 것들이 가능하게 되고 곡선 그리기, 그라데이션을 이용한 색지정, 간단한 애니메이션 효과 등등 표현할 수 있는 범위가 한층 더 넓어지게 되었다.
> 
> 각종 웹브라우저에서는 물론이거니와 (Iu는 버전 9 이상부터) 특히 스마트폰의 게임이나 앱 제작에 좀 더 시각적인 효과를 줄 수가 있게 되어 일반 유저들에게 더 많은 즐거움을 줄 수가 있게 되었다.
> 
> 캔버스란 한 마디로 스크립트를 사용해서 그래프, 도형, 이미지들을 그릴 수 있는 html5의 요소로 이해하면 된다.

##### 기본적인 사용법

1. HTML 페이지 내의 원하는 곳에 < canvas> 태그 위치시키기

2. Javascript를 이용해서 캔버스 요소 즉 오브젝트를 생성하기

3. 드로잉 할 컨텍스트를 가져와서 생성하기

4. 컨텍스트의 속성 및 함수를 이용해서 실질적으로 드로잉 하기
   
   - 탬플릿 코드
     
     ```html
     <!DOCTYPE html>
     <html>
     <head>
         <meta charset="UTF-8">
         <title>캔버스 튜토리얼</title>
     </head>
     <body>
         <!-- 1. 캔버스 태그 삽입 -->
         <canvas id="p-canvas" width="300" height="300"></canvas>
         <script>
             // 2. 캔버스요소 가져오기        
             var ele_canvas = document.getElementById("p-canvas");
             // 3. 드로잉용 컨텍스트 생성        
             var context_canvas = ele_canvas.getContext("2d");
             // 4. 생성한 컨텍스트를 이용해서 드로잉하기
             context_canvas.fillStyle = "#cc0000"; // 색상
             context_canvas.fillRect(0, 0, 300, 300); // 도형
         </script>
     </body>
     </html>
     ```

##### 선과 면!

- 도형을 드로잉 할 때 우리는 좀 더 디테일하게 표현을 하고 싶어 질 때가 있는데 그럴 경우에는 아래와 같은 속성들을 사용해서 표현을 하면 된다.
  
  | strokeStyle    | 선색                                     |
  |:--------------:|:--------------------------------------:|
  | **lineWidth**  | **선의 굵기**                              |
  | **lineCap**    | **선의 끝부분의 모양 형태**                      |
  | **lineJoin**   | **선의 연결 형태**                           |
  | **miterLimit** | **lineJoin의 값이 miter의 경우 연결되는 부분의 길이** |
  | **fillStyle**  | **면색**                                 |
  
  - 예제 코드
    
    ```html
    <!DOCTYPE html>
    <html>
    <head>
        <meta charset="UTF-8">
       <title>캔버스 튜토리얼2</title>
    </head>
    <body>
        <!-- 1. 캔버스 태그 삽입 -->
        <canvas id="p-canvas" width="300" height="300"></canvas>
        <script>
            // 2. 캔버스요소 가져오기        
            var ele_canvas = document.getElementById("p-canvas");
            // 3. 드로잉용 컨텍스트 생성        
            var context_canvas = ele_canvas.getContext("2d");
            // 4. 생성한 컨텍스트를 이용해서 드로잉하기
            context_canvas.strokeStyle = "red"; // border(선)색
            context_canvas.lineWidth = "20";
            context_canvas.fillStyle = "#c1c1c1"; // 면색상
    
            //드로잉        
            context_canvas.rect(20, 20, 200, 200); // 도형
            context_canvas.stroke(); // 선        
            context_canvas.fill(); // 면색        
        </script>
    </body>
    </html>
    ```
    
    - 선과 면색의 값을 지정한 후에 실제로 캔버스에 ( 웹상에 보여질 ) 도형과 선, 그리고 면을 드로잉해 주는 내용이다. strokeStyle에서 선색을, lineWidth에서 선의 굵기를, fillStyle에서 면색을 지정해 주었다.
    
    - 템플릿과 다른점 : 템플릿은 fillRect함수를 사용했는데 예제에서는 Rect함수 사용(Rect는 사각형안에 색이 채워지지 않음)
    
    - Rect함수는 stroke함수가 실행되어졌을 때 선이 그려지고 fill함수가 실행되어졌을 때에 면색이 채워지면서 비로소 원하는 형태의 드로잉이 되어진다.
