<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Arcade Portrait</title>

<!-- Google Pixel Arcade Font -->
<link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap" rel="stylesheet">

<style>
  body {
    margin: 0;
    font-family: 'Press Start 2P', cursive;
    background-color: #0d0d0d;
    color: #00ffcc;
    display: flex;
    flex-direction: column;
    height: 100vh;
    background-image: repeating-linear-gradient(
      to bottom,
      rgba(255, 255, 255, 0.02) 0px,
      rgba(255, 255, 255, 0.02) 2px,
      transparent 2px,
      transparent 4px
    );
  }

  header {
    text-align: center;
    padding: 1rem;
    font-size: 1.2rem;
    color: #ff00ff;
    text-shadow: 0 0 10px #ff00ff, 0 0 20px #ff00ff;
  }

  main {
    flex: 1;
    display: flex;
    flex-direction: column;
    padding: 0.5rem;
    gap: 1rem;
    overflow-y: auto;
  }

  .terminal {
    flex: 1;
    background: #000;
    border: 2px solid #00ffcc;
    padding: 1rem;
    overflow-y: auto;
    box-shadow: 0 0 15px #00ffcc;
    font-size: 0.8rem;
    line-height: 1.5;
    white-space: pre-wrap;
  }

  .buttons {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
  }

  .btn {
    background: black;
    color: #fff;
    border: 2px solid #ff00ff;
    padding: 0.8rem;
    text-align: center;
    cursor: pointer;
    transition: all 0.2s ease;
    text-shadow: 0 0 5px #ff00ff;
  }

  .btn:hover {
    background: #ff00ff;
    color: black;
    box-shadow: 0 0 10px #ff00ff, 0 0 20px #ff00ff;
  }
</style>
</head>

<body>
  <header>🎮 RETRO ARCADE 🎮</header>
  <main>
    <div class="terminal" id="terminal">
      WELCOME TO THE ARCADE!<br>
      > Press a button below to start...
    </div>

    <div class="buttons">
      <div class="btn" onclick="runGame()">▶ START GAME</div>
      <div class="btn" onclick="showHelp()">ℹ HELP</div>
      <div class="btn" onclick="clearTerminal()">🗑 CLEAR</div>
    </div>
  </main>

<script>
function addToTerminal(text) {
  const terminal = document.getElementById("terminal");
  terminal.innerHTML += "\n" + text;
  terminal.scrollTop = terminal.scrollHeight;
}

function runGame() {
  addToTerminal("> GAME STARTED! Loading...");
  setTimeout(() => {
    addToTerminal("🚀 You blast off into space!");
  }, 1000);
}

function showHelp() {
  addToTerminal("> HELP: Use the buttons to control the game. Have fun!");
}

function clearTerminal() {
  document.getElementById("terminal").innerHTML = "> Terminal cleared.";
}
</script>

</body>
</html>
