<!DOCTYPE html>
<html lang="az">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Xərc Hesablayıcı</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 600px;
            margin: 0 auto;
            padding: 20px;
        }
        input, button {
            display: block;
            width: 100%;
            margin-bottom: 10px;
            padding: 10px;
            box-sizing: border-box;
        }
        button {
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
        #result {
            margin-top: 20px;
            font-weight: bold;
        }
        #temizle {
            background-color: #f44336;
        }
        #temizle:hover {
            background-color: #d32f2f;
        }
        .button-container {
            display: flex;
            gap: 10px;
        }
        .button-container button {
            flex: 1;
        }
    </style>
</head>
<body>
    <h1>Xərc Hesablayıcı</h1>
    <input type="number" id="sahil" placeholder="Sahil qoyduğu məbləği daxil edin">
    <input type="number" id="rufet" placeholder="Rüfətin qoyduğu məbləği daxil edin">
    <input type="number" id="nusret" placeholder="Nüsrətin qoyduğu məbləği daxil edin">
    <div class="button-container">
        <button onclick="hesabla()">Hesabla</button>
        <button id="temizle" onclick="temizle()">Təmizlə</button>
    </div>
    <div id="result"></div>

    <script>
        function hesabla() {
            let sahil = parseFloat(document.getElementById('sahil').value);
            let rufet = parseFloat(document.getElementById('rufet').value);
            let nusret = parseFloat(document.getElementById('nusret').value);
            let result = document.getElementById('result');
            let message = '';

            let her_biri = (sahil + rufet + nusret) / 3;
            let QHVM = (rufet + nusret) / 2;

            if (sahil > her_biri) {
                message += `Sahilə Nüsrət ${(sahil - her_biri).toFixed(1)} manat verməlidir!<br>`;
            } else if (sahil === her_biri && nusret === her_biri && rufet === her_biri) {
                message += "Heç kim heç kimə heçnə vermir.<br>";
            } else {
                message += `Sahil Nüsrətə ${(her_biri - sahil).toFixed(1)} manat verməlidir.<br>`;
            }

            if (QHVM > rufet) {
                message += `Rufət Nüsrətə ${((QHVM - rufet) - (her_biri - sahil) / 2).toFixed(1)} manat verməlidir.<br>`;
            } else if (her_biri === rufet) {
                message += "Rufətə Heçnə verilmir!<br>";
            } else if (nusret === rufet && sahil > her_biri) {
                message += `Nüsrətə Rüfət ${(her_biri - rufet).toFixed(1)} manat verməlidir.<br>`;
            } else if (nusret === rufet && sahil < her_biri) {
                message += `Nüsrət Rüfətə ${(nusret - her_biri).toFixed(1)} manat verməlidir.<br>`;
            } else {
                message += `Nüsrət Rüfətə ${((rufet - QHVM) + ((her_biri - sahil) / 2)).toFixed(1)} manat verməlidir.<br>`;
            }

            result.innerHTML = message;
        }

        function temizle() {
            document.getElementById('sahil').value = '';
            document.getElementById('rufet').value = '';
            document.getElementById('nusret').value = '';
            document.getElementById('result').innerHTML = '';
        }
    </script>
</body>
</html>
