---
title: 위키 작성 템플릿
description: 위키의 템플릿들을 저장하는곳입니다.
published: true
date: 2023-07-13T07:47:37.928Z
tags: 
editor: markdown
dateCreated: 2023-07-10T14:03:27.543Z
---

# Header
한국어 Here


## 예제 1

- OOTB 모듈을 활용한 Object 및 Property 로드

```js
let obj = clientDataModel.getObject(uid); // uid를 이용해 ModelObject를 가져옴.

clientDataModel.getProperty(obj , "object_name"); // ModelObject가 가지고 있는 속성.

console.log(obj);
``` 

## 예제 2 

Tempermonkey에 미리 정의한 함수 활용

```js
let obj = getObj(uid); // arr 지원

getProps(uids , props); // uid arr 와 obj arr 지원

console.log(obj);
```

## 베지어 곡선

<br></br>

<canvas id="Canvas1" width="600" height="400" style="border: 1px solid black; border-radius:5px;">
  
</canvas>
<script>
  var cv = document.getElementById("Canvas1");
  var ctx = cv.getContext("2d");
  function gradient(a, b) {
        return (b.y-a.y)/(b.x-a.x);
    }
          
    function bzCurve(points, f, t) {
        if (typeof(f) == 'undefined') f = 0.3;
        if (typeof(t) == 'undefined') t = 0.6;
      
        ctx.beginPath();
        ctx.moveTo(points[0].x, points[0].y);
      
        var m = 0;
        var dx1 = 0;
        var dy1 = 0;
          
        var preP = points[0];
          
        for (var i = 1; i < points.length; i++) {
            var curP = points[i];
            nexP = points[i + 1];
            if (nexP) {
                m = gradient(preP, nexP);
                dx2 = (nexP.x - curP.x) * -f;
                dy2 = dx2 * m * t;
            } else {
                dx2 = 0;
                dy2 = 0;
            }
              
            ctx.bezierCurveTo(
                preP.x - dx1, preP.y - dy1,
                curP.x + dx2, curP.y + dy2,
                curP.x, curP.y
            );
          
            dx1 = dx2;
            dy1 = dy2;
            preP = curP;
        }
        ctx.stroke();
    }
      
    // Generate random data
    var lines = [];    
    var X = 10;
    var t = 40; // control the width of X.
    for (var i = 0; i < 100; i++ ) {
        Y = Math.floor((Math.random() * 300) + 50);
        p = { x: X, y: Y };
        lines.push(p);
        X = X + t;
    }
      
    // Draw smooth line
    ctx.setLineDash([0]);
    ctx.lineWidth = 2;
    ctx.strokeStyle = "green";
    bzCurve(lines, 0.3, 1);
  
  console.log("VV!");
</script>