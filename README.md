<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ALFRED AI</title>

<style>
* {
    box-sizing: border-box;
}

body {
    margin: 0;
    background: #020814;
    color: #00cfff;
    font-family: Arial, sans-serif;
    text-align: center;
}

header {
    padding: 25px;
    font-size: 27px;
    font-weight: bold;
    letter-spacing: 5px;
    text-shadow: 0 0 15px #00cfff;
}

.status {
    color: #00ffb3;
    font-size: 12px;
    letter-spacing: 3px;
}

.core {
    width: 190px;
    height: 190px;
    border: 3px solid #00cfff;
    border-radius: 50%;
    margin: 55px auto 25px;
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: 0 0 25px #008cff,
                inset 0 0 25px #008cff;
    animation: pulse 2s infinite;
}

.core span {
    font-size: 65px;
    text-shadow: 0 0 20px #00cfff;
}

@keyframes pulse {
    50% {
        box-shadow: 0 0 50px #00cfff,
                    inset 0 0 35px #008cff;
    }
}

h2 {
    letter-spacing: 4px;
}

#response {
    min-height: 55px;
    margin: 20px;
    color: #b8eaff;
}

input {
    width: 65%;
    padding: 15px;
    border: 1px solid #00cfff;
    border-radius: 25px;
    background: #07182c;
    color: white;
    outline: none;
}

button {
    padding: 14px 18px;
    margin: 7px;
    border: 1px solid #00cfff;
    border-radius: 25px;
    background: #062746;
    color: #00cfff;
    font-weight: bold;
}

button:active {
    background: #008cff;
    color: white;
}

.panel {
    margin: 25px 15px;
    padding: 15px;
    border: 1px solid #006b99;
    border-radius: 15px;
    background: #061629;
}

footer {
    padding: 25px;
    font-size: 11px;
    color: #527c99;
}
</style>
</head>

<body>

<header>ALFRED AI</header>

<div class="status">● SISTEMA ONLINE</div>

<div class="core">
    <span>◉</span>
</div>

<h2>ALFRED</h2>

<p>Seu assistente pessoal inteligente</p>

<div id="response">
    Olá! Sou ALFRED. Como posso ajudar?
</div>

<div>
    <input id="message"
    placeholder="Digite um comando...">

    <button onclick="sendMessage()">ENVIAR</button>
</div>

<div>
    <button onclick="listen()">🎙 FALAR COM ALFRED</button>
</div>

<div class="panel">
    <h3>PAINEL DO SISTEMA</h3>
    <p>🧠 Inteligência: aguardando conexão</p>
    <p>🎙️ Reconhecimento de voz: disponível quando suportado</p>
    <p>🌐 Internet: disponível</p>
    <p>🤖 Assistente: inicializado</p>
</div>

<footer>
    ALFRED AI — PERSONAL INTELLIGENCE SYSTEM
</footer>

<script>

function speak(text) {
    if (!('speechSynthesis' in window)) return;

    speechSynthesis.cancel();

    let voice = new SpeechSynthesisUtterance(text);
    voice.lang = "pt-BR";
    voice.rate = 0.9;
    voice.pitch = 0.75;

    speechSynthesis.speak(voice);
}

function sendMessage() {

    let input = document.getElementById("message");
    let text = input.value.trim();

    if (!text) return;

    let answer = "Comando recebido. Ainda estou em fase de desenvolvimento. Minha inteligência artificial será conectada em breve.";

    document.getElementById("response").innerText =
        "Você: " + text + "\nALFRED: " + answer;

    speak(answer);

    input.value = "";
}

function listen() {

    const SpeechRecognition =
        window.SpeechRecognition ||
        window.webkitSpeechRecognition;

    if (!SpeechRecognition) {
        alert("Reconhecimento de voz não disponível neste navegador.");
        return;
    }

    let recognition = new SpeechRecognition();

    recognition.lang = "pt-BR";
    recognition.start();

    recognition.onresult = function(event) {
        document.getElementById("message").value =
            event.results[0][0].transcript;

        sendMessage();
    };

    recognition.onerror = function() {
        alert("Não consegui reconhecer sua voz. Tente novamente.");
    };
}

</script>

</body>
</html>