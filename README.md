Sorin studio filme și povestei bine ai venit în Sorin studio o poveste o legenda HTML

<!DOCTYPE html>
<html lang="ro">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Sorin Studio - Filme și Povești</title>
<style>
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #101426;
  color: white;
  text-align: center;
}
header {
  background: #202b50;
  padding: 25px 10px;
}
h1 { color: #ffd166; }
main {
  padding: 20px;
  max-width: 650px;
  margin: auto;
}
button {
  background: #e6a23c;
  color: #171717;
  border: none;
  padding: 13px 18px;
  margin: 6px;
  border-radius: 9px;
  font-size: 16px;
  cursor: pointer;
}
textarea, input {
  width: 95%;
  box-sizing: border-box;
  padding: 12px;
  margin: 10px 0;
  border-radius: 8px;
  font-size: 16px;
}
textarea { min-height: 180px; }
.card {
  background: #202b50;
  padding: 18px;
  margin: 15px 0;
  border-radius: 12px;
}
</style>
</head>
<body>

<header>
<h1>🎬 Sorin Studio</h1>
<p>Filme și Povești</p>
<p>Bine ai venit în studioul tău!</p>
</header>

<main>
<div class="card">
<h2>📖 Creează o poveste</h2>
<input id="titlu" placeholder="Titlul poveștii">
<textarea id="poveste" placeholder="Scrie povestea ta aici..."></textarea>
<button onclick="salveaza()">💾 Salvează povestea</button>
<button onclick="citeste()">🔊 Ascultă povestea</button>
</div>

<div class="card">
<h2>🎥 Studioul de filme</h2>
<p>Pregătește scenariul filmului tău aici.</p>
<textarea id="film" placeholder="Scrie scenele și dialogurile filmului..."></textarea>
<button onclick="salveazaFilm()">Salvează scenariul</button>
</div>

<div class="card">
<h2>📚 Poveștile mele</h2>
<div id="lista">Poveștile salvate vor apărea aici.</div>
</div>
</main>

<script>
function salveaza() {
  let titlu = document.getElementById("titlu").value;
  let text = document.getElementById("poveste").value;
  if (!text.trim()) {
    alert("Scrie mai întâi povestea!");
    return;
  }
  let lista = JSON.parse(localStorage.getItem("povesti") || "[]");
  lista.push({titlu: titlu || "Poveste fără titlu", text: text});
  localStorage.setItem("povesti", JSON.stringify(lista));
  afiseaza();
  alert("Poveste salvată!");
}
function afiseaza() {
  let lista = JSON.parse(localStorage.getItem("povesti") || "[]");
  document.getElementById("lista").innerHTML = "";
  lista.forEach(function(p) {
    let div = document.createElement("p");
    div.textContent = p.titlu;
    document.getElementById("lista").appendChild(div);
  });
}
function citeste() {
  let text = document.getElementById("poveste").value;
  if (!text.trim()) {
    alert("Scrie mai întâi povestea!");
    return;
  }
  let voce = new SpeechSynthesisUtterance(text);
  voce.lang = "ro-RO";
  speechSynthesis.speak(voce);
}
function salveazaFilm() {
  let text = document.getElementById("film").value;
  if (!text.trim()) {
    alert("Scrie mai întâi scenariul!");
    return;
  }
  localStorage.setItem("scenariuFilm", text);
  alert("Scenariul filmului a fost salvat!");
}
afiseaza();
</script>

</body>
</html>
