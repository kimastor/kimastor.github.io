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

    <!-- JavaScript here -->
</body>
</html>
