
<html>
<head>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }

        label {
            display: inline-block;
            width: 150px;
        }

        input[type="datetime-local"] {
            width: 300px;
            padding: 5px;
        }

        button {
            padding: 10px 20px;
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
        }

        #result {
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h2>Shift Calculation</h2>
    <label for="startDate">Start Date & Time:</label>
    <input type="datetime-local" id="startDate" required><br><br>

    <label for="endDate">End Date & Time:</label>
    <input type="datetime-local" id="endDate" required><br><br>

    <label for="rate">Rate:</label>
    <input type="number" id="rate" required><br><br>

    <button onclick="calculateShifts()">Calculate</button>

    <div id="result"></div>

    <script>
        function calculateShifts() {
            var startDate = new Date(document.getElementById('startDate').value);
            var endDate = new Date(document.getElementById('endDate').value);
            var rate = parseInt(document.getElementById('rate').value);

            var hoursDiff = Math.abs(endDate - startDate) / 36e5;
            var hours = Math.floor(hoursDiff);
            var minutes = Math.floor((hoursDiff % 1) * 60);

            var shifts = Math.floor(hoursDiff / 4);
            var applicableShifts = Math.max(0, shifts - 12);
            var totalRate = rate * applicableShifts;

            document.getElementById('result').innerHTML = `
                <p>Hours Between: ${hours} hours ${minutes} minutes</p>
                <p>Shift Count: ${shifts}</p>
                <p>Applicable Shifts: ${applicableShifts}</p>
                <p>Total Rate: $${totalRate}</p>
            `;
        }
    </script>
</body>
</html>
