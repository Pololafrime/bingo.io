<!DOCTYPE html>
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
            grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
            gap: 10px;
            margin: 20px auto;
            max-width: 800px;
        }
        .bingo-item {
            border: 2px solid #ccc;
            border-radius: 10px;
            padding: 10px;
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
            width: 100%;
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
    </style>
</head>
<body>
    <h1>Bingo Game</h1>
    <button id="add-button">Add Bingo Item</button>
    <div class="bingo-container" id="bingo-container">
        <!-- Bingo items will appear here -->
    </div>

    <script>
        const container = document.getElementById('bingo-container');
        const addButton = document.getElementById('add-button');

        addButton.addEventListener('click', () => {
            const item = document.createElement('div');
            item.className = 'bingo-item';

            const textInput = document.createElement('input');
            textInput.type = 'text';
            textInput.placeholder = 'Enter text';

            item.appendChild(textInput);

            item.addEventListener('click', () => {
                item.classList.toggle('checked');
            });

            container.appendChild(item);
        });
    </script>
</body>
</html>
