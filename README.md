<script>
const correctAnswers = { 
  /* keep your same card data here */ 
};

let currentCard = null;
let waitingForAnswer = false;

const terminal = document.getElementById("terminal");
const termInput = document.getElementById("termInput");

function appendLine(text) {
  const div = document.createElement("div");
  div.textContent = text;
  terminal.appendChild(div);
  terminal.scrollTop = terminal.scrollHeight;
}

function printWelcome() {
  appendLine("Welcome to FunStep!");
  appendLine("Step 1: Type the card number to see the question.");
  appendLine("Step 2: Type the answer exactly as it should be.");
}

function handleCardNumber(input) {
  if (!/^\d+$/.test(input)) {
    appendLine("❌ Please enter a valid card number.");
    return;
  }
  const num = parseInt(input, 10);
  if (!correctAnswers[num]) {
    appendLine(`❌ Card ${num} not found.`);
    return;
  }
  currentCard = num;
  waitingForAnswer = true;
  appendLine(`📜 Card ${num}: ${correctAnswers[num].question}`);
  appendLine("Now type your answer:");
  termInput.placeholder = "Type your answer";
}

function handleAnswer(input) {
  const answer = input.trim().toLowerCase();
  const validAnswers = correctAnswers[currentCard].answers.map(a => a.toLowerCase());

  if (validAnswers.includes(answer)) {
    appendLine("✅ Correct!");
  } else {
    appendLine("❌ Wrong.");
  }

  waitingForAnswer = false;
  currentCard = null;
  appendLine("Type another card number to continue.");
  termInput.placeholder = "Type card number first";
}

function sendCommand() {
  const value = termInput.value.trim();
  if (!value) return;
  appendLine("> " + value);

  if (!waitingForAnswer) {
    handleCardNumber(value);
  } else {
    handleAnswer(value);
  }
  termInput.value = "";
}

termInput.addEventListener("keydown", e => {
  if (e.key === "Enter") sendCommand();
});

printWelcome();
</script>
