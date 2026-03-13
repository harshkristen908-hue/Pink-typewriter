<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Birthday Glow Pink Typewriter</title>

<style>
body {
  margin:0;
  padding:0;
  background: linear-gradient(#ffd6e8,#ffe6f0);
  font-family:'Courier New', monospace;
  overflow:hidden;
  transition: background 1s ease;
}

#container{
  display:flex;
  flex-direction:column;
  align-items:center;
  padding:15px;
  height:100vh;
  position:relative;
}

h1{
  color:#d63384;
  margin-bottom:10px;
}

#typing-area{
  width:95%;
  max-width:700px;
  height:50vh;
  background:#fff0f6;
  color:#d63384;
  font-size:18px;
  padding:15px;
  border-radius:10px;
  border:3px solid #ffb6c1;
  outline:none;
  resize:none;
}

button{
  margin:10px 5px;
  padding:10px 20px;
  background:#ff85c0;
  border:none;
  border-radius:5px;
  color:white;
  font-size:16px;
  cursor:pointer;
}

button:hover{
  background:#ff5fa1;
}

.sparkle,.confetti{
  position:absolute;
  pointer-events:none;
  font-size:18px;
}

.sparkle{
  animation:floatUp 2s linear forwards;
}

@keyframes floatUp{
  0%{opacity:1;transform:translateY(0);}
  100%{opacity:0;transform:translateY(-120px);}
}

.confetti{
  animation:fall 3s linear forwards;
}

@keyframes fall{
  0%{top:-10px;opacity:1;}
  100%{top:100vh;opacity:0;}
}

#keyboard{
  margin-top:15px;
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(40px,1fr));
  gap:5px;
  width:95%;
  max-width:700px;
}

.key{
  background:#ffc0d0;
  padding:12px;
  border-radius:5px;
  text-align:center;
  color:white;
  font-weight:bold;
  cursor:pointer;
}

.key:active{
  background:#ff85c0;
}
</style>
</head>

<body>

<div id="container">

<h1>🎂 Birthday Glow Typewriter 🎀</h1>

<textarea id="typing-area" placeholder="Type something magical..."></textarea>

<div>
<button onclick="playBell()">🔔 Bell</button>
<button onclick="celebrate()">🎉 Confetti</button>
<button onclick="saveText()">💾 Save</button>
</div>

<div id="keyboard"></div>

</div>

<audio id="click-sound" src="https://www.soundjay.com/keyboard/typewriter-key-1.mp3"></audio>
<audio id="bell-sound" src="https://www.soundjay.com/keyboard/typewriter-bell-1.mp3"></audio>

<script>

const typingArea = document.getElementById("typing-area");
const keyboard = document.getElementById("keyboard");
const clickSound = document.getElementById("click-sound");
const bellSound = document.getElementById("bell-sound");
const container = document.getElementById("container");

const keys="ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789 ,.!?";

for(let char of keys){
  const key=document.createElement("div");
  key.className="key";
  key.textContent=char;

  key.onclick=()=>{
    typingArea.value+=char;
    playClick();
  }

  keyboard.appendChild(key);
}

function playClick(){
  clickSound.currentTime=0;
  clickSound.play();
  sparkle();
}

function sparkle(){
  const spark=document.createElement("span");
  const icons=["✨","💖","🌸","💫"];
  spark.textContent=icons[Math.floor(Math.random()*icons.length)];
  spark.className="sparkle";

  spark.style.left=Math.random()*90+"%";
  spark.style.top=Math.random()*80+"%";

  container.appendChild(spark);

  setTimeout(()=>spark.remove(),2000);
}

typingArea.addEventListener("keypress",playClick);

function playBell(){
  bellSound.play();
}

function celebrate(){

  for(let i=0;i<40;i++){

    const conf=document.createElement("span");
    const icons=["🎉","✨","💖","🌸"];

    conf.textContent=icons[Math.floor(Math.random()*icons.length)];
    conf.className="confetti";

    conf.style.left=Math.random()*100+"%";

    container.appendChild(conf);

    setTimeout(()=>conf.remove(),3000);
  }
}

function saveText(){

  const text=typingArea.value;

  const blob=new Blob([text],{type:"text/plain"});

  const link=document.createElement("a");

  link.href=URL.createObjectURL(blob);

  link.download="typewriter_text.txt";

  link.click();
}

</script>

</body>
</html>
