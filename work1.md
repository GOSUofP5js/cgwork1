# 지형 만들기 및 작품

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

