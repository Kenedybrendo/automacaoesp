<!DOCTYPE html>
<html lang="pt">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Controle de LEDs</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            text-align: center;
            margin: 0;
            padding: 20px;
        }

        h1 {
            color: #333;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background-color: white;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        .button {
            padding: 15px 32px;
            font-size: 16px;
            cursor: pointer;
            border-radius: 5px;
            margin: 10px;
            width: 150px;
            transition: background-color 0.3s ease;
        }

        .slider-container {
            margin: 20px 0;
        }

        .slider {
            width: 80%;
            height: 15px;
            margin: 10px 0;
        }

        .slider-value {
            font-size: 18px;
            margin-top: 5px;
        }

        .btn-container {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 20px;
        }

        .led-label {
            font-weight: bold;
            margin-top: 10px;
            display: block;
        }

    </style>
</head>
<body>

    <div class="container">
        <h1>Controle de LEDs</h1>

        <!-- Botões de Controle ON/OFF para LEDs -->
        <div class="btn-container">
            <div>
                <span class="led-label">LED 1</span>
                <button id="button1" class="button" onclick="toggleLED(1)">OFF</button>
            </div>
            <div>
                <span class="led-label">LED 2</span>
                <button id="button2" class="button" onclick="toggleLED(2)">OFF</button>
            </div>
            <div>
                <span class="led-label">LED 3</span>
                <button id="button3" class="button" onclick="toggleLED(3)">OFF</button>
            </div>
            <div>
                <span class="led-label">LED 4</span>
                <button id="button4" class="button" onclick="toggleLED(4)">OFF</button>
            </div>
            <div>
                <span class="led-label">LED 5</span>
                <button id="button5" class="button" onclick="toggleLED(5)">OFF</button>
            </div>
            <div>
                <span class="led-label">LED 6</span>
                <button id="button6" class="button" onclick="toggleLED(6)">OFF</button>
            </div>
            <div>
                <span class="led-label">LED 7</span>
                <button id="button7" class="button" onclick="toggleLED(7)">OFF</button>
            </div>
            <div>
                <span class="led-label">LED 8</span>
                <button id="button8" class="button" onclick="toggleLED(8)">OFF</button>
            </div>

            
        </div>

        <!-- Sliders para Controle de Brilho para cada LED -->
        <div class="slider-container">
            <label>Controle de Brilho LED 4 (0-100%)</label>
            <input type="range" class="slider" id="brightnessSlider4" min="0" max="255" value="128" onchange="updateBrightness(4, this.value)">
            <div class="slider-value">Brilho: <span id="brightnessValue4">50%</span></div>
        </div>

        <div class="slider-container">
            <label>Controle de Brilho LED 5 (0-100%)</label>
            <input type="range" class="slider" id="brightnessSlider5" min="0" max="255" value="128" onchange="updateBrightness(5, this.value)">
            <div class="slider-value">Brilho: <span id="brightnessValue5">50%</span></div>
        </div>

        <div class="slider-container">
            <label>Controle de Brilho LED 6 (0-100%)</label>
            <input type="range" class="slider" id="brightnessSlider6" min="0" max="255" value="128" onchange="updateBrightness(6, this.value)">
            <div class="slider-value">Brilho: <span id="brightnessValue6">50%</span></div>
        </div>

        <div class="slider-container">
            <label>Controle de Brilho LED 7 (0-100%)</label>
            <input type="range" class="slider" id="brightnessSlider7" min="0" max="255" value="128" onchange="updateBrightness(7, this.value)">
            <div class="slider-value">Brilho: <span id="brightnessValue7">50%</span></div>
        </div>

        <div class="slider-container">
            <label>Controle de Brilho LED 8 (0-100%)</label>
            <input type="range" class="slider" id="brightnessSlider8" min="0" max="255" value="128" onchange="updateBrightness(8, this.value)">
            <div class="slider-value">Brilho: <span id="brightnessValue8">50%</span></div>
        </div>

    </div>

    <script>
        // Função para alternar os LEDs
        function toggleLED(led) {
            var button = document.getElementById("button" + led);
            var currentState = button.innerHTML;

            if (currentState === "OFF") {
                button.innerHTML = "ON";
                button.style.backgroundColor = "green";
                // Enviar requisição para ligar o LED via URL
                fetch(http://192.168.100.81/on${led})
                    .then(response => response.text())
                    .then(data => console.log(data));
            } else {
                button.innerHTML = "OFF";
                button.style.backgroundColor = "red";
                // Enviar requisição para desligar o LED via URL
                fetch(http://192.168.100.81/off${led})
                    .then(response => response.text())
                    .then(data => console.log(data));
            }
        }

        // Função para converter o valor do slider (0-255) para porcentagem
        function updateBrightness(led, value) {
            // Calcular a porcentagem
            let percentage = Math.round((value / 255) * 100);

            // Atualizar o texto da porcentagem no HTML
            document.getElementById(brightnessValue${led}).textContent = ${percentage}%;

            // Enviar requisição para ajustar o brilho do LED via URL
            fetch(http://192.168.100.81/brightness${led}?value=${value})
                .then(response => response.text())
                .then(data => console.log(data));
        }
    </script>

</body>
</html>
