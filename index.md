<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Jeu de Piste de Noël</title>
<style>
 body { font-family: Arial, sans-serif; background:#f6f2ff; margin:0; padding:20px; }
 h1,h2{ color:#b30000; }
 .section { display:none; padding:20px; background:white; border-radius:12px; box-shadow:0 0 10px rgba(0,0,0,0.1); }
 .active { display:block; }
 button{ padding:10px 20px; border:none; background:#b30000; color:white; border-radius:8px; cursor:pointer; margin-top:15px; }
 input{ padding:8px; width:100%; margin-top:10px; }
 .success{ color:green; font-weight:bold; }
 .error{ color:red; }
</style>
<audio id="bgmusic" src="https://cdn.pixabay.com/audio/2022/12/13/audio_0dd8f6d5b8.mp3" autoplay loop></audio>
<script>
window.addEventListener('click',()=>{document.getElementById('bgmusic').play();},{once:true});
</script>
</head>
<body>
<script>
// Countdown per day
function unlockDays(){
 const today=new Date();
 const start=new Date(today.getFullYear(),11,1); // 1 Dec
 const diff=Math.floor((today-start)/86400000)+1;
 for(let i=1;i<=5;i++){
   const btn=document.getElementById('btn'+i);
   if(diff>=i) btn.disabled=false;
 }
}
window.onload=unlockDays;
</script>
<h1>🎄 Jeu de Piste de Noël 🎅</h1>
<p>Bienvenue dans le jeu de piste de Noël ! Complète chaque jour pour avancer.</p>

<!-- Navigation -->
<button id="btn1" onclick="show('j1')">Jour 1</button>
<button id="btn2" onclick="show('j2')" disabled>Jour 2</button>
<button id="btn3" onclick="show('j3')" disabled>Jour 3</button>
<button id="btn4" onclick="show('j4')" disabled>Jour 4</button>
<button id="btn5" onclick="show('j5')" disabled>Jour 5</button>

<!-- JOUR 1 -->
<div id="j1" class="section">
<h2>Jour 1 – L'Énigme d'ouverture</h2>
<p>Qui est l'être barbu préféré des enfants, qui passe parfois par la cheminée ?</p>
<input id="r1" placeholder="Ta réponse...">
<p id="f1"></p>
<button onclick="check('r1','PÈRE NOËL','f1')">Vérifier</button>
</div>

<!-- JOUR 2 -->
<div id="j2" class="section">
<h2>Jour 2 – Les lieux mystères</h2>
<p>Énigme : Je suis l'endroit où tout le monde passe en arrivant. Que suis-je ?</p>
<input id="r2" placeholder="Ta réponse...">
<p id="f2"></p>
<button onclick="checkContains('r2','ACCUEIL','f2')">Vérifier</button>
</div>

<!-- JOUR 3 -->
<div id="j3" class="section">
<h2>Jour 3 – Puzzle & message codé</h2>
<p>Message codé : 🎄❄️🦌🦌❄️✨ – Quel est le mot ?</p>
<input id="r3" placeholder="Ta réponse...">
<p id="f3"></p>
<button onclick="checkContains('r3','RENNES','f3')">Vérifier</button>
</div>

<!-- JOUR 4 -->
<div id="j4" class="section">
<h2>Jour 4 – Le Cadeau Mystère</h2>
<p>Énigme : Mot mélangé « REV ». Remets-le en ordre.</p>
<input id="r4" placeholder="Ta réponse..."><p id="f4"></p>
<button onclick="checkContains('r4','REVE','f4')">Vérifier</button>
</div>

<!-- JOUR 5 -->
<div id="j5" class="section">
<h2>Jour 5 – Le Défi des Sens</h2>
<p>Indice : Parfum chaud, sucré, épicé. Qui suis‑je ?</p>
<input id="r5" placeholder="Ta réponse..."><p id="f5"></p>
<button onclick="checkContains('r5','CANNELLE','f5')">Vérifier</button>
</div>

<script>
function show(id){ document.querySelectorAll('.section').forEach(s=>s.classList.remove('active')); document.getElementById(id).classList.add('active'); }

function normalize(t){ return t.trim().toUpperCase().replace(/[ÉÈÊË]/g,'E').replace(/[ÀÂ]/g,'A').replace(/[ÙÛ]/g,'U').replace(/[Ô]/g,'O'); }

function check(id,correct,fid){ let v=normalize(document.getElementById(id).value); if(v===normalize(correct)){ document.getElementById(fid).innerHTML='<span class="success">✔ Bonne réponse !</span>'; } else { document.getElementById(fid).innerHTML='<span class="error">❌ Mauvaise réponse</span>'; }}

function checkContains(id,correct,fid){ let v=normalize(document.getElementById(id).value); if(v.includes(normalize(correct))){ document.getElementById(fid).innerHTML='<span class="success">✔ Bonne réponse !</span>'; } else { document.getElementById(fid).innerHTML='<span class="error">❌ Essaie encore</span>'; }}
</script>
</body>
</html>
