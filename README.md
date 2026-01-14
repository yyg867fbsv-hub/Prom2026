<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <title>Darija QR Code Generator - Sseft QR Code Dyalk!</title>
    <!-- Hadi library bach ngeneriw l'QR Code -->
    <script src="https://cdn.jsdelivr.net/npm/qrcode@1.5.3/build/qrcode.min.js"></script>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #6a11cb 0%, #2575fc 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            color: #333;
        }

        .container {
            background-color: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.2);
            padding: 40px;
            width: 100%;
            max-width: 500px;
            text-align: center;
            border: 2px solid #4a00e0;
        }

        h1 {
            color: #4a00e0;
            margin-bottom: 25px;
            font-size: 2.2rem;
            text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.1);
        }

        .tagline {
            color: #6c757d;
            margin-bottom: 30px;
            font-size: 1.1rem;
        }

        .input-group {
            margin-bottom: 30px;
            text-align: right;
        }

        label {
            display: block;
            margin-bottom: 10px;
            font-weight: bold;
            color: #4a00e0;
            font-size: 1.2rem;
        }

        input {
            width: 100%;
            padding: 15px;
            border: 2px solid #6a11cb;
            border-radius: 10px;
            font-size: 1.1rem;
            transition: all 0.3s;
            text-align: center;
        }

        input:focus {
            outline: none;
            border-color: #2575fc;
            box-shadow: 0 0 0 3px rgba(37, 117, 252, 0.2);
        }

        .button-group {
            display: flex;
            gap: 15px;
            justify-content: center;
            flex-wrap: wrap;
        }

        button {
            padding: 15px 30px;
            border: none;
            border-radius: 10px;
            font-size: 1.1rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            flex: 1;
            min-width: 160px;
        }

        #generateBtn {
            background: linear-gradient(to right, #6a11cb, #2575fc);
            color: white;
        }

        #generateBtn:hover {
            transform: translateY(-3px);
            box-shadow: 0 7px 14px rgba(106, 17, 203, 0.3);
        }

        #clearBtn {
            background-color: #f8f9fa;
            color: #6a11cb;
            border: 2px solid #6a11cb;
        }

        #clearBtn:hover {
            background-color: #e9ecef;
            transform: translateY(-3px);
        }

        .qr-container {
            margin: 35px auto;
            padding: 20px;
            background: white;
            border-radius: 15px;
            display: inline-block;
            box-shadow: inset 0 0 10px rgba(0, 0, 0, 0.1);
            min-height: 256px;
            min-width: 256px;
            border: 2px dashed #6a11cb;
        }

        #qrcode {
            display: flex;
            justify-content: center;
            align-items: center;
        }

        #qrcode img {
            border-radius: 10px;
            border: 1px solid #ddd;
        }

        .instructions {
            background-color: #f0f7ff;
            border-radius: 10px;
            padding: 20px;
            margin-top: 30px;
            text-align: right;
            border-right: 5px solid #2575fc;
        }

        .instructions h3 {
            color: #4a00e0;
            margin-bottom: 10px;
        }

        .instructions ol {
            padding-right: 20px;
        }

        .instructions li {
            margin-bottom: 8px;
            line-height: 1.6;
        }

        .footer {
            margin-top: 25px;
            color: #6c757d;
            font-size: 0.9rem;
            border-top: 1px solid #eee;
            padding-top: 15px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🚀 Darija QR Code Generator</h1>
        <p class="tagline">Sseft QR Code b dik smitk f wa9t record!</p>

        <div class="input-group">
            <label for="textInput">💬 Kteb smitek aw chi haja:</label>
            <input type="text" id="textInput" placeholder="T3ayt yaddek, kteb hna...">
        </div>

        <div class="button-group">
            <button id="generateBtn">🔄 Sseft QR Code</button>
            <button id="clearBtn">🧹 Saffi koulchi</button>
        </div>

        <div class="qr-container">
            <div id="qrcode"></div>
        </div>

        <div class="instructions">
            <h3>📚 Kifach tst3em had l'outil:</h3>
            <ol>
                <li><strong>Kteb chi haja</strong> f dak l'input fou9.</li>
                <li><strong>Dgha 3la "Sseft QR Code"</strong> bach tgeneriha.</li>
                <li><strong>Stanna chwya</strong> bach yban l'QR code.</li>
                <li><strong>Scanneyha</strong> b mobile dyalek b app dyal QR!</li>
                <li>Bach tsaffi koulchi, dgha 3la "Saffi koulchi".</li>
            </ol>
        </div>

        <p class="footer">© 2023 - Dir bhal ma bghiti 🇲🇦</p>
    </div>

    <script>
        // Hna ghanbda l'JavaScript
        document.addEventListener('DOMContentLoaded', function() {
            const inputField = document.getElementById('textInput');
            const generateBtn = document.getElementById('generateBtn');
            const clearBtn = document.getElementById('clearBtn');
            const qrcodeDiv = document.getElementById('qrcode');
            
            let currentQRCode = null;

            // Fonction bach ngeneriw QR Code
            generateBtn.addEventListener('click', function() {
                const text = inputField.value.trim();
                
                if (!text) {
                    alert('A sahbi, khli wahd l'haja f dak l'input bach ngeneriw QR Code!');
                    return;
                }
                
                // Saffi l'QR Code l'qdim
                qrcodeDiv.innerHTML = '';
                
                // Genera l'QR Code jdid
                currentQRCode = new QRCode(qrcodeDiv, {
                    text: text,
                    width: 256,
                    height: 256,
                    colorDark: "#4a00e0",
                    colorLight: "#ffffff",
                    correctLevel: QRCode.CorrectLevel.H
                });
                
                // Rani fach tghenniya!
                console.log('QR Code generated for:', text);
            });

            // Fonction bach nsaffiw koulchi
            clearBtn.addEventListener('click', function() {
                inputField.value = '';
                qrcodeDiv.innerHTML = '<p style="color: #6c757d; padding: 40px;">Hna ghayban l'QR code...</p>';
                currentQRCode = null;
                inputField.focus();
            });

            // Bach n9edro ngeneriw QR Code b 'Enter' kam
            inputField.addEventListener('keyup', function(event) {
                if (event.key === 'Enter') {
                    generateBtn.click();
                }
            });
            
            // I3amer l'input b chi haja bach tbedda
            inputField.value = '3ayche Darija!';
            generateBtn.click();
        });
    </script>
</body>
</html>
