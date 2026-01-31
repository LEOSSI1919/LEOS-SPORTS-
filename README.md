<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<title>LEOS Sports | Football 2026</title>
<meta name="viewport" content="width=device-width, initial-scale=1">

<style>
body{margin:0;font-family:Arial;background:#0b0b0b;color:#fff}
header{background:#111;padding:15px;position:sticky;top:0}
header h1{margin:0;color:#00ffcc;font-size:20px}
nav{margin-top:8px}
nav button{background:none;border:none;color:#fff;margin-right:10px;font-size:14px}
nav button:hover{color:#00ffcc}
section{padding:15px;display:none}
section.active{display:block}
.match, .box{background:#1a1a1a;padding:10px;margin-bottom:8px;border-radius:5px}
footer{text-align:center;font-size:12px;color:#aaa;padding:15px}
</style>
</head>

<body>

<header>
<h1>LEOS Sports</h1>
<nav>
<button onclick="show('home')">Home</button>
<button onclick="show('live')">Live</button>
<button onclick="show('standings')">Klasemen</button>
<button onclick="show('fixtures')">Jadwal</button>
<button onclick="show('news')">Berita</button>
</nav>
</header>

<section id="home" class="active">
<div class="box">
<h3>Selamat Datang di LEOS Sports</h3>
<p>Portal sepakbola 2026. Fokus Eropa, Liga Indonesia, Bundesliga, Ligue 1.</p>
</div>
</section>

<section id="live">
<h3>Live Score</h3>
<div id="liveData">Memuat data...</div>
</section>

<section id="standings">
<h3>Klasemen</h3>
<div class="box">
<p>Klasemen liga akan ditampilkan di sini.</p>
<p>(Tahap berikutnya: otomatis via API)</p>
</div>
</section>

<section id="fixtures">
<h3>Jadwal Pertandingan</h3>
<div class="box">
<p>Jadwal pertandingan terbaru.</p>
<p>(Tahap berikutnya: otomatis via API)</p>
</div>
</section>

<section id="news">
<h3>Berita Sepakbola</h3>
<div class="box">Liga Eropa musim 2026 semakin ketat.</div>
<div class="box">Liga 1 Indonesia terus berkembang.</div>
<div class="box">Transfer pemain besar terjadi di Eropa.</div>
</section>

<footer>
© 2026 LEOS Sports
</footer>

<script>
function show(id){
document.querySelectorAll("section").forEach(s=>s.classList.remove("active"));
document.getElementById(id).classList.add("active");
}

const API_KEY="3d2c930b1ae931073c5fb6110d56f22d";

fetch("https://api-football-v1.p.rapidapi.com/v3/fixtures?live=all",{
headers:{
"X-RapidAPI-Key":API_KEY,
"X-RapidAPI-Host":"api-football-v1.p.rapidapi.com"
}})
.then(r=>r.json())
.then(d=>{
let html="";
if(!d.response || d.response.length===0){
html="Tidak ada pertandingan live.";
}else{
d.response.slice(0,10).forEach(m=>{
html+=`<div class="match">
${m.league.name}<br>
${m.teams.home.name}
<b>${m.goals.home} - ${m.goals.away}</b>
${m.teams.away.name}
</div>`;
});
}
document.getElementById("liveData").innerHTML=html;
})
.catch(()=>{
document.getElementById("liveData").innerHTML="Gagal memuat data.";
});
</script>

</body>
</html>
