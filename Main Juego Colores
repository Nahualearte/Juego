<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Juego de Colores</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: black;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        .scoreboard {
            display: flex;
            justify-content: space-around;
            width: 400px;
            font-size: 24px;
            color: white;
            margin-bottom: 20px;
        }
        .grid {
            display: grid;
            grid-template-columns: repeat(6, 100px);
            grid-template-rows: repeat(4, 100px);
            gap: 5px;
            margin-bottom: 40px;
        }
        .cell {
            width: 100px;
            height: 100px;
            background-color: gray;
            transition: background-color 0.5s ease-in-out;
            cursor: pointer;
        }
        .cell.blue {
            background-color: blue;
        }
        .cell.red {
            background-color: red;
        }
        .trail {
            box-shadow: 0 0 15px white;
        }
        #winner-message {
            font-size: 24px;
            color: yellow;
            margin-bottom: 20px;
        }
        .buttons {
            display: flex;
            gap: 20px;
        }
        button {
            padding: 15px 30px;
            font-size: 18px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="scoreboard">
        <div>Tiempo: <span id="timer">60</span>s</div>
        <div>Azul: <span id="score-blue">0</span></div>
        <div>Rojo: <span id="score-red">0</span></div>
    </div>
    <div class="grid" id="grid"></div>
    <div id="winner-message"></div>
    <div class="buttons">
        <button onclick="startGame()">Jugar</button>
        <button onclick="resetGame()">Reiniciar</button>
    </div>

    <script>
        const rows = 4;
        const cols = 6;
        const colors = ['blue', 'red'];
        let score = { blue: 0, red: 0 };
        let timeLeft = 60;
        let gameInterval;
        let timerInterval;

        function createGrid() {
            const grid = document.getElementById('grid');
            grid.innerHTML = '';
            for (let i = 0; i < rows * cols; i++) {
                const cell = document.createElement('div');
                cell.classList.add('cell');
                cell.dataset.color = 'gray';
                cell.onclick = () => handleClick(cell);
                grid.appendChild(cell);
            }
        }

        function updateColors() {
            const cells = Array.from(document.querySelectorAll('.cell'));
            let shuffledColors = Array(rows * cols / 2).fill(colors[0])
                .concat(Array(rows * cols / 2).fill(colors[1]))
                .sort(() => Math.random() - 0.5);
            
            for (let row = 0; row < rows; row++) {
                setTimeout(() => {
                    for (let col = 0; col < cols; col++) {
                        let index = row * cols + col;
                        let cell = cells[index];
                        if (cell.dataset.color !== shuffledColors[index]) {
                            cell.classList.remove('blue', 'red');
                            cell.classList.add(shuffledColors[index]);
                            cell.dataset.color = shuffledColors[index];
                            cell.classList.add('trail');
                            setTimeout(() => cell.classList.remove('trail'), 300);
                        }
                    }
                }, row * 150);
            }
        }

        function handleClick(cell) {
            const color = cell.dataset.color;
            if (colors.includes(color)) {
                score[color]++;
                document.getElementById(`score-${color}`).textContent = score[color];
                cell.dataset.color = 'gray';
                cell.classList.remove('blue', 'red');
            }
        }

        function startGame() {
            score = { blue: 0, red: 0 };
            document.getElementById('score-blue').textContent = 0;
            document.getElementById('score-red').textContent = 0;
            document.getElementById('winner-message').textContent = '';
            timeLeft = 60;
            document.getElementById('timer').textContent = timeLeft;
            createGrid();
            updateColors();
            gameInterval = setInterval(updateColors, 1000);
            timerInterval = setInterval(() => {
                timeLeft--;
                document.getElementById('timer').textContent = timeLeft;
                if (timeLeft <= 0) {
                    clearInterval(gameInterval);
                    clearInterval(timerInterval);
                    declareWinner();
                }
            }, 1000);
        }

        function declareWinner() {
            let message = 'Empate';
            if (score.blue > score.red) message = '¡Ganó Azul!';
            if (score.red > score.blue) message = '¡Ganó Rojo!';
            document.getElementById('winner-message').textContent = message;
        }

        function resetGame() {
            clearInterval(gameInterval);
            clearInterval(timerInterval);
            startGame();
        }
    </script>
</body>
</html>
