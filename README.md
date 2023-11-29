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

        function assignGifts(seed) {
            const pseudoRandom = new Math.seedrandom(seed);
            let participantsShuffled = shuffleArray(participants.slice(), pseudoRandom);
            let assignment = {};

            for (let i = 0; i < participantsShuffled.length; i++) {
                let giver = participantsShuffled[i];
                let receiver = participantsShuffled[(i + 1) % participantsShuffled.length];
                assignment[giver] = receiver;
            }

            // Check if anyone is assigned to themselves
            for (let participant in assignment) {
                if (participant === assignment[participant]) {
                    // Find someone who isn't assigned to themselves and swap assignments
                    for (let swap in assignment) {
                        if (swap !== assignment[swap] && participant !== assignment[swap]) {
                            let temp = assignment[participant];
                            assignment[participant] = assignment[swap];
                            assignment[swap] = temp;
                            break;
                        }
                    }
                }
            }

            return assignment;
        }

        // ... remaining JavaScript ...
    </script>
</body>
</html>
