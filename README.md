<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>For My Cutest Girl 💕</title>

  <!-- Cute Google Font -->
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
      font-size:2.4rem;
      color:#ff5fa2;
      margin-bottom:15px;
    }
    p{
      font-size:1.15rem;
      max-width:720px;
      margin:0 auto 20px;
      line-height:1.7;
    }
    .page{display:none;min-height:100vh;padding:40px 20px;}
    .page.active{display:block;}
    button{
      padding:12px 28px;
      font-size:1rem;
      border:none;
      border-radius:30px;
      cursor:pointer;
      margin:10px;
      background:#ff6fae;
      color:#fff;
      box-shadow:0 6px 15px rgba(255,111,174,.4);
      font-family:'Quicksand',sans-serif;
    }
    button:hover{transform:scale(1.05);}
    .back{background:#bbb;color:#333;}
    img{
      max-width:290px;
      border-radius:22px;
      margin:20px 0;
      box-shadow:0 10px 25px rgba(0,0,0,.15);
    }
    .boxes{
      display:grid;
      grid-template-columns:repeat(auto-fit,minmax(200px,1fr));
      gap:22px;margin-top:30px;
    }
    .box{
      background:#fff;
      border-radius:25px;
      padding:28px;
      box-shadow:0 12px 30px rgba(0,0,0,.12);
      cursor:pointer;
      font-size:1.25rem;
      font-family:'Pacifico',cursive;
    }
    .box:hover{transform:translateY(-6px);}

    /* Tic Tac Toe */
    .board{display:grid;grid-template-columns:repeat(3,72px);gap:8px;justify-content:center;margin:20px auto;}
    .cell{width:72px;height:72px;font-size:2rem;background:#ffe6f0;border-radius:14px;display:flex;align-items:center;justify-content:center;cursor:pointer;font-family:'Pacifico',cursive;}
  </style>
</head>
<body>

<!-- QUESTION -->
<div class="page active" id="q">
  <h1>Hiiii my babyyyy 🥺💗</h1>
  <p>Before we start… answer this honestly okayyy? 😳💕</p>
  <h1>Do you love me? 💕</h1>
  <button onclick="show('boxes')">Yesss foreverrr 😘</button>
  <button onclick="show('no')">Nope 😒</button>
</div>

<!-- NO -->
<div class="page" id="no">
  <h1>HOW DARE YOUUU 😤💔</h1>
  <p>That was the wrong answer missy 😠</p>
  <img src="gun.jpeg">
  <br>
  <button onclick="show('q')">Try again properly 👉🥺</button>
</div>

<!-- BOXES -->
<div class="page" id="boxes">
  <h1>YAYYYY 🥰💝</h1>
  <p>Choose a cute lil box baby 💕</p>
  <img src="box.jpeg">
  <div class="boxes">
    <div class="box" onclick="show('b1')">🎁 Compliment Box</div>
    <div class="box" onclick="show('b2')">🤗 Hug Box</div>
    <div class="box" onclick="show('b3')">💌 Love Box</div>
    <div class="box" onclick="show('b4')">🎮 Fun Box</div>
  </div>
</div>

<!-- BOX 1 -->
<div class="page" id="b1">
  <h1>HEY YOUUU 😳💖</h1>
  <p>You are the mostesttttt beautiful girl in the whole entire universe ✨💗
     I still don’t understand how you’re THIS pretty 🥺</p>
  <img src="flower.jpeg">
  <br><button class="back" onclick="show('boxes')">⬅ Go back cutie</button>
</div>

<!-- BOX 2 -->
<div class="page" id="b2">
  <h1>I MISS YOUUU SOOO MUCH 😭💞</h1>
  <p>Hyyyyy my loveee, I’m missingg youu sooo sooo much 🫂
     Please accept this warm virtual hug 💕</p>
  <img src="hug.jpeg">
  <br><button class="back" onclick="show('boxes')">⬅ Backkk</button>
</div>

<!-- BOX 3 -->
<div class="page" id="b3">
  <h1>BEST GIRLFRIEND EVER 🥹💘</h1>
  <p>You are the best girlfriend in the worldddddd 😤💗
     I’m so lucky to have you it’s unreal 😌</p>
  <img src="cute.jpeg">
  <br><button class="back" onclick="show('boxes')">⬅ Back baby</button>
</div>

<!-- BOX 4 GAME -->
<div class="page" id="b4">
  <h1>OKAY CUTIE 😼🎮</h1>
  <p>Beat me in Tic Tac Toe and steal my heart completely 😏💞</p>
  <div class="board" id="board"></div>
  <p id="msg"></p>
  <button class="back" onclick="show('boxes')">⬅ Choose again</button>
</div>

<!-- FINAL -->
<div class="page" id="final">
  <h1>WAIFU MATERIAL 💍💖</h1>
  <img src="kiss.jpeg">
  <p>
    You are beautiful in ways words don’t even know how to explain 🥺✨
    Your smile melts my heart, your laugh makes my day brighter,
    and your love makes my world feel complete 💕
    You are my favorite person, my safe place,
    and my forever kind of girl 💗
  </p>
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
    if(win('X'))return victory();
    ai();
  }

  function ai(){
    let e=cells.map((v,i)=>v==''?i:null).filter(v=>v!==null);
    if(!e.length)return reset();
    cells[e[Math.floor(Math.random()*e.length)]]='O';
    if(win('O'))return reset();
    draw();
  }

  function win(p){
    const w=[[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]];
    return w.some(a=>a.every(i=>cells[i]===p));
  }

  function victory(){
    over=true;
    msg.innerText='YAYYYY 😍💖 like this you have won my heart tooooo babeeee';
    setTimeout(()=>show('final'),5000);
  }

  function reset(){cells=Array(9).fill('');draw();}

  draw();
</script>

</body>
</html>
