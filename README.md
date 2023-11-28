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
    <!DOCTYPE html>
<html lang="sv">
<head>
    <!-- Övriga head-element -->
</head>
<body>
    <!-- Övriga body-element -->

    <script>
        const participants = ['Cindra', 'Kim', 'Zina', 'Lisbeth', 'Peter', 'Classe', 'Elsa', 'Barry', 'Kristina'];
        let assignments = {};

        function startGame() {
            const seed = document.getElementById('seedInput').value;
            assignments = assignGifts(seed);
            displayButtons();
        }

        function assignGifts(seed) {
            const pseudoRandom = new Math.seedrandom(seed);
            let shuffled = participants.slice();
            let recipients = participants.slice();
            let assignment = {};

            shuffled.forEach(name => {
                let recipientIndex;
                do {
                    recipientIndex = Math.floor(pseudoRandom() * recipients.length);
                } while (recipients[recipientIndex] === name);
                assignment[name] = recipients.splice(recipientIndex, 1)[0];
            });

            return assignment;
        }

        function displayButtons() {
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
            assignmentText.innerHTML = `${name}, du ska köpa en julklapp till ${assignee}! <br><img src='https://github.com/kimastor/kimastor.github.io/blob/main/DALL%C2%B7E%202023-11-28%2020.15.55%20-%20An%20illustration%20in%20the%20style%20of%20early%2020th-century%20Swedish%20artists%20like%20John%20Bauer,%20similar%20to%20the%20first%20and%20third%20images,%20depicting%20a%20gnome%20with%20a%20th.png?raw=true' alt='Presentlåda' style='width:100px; height:auto;'>`;
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


</body>
</html>
