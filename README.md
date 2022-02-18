# AbdulSama123.github.iovar canvas = document.getElementById("cl");
var ctx = canvas.getContext("2d");
var mas=[];
var count=0;
var stop=0;
var population = 0;
var stop = 0;
ctx.fillStyle = "dark blue";

function level1() {
  mas[14][4] = 1;
  mas[16][4] = 1;
  level = 1;
  population = 2;
  document.getElementById('popul').innerHTML = population;
  document.getElementById('info').innerHTML =
    'Размер популяции должен быть равен 3 к 10 поколению. Надо поставить 1 точку';
  drawField();
}

function level2 (){
  mas[15][14] = 1;
  mas[15][15] = 1;
  level = 2;
  population = 2;
  document.getElementById('popul').innerHTML = population;
  document.getElementById('info').innerHTML =
    'Размер популяции должен быть равен 4 к 10 поколению. Надо поставить 1 точку.';
  drawField();
}
function level3 (){
  mas[4][4] = 1;
  mas[5][4] = 1;
  mas[25][4] = 1;
  mas[25][5] = 1;
  mas[4][24] = 1;
  mas[4][25] = 1;
  mas[24][25] = 1;
  mas[25][25] = 1;
  level = 3;
  population = 8;
  document.getElementById('popul').innerHTML = population;
  document.getElementById('info').innerHTML =
    'Размер популяции должен быть равен 16 к 10 поколению. Надо поставить 4 точки.';
  drawField();
}
function level4 (){
  level = 4;
  population = 0;
  document.getElementById('popul').innerHTML = population;
  document.getElementById('info').innerHTML =
    'Размер популяции должен быть равен 3 к 10 поколению. Надо поставить 10 точек.';
  drawField();
}
function level5 (){
  mas[14][14] = 1;
  mas[14][15] = 1;
  mas[15][14] = 1;
  mas[15][15] = 1;
  level = 5;
  population = 4;
  document.getElementById('popul').innerHTML = population;
  document.getElementById('info').innerHTML =
    'Размер популяции должен быть равен 0 к 5 поколению. Надо поставить 1 точку.';
  drawField();
}

function level6 (){
  mas[14][14] = 1;
  mas[14][13] = 1;
  mas[13][14] = 1;
  mas[13][13] = 1;
  level = 6;
  population = 10;
  document.getElementById('popul').innerHTML = population;
  document.getElementById('info').innerHTML =
    'Размер популяции должен быть равен 0 к 7 поколению. Надо поставить 2 точку.';
  drawField();
}

canvas.onclick = function(event) {
  var x = event.offsetX;
  var y = event.offsetY;
  console.log(x);
  console.log(y);
  x = Math.floor(x/10);
  y = Math.floor(y/10);
  mas[y][x]=1;
  console.log(mas);
  drawField();
}

function goLife() {
  var n = 30,
    m = 30;
  for (var i = 0; i < m; i++) {
    mas[i] = [];
    for (var j = 0; j < n; j++) {
      mas[i][j] = [0];
    }
  }
}
goLife();
function stopLife() {
  stop = 1;
  //console.log(stop);
}

function clearField() {
  ctx.clearRect(0, 0, 300, 300);
  for (var i = 0; i < 30; i++) {
    for (var j = 0; j < 30; j++) {
      mas[i][j] = [0];
    }
  }
  count = 0;
  document.getElementById('count').innerHTML = count;
  stop = 0;
  population = 0;
  document.getElementById('popul').innerHTML = population;
  document.getElementById('info').innerHTML = 'EMPTY';
}



function drawField() {
  ctx.clearRect(0, 0, 300, 300);

  for (var i = 0; i < 30; i++) {
    for (var j = 0; j < 30; j++) {
      if (mas[i][j] == 1) {
        ctx.fillRect(j * 10, i * 10, 10, 10);
      }
    }
  }
}

function startLife() {
  var mas2 = [];
  //console.log(mas);
  for (var i = 0; i < 30; i++) {
    mas2[i] = [];

    for (var j = 0; j < 30; j++) {
      var neighbors = 0;
      if (mas[fpm(i) - 1][j] == 1) neighbors++;
      if (mas[i][fpp(j) + 1] == 1) neighbors++;
      if (mas[fpp(i) + 1][j] == 1) neighbors++;
      if (mas[i][fpm(j) - 1] == 1) neighbors++;
      if (mas[fpm(i) - 1][fpp(j) + 1] == 1) neighbors++;
      if (mas[fpp(i) + 1][fpp(j) + 1] == 1) neighbors++;
      if (mas[fpp(i) + 1][fpm(j) - 1] == 1) neighbors++;
      if (mas[fpm(i) - 1][fpm(j) - 1] == 1) neighbors++;
     
      if (mas[i][j] ==1 && neighbors < 2) mas2[i][j] = 0;
      if (mas[i][j] ==1 && neighbors > 3) mas2[i][j] = 0;
      if (mas[i][j] ==1 && neighbors ==2 || neighbors ==3) mas2[i][j] =1;
      if (mas[i][j] ==0 && neighbors ==3) mas2[i][j] = 1;
    }
  }
  mas = mas2;
  drawField();
  count_population();
  count++;
  if ((level == 1)) {
    check1level();
  }
  if ((level == 2)) {
    check2level();
  }
  if ((level == 3)) {
    check3level();
  }
  if ((level == 4)) {
    check4level();
  }
  if ((level == 5)) {
    check5level();
  }
  if ((level == 6)) {
    check6level();
  }
  document.getElementById('count').innerHTML = count;
  document.getElementById('popul').innerHTML = population;
  if (stop == 0) timer = setTimeout(startLife, 700);
}
function fpm(i) {
  if(i==0) return 30;
  else return i;
}
 function fpp(i) {
   if(i==29) return -1;
   else return i;
 }

