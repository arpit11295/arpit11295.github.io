<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Love Test for My GF</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #ffe6f2;
            color: #333;
            text-align: center;
            padding: 20px;
        }
        .container {
            max-width: 800px;
            margin: 0 auto;
        }
        button {
            background-color: #ff69b4;
            color: white;
            border: none;
            padding: 10px 20px;
            margin: 10px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
        }
        button:hover {
            background-color: #ff1493;
        }
        .gifts {
            display: none;
            grid-template-columns: repeat(2, 1fr);
            gap: 20px;
            margin-top: 20px;
        }
        .gift-box {
            border: 2px solid #ff69b4;
            padding: 20px;
            border-radius: 10px;
            background-color: #fff;
        }
        .kitty {
            font-size: 50px;
            margin: 10px;
        }
        .tictactoe {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 5px;
            margin: 20px auto;
            width: 150px;
        }
        .cell {
            width: 50px;
            height: 50px;
            border: 1px solid #333;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
            cursor: pointer;
            background-color: #f9f9f9;
        }
        .cell:hover {
            background-color: #e0e0e0;
        }
        .message {
            font-size: 18px;
            margin: 20px;
        }
        .paragraph {
            display: none;
            margin-top: 20px;
            font-style: italic;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1 id="question">Do you love me? (Yes or No)</h1>
        <button id="yesBtn">Yes</button>
        <button id="noBtn">No</button>
        <button id="tryAgainBtn" style="display: none;">Try Again</button>
        <div id="dareMessage" style="display: none;">
            <h2>How dare you!</h2>
        </div>
        <div class="gifts" id="gifts">
            <div class="gift-box">
                <h3>Gift 1: Virtual Hug</h3>
                <div class="kitty">🐱🤗🐱</div>
                <p>A warm virtual hug from cute kitties!</p>
            </div>
            <div class="gift-box">
                <h3>Gift 2: Beauty Compliment</h3>
                <p>💖 You are the most beautiful person in the world, my adorable waifu! 💖</p>
            </div>
            <div class="gift-box">
                <h3>Gift 3: Flying Kiss</h3>
                <div class="kitty">🐱💋</div>
                <p>A flying kiss from your favorite kitty! Mwah!</p>
            </div>
            <div class="gift-box">
                <h3>Gift 4: Tic-Tac-Toe Challenge</h3>
                <div class="tictactoe" id="board">
                    <div class="cell" data-index="0"></div>
                    <div class="cell" data-index="1"></div>
                    <div class="cell" data-index="2"></div>
                    <div class="cell" data-index="3"></div>
                    <div class="cell" data-index="4"></div>
                    <div class="cell" data-index="5"></div>
                    <div class="cell" data-index="6"></div>
                    <div class="cell" data-index="7"></div>
                    <div class="cell" data-index="8"></div>
                </div>
                <div class="message" id="gameMessage"></div>
                <div class="paragraph" id="waifuParagraph">
                    <h4>Certified Waifu Material</h4>
                    <p>You are my everything, my sunshine on a rainy day, my favorite anime character come to life. With your smile that lights up the room and your heart that's kinder than a thousand kittens, you've captured my heart forever. You're not just beautiful; you're magical, and I promise to cherish you always. Love you to the moon and back! 🌙💕</p>
                </div>
            </div>
        </div>
    </div>

    <script>
        const question = document.getElementById('question');
        const yesBtn = document.getElementById('yesBtn');
        const noBtn = document.getElementById('noBtn');
        const tryAgainBtn = document.getElementById('tryAgainBtn');
        const dareMessage = document.getElementById('dareMessage');
        const gifts = document.getElementById('gifts');
        const board = document.getElementById('board');
        const cells = document.querySelectorAll('.cell');
        const gameMessage = document.getElementById('gameMessage');
        const waifuParagraph = document.getElementById('waifuParagraph');

        let gameState = ['', '', '', '', '', '', '', '', ''];
        let currentPlayer = 'X'; // User is X, AI is O
        let gameActive = true;

        noBtn.addEventListener('click', () => {
            question.style.display = 'none';
            yesBtn.style.display = 'none';
            noBtn.style.display = 'none';
            dareMessage.style.display = 'block';
            tryAgainBtn.style.display = 'block';
        });

        tryAgainBtn.addEventListener('click', () => {
            question.style.display = 'block';
            yesBtn.style.display = 'inline-block';
            noBtn.style.display = 'inline-block';
            dareMessage.style.display = 'none';
            tryAgainBtn.style.display = 'none';
            gifts.style.display = 'none';
        });

        yesBtn.addEventListener('click', () => {
            question.style.display = 'none';
            yesBtn.style.display = 'none';
            noBtn.style.display = 'none';
            gifts.style.display = 'grid';
        });

        // Tic-Tac-Toe logic
        cells.forEach(cell => {
            cell.addEventListener('click', handleCellClick);
        });

        function handleCellClick(event) {
            const index = event.target.getAttribute('data-index');
            if (gameState[index] !== '' || !gameActive) return;

            gameState[index] = currentPlayer;
            event.target.textContent = currentPlayer;

            if (checkWin()) {
                gameActive = false;
                gameMessage.textContent = 'Yayy you won myy heart!';
                setTimeout(() => {
                    waifuParagraph.style.display = 'block';
                }, 5000);
                return;
            }

            // AI makes a move (intentionally bad to let user win easily)
            currentPlayer = 'O';
            setTimeout(() => {
                aiMove();
            }, 500);
        }

        function aiMove() {
            // Simple AI: pick a random empty cell, but avoid blocking wins to make it easy
            let available = gameState.map((val, idx) => val === '' ? idx : null).filter(val => val !== null);
            if (available.length > 0) {
                let move = available[Math.floor(Math.random() * available.length)];
                gameState[move] = 'O';
                cells[move].textContent = 'O';
                currentPlayer = 'X';
            }
        }

        function checkWin() {
            const winConditions = [
                [0, 1, 2], [3, 4, 5], [6, 7, 8],
                [0, 3, 6], [1, 4, 7], [2, 5, 8],
                [0, 4, 8], [2, 4, 6]
            ];
            return winConditions.some(condition => {
                return condition.every(index => gameState[index] === currentPlayer);
            });
        }
    </script>
</body>
</html># arpit11295.github.io
