<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bingo Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 20px;
        }
        .bingo-container {
            display: grid;
            gap: 10px;
            margin: 20px auto;
            max-width: 800px;
        }
        .bingo-item {
            border: 2px solid #ccc;
            border-radius: 10px;
            width: 100%;
            aspect-ratio: 1 / 1;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            background-color: #f9f9f9;
            cursor: pointer;
            transition: background-color 0.3s, box-shadow 0.3s;
        }
        .bingo-item.checked {
            background-color: #b2f7b2;
            box-shadow: 0 0 10px #4caf50;
        }
        .bingo-item input[type="text"] {
            margin: 5px 0;
            border: 1px solid #ccc;
            border-radius: 5px;
            padding: 5px;
            width: 90%;
            box-sizing: border-box;
        }
        #add-button {
            margin: 20px auto;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            background-color: #4caf50;
            color: white;
            cursor: pointer;
            font-size: 16px;
            transition: background-color 0.3s;
        }
        #add-button:hover {
            background-color: #45a049;
        }
        #bingo-alert {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: rgba(0, 0, 0, 0.8);
            color: white;
            padding: 20px 40px;
            border-radius: 10px;
            font-size: 24px;
            z-index: 1000;
        }
    </style>
</head>
<body>
    <h1>Bingo Game</h1>
    <button id="add-button">Add Bingo Item</button>
    <div class="bingo-container" id="bingo-container">
        <!-- Bingo items will appear here -->
    </div>
    <div id="bingo-alert">BINGO!</div>

    <script>
        const container = document.getElementById('bingo-container');
        const addButton = document.getElementById('add-button');
        const alertBox = document.getElementById('bingo-alert');

        let itemCount = 0;
        let gridSize = 0;

        function checkBingo() {
            const items = Array.from(container.children);
            const checked = items.map(item => item.classList.contains('checked'));

            // Check rows and columns
            for (let i = 0; i < gridSize; i++) {
                const row = checked.slice(i * gridSize, (i + 1) * gridSize);
                const column = checked.filter((_, index) => index % gridSize === i);

                if (row.every(Boolean) || column.every(Boolean)) {
                    showBingoAlert();
                    return;
                }
            }

            // Check diagonals
            const diagonal1 = checked.filter((_, index) => index % (gridSize + 1) === 0);
            const diagonal2 = checked.filter((_, index) => index % (gridSize - 1) === 0 && index > 0 && index < checked.length - 1);

            if (diagonal1.every(Boolean) || diagonal2.every(Boolean)) {
                showBingoAlert();
            }
        }

        function showBingoAlert() {
            alertBox.style.display = 'block';
            setTimeout(() => {
                alertBox.style.display = 'none';
            }, 3000);
        }

        addButton.addEventListener('click', () => {
            const item = document.createElement('div');
            item.className = 'bingo-item';

            const textInput = document.createElement('input');
            textInput.type = 'text';
            textInput.placeholder = 'Enter text';

            item.appendChild(textInput);

            item.addEventListener('click', () => {
                item.classList.toggle('checked');
                checkBingo();
            });

            container.appendChild(item);
            itemCount++;

            gridSize = Math.ceil(Math.sqrt(itemCount));
            container.style.gridTemplateColumns = `repeat(${gridSize}, 1fr)`;
        });
    </script>
</body>
</html>