function count_population() {
  population=0;
  for (var i = 0; i < 30; i++) {
    for (var j = 0; j < 30; j++) {
      if (mas[i][j] == 1) {
        population++;
      }
    }
  }
  console.log(population);
}

function check1level() {
  
  if (count == 10 && population == 3) {
    stopLife();
    document.getElementById('info').innerHTML = 'You score!';
  } else if (count > 10 && population != 3) {
    stopLife();
    document.getElementById('info').innerHTML = 'Didn’t work, Try again';
  }
}

function check2level() {

  if (count == 10 && population == 4) {
    stopLife();
    document.getElementById('info').innerHTML = 'You score!';
  } else if (count > 10 && population != 4) {
    stopLife();
    document.getElementById('info').innerHTML = 'Didn’t work, Try again';
  }
}

function check3level() {

  if (count == 10 && population == 16) {
    stopLife();
    document.getElementById('info').innerHTML = 'You score!';
  } else if (count > 10 && population != 16) {
    stopLife();
    document.getElementById('info').innerHTML = 'Didn’t work, Try again';
  }
}

function check4level() {

  if (count == 10 && population >= 3) {
    stopLife();
    document.getElementById('info').innerHTML = 'You score!';
  } else if (count > 10 && population <= 3) {
    stopLife();
    document.getElementById('info').innerHTML = 'Didn’t work, Try again';
  }
}

function check5level() {

  if (count == 5 && population == 0) {
    stopLife();
    document.getElementById('info').innerHTML = 'You score!';
  } else if (count > 5 && population != 0) {
    stopLife();
    document.getElementById('info').innerHTML = 'Didn’t work, Try again';
  }
}


 document.getElementById('start').onclick = startLife;
 document.getElementById('level1').onclick = level1;
 document.getElementById('level2').onclick = level2;
 document.getElementById('level3').onclick = level3;
 document.getElementById('level4').onclick = level4;
 document.getElementById('level5').onclick = level5;
 document.getElementById('level6').onclick = level6;
 document.getElementById('stop').onclick = stopLife;
 document.getElementById('clearF').onclick = clearField;

#cl  {
  width: 300px;
  height: 300px;
  border: 3px solid black;
  margin: 40px;
  background-image: url(https://static.wikia.nocookie.net/jjba/images/a/a7/StairwayToHeavenWSJ.jpg/revision/latest/scale-to-width-down/590?cb=20170929045120);
}

.Navigation li 	{
	height: auto;
	width: 87px;
	float: left;
	text-align: center;
	list-style: none;
	font:12px "Bonveno", "Century Gothic";
	padding: 0;
	margin: 0;
	background-color: rgb(247, 242, 0);
	border: 1px solid rgb(189, 29, 29);
	box-shadow: 0 1px 0 rgba(255,255,255, .9) inset, 0 1px 3px rgba(0,0,0, .1);
	border-radius: 3px;
  margin-left:10px;
}

nav {
  margin: 27px auto 0;
  position: relative;
  width: 800px;
  height: 50px;
  background-color: #345e42;
  border-radius: 8px;
  font-size: 0;
}
nav a {
  line-height: 50px;
  height: 100%;
  font-size: 15px;
  display: inline-block;
  position: relative;
  z-index: 1;
  text-decoration: none;
  text-transform: uppercase;
  text-align: center;
  color: white;
  cursor: pointer;
}
nav .animation {
  position: absolute;
  height: 100%;
  top: 0;
  z-index: 0;
  transition: all .5s ease 0s;
  border-radius: 8px;
}
a:nth-child(1) {
  width: 100px;
}
a:nth-child(2) {
  width: 110px;
}
a:nth-child(3) {
  width: 100px;
}
a:nth-child(4) {
  width: 160px;
}
a:nth-child(5) {
  width: 120px;
}
a:nth-child(6) {
  width: 200px;
}




nav .start-home, a:nth-child(1):hover~.animation {
  width: 100px;
  left: 0;
  background-color: #c0cc15;
}
nav .start-about, a:nth-child(2):hover~.animation {
  width: 110px;
  left: 100px;
  background-color: #3cbfe7;
}
nav .start-blog, a:nth-child(3):hover~.animation {
  width: 100px;
  left: 210px;
  background-color: #00ff2a;
}
nav .start-portefolio, a:nth-child(4):hover~.animation {
  width: 160px;
  left: 310px;
  background-color: #da4500d7;
}
nav .start-contact, a:nth-child(5):hover~.animation {
  width: 120px;
  left: 470px;
  background-color: #e622b5;
}
nav .start-contact, a:nth-child(6):hover~.animation {
  width: 200px;
  left: 600px;
  background-color: #e62222;
}





body {
  font-size: 12px;
  font-family: sans-serif;
  background: #8300fd;
}
h1 {
  text-align: center;
  margin: 40px 0 40px;
  text-align: center;
  font-size: 30px;
  color: #000000;
  text-shadow: 2px 2px 4px #c0cc15;
  font-family: 'Cherry Swash', cursive;
}

p {
   
    bottom: 20px;
    width: 100%;
    text-align: center;
    color: #f1ecef;
    font-family: 'Cherry Swash',cursive;
    font-size: 16px;
}

span {
    color: #eeff05;
}



