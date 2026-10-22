
<!DOCTYPE html>
<html lang="uz">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>VYRO — Kino va videolar</title>
<style>
*{box-sizing:border-box}
body{margin:0;background:#10111a;color:white;font-family:Arial,sans-serif;padding-bottom:75px}
header{padding:20px;background:#191a29;display:flex;justify-content:space-between;align-items:center}
.logo{font-size:27px;font-weight:900;color:#ad8aff}
.diamond{background:#29213e;padding:10px;border-radius:12px}
nav{display:flex;gap:9px;padding:12px;overflow:auto}
button{border:0;border-radius:12px;padding:12px;background:#28283b;color:white;font-weight:bold}
button.active,.main{background:#8055f5}
h2{padding:0 15px;font-size:20px}
.hero{margin:12px;padding:22px;border-radius:20px;background:linear-gradient(135deg,#5d32b5,#171a32);min-height:145px}
.hero h2{padding:0;font-size:27px}
.cards{display:grid;grid-template-columns:1fr 1fr;gap:12px;padding:12px}
.card{background:#1b1c2b;border-radius:15px;overflow:hidden}
.poster{height:125px;background:linear-gradient(135deg,#35265f,#1d5671);display:grid;place-items:center;font-size:42px}
.card p{padding:0 10px;font-weight:bold}
.card button{margin:0 8px 10px}
.panel{display:none;padding:12px}
.panel.show{display:block}
.video{background:#1d1e2c;border-radius:16px;padding:16px;margin-bottom:12px}
.bottom{position:fixed;bottom:0;left:0;right:0;background:#191a29;display:flex;justify-content:space-around;padding:12px 3px}
.bottom button{background:transparent;font-size:12px;padding:8px}
.small{color:#bbb;font-size:13px}
</style>
</head>
<body>
<header>
  <div><div class="logo">VYRO ✦</div><div class="small">Kino · Video · Olmos</div></div>
  <div class="diamond">💎 <span id="diamonds">10</span></div>
</header>
<nav>
  <button class="active" onclick="openTab('home',this)">Bosh sahifa</button>
  <button onclick="openTab('movies',this)">Kinolar</button>
  <button onclick="openTab('videos',this)">Videolar</button>
  <button onclick="openTab('wallet',this)">Olmos</button>
</nav>
<section id="home" class="panel show">
  <div class="hero">
    <div>🇺🇿 O‘ZBEKCHA KO‘NGILOCHAR OLAM</div>
    <h2>Ko‘r. Zavqlan. Olmos yig‘!</h2>
    <p>Sevimli kinolaring va qisqa videolaring bir joyda.</p>
    <button class="main" onclick="openTab('videos')">Videolarni ko‘r ▶</button>
  </div>
  <h2>Ommabop bo‘limlar</h2>
  <div class="cards">
    <div class="card"><div class="poster">🎬</div><p>Yangi kinolar</p></div>
    <div class="card"><div class="poster">▶️</div><p>Qisqa videolar</p></div>
    <div class="card"><div class="poster">💎</div><p>Olmos yig‘ish</p></div>
    <div class="card"><div class="poster">🎡</div><p>Charxpalak</p></div>
  </div>
</section>
<section id="movies" class="panel">
  <h2>🎬 Kino olami</h2>
  <p class="small" style="padding:0 12px">Film treylerlari va ruxsat etilgan tomosha manbalari.</p>
  <div class="video"><h3>Yangi filmlar</h3><p>2026-yil filmlari katalogi tez orada qo‘shiladi.</p></div>
  <div class="video"><h3>Sevimli janrlar</h3><p>Komediya · Sarguzasht · Fantastika · Drama</p></div>
</section>
<section id="videos" class="panel">
  <h2>▶️ Qisqa videolar</h2>
  <div class="video"><h3>VYRO sinov videosi</h3><p>Bu hozircha demo post. Haqiqiy video manbasi keyin ulanadi.</p>
    <button onclick="like(this)">♡ Layk <span>0</span></button>
    <button onclick="commentDemo()">💬 Izoh</button>
    <button onclick="savePost(this)">🔖 Saqlash</button>
    <button onclick="sharePost()">↗ Ulashish</button>
  </div>
</section>
<section id="wallet" class="panel">
  <h2>💎 Olmos hamyoni</h2>
  <div class="hero"><h2>💎 <span id="wallet">10</span> olmos</h2><p>Virtual sinov balansi.</p></div>
  <div class="video"><h3>Kunlik tashrif</h3><p>Demo: tugmani bosib sinov olmosi ol.</p><button class="main" onclick="daily()">+5 olmos</button></div>
  <div class="video"><h3>🎡 Charxpalak</h3><p>Sinov rejimida aylantirish 2 olmos turadi.</p><button class="main" onclick="spin()">Aylantirish</button><p id="result"></p></div>
</section>
<div class="bottom">
  <button onclick="openTab('home')">🏠<br>Bosh sahifa</button>
  <button onclick="openTab('movies')">🎬<br>Kino</button>
  <button onclick="openTab('videos')">▶️<br>Video</button>
  <button onclick="openTab('wallet')">💎<br>Olmos</button>
</div>
<script>
let balance=10, dailyUsed=false;
function update(){document.getElementById('diamonds').textContent=balance;document.getElementById('wallet').textContent=balance}
function openTab(id,btn){
 document.querySelectorAll('.panel').forEach(p=>p.classList.remove('show'));
 document.getElementById(id).classList.add('show');
 document.querySelectorAll('nav button').forEach(b=>b.classList.remove('active'));
 if(btn)btn.classList.add('active');
 window.scrollTo(0,0)
}
function like(btn){let s=btn.querySelector('span');let n=Number(s.textContent);s.textContent=n?0:1;btn.firstChild.textContent=n?'♡ Layk ':'♥ Layk '}
function savePost(btn){btn.textContent=btn.textContent.includes('Saqlangan')?'🔖 Saqlash':'✓ Saqlangan'}
function commentDemo(){alert('Izohlar funksiyasi keyingi versiyada serverga ulanadi.')}
function sharePost(){if(navigator.share){navigator.share({title:'VYRO',text:'VYRO dagi videoni ko‘r!',url:location.href})}else{alert('Brauzer menyusidan havolani ulashishing mumkin.')}}
function daily(){if(dailyUsed){alert('Kunlik demo mukofoti olindi.');return}balance+=5;dailyUsed=true;update();alert('5 virtual olmos qo‘shildi!')}
function spin(){if(balance<2){alert('Olmos yetarli emas.');return}balance-=2;let prize=Math.floor(Math.random()*6);balance+=prize;update();document.getElementById('result').textContent='Natija: '+prize+' olmos! (demo)'}
update();
</script>
</body>
</html>
