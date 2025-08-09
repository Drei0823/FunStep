<script>
const correctAnswers = {
  // ... (keep your same question set)
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

function normalize(str) {
  return str
    .toLowerCase()
    .replace(/\s+/g, " ")
    .replace(/≥/g, ">=")
    .replace(/≤/g, "<=")
    .trim();
}

function printWelcome() {
  appendLine("Welcome to FunStep!");
  appendLine("Step 1: Type the card number to see the question.");
  appendLine("Step 2: Type the answer.");
}

function handleCardNumber(input) {
  const num = parseInt(input);
  if (isNaN(num)) {
    appendLine(`❌ Please enter a valid card number.`);
    return;
  }
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
  const answer = normalize(input);
  const validAnswers = correctAnswers[currentCard].answers.map(a => normalize(a));
  
  if (validAnswers.includes(answer)) {
    appendLine("✅ Correct!");
  } else {
    appendLine(`❌ Wrong. Correct answer(s): ${correctAnswers[currentCard].answers.join(" or ")}`);
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
