<p align="left"> <img src="https://komarev.com/ghpvc/?username=uttiyasarkar&color=brightgreen&style=for-the-badge&label=Visitors" alt="uttiyasarkar" /> </p>

| [![](https://github-readme-stats.vercel.app/api?username=uttiyasarkar&include_all_commits=true&line_height=19&count_private=true&hide_title=true&theme=tokyonight)](https://github.com/anuraghazra/github-readme-stats) | [![ ](https://github-readme-stats-git-masterrstaa-rickstaa.vercel.app/api/top-langs/?username=uttiyasarkar&layout=compact&hide_title=true&exclude_repo=LEAPS,dot-emacs&hide_progress=true&theme=tokyonight)](https://github.com/anuraghazra/github-readme-stats) |
|--------------|-----------|

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Conway's Game of Life</title>
    <style>
        /* Add your CSS styling here */
        body {
            text-align: center;
        }

        .grid-container {
            display: grid;
            grid-template-columns: repeat(20, 30px);
            gap: 1px;
        }

        .cell {
            width: 30px;
            height: 30px;
            border: 1px solid #ccc;
            background-color: white;
        }
    </style>
</head>
<body>
    <h1>Conway's Game of Life</h1>
    <div id="game-container" class="grid-container"></div>
    <br>
    <button onclick="randomize()">Randomize</button>
    <button onclick="clearGrid()">Clear</button>
    <button onclick="nextGeneration()">Next Generation</button>

    <script>
        // Add your JavaScript logic here
        const width = 20;
        const height = 20;
        let grid = new Array(height).fill(0).map(() => new Array(width).fill(0));

        function createGrid() {
            const gameContainer = document.getElementById("game-container");
            gameContainer.innerHTML = "";

            for (let i = 0; i < height; i++) {
                for (let j = 0; j < width; j++) {
                    const cell = document.createElement("div");
                    cell.classList.add("cell");
                    cell.onclick = () => toggleCell(i, j);
                    gameContainer.appendChild(cell);
                }
            }
        }

        function randomize() {
            grid = grid.map(row => row.map(() => Math.random() > 0.5 ? 1 : 0));
            updateGrid();
        }

        function clearGrid() {
            grid = grid.map(row => row.map(() => 0));
            updateGrid();
        }

        function toggleCell(i, j) {
            grid[i][j] = 1 - grid[i][j];
            updateGrid();
        }

        function updateGrid() {
            const cells = document.querySelectorAll(".cell");
            cells.forEach((cell, index) => {
                const i = Math.floor(index / width);
                const j = index % width;
                cell.style.backgroundColor = grid[i][j] === 1 ? "black" : "white";
            });
        }

        function countNeighbors(i, j) {
            let count = 0;
            for (let x = i - 1; x <= i + 1; x++) {
                for (let y = j - 1; y <= j + 1; y++) {
                    if (x >= 0 && x < height && y >= 0 && y < width && (x !== i || y !== j)) {
                        count += grid[x][y];
                    }
                }
            }
            return count;
        }

        function nextGeneration() {
            const newGrid = new Array(height).fill(0).map(() => new Array(width).fill(0));

            for (let i = 0; i < height; i++) {
                for (let j = 0; j < width; j++) {
                    const neighbors = countNeighbors(i, j);

                    if (grid[i][j] === 1) {
                        // Cell is alive
                        if (neighbors === 2 || neighbors === 3) {
                            newGrid[i][j] = 1;
                        }
                    } else {
                        // Cell is dead
                        if (neighbors === 3) {
                            newGrid[i][j] = 1;
                        }
                    }
                }
            }

            grid = newGrid;
            updateGrid();
        }

        // Initialize the grid
        createGrid();
    </script>
</body>
</html>
