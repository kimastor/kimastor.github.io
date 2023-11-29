<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@picocss/pico@1/css/pico.min.css">
    <title>Julklappsleken</title>
    <style>
        /* ... existing CSS ... */
    </style>
</head>
<body>
    <!-- ... existing HTML ... -->

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

        // ... existing JavaScript ...

        function confirmSelection(name, assignee) {
            const confirmPopup = document.getElementById('confirmPopup');
            confirmPopup.innerHTML = `<p>Är du säker på att du vill se vem ${name} ska köpa en julklapp till?</p><button onclick='showAssignment("${name}", "${assignee}")'>Ja</button><button onclick='closePopup("confirmPopup")'>Nej</button>`;
            confirmPopup.style.display = 'block';
        }

        // ... remaining JavaScript ...
    </script>
</body>
</html>
