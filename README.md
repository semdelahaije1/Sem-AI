# Sem-AI
een ai gemaakt door Sem de la Haije

<!DOCTYPE html>
<html lang="nl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Sem AI</title>
  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #0b0b12;
      color: #f5f5ff;
      min-height: 100vh;
      display: flex;
      justify-content: center;
    }

    .app {
      width: 100%;
      max-width: 850px;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      padding: 24px;
    }

    header {
      display: flex;
      align-items: center;
      gap: 12px;
      padding: 10px 0 22px;
      border-bottom: 1px solid #252538;
    }

    .logo {
      width: 45px;
      height: 45px;
      border-radius: 15px;
      display: grid;
      place-items: center;
      font-size: 23px;
      font-weight: bold;
      background: linear-gradient(135deg, #8065ff, #28c9ff);
    }

    h1 {
      font-size: 22px;
      margin: 0 0 5px;
    }

    .status {
      color: #a4a4bb;
      font-size: 13px;
    }

    .status span {
      color: #56e39b;
    }

    #chat {
      flex: 1;
      padding: 28px 0;
      display: flex;
      flex-direction: column;
      gap: 18px;
    }

    .welcome {
      text-align: center;
      margin: auto 0;
      padding: 30px 10px;
    }

    .welcome .big-logo {
      font-size: 48px;
      margin-bottom: 15px;
    }

    .welcome h2 {
      font-size: 29px;
      margin: 0 0 10px;
    }

    .welcome p {
      color: #a4a4bb;
      line-height: 1.6;
    }

    .message {
      max-width: 82%;
      padding: 14px 17px;
      border-radius: 18px;
      line-height: 1.6;
      overflow-wrap: anywhere;
      white-space: pre-wrap;
    }

    .user {
      align-self: flex-end;
      background: linear-gradient(135deg, #7158e8, #5141b5);
      border-bottom-right-radius: 5px;
    }

    .bot {
      align-self: flex-start;
      background: #191927;
      border: 1px solid #29293e;
      border-bottom-left-radius: 5px;
    }

    .label {
      display: block;
      font-size: 11px;
      color: #bdb5ff;
      margin-bottom: 6px;
      font-weight: bold;
    }

    .composer {
      border: 1px solid #34344b;
      background: #151521;
      border-radius: 20px;
      padding: 10px;
      display: flex;
      gap: 10px;
      box-shadow: 0 8px 35px #0003;
    }

    #bericht {
      flex: 1;
      min-width: 0;
      padding: 12px;
      border: 0;
      outline: 0;
      background: transparent;
      color: white;
      font-size: 16px;
    }

    #bericht::placeholder {
      color: #85859e;
    }

    button {
      border: 0;
      border-radius: 14px;
      padding: 0 20px;
      color: white;
      font-size: 15px;
      font-weight: bold;
      cursor: pointer;
      background: linear-gradient(135deg, #8065ff, #388bff);
    }

    button:hover {
      filter: brightness(1.12);
    }

    button:disabled {
      opacity: 0.5;
      cursor: not-allowed;
    }

    .hint {
      text-align: center;
      color: #77778f;
      font-size: 12px;
      padding: 12px 0 0;
    }

    @media (max-width: 500px) {
      .app {
        padding: 16px;
      }

      .message {
        max-width: 92%;
      }

      .welcome h2 {
        font-size: 25px;
      }

      button {
        padding: 0 14px;
      }
    }
  </style>
</head>

<body>
  <main class="app">
    <header>
      <div class="logo">S</div>
      <div>
        <h1>Sem AI</h1>
        <div class="status"><span>●</span> Jouw eigen chatbot</div>
      </div>
    </header>

    <section id="chat" aria-live="polite">
      <div class="welcome" id="welkom">
        <div class="big-logo">✦</div>
        <h2>Hoi! Ik ben Sem AI.</h2>
        <p>Stel me een vraag en we gaan aan de slag.</p>
      </div>
    </section>

    <form class="composer" id="chat-form">
      <input
        id="bericht"
        type="text"
        placeholder="Stel een vraag aan Sem AI..."
        autocomplete="off"
        maxlength="2000"
        required
      >
      <button id="verzend" type="submit">Stuur ↑</button>
    </form>

    <div class="hint">
      Sem AI is nog in ontwikkeling.
    </div>
  </main>

  <script>
    const form = document.querySelector("#chat-form");
    const input = document.querySelector("#bericht");
    const chat = document.querySelector("#chat");
    const knop = document.querySelector("#verzend");

    function voegBerichtToe(naam, tekst, soort) {
      const bericht = document.createElement("div");
      bericht.className = `message ${soort}`;

      const label = document.createElement("span");
      label.className = "label";
      label.textContent = naam;

      const inhoud = document.createElement("div");
      inhoud.textContent = tekst;

      bericht.append(label, inhoud);
      chat.appendChild(bericht);

      return bericht;
    }

    function geefAntwoord(bericht) {
      const tekst = bericht.toLowerCase();

      if (/\b(hallo|hoi|hey|heyy|hi)\b/.test(tekst)) {
        return "Hoi! 👋 Welkom bij Sem AI. Waarmee kan ik je helpen?";
      }

      if (tekst.includes("hoe gaat het")) {
        return "Bedankt voor het vragen! 😄 Ik ben klaar om je te helpen. Hoe gaat het met jou?";
      }

      if (
        tekst.includes("wie ben je") ||
        tekst.includes("jouw naam") ||
        tekst.includes("wie heeft je gemaakt")
      ) {
        return "Ik ben Sem AI, een chatbot die door Sem is gemaakt! 🚀";
      }

      if (tekst.includes("wat kun je")) {
        return "Ik kan momenteel reageren op een aantal vragen. Mijn maker is bezig om mij slimmer te maken!";
      }

      if (
        tekst.includes("hoofdstad van frankrijk")
      ) {
        return "De hoofdstad van Frankrijk is Parijs. 🇫🇷";
      }

      if (tekst.includes("1+1") || tekst.includes("1 + 1")) {
        return "1 + 1 = 2! 🧮";
      }

      if (tekst.includes("bedankt") || tekst.includes("dank je")) {
        return "Graag gedaan! 😊";
      }

      if (tekst.includes("grap")) {
        return "Waarom neemt een computer nooit vakantie? Omdat hij bang is om zijn werkgeheugen te verliezen! 😂";
      }

      return "Goede vraag! Ik weet daar nog niet genoeg over. Ik ben op dit moment een eenvoudige chatbot. Later kunnen we mij verbinden met een echte AI-dienst! 🧠";
    }

    form.addEventListener("submit", function(event) {
      event.preventDefault();

      const tekst = input.value.trim();

      if (!tekst) return;

      const welkom = document.querySelector("#welkom");
      if (welkom) welkom.remove();

      voegBerichtToe("Jij", tekst, "user");
      input.value = "";
      knop.disabled = true;

      const antwoord = geefAntwoord(tekst);
      voegBerichtToe("Sem AI", antwoord, "bot");

      knop.disabled = false;
      input.focus();

      chat.scrollTop = chat.scrollHeight;
    });
  </script>
</body>
</html>

