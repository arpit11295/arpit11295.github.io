<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>For My Love ❤️</title>
  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(135deg, #ffd6e8, #fff);
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
      padding: 12px 22px;
      font-size: 1rem;
      border: none;
      border-radius: 25px;
      cursor: pointer;
      margin: 10px;
      background: #ff6fae;
      color: white;
    }
    button:hover { opacity: 0.9; }

    img {
      max-width: 280px;
      border-radius: 20px;
      margin: 20px 0;
    }

    .grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
      gap: 20px;
      margin-top: 30px;
    }

    .card {
      background: white;
      border-radius: 20px;
      padding: 15px;
      box-shadow: 0 10px 25px rgba(0,0,0,0.1);
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
<div class="page active" id="page1">
  <h1>Do you love me? 💕</h1>
  <button onclick="loveYes()">Yes</button>
  <button onclick="loveNo()">No</button>
</div>

<!-- PAGE 1 NO -->
<div class="page" id="pageNo">
  <h1>How dare you!! 😤</h1>
  <img src="photo1.jpg" alt="Angry cute" />
  <br />
  <button onclick="backToQuestion()">Try Again</button>
</div>

<!-- PAGE 2 -->
<div class="page" id="page2">
  <h1>For My Beautiful Girl 💖</h1>
  <div class="grid">

    <div class="card">
      <p>You are the mostesttt beautiful girl in the world 💕</p>
      <img src="photo3.jpg" />
    </div>

    <div class="card">
      <p>Hyyyyy I am missingg youu soo soo much 🫂<br/>Here is your virtual hug</p>
      <img src="photo4.jpg" />
    </div>

    <div class="card">
      <p>You are the best girlfriend in the worldddddd 💘</p>
      <img src="photo5.jpg" />
    </div>

    <div class="card">
      <p>Beat me in Tic Tac Toe 😼</p>
      <div class="board" id="board"></div>
      <p id="gameMsg"></p>
    </div>

  </div>
</div>

<!-- PAGE 3 -->
<div class="page" id="page3">
  <h1>WAIFU MATERIAL 💞</h1>
  <p>
    You are insanely beautiful, not just by looks but by heart.
    The way you smile, the way you care, the way you exist — everything about you feels magical.
    You are warmth, comfort, chaos, and peace all at once.
    Anyone would be lucky to love you, and I feel like the luckiest person alive.
  </p>
</div>

<script>
  function show(id) {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
  }

  function loveYes() { show('page2'); }
  function loveNo() { show('pageNo'); }
  function backToQuestion() { show('page1'); }

  /* Tic Tac Toe */
  const board = document.getElementById('board');
  const msg = document.getElementById('gameMsg');
  let cells = Array(9).fill('');
  let gameOver = false;

  function render() {
    board.innerHTML = '';
    cells.forEach((c, i) => {
      const div = document.createElement('div');
      div.className = 'cell';
      div.innerText = c;
      div.onclick = () => move(i);
      board.appendChild(div);
    });
  }

  function move(i) {
    if (cells[i] || gameOver) return;
    cells[i] = 'X';
    if (checkWin('X')) return win();
    aiMove();
  }

  function aiMove() {
    let empty = cells.map((v,i)=>v==''?i:null).filter(v=>v!==null);
    if (!empty.length) return reset();
    cells[empty[Math.floor(Math.random()*empty.length)]] = 'O';
    if (checkWin('O')) return reset();
    render();
  }

  function checkWin(p) {
    const w = [[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]];
    return w.some(a => a.every(i => cells[i]===p));
  }

  function win() {
    gameOver = true;
    msg.innerText = 'Yayyy like this you have won my heart tooooo babe 💖';
    setTimeout(()=>show('page3'), 5000);
  }

  function reset() {
    cells = Array(9).fill('');
    render();
  }

  render();
</script>

</body>
</html>
