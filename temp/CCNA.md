# CCNA
## Common Port
## IPv6
## TCP
- FTP data (20)
- FTP control (21)
- SSH (22)
- Telnet (23)
- SMTP (25)
- HTTP (80)
- POP3 (110)
- HTTPS (443)

## UDP
- DHCP server (67)
- DHCP client (68)
- TFTP (69)
- SNMP agent (161)
- SNMP manager (162)
- Syslog (514)

## TCP & UDP
- DNS (53)

Here’s a game to help you to remeber the port number

### Updated Code:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Port Number Game</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f9;
      text-align: center;
      margin: 0;
      padding: 0;
    }
    h1, h2 {
      color: #444;
    }
    .game-container {
      max-width: 600px;
      margin: 20px auto;
      padding: 20px;
      background-color: #fff;
      border-radius: 10px;
      box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    }
    .question {
      font-size: 1.5rem;
      margin-bottom: 20px;
    }
    input {
      font-size: 1rem;
      padding: 10px;
      margin: 10px;
      width: 80%;
      border: 2px solid #ddd;
      border-radius: 5px;
    }
    button {
      font-size: 1rem;
      padding: 10px 20px;
      background-color: #007BFF;
      color: #fff;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    button:hover {
      background-color: #0056b3;
    }
    .score {
      margin-top: 20px;
      font-size: 1.2rem;
    }
  </style>
</head>
<body>
  <h1>CCNA Port Number Game</h1>
  <div class="game-container">
    <h2>Common Ports</h2>
    <div class="question" id="question">Loading...</div>
    <input type="text" id="answer" placeholder="Enter name/port & protocol (e.g., SSH TCP)">
    <button onclick="checkAnswer()">Submit</button>
    <div class="score" id="score">Score: 0</div>
  </div>

  <script>
    // Data for the game
    const ports = [
      { name: "FTP data", port: 20, type: "TCP" },
      { name: "FTP control", port: 21, type: "TCP" },
      { name: "SSH", port: 22, type: "TCP" },
      { name: "Telnet", port: 23, type: "TCP" },
      { name: "SMTP", port: 25, type: "TCP" },
      { name: "HTTP", port: 80, type: "TCP" },
      { name: "POP3", port: 110, type: "TCP" },
      { name: "HTTPS", port: 443, type: "TCP" },
      { name: "DHCP server", port: 67, type: "UDP" },
      { name: "DHCP client", port: 68, type: "UDP" },
      { name: "TFTP", port: 69, type: "UDP" },
      { name: "SNMP agent", port: 161, type: "UDP" },
      { name: "SNMP manager", port: 162, type: "UDP" },
      { name: "Syslog", port: 514, type: "UDP" },
      { name: "DNS", port: 53, type: "TCP & UDP" }
    ];

    let currentQuestion = {};
    let score = 0;

    // Function to pick a random question
    function getRandomQuestion() {
      const randomIndex = Math.floor(Math.random() * ports.length);
      currentQuestion = ports[randomIndex];
      const askForPort = Math.random() > 0.5; // Randomly decide to ask for port or name
      return askForPort
        ? `What is the port number for ${currentQuestion.name}?`
        : `What application uses port ${currentQuestion.port}?`;
    }

    // Function to load a new question
    function loadQuestion() {
      document.getElementById("question").textContent = getRandomQuestion();
      document.getElementById("answer").value = ""; // Clear the input
    }

    // Function to check the player's answer
    function checkAnswer() {
      const playerAnswer = document.getElementById("answer").value.trim();
      const correctAnswer =
        currentQuestion.name.toLowerCase() === playerAnswer.split(" ")[0].toLowerCase() ||
        currentQuestion.port.toString() === playerAnswer.split(" ")[0];

      const correctProtocol = currentQuestion.type.toLowerCase() === playerAnswer.split(" ")[1]?.toLowerCase();

      if (correctAnswer && correctProtocol) {
        score++;
        alert("Correct!");
      } else {
        alert(
          `Incorrect! The correct answer is ${currentQuestion.name} ${currentQuestion.port} ${currentQuestion.type}.`
        );
      }

      // Update the score and load a new question
      document.getElementById("score").textContent = `Score: ${score}`;
      loadQuestion();
    }

    // Function to handle "Enter" key press
    document.getElementById("answer").addEventListener("keydown", function(event) {
      if (event.key === "Enter") {
        checkAnswer();
      }
    });

    // Initialize the game
    loadQuestion();
  </script>
</body>
</html>
```

