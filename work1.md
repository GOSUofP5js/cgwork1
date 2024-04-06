# 지형 만들기 및 작품

#### 20171111 김종준

Code
--
```
let cols, rows;
let scl = 20;
let w = 1400;
let h = 1000;

let flying = 0;
let angle = 0;

let terrain = [];

function setup() {
  createCanvas(600, 600, WEBGL);
  cols = w / scl;
  rows = h / scl;

  for (let x = 0; x < cols; x++) {
    terrain[x] = [];
    for (let y = 0; y < rows; y++) {
      terrain[x][y] = 0; //specify a default value for now
    }
  }
   noStroke();
}

function draw() {

  flying -= 0.1;
  let yoff = flying;
  for (let y = 0; y < rows; y++) {
    var xoff = 0;
    for (let x = 0; x < cols; x++) {
      terrain[x][y] = map(noise(xoff, yoff), 0, 1, -100, 100);
      xoff += 0.2;
    }
    yoff += 0.2;
  }
  background(0, 128, 255);
  rotateX(PI / 3);
  fill(164, 164, 164, 196);
  translate(-w / 2, -h / 2);
  for (let y = 0; y < rows - 1; y++) {
    beginShape(TRIANGLE_STRIP);
    for (let x = 0; x < cols; x++) {
      let v = terrain[x][y];
      fill(v+128, 10, 300, v+150);
      vertex(x * scl, y * scl, terrain[x][y]);
      vertex(x * scl, (y + 1) * scl, terrain[x][y + 1]);
      }
      endShape();
  }
  push(); 
  translate(w / 2, h / 2);
  translate(mouseX - width / 2, (mouseY - height / 2) * 6);
  rotate(PI / 5);    
  normalMaterial(); // 지형의 색상을 바꾼다. 재질을 바꾸고, 조명
  fill(139, 69, 19);
  box(150, 50, 200);
  
  // 배 모양 그리기
  drawBoat();
}

function drawBoat() {
  push(); // 현재 변환 상태 저장
  rotateX(0); // X축 기준으로 회전
  rotateY(180); // Y축 기준으로 회전
  rotateZ(90); // Z축 기준으로 회전
  // 아랫부분 좁은 몸체
  fill(139, 0, 19); // 갈색
  translate(0, 100, 0); // 몸체 위치 설정
  box(200, 50, 100); // 박스 모양의 배를 그림
  
  // 윗부분 넓은 몸체
  fill(109, 39, 19); // 갈색
  rotateY(30);
  translate(0, -75, 0); // 몸체 위치 조정
  box(250, 100, 150); // 박스 모양의 배를 그림
  
  // 돛을 올리기 위한 대
  fill(184, 134, 11); // 연한 갈색
  translate(0, -100, 0);
  cylinder(5, 400); // 원기둥 모양의 돛을 그림
  
  // 돛
  fill(255); // 흰색
  translate(0, -100, 0); // 돛의 위치 조정
  rotateX(HALF_PI); // X축 기준으로 90도 회전
  rotateY(HALF_PI);
  beginShape();
  vertex(-100, 0, 0); // 삼각형의 꼭지점 1
  vertex(100, 0, 0); // 삼각형의 꼭지점 2
  vertex(0, -150, 0); // 삼각형의 꼭지점 3
  endShape(CLOSE);
  
  pop(); // 변환 상태 복원
}
```
result
---
<img width="40%" src="https://github.com/GOSUofP5js/cgwork1/assets/164286458/59440fb7-165e-4c7f-838d-dda304910bc1"/>

소감문
---

p5.js를 사용하여 지형을 만든다는 행위 자체가 참 색다른 경험이었습니다. 그리고, 코드를 통해 형태를 만들어내는 과정에서 창의력을 발휘할 수 있었고, 시각적인 표현을 통해 예술적인 즐거움을 느낄 수 있었습니다. 또한, 3D 도면을 생성함으로써 구조를 더 잘 이해할 수 있었습니다. 이러한 프로젝트를 통해 코딩과 미술이 접목된 창의적인 활동이 너무 즐거워 졌습니다. 앞으로 다가올 새로운 지식 또한, 너무 기다려지고 궁금합니다. 반면에, p5.js로 이런 디테일 적이고 크게 느껴지는 지형이나 여러가지 활동들을 할수 있다는걸 깨달았습니다. 단순한 웹 에디터라고 생각한 제 자신이 한없이 작아지는 느낌입니다. 포토샵이나 애프터 이펙트 처럼 직접적인 편집이나 제작이 아닌 코드로 제작하는게 아직 적응하기 어렵고 미숙하지만 더욱더 증진하여 좋은 결과 보여드리겠습니다.

