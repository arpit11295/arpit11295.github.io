
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>For My Cutest Girl 💕</title>

<link href="https://fonts.googleapis.com/css2?family=Pacifico&family=Quicksand:wght@400;600&display=swap" rel="stylesheet">

<style>
body{
  margin:0;
  font-family:'Quicksand',sans-serif;
  background:linear-gradient(135deg,#ffd6e8,#fff1f7);
  text-align:center;
  color:#444;
}

h1{
  font-family:'Pacifico',cursive;
  color:#ff4f9a;
}

.page{display:none;min-height:100vh;padding:40px 20px;}
.page.active{display:block;}

button{
  padding:12px 28px;
  border:none;
  border-radius:30px;
  cursor:pointer;
  margin:10px;
  background:#ff4f9a;
  color:white;
  font-size:1rem;
}

.back{background:#bbb;color:#333;}

img{
  max-width:280px;
  border-radius:20px;
  margin:20px 0;
  box-shadow:0 10px 25px rgba(0,0,0,.2);
}

.boxes{
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(200px,1fr));
  gap:20px;
}

.box{
  background:white;
  border-radius:25px;
  padding:25px;
  box-shadow:0 10px 25px rgba(0,0,0,.15);
  font-family:'Pacifico',cursive;
  font-size:1.2rem;
  cursor:pointer;
}

/* TIC TAC TOE */
.board{
  display:grid;
  grid-template-columns:repeat(3,80px);
  gap:10px;
  justify-content:center;
  margin:25px auto;
}

.cell{
  width:80px;
  height:80px;
  font-size:2.4rem;
  background:#ff3d8d;
  color:white;
  border-radius:16px;
  display:flex;
  align-items:center;
  justify-content:center;
  cursor:pointer;
  font-family:'Pacifico',cursive;
  box-shadow:0 8px 18px rgba(255,61,141,.7);
  transition:.2s;
}

.cell:hover{
  background:#ff1f7a;
  transform:scale(1.08);
}

.cell.win{
  background:#7bffb2 !important;
  color:#333;
  animation:pop .4s infinite alternate;
}

@keyframes pop{
  from{transform:scale(1);}
  to{transform:scale(1.12);}
}
</style>
</head>

<body>

<!-- QUESTION -->
<div class="page active" id="q">
  <h1>Hiiii my babyyyy 🥺💗</h1>
  <h1>Do you love me? 💕</h1>
  <button onclick="show('boxes')">Yesss foreverrr 😘</button>
  <button onclick="show('no')">Nope 😒</button>
</div>

<!-- NO -->
<div class="page" id="no">
  <h1>WRONG ANSWER 😤💔</h1>
  <img src="gun.jpeg">
  <br>
  <button onclick="show('q')">Try again 🥺</button>
</div>

<!-- BOXES -->
<div class="page" id="boxes">
  <h1>Choose a cute box 💝</h1>
  <div class="boxes">
    <div class="box" onclick="show('b1')">🎁 Compliment</div>
    <div class="box" onclick="show('b2')">🤗 Hug</div>
    <div class="box" onclick="show('b3')">💌 Love</div>
    <div class="box" onclick="show('b4')">🎮 Game</div>
  </div>
</div>

<!-- GAME -->
<div class="page" id="b4">
  <h1>Beat me and win my heart 😼💖</h1>
  <div class="board" id="board"></div>
  <p id="msg"></p>
  <button class="back" onclick="show('boxes')">⬅ Back</button>
</div>

<!-- FINAL -->
<div class="page" id="final">
  <h1>YOU WON MY HEART 💍💖</h1>
  <img src="kiss.jpeg">
  <p>You’re my forever girl 🥺✨</p>
</div>

<script>
function show(id){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.getElementById(id).classList.add('active');
}

const board=document.getElementById('board');
const msg=document.getElementById('msg');
let cells=Array(9).fill('');
let over=false;

const wins=[
  [0,1,2],[3,4,5],[6,7,8],
  [0,3,6],[1,4,7],[2,5,8],
  [0,4,8],[2,4,6]
];

function draw(){
  board.innerHTML='';
  cells.forEach((c,i)=>{
    const d=document.createElement('div');
    d.className='cell';
    d.innerText=c;
    d.onclick=()=>play(i);
    board.appendChild(d);
  });
}

function play(i){
  if(cells[i]||over)return;
  cells[i]='X';
  draw();
  const win=checkWin('X');
  if(win) return victory(win);
  ai();
}

function ai(){
  let empty=cells.map((v,i)=>v==''?i:null).filter(v=>v!==null);
  if(!empty.length) return reset();
  cells[empty[Math.floor(Math.random()*empty.length)]]='O';
  draw();
}

function checkWin(p){
  return wins.find(w=>w.every(i=>cells[i]===p));
}

function victory(line){
  over=true;
  msg.innerText='OMG YOU WON 😍💖';
  document.querySelectorAll('.cell').forEach((c,i)=>{
    if(line.includes(i)) c.classList.add('win');
  });
  setTimeout(()=>show('final'),4500);
}

function reset(){
  cells=Array(9).fill('');
  over=false;
  msg.innerText='';
  draw();
}

draw();
</script>

</body>
</html>

