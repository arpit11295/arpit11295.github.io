<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>For My Girlfriend ❤️</title>
  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(135deg, #ffd6e8, #ffffff);
      text-align: center;
      color: #333;
    }
    .page {
      display: none;
      min-height: 100vh;
      padding: 40px 20px;
    }
    .page.active { display: block; }

    h1 { font-size: 2.2rem; margin-bottom: 20px; }
    p { font-size: 1.1rem; max-width: 700px; margin: 0 auto 20px; }

    button {
      padding: 12px 24px;
      font-size: 1rem;
      border: none;
      border-radius: 25px;
      cursor: pointer;
      margin: 10px;
      background: #ff6fae;
      color: white;
    }

    img {
      max-width: 280px;
      border-radius: 20px;
      margin: 20px 0;
    }

    .boxes {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 20px;
      margin-top: 30px;
    }

    .box {
      background: white;
      border-radius: 20px;
      padding: 20px;
      box-shadow: 0 10px 25px rgba(0,0,0,0.1);
      cursor: pointer;
    }

    /* Tic Tac Toe */
    .board {
      display: grid;
      grid-template-columns: repeat(3, 70px);
      gap: 8px;
      justify-content: center;
      margin: 15px auto;
    }
    .cell {
      width: 70px;
      height: 70px;
      font-size: 2rem;
      background: #ffe6f0;
      border-radius: 12px;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
    }
  </style>
</head>
<body>

<!-- PAGE 1 -->
<div class="page active" id="q">
  <h1>Do you love me? 💕</h1>
  <button onclick="show('boxes')">Yes</button>
  <button onclick="show('no')">No</button>
</div>

<!-- NO PAGE -->
<div class="page" id="no">
  <h1>How dare you!! 😤</h1>
  <img src="gun.jpeg" />
  <br />
  <button onclick="show('q')">Try Again</button>
</div>

<!-- BOX PAGE -->
<div class="page" id="boxes">
  <h1>Choose a Box 💝</h1>
  <img src="box.jpeg" />
  <div class="boxes">
    <div class="box" onclick="show('b1')">🎁 Box 1</div>
    <div class="box" onclick="show('b2')">🎀 Box 2</div>
    <div class="box" onclick="show('b3')">💌 Box 3</div>
    <div class="box" onclick="show('b4')">🎮 Box 4</div>
  </div>
</div>

<!-- BOX 1 -->
<div class="page" id="b1">
  <h1>You are the mostesttt beautiful girl in the world 💖</h1>
  <img src="flower.jpeg" />
</div>

<!-- BOX 2 -->
<div class="page" id="b2">
  <h1>Hyyyyy I am missingg youu soo soo much 🫂</h1>
  <p>Here is your virtual hug</p>
  <img src="hug.jpeg" />
</div>

<!-- BOX 3 -->
<div class="page" id="b3">
  <h1>You are the best girlfriend in the worldddddd 💘</h1>
  <img src="kiss.jpeg" />
</div>

<!-- BOX 4 GAME -->
<div class="page" id="b4">
  <h1>Beat me in Tic Tac Toe 😼</h1>
  <div class="board" id="board"></div>
  <p id="msg"></p>
</div>

<!-- FINAL PAGE -->
<div class="page" id="final">
  <h1>WAIFU MATERIAL 💞</h1>
  <p>
    You are beautiful in ways words will never fully explain.
    Your smile feels like home, your presence feels like peace,
    and your love feels like magic.
    Every little thing about you makes my world brighter.
    I’m so proud to call you mine.
  </p>
</div>

<script>
  function show(id) {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
  }

  /* Tic Tac Toe */
  const board = document.getElementById('board');
  const msg = document.getElementById('msg');
  let cells = Array(9).fill('');
  let gameOver = false;

  function draw() {
    board.innerHTML = '';
    cells.forEach((c,i)=>{
      const d = document.createElement('div');
      d.className='cell'; d.innerText=c;
      d.onclick=()=>play(i);
      board.appendChild(d);
    });
  }

  function play(i){
    if(cells[i]||gameOver) return;
    cells[i]='X';
    if(win('X')) return victory();
    ai();
  }

  function ai(){
    let e=cells.map((v,i)=>v==''?i:null).filter(v=>v!==null);
    if(!e.length) return reset();
    cells[e[Math.floor(Math.random()*e.length)]]='O';
    if(win('O')) return reset();
    draw();
  }

  function win(p){
    const w=[[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]];
    return w.some(a=>a.every(i=>cells[i]===p));
  }

  function victory(){
    gameOver=true;
    msg.innerText='Yayyy like this you have won my heart tooooo babe 💖';
    setTimeout(()=>show('final'),5000);
  }

  function reset(){
    cells=Array(9).fill('');
    draw();
  }

  draw();
</script>

</body>
</html>
