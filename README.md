<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@picocss/pico@1/css/pico.min.css">
    <title>Julklappsleken</title>
    <style>
        body {
            background-color: lightgrey; /* Consistent background color */
            margin: 0;
            padding: 0;
            font-family: Arial, sans-serif;
        }
        .container {
            background-color: #fff; /* Optional: different background for the content area */
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            max-width: 600px;
            margin: 50px auto; /* Centers the container */
        }
        button {
            background-color: darkred;
            color: white;
            margin: 5px;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        button:hover {
            background-color: #a83232;
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
            text-align: center;
            z-index: 1000; /* Ensures popup is above all other content */
        }
        #assignmentPopup img {
            display: block;
            margin-left: auto;
            margin-right: auto;
            width: 100px;
            height: auto;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Välkommen till Julklappsleken!</h2>
        <h3>Ange kod 24 för att starta spelet</h3>
        <input type="number" id="seedInput" placeholder="Ange kod här" value="24">
        <button id="startGameButton">Starta spelet</button>
        <div id="names" style="display:none;"></div>
    </div>

    <div id="confirmPopup" class="popup"></div>
    <div id="assignmentPopup" class="popup">
        <p id="assignmentText"></p>
        <button onclick="closePopup('assignmentPopup')">Stäng</button>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/seedrandom/2.4.4/seedrandom.min.js"></script>
    <script>
        const participants = ['Cindra', 'Kim', 'Zina', 'Lisbeth', 'Peter', 'Classe', 'Elsa', 'Barry', 'Kristina'];

        document.addEventListener('DOMContentLoaded', () => {
            document.getElementById('startGameButton').addEventListener('click', startGame);
        });

        function startGame() {
            const seed = document.getElementById('seedInput').value;
            const assignments = assignGifts(seed);
            displayButtons(assignments);
        }

        function assignGifts(seed) {
            const pseudoRandom = new Math.seedrandom(seed);
            let participantsShuffled = shuffleArray(participants.slice(), pseudoRandom);
            let assignment = {};

            for (let i = 0; i < participantsShuffled.length; i++) {
                let giver = participantsShuffled[i];
                let receiver = participantsShuffled[(i + 1) % participantsShuffled.length];
                if (giver === receiver) {
                    [assignment[giver], assignment[participantsShuffled[0]]] = [assignment[participantsShuffled[0]], giver];
                } else {
                    assignment[giver] = receiver;
                }
            }
            return assignment;
        }

        function shuffleArray(array, pseudoRandom) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(pseudoRandom() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        function displayButtons(assignments) {
            const namesDiv = document.getElementById('names');
            namesDiv.innerHTML = '';
            participants.forEach(name => {
                const button = document.createElement('button');
                button.innerText = name;
                button.onclick = () => confirmSelection(name, assignments[name]);
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
            assignmentText.innerHTML = `${name}, du ska köpa en julklapp till ${assignee}! <br><img src='https://github.com/kimastor/kimastor.github.io/blob/main/DALL%C2%B7E%202023-11-28%2020.15.55%20-%20An%20illustration%20in%20the%20style%20of%20early%2020th-century%20Swedish%20artists%20like%20John%20Bauer,%20similar%20to%20the%20first%20and%20third%20images,%20depicting%20a%20gnome%20with%20a%20th.png?raw=true' alt='Presentlåda' style='width:100px; height:auto;'>";
            closePopup('confirmPopup');
            document.getElementById('assignmentPopup').style.display = 'block';
        }

        function closePopup(popupId) {
            document.getElementById(popupId).style.display = 'none';
        }
    </script>
</body>
</html>
