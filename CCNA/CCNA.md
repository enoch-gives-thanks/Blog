# CCNA
https://stackoverflow.com/questions/14951321/how-to-display-html-content-in-github-readme-md
## Common Port
---

### **TCP**
- **FTP data (20)**: Used for transferring files in active FTP mode.
- **FTP control (21)**: Used for FTP commands and control communication.
- **SSH (22)**: Secure Shell, used for secure remote login and other secure network services.
- **Telnet (23)**: Unencrypted remote login service (largely deprecated due to lack of security).
- **SMTP (25)**: Simple Mail Transfer Protocol, used for sending emails.
- **HTTP (80)**: Hypertext Transfer Protocol, used for unencrypted web traffic.
- **POP3 (110)**: Post Office Protocol version 3, used for retrieving emails from a server.
- **HTTPS (443)**: Hypertext Transfer Protocol Secure, used for encrypted web traffic via SSL/TLS.

---

### **UDP**
- **DHCP server (67)**: Dynamic Host Configuration Protocol for assigning IP addresses (server-side port).
- **DHCP client (68)**: Dynamic Host Configuration Protocol for receiving assigned IP addresses (client-side port).
- **TFTP (69)**: Trivial File Transfer Protocol, used for simple, unsecured file transfer.
- **SNMP agent (161)**: Simple Network Management Protocol, used for monitoring and managing devices.
- **SNMP manager (162)**: Used by SNMP managers to receive traps/alerts from agents.
- **Syslog (514)**: Used for logging system messages in a network.

---

### **TCP & UDP**
- **DNS (53)**: Domain Name System uses:
  - **UDP for queries**: Most DNS queries are transmitted over UDP for efficiency.
  - **TCP for zone transfers or large queries**: Used when data exceeds the UDP size limit (512 bytes traditionally, though larger sizes are supported with EDNS).

---
SNMP over TCP is not the same as SNMPv3. They are two separate concepts.

1. SNMP over TCP:
   - SNMP over TCP refers to the use of TCP (Transmission Control Protocol) as the transport protocol for SNMP communication instead of the standard UDP (User Datagram Protocol).
   - It provides a reliable, connection-oriented communication channel for SNMP messages.
   - SNMP over TCP can be used with any version of SNMP (v1, v2c, or v3).
   - The default TCP port for SNMP over TCP is not officially assigned by IANA (Internet Assigned Numbers Authority). However, some implementations use TCP port 161 for agent-to-manager communication and TCP port 162 for manager-to-agent communication (trap messages).

2. SNMPv3:
   - SNMPv3 is version 3 of the SNMP protocol, which introduces enhanced security features compared to previous versions (SNMPv1 and SNMPv2).
   - It provides authentication, encryption, and access control mechanisms to ensure secure communication between SNMP managers and agents.
   - SNMPv3 operates independently of the transport protocol and can work with either UDP or TCP.
   - When using SNMPv3 over UDP (the most common approach), it uses UDP port 161 for agent-to-manager communication and UDP port 162 for manager-to-agent communication (trap messages).

So, to answer your question directly:
- SNMP over TCP is not the same as SNMPv3. SNMP over TCP refers to the transport protocol used, while SNMPv3 refers to the version of the SNMP protocol itself.
- When using SNMP over TCP, the commonly used ports are TCP port 161 for agent-to-manager communication and TCP port 162 for manager-to-agent communication (trap messages). However, these ports are not officially assigned and may vary depending on the specific implementation.

It's important to note that SNMP over UDP remains the most widely used and standard approach for SNMP communication. SNMP over TCP is less common and not supported by all SNMP implementations.
### Notes:
1. The port numbers and protocols you've listed are correct and standard according to IANA (Internet Assigned Numbers Authority).  
2. **DNS (53)** is indeed used with both TCP and UDP, depending on the use case.  
3. Consider adding more context or examples if teaching or learning. For instance:
   - Mention that **SMTP (25)** is often blocked by ISPs for outgoing emails and replaced by ports like **587** or **465** (SMTP with SSL/TLS).
   - Explain that **Telnet (23)** is largely replaced by **SSH (22)** for security reasons.

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

## IPv6
Your information is **mostly correct**, but there are a few points that can be clarified or expanded upon. Here's the corrected and verified list:
