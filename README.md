<!DOCTYPE html>
<html>
<head>
    <title>Advanced Head & Tail Game</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <style>
        body {
            margin: 0;
            font-family: Arial, sans-serif;
            background: linear-gradient(135deg, #667eea, #764ba2);
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .app {
            background: white;
            width: 320px;
            padding: 20px;
            border-radius: 25px;
            box-shadow: 0 15px 30px rgba(0,0,0,0.2);
            text-align: center;
        }

        h2 {
            margin-bottom: 10px;
        }

        .coin {
            width: 160px;
            height: 160px;
            border-radius: 50%;
            margin: 20px auto;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 26px;
            font-weight: bold;
            color: white;
            transition: transform 0.6s ease-in-out;
        }

        .head {
            background: blue;
        }

        .tail {
            background: pink;
        }

        .spin {
            transform: rotateY(720deg);
        }

        button {
            padding: 10px 15px;
            margin: 5px;
            border: none;
            border-radius: 20px;
            cursor: pointer;
            font-size: 14px;
            font-weight: bold;
        }

        .flip-btn {
            background: #667eea;
            color: white;
        }

        .mode-btn {
            background: #764ba2;
            color: white;
        }

        .reset-btn {
            background: crimson;
            color: white;
        }

        .mode-display {
            margin-top: 10px;
            font-weight: bold;
        }

    </style>
</head>
<body>

<div class="app">
    <h2>Head & Tail Game</h2>

    <div id="coin" class="coin head">HEAD</div>

    <button class="flip-btn" onclick="flipCoin()">Flip</button>
    <button class="mode-btn" onclick="toggleMode()">Switch Mode</button>
    <button class="reset-btn" onclick="resetGame()">Reset</button>

    <div class="mode-display" id="modeDisplay">Mode: Pattern</div>
</div>

<script>
    let pattern = [
        "HEAD","HEAD","HEAD","HEAD","HEAD",
        "TAIL","TAIL","TAIL","TAIL","TAIL",
        "HEAD","HEAD","HEAD","HEAD","HEAD"
    ];

    let index = 0;
    let mode = "pattern"; // pattern or random

    function flipCoin() {
        let coin = document.getElementById("coin");

        coin.classList.add("spin");

        setTimeout(() => {

            let result;

            if (mode === "pattern") {
                if (index >= pattern.length) {
                    index = 0;
                }
                result = pattern[index];
                index++;
            } else {
                result = Math.random() < 0.5 ? "HEAD" : "TAIL";
            }

            if (result === "HEAD") {
                coin.className = "coin head";
                coin.innerText = "HEAD";
            } else {
                coin.className = "coin tail";
                coin.innerText = "TAIL";
            }

            coin.classList.remove("spin");

        }, 600);
    }

    function toggleMode() {
        mode = mode === "pattern" ? "random" : "pattern";
        document.getElementById("modeDisplay").innerText =
            "Mode: " + (mode === "pattern" ? "Pattern" : "Random");
    }

    function resetGame() {
        index = 0;
        document.getElementById("coin").className = "coin head";
        document.getElementById("coin").innerText = "HEAD";
    }
</script>

</body>
</html>
