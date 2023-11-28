<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@picocss/pico@1/css/pico.min.css">
    <title>Julklappsleken</title>
    <style>
        body {
            background-color: lightgrey;
        }
        button {
            background-color: darkred;
            color: white;
            margin: 5px;
        }
        .popup {
            display: none;
            position: fixed;
            left: 50%;
            top: 50%;
            transform: translate(-50%, -50%);
            background-color: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
    </style>
</head>
<body>
    <main class="container">
        <div class="grid">
            <section>
                <hgroup>
                    <h2>Välkommen till Julklappsleken!</h2>
                    <h3>Ange kod 24 för att starta spelet</h3>
                </hgroup>
                <input type="number" id="seedInput" placeholder="Ange kod här" value="24">
                <button onclick="startGame()">Starta spelet</button>
                <div id="names" style="display:none;"></div>
            </section>
        </div>
    </main>
    <div id="confirmPopup" class="popup"></div>
    <div id="assignmentPopup" class="popup">
        <p id="assignmentText"></p>
        <button onclick="closePopup('assignmentPopup')">Stäng</button>
    </div>
    <script>
        const participants = ['Cindra', 'Kim', 'Zina', 'Lisbeth', 'Peter', 'Classe', 'Elsa', 'Barry', 'Kristina'];

        function startGame() {
            const seed = document.getElementById('seedInput').value;
            const shuffledParticipants = shuffleArray(participants, seed);
            displayButtons(shuffledParticipants);
        }

        function shuffleArray(array, seed) {
            let currentIndex = array.length, temporaryValue, randomIndex;
            const pseudoRandom = new Math.seedrandom(seed);

            while (0 !== currentIndex) {
                randomIndex = Math.floor(pseudoRandom() * currentIndex);
                currentIndex -= 1;
                temporaryValue = array[currentIndex];
                array[currentIndex] = array[randomIndex];
                array[randomIndex] = temporaryValue;
            }

            return array;
        }

        function displayButtons(shuffledArray) {
            const namesDiv = document.getElementById('names');
            namesDiv.innerHTML = '';
            shuffledArray.forEach((name, index) => {
                const button = document.createElement('button');
                button.innerText = name;
                button.onclick = () => confirmSelection(name, shuffledArray[(index + 1) % shuffledArray.length]);
                namesDiv.appendChild(button);
            });
            namesDiv.style.display = 'block';
        }

        function confirmSelection(name, assignee) {
            const confirmPopup = document.getElementById('confirmPopup');
            confirmPopup.innerHTML = `<p>Är du säker på att du vill se vem ${name} ska köpa en julklapp till?</p><button onclick='showAssignment(\"${name}\", \"${assignee}\")'>Ja</button><button onclick='closePopup(\"confirmPopup\")'>Nej</button>`;
            confirmPopup.style.display = 'block';
        }

        function showAssignment(name, assignee) {
            const assignmentText = document.getElementById('assignmentText');
            assignmentText.innerText = `${name}, du ska köpa en julklapp till ${assignee}!`;
            closePopup('confirmPopup');
            document.getElementById('assignmentPopup').style.display = 'block';
        }

        function closePopup(popupId) {
            document.getElementById(popupId).style.display = 'none';
        }
    </script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/seedrandom/2.4.4/seedrandom.min.js"></script>
</body>
</html>
