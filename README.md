# Pro-Packs-26
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover, user-scalable=no">
<title>FC 25 Ultimate Opener</title>
<link href="https://fonts.googleapis.com/css2?family=Oswald:wght@400;700&family=Outfit:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #0f141e; --dark: #07090d;
  --accent: #3bf6ff; --purple: #6e45ff;
  --card-w: 160px; --card-h: 240px; /* Bigger cards for stats */
}
* { box-sizing: border-box; -webkit-tap-highlight-color: transparent; user-select: none; }
body { margin: 0; background: radial-gradient(circle at 50% 0%, #1e2a45, #0a0e14 80%); 
       font-family: 'Outfit', sans-serif; color: #fff; min-height: 100vh; padding-bottom: 90px; }

/* LAYOUT */
.topbar { position: fixed; top: 0; left:0; right:0; padding: 15px 20px; background: rgba(15,20,30,0.95); backdrop-filter: blur(10px); z-index: 50; display: flex; justify-content: space-between; border-bottom: 1px solid rgba(255,255,255,0.1); }
.brand { font-family: 'Oswald'; font-size: 22px; letter-spacing: 1px; }
.brand span { color: var(--accent); }
.coins { background: rgba(0,0,0,0.4); padding: 5px 12px; border-radius: 20px; font-weight: 700; color: #ffd700; border: 1px solid rgba(255,215,0,0.3); }

/* VIEWS */
.view { display: none; padding: 80px 20px 20px; max-width: 1000px; margin: 0 auto; animation: fade 0.3s; }
.view.active { display: block; }
@keyframes fade { from {opacity:0; transform:translateY(10px);} to {opacity:1; transform:translateY(0);} }

/* STORE */
.pack-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(160px, 1fr)); gap: 15px; }
.pack { background: linear-gradient(145deg, #1c2533, #111); border: 1px solid rgba(255,255,255,0.1); border-radius: 12px; padding: 15px; text-align: center; cursor: pointer; transition: 0.2s; position: relative; overflow: hidden; }
.pack:hover { border-color: var(--accent); transform: translateY(-5px); }
.pack-img { height: 100px; background: radial-gradient(circle, #444, #111); margin-bottom: 10px; border-radius: 8px; display: flex; align-items: center; justify-content: center; font-family: 'Oswald'; font-size: 36px; color: rgba(255,255,255,0.1); }
.pack h3 { margin: 5px 0; font-size: 16px; }
.price { color: #ffd700; font-weight: 700; font-size: 14px; background: rgba(0,0,0,0.5); padding: 4px 8px; border-radius: 6px; display: inline-block; }

/* FUT CARD DESIGN */
.card {
  width: var(--card-w); height: var(--card-h); position: relative; margin: 8px; display: inline-block;
  background: #222; border: 2px solid #aaa; 
  clip-path: polygon(20% 0, 80% 0, 100% 20%, 100% 100%, 0 100%, 0 20%);
  border-radius: 0 0 15px 15px; cursor: pointer; transition: 0.2s; box-shadow: 0 5px 15px rgba(0,0,0,0.5);
}
.card:hover { transform: scale(1.05); z-index: 10; }

/* Rarity Backgrounds */
.c-gold { background: radial-gradient(ellipse at center, #f5d878, #a07e32); border-color: #f7e199; color: #3e3012; }
.c-silver { background: radial-gradient(ellipse at center, #e6e6e6, #949494); border-color: #fff; color: #222; }
.c-bronze { background: radial-gradient(ellipse at center, #e8b382, #7d5032); border-color: #e8b382; color: #381e10; }
.c-icon { background: linear-gradient(135deg, #fff, #d4c08b); border-color: #bfa567; color: #57461f; }
.c-totw { background: #000; border-color: #ffd700; color: #ffd700; }
.c-totw .name { color: #ffd700; border-color: rgba(255,215,0,0.3); }

/* Card Elements */
.c-top { position: absolute; top: 18px; left: 14px; line-height: 1; text-align: center; }
.ovr { font-family: 'Oswald'; font-size: 34px; font-weight: 700; border-bottom: 1px solid rgba(0,0,0,0.2); padding-bottom: 2px; margin-bottom: 2px; }
.pos { font-size: 12px; font-weight: 700; margin-bottom: 4px; }
.nat { font-size: 20px; }

.p-img { position: absolute; top: 35px; right: 8px; width: 90px; height: 95px; object-fit: contain; filter: drop-shadow(4px 4px 4px rgba(0,0,0,0.3)); }

.p-info { position: absolute; bottom: 0; width: 100%; height: 85px; text-align: center; }
.name { font-family: 'Oswald'; font-size: 16px; text-transform: uppercase; font-weight: 700; border-bottom: 1px solid rgba(0,0,0,0.1); margin: 0 12px 4px; white-space: nowrap; overflow: hidden; }
.club { font-size: 10px; font-weight: 600; text-transform: uppercase; opacity: 0.8; margin-bottom: 6px; }

/* STATS GRID */
.stats { display: grid; grid-template-columns: 1fr 1fr; gap: 0 8px; font-family: 'Outfit'; font-size: 10px; padding: 0 16px; font-weight: 700; opacity: 0.9; text-align: left; }
.stat-row { display: flex; justify-content: space-between; }
.s-lbl { opacity: 0.7; }

/* ANIMATION OVERLAY */
.overlay { position: fixed; inset: 0; background: #000; z-index: 100; display: none; align-items: center; justify-content: center; flex-direction: column; }
.overlay.active { display: flex; }
.flare { width: 1px; height: 1px; box-shadow: 0 0 400px 200px var(--accent); opacity: 0; transition: 1s; }
.flare.boom { opacity: 1; }
.walkout { transform: scale(0.1); opacity: 0; transition: 0.8s cubic-bezier(0.175, 0.885, 0.32, 1.275); }
.walkout.show { transform: scale(1.6); opacity: 1; }
.results { display: none; width: 100%; height: 100%; background: rgba(10,14,20,0.95); overflow-y: auto; padding: 80px 20px; text-align: center; }
.results.show { display: block; }
.btn-grp { position: fixed; bottom: 20px; display: flex; gap: 10px; z-index: 101; }
.btn { padding: 12px 24px; border-radius: 30px; border: none; font-weight: 700; cursor: pointer; }
.btn-primary { background: var(--accent); color: #000; }
.btn-danger { background: #ff4757; color: #fff; }

/* NAV */
.nav { position: fixed; bottom: 20px; left: 50%; transform: translateX(-50%); background: #1c2533; padding: 5px; border-radius: 30px; display: flex; gap: 5px; border: 1px solid rgba(255,255,255,0.1); z-index: 40; }
.nav-item { padding: 10px 20px; border-radius: 25px; color: #888; font-weight: 600; font-size: 13px; cursor: pointer; }
.nav-item.active { background: var(--accent); color: #000; }

/* SQUAD BUILDER */
.pitch { background: linear-gradient(#2e5c32, #244b28); height: 500px; border-radius: 10px; border: 3px solid rgba(255,255,255,0.2); position: relative; margin-top: 20px; }
.slot { width: 70px; height: 90px; background: rgba(0,0,0,0.3); border: 2px dashed rgba(255,255,255,0.2); position: absolute; transform: translate(-50%, -50%); border-radius: 5px; display: flex; align-items: center; justify-content: center; font-size: 12px; font-weight: 700; color: rgba(255,255,255,0.5); cursor: pointer; }
.slot:hover { border-color: var(--accent); }
.slot .card { transform: scale(0.45); margin: 0; pointer-events: none; }
</style>
</head>
<body>

<div class="topbar">
  <div class="brand">FC <span>25</span></div>
  <div class="coins">🪙 <span id="ui-coins">0</span></div>
</div>

<div id="v-store" class="view active">
  <h2 style="margin-top:0">Store</h2>
  <div class="pack-grid" id="pack-list"></div>
</div>

<div id="v-club" class="view">
  <div style="display:flex; justify-content:space-between; align-items:center;">
    <h2>My Club (<span id="club-count">0</span>)</h2>
    <button class="btn btn-danger" style="padding:8px 16px; font-size:12px;" onclick="game.qsAll()">QS All</button>
  </div>
  <div id="club-grid" style="display:flex; flex-wrap:wrap; justify-content:center;"></div>
</div>

<div id="v-squad" class="view">
  <h2>Squad Builder (4-4-2)</h2>
  <div class="pitch" id="pitch"></div>
  <button class="btn btn-danger" style="width:100%; margin-top:10px" onclick="game.clearSquad()">Clear Squad</button>
</div>

<div class="overlay" id="overlay">
  <div class="flare" id="flare"></div>
  <div class="walkout" id="walkout-stage"></div>
  <div class="results" id="results-screen">
    <h2>Pack Result</h2>
    <div id="new-cards" style="display:flex; flex-wrap:wrap; justify-content:center; gap:10px; margin-bottom: 60px;"></div>
    <div class="btn-grp">
      <button class="btn btn-primary" onclick="game.store()">Send to Club</button>
      <button class="btn btn-danger" onclick="game.qs()">Quick Sell (<span id="qs-val">0</span>)</button>
    </div>
  </div>
</div>

<div class="nav">
  <div class="nav-item active" onclick="game.nav('store')">Store</div>
  <div class="nav-item" onclick="game.nav('club')">Club</div>
  <div class="nav-item" onclick="game.nav('squad')">Squad</div>
</div>

<script>
/* --- 1. PLAYER DATABASE & STAT GENERATOR --- */
const DB = [];

// Helper to calculate stats based on Position & Overall
const getStats = (ovr, pos) => {
  const r = (min, max) => Math.floor(Math.random() * (max - min + 1) + min);
  let s = { pac:0, sho:0, pas:0, dri:0, def:0, phy:0 };
  
  // Random variance relative to rating
  const base = ovr; 
  
  if (pos === 'GK') {
    // Goalkeeper: PAC=DIV, SHO=HAN, PAS=KIC, DRI=REF, DEF=SPD, PHY=POS
    s.pac = r(base-5, base+2); // DIV
    s.sho = r(base-5, base+2); // HAN
    s.pas = r(base-10, base+5); // KIC
    s.dri = r(base-5, base+5); // REF
    s.def = r(30, 60);         // SPD
    s.phy = r(base-10, base);  // POS
  } else if (['ST','CF','RW','LW','RF','LF'].includes(pos)) {
    // Attackers
    s.pac = r(base-5, 99); s.sho = r(base-5, base+2); s.pas = r(base-15, base-5);
    s.dri = r(base-5, base+2); s.def = r(30, 55); s.phy = r(60, 85);
  } else if (['CM','CAM','CDM','LM','RM'].includes(pos)) {
    // Midfielders
    s.pac = r(65, 85); s.sho = r(60, 80); s.pas = r(base-2, base+3);
    s.dri = r(base-5, base+2); s.def = r(55, 75); s.phy = r(60, 80);
  } else {
    // Defenders
    s.pac = r(60, 85); s.sho = r(40, 60); s.pas = r(60, 80);
    s.dri = r(60, 75); s.def = r(base-3, base+2); s.phy = r(base-5, base+3);
  }
  return s;
};

const add = (club, league, players) => {
  players.forEach(p => {
    const stats = getStats(p[1], p[2]);
    DB.push({
      name: p[0], ovr: p[1], pos: p[2], nat: p[3], type: p[4]||'gold', club: club, league: league, stats: stats
    });
  });
};

// --- DATABASE LOADING (Hardcoded Clubs) ---
const PL = "Premier League";
add("Man City", PL, [["Haaland",91,"ST","🇳🇴"],["De Bruyne",90,"CM","🇧🇪"],["Rodri",89,"CDM","🇪🇸"],["Foden",88,"RW","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Dias",88,"CB","🇵🇹"],["Ederson",88,"GK","🇧🇷"],["Silva",87,"CM","🇵🇹"],["Gvardiol",86,"LB","🇭🇷"]]);
add("Arsenal", PL, [["Odegaard",89,"CM","🇳🇴"],["Saka",89,"RW","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Saliba",88,"CB","🇫🇷"],["Rice",88,"CDM","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Gabriel",87,"CB","🇧🇷"],["Raya",86,"GK","🇪🇸"],["Havertz",85,"ST","🇩🇪"],["Calafiori",84,"LB","🇮🇹"]]);
add("Liverpool", PL, [["Salah",90,"RW","🇪🇬"],["Alisson",89,"GK","🇧🇷"],["Van Dijk",89,"CB","🇳🇱"],["Mac Allister",86,"CM","🇦🇷"],["Trent AA",86,"RB","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Diaz",85,"LW","🇨🇴"]]);
add("Man Utd", PL, [["Fernandes",87,"CAM","🇵🇹"],["Martinez",84,"CB","🇦🇷"],["De Ligt",84,"CB","🇳🇱"],["Rashford",83,"LW","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Onana",83,"GK","🇨🇲"],["Mainoo",82,"CM","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Yoro",79,"CB","🇫🇷","silver"]]);
add("Chelsea", PL, [["Palmer",86,"CAM","🏴󠁧󠁢󠁥󠁮󠁧󠁿","totw"],["James",84,"RB","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Nkunku",84,"CF","🇫🇷"],["Caicedo",83,"CDM","🇪🇨"],["Neto",82,"LW","🇵🇹"],["Sancho",82,"LW","🏴󠁧󠁢󠁥󠁮󠁧󠁿"]]);
add("Spurs", PL, [["Son",87,"LW","🇰🇷"],["Maddison",85,"CAM","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Romero",85,"CB","🇦🇷"],["Van de Ven",83,"CB","🇳🇱"]]);
add("Newcastle", PL, [["Isak",85,"ST","🇸🇪"],["Guimaraes",85,"CM","🇧🇷"],["Gordon",84,"LW","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Tonali",84,"CDM","🇮🇹"]]);
add("Aston Villa", PL, [["Martinez",87,"GK","🇦🇷"],["Watkins",85,"ST","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["McGinn",83,"CM","🏴󠁧󠁢󠁳󠁣󠁴󠁿"],["Onana",80,"CDM","🇧🇪"]]);
add("West Ham", PL, [["Bowen",83,"RW","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Paqueta",84,"CAM","🇧🇷"],["Kudus",83,"RW","🇬🇭"]]);

const ES = "La Liga";
add("Real Madrid", ES, [["Mbappe",91,"ST","🇫🇷"],["Bellingham",90,"CAM","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Vinicius",90,"LW","🇧🇷"],["Courtois",89,"GK","🇧🇪"],["Valverde",88,"CM","🇺🇾"],["Rudiger",87,"CB","🇩🇪"],["Endrick",79,"ST","🇧🇷","silver"]]);
add("Barcelona", ES, [["Lewandowski",88,"ST","🇵🇱"],["Ter Stegen",88,"GK","🇩🇪"],["Pedri",86,"CM","🇪🇸"],["De Jong",86,"CM","🇳🇱"],["Yamal",83,"RW","🇪🇸","totw"],["Olmo",84,"CAM","🇪🇸"],["Raphinha",85,"LW","🇧🇷"]]);
add("Atletico", ES, [["Griezmann",88,"ST","🇫🇷"],["Oblak",88,"GK","🇸🇮"],["Alvarez",86,"ST","🇦🇷"],["De Paul",84,"CM","🇦🇷"]]);

const DE = "Bundesliga";
add("Bayern", DE, [["Kane",90,"ST","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Musiala",88,"CAM","🇩🇪"],["Neuer",87,"GK","🇩🇪"],["Kimmich",87,"CDM","🇩🇪"],["Olise",84,"RW","🇫🇷"]]);
add("Leverkusen", DE, [["Wirtz",88,"CAM","🇩🇪"],["Xhaka",85,"CM","🇨🇭"],["Grimaldo",86,"LB","🇪🇸"],["Frimpong",85,"RWB","🇳🇱"]]);

const IT = "Serie A";
add("Inter", IT, [["Lautaro",89,"ST","🇦🇷"],["Barella",87,"CM","🇮🇹"],["Bastoni",86,"CB","🇮🇹"],["Thuram",85,"ST","🇫🇷"]]);
add("Milan", IT, [["Leao",87,"LW","🇵🇹"],["Theo",86,"LB","🇫🇷"],["Maignan",87,"GK","🇫🇷"],["Pulisic",84,"RW","🇺🇸"]]);
add("Juventus", IT, [["Vlahovic",84,"ST","🇷🇸"],["Bremer",85,"CB","🇧🇷"],["Luiz",84,"CM","🇧🇷"]]);
add("Napoli", IT, [["Kvara",86,"LW","🇬🇪"],["Lukaku",84,"ST","🇧🇪"],["McTominay",81,"CM","🏴󠁧󠁢󠁳󠁣󠁴󠁿"]]);

const FR = "Ligue 1";
add("PSG", FR, [["Dembele",86,"RW","🇫🇷"],["Donnarumma",87,"GK","🇮🇹"],["Marquinhos",87,"CB","🇧🇷"],["Hakimi",86,"RB","🇲🇦"],["Vitinha",85,"CM","🇵🇹"]]);

const PT = "Liga Portugal";
add("Sporting", PT, [["Gyokeres",85,"ST","🇸🇪","totw"],["Goncalves",82,"LW","🇵🇹"]]);
add("Benfica", PT, [["Di Maria",84,"RW","🇦🇷"],["Otamendi",81,"CB","🇦🇷"]]);
add("Porto", PT, [["Costa",84,"GK","🇵🇹"]]);

/* --- 2. GAME ENGINE --- */
const store = {
  get: k => JSON.parse(localStorage.getItem('fc25_'+k)) || null,
  set: (k,v) => localStorage.setItem('fc25_'+k, JSON.stringify(v))
};
let state = store.get('data') || { coins: 5000, club: [], squad: {} };
const packs = {
  bronze: {id:'bronze', title:'Bronze Pack', price:500, count:12, min:60, max:74},
  gold: {id:'gold', title:'Gold Pack', price:7500, count:12, min:75, max:86},
  promo: {id:'promo', title:'Ultimate Pack', price:25000, count:20, min:82, max:99},
  league_pl: {id:'league_pl', title:'PL Prime Pack', price:15000, count:6, min:80, max:99, filter:'Premier League'}
};

const game = {
  init: () => {
    document.getElementById('ui-coins').innerText = state.coins.toLocaleString();
    document.getElementById('club-count').innerText = state.club.length;
    game.renderStore();
    game.buildPitch();
  },
  
  nav: (id) => {
    document.querySelectorAll('.view').forEach(e=>e.classList.remove('active'));
    document.getElementById('v-'+id).classList.add('active');
    document.querySelectorAll('.nav-item').forEach(e=>e.classList.remove('active'));
    event.currentTarget.classList.add('active');
  },
  
  renderStore: () => {
    const el = document.getElementById('pack-list');
    el.innerHTML = '';
    Object.values(packs).forEach(p => {
      el.innerHTML += `
        <div class="pack" onclick="game.open('${p.id}')">
          <div class="pack-img">⚽</div>
          <h3>${p.title}</h3>
          <div class="price">${p.price.toLocaleString()}</div>
        </div>
      `;
    });
  },
  
  open: (id) => {
    const p = packs[id];
    if(state.coins < p.price) return alert("Not enough coins!");
    state.coins -= p.price;
    document.getElementById('ui-coins').innerText = state.coins.toLocaleString();
    
    // Generate Cards
    let pulled = [];
    for(let i=0; i<p.count; i++) {
      let pool = DB.filter(x => x.ovr >= p.min && x.ovr <= p.max);
      if(p.filter) pool = pool.filter(x => x.league === p.filter);
      if(!pool.length) pool = DB; 
      
      let c1 = pool[Math.floor(Math.random()*pool.length)];
      let c2 = pool[Math.floor(Math.random()*pool.length)];
      let chosen = c1.ovr < c2.ovr ? c1 : c2;
      if(Math.random() < 0.05) chosen = pool.sort((a,b)=>b.ovr-a.ovr)[0];
      
      pulled.push({...chosen, uid: Date.now()+Math.random()});
    }
    
    pulled.sort((a,b) => b.ovr - a.ovr);
    game.currentPack = pulled;
    game.animate(pulled);
  },
  
  animate: (cards) => {
    const best = cards[0];
    const ov = document.getElementById('overlay');
    const stage = document.getElementById('walkout-stage');
    const flare = document.getElementById('flare');
    const res = document.getElementById('results-screen');
    const grid = document.getElementById('new-cards');
    
    ov.classList.add('active');
    res.classList.remove('show');
    stage.innerHTML = '';
    flare.className = 'flare';
    
    setTimeout(() => {
      flare.classList.add('boom');
      stage.innerHTML = game.cardHTML(best);
      const cardEl = stage.querySelector('.card');
      cardEl.classList.add('walkout');
      setTimeout(() => cardEl.classList.add('show'), 100);
      
      setTimeout(() => {
        stage.innerHTML = '';
        res.classList.add('show');
        grid.innerHTML = '';
        cards.forEach(c => grid.innerHTML += game.cardHTML(c));
        const val = cards.reduce((a,b)=>a+(b.ovr*10),0);
        document.getElementById('qs-val').innerText = val.toLocaleString();
      }, 3000);
    }, 500);
  },
  
  cardHTML: (p) => {
    // Determine labels based on position
    const isGK = p.pos === 'GK';
    const labels = isGK ? ['DIV','HAN','KIC','REF','SPD','POS'] : ['PAC','SHO','PAS','DRI','DEF','PHY'];
    const s = p.stats;
    const vals = isGK ? [s.pac, s.sho, s.pas, s.dri, s.def, s.phy] : [s.pac, s.sho, s.pas, s.dri, s.def, s.phy];

    return `
      <div class="card c-${p.type}">
        <div class="c-top">
          <div class="ovr">${p.ovr}</div>
          <div class="pos">${p.pos}</div>
        </div>
        
        <img src="https://raw.githubusercontent.com/FortAwesome/Font-Awesome/6.x/svgs/solid/user.svg" class="p-img" style="opacity:0.6">
        
        <div class="p-info">
          <div class="name">${p.name}</div>
          <div class="club"><span style="font-size:14px; margin-right:4px">${p.nat}</span> ${p.club}</div>
          <div class="stats">
             <div class="stat-row"><span>${vals[0]}</span><span class="s-lbl">${labels[0]}</span></div>
             <div class="stat-row"><span>${vals[3]}</span><span class="s-lbl">${labels[3]}</span></div>
             <div class="stat-row"><span>${vals[1]}</span><span class="s-lbl">${labels[1]}</span></div>
             <div class="stat-row"><span>${vals[4]}</span><span class="s-lbl">${labels[4]}</span></div>
             <div class="stat-row"><span>${vals[2]}</span><span class="s-lbl">${labels[2]}</span></div>
             <div class="stat-row"><span>${vals[5]}</span><span class="s-lbl">${labels[5]}</span></div>
          </div>
        </div>
      </div>
    `;
  },
  
  store: () => {
    state.club = [...state.club, ...game.currentPack];
    game.save();
    game.close();
    game.renderClub();
  },
  
  qs: () => {
    const val = game.currentPack.reduce((a,b)=>a+(b.ovr*10),0);
    state.coins += val;
    game.save();
    game.close();
    document.getElementById('ui-coins').innerText = state.coins.toLocaleString();
  },
  
  qsAll: () => {
     if(!confirm("Quick sell all players in club?")) return;
     const val = state.club.reduce((a,b)=>a+(b.ovr*10),0);
     state.coins += val;
     state.club = [];
     game.save();
     game.renderClub();
     document.getElementById('ui-coins').innerText = state.coins.toLocaleString();
  },
  
  close: () => {
    document.getElementById('overlay').classList.remove('active');
  },
  
  renderClub: () => {
    const el = document.getElementById('club-grid');
    el.innerHTML = '';
    state.club.sort((a,b) => b.ovr - a.ovr).forEach(p => {
      const div = document.createElement('div');
      div.innerHTML = game.cardHTML(p);
      div.onclick = () => game.addToSquad(p);
      el.appendChild(div);
    });
    document.getElementById('club-count').innerText = state.club.length;
  },
  
  /* SQUAD BUILDER LOGIC */
  positions: [
    {id:'gk', l:50, t:85, p:'GK'},
    {id:'lb', l:15, t:70, p:'LB'}, {id:'cb1', l:38, t:70, p:'CB'}, {id:'cb2', l:62, t:70, p:'CB'}, {id:'rb', l:85, t:70, p:'RB'},
    {id:'lm', l:15, t:45, p:'LW'}, {id:'cm1', l:38, t:45, p:'CM'}, {id:'cm2', l:62, t:45, p:'CM'}, {id:'rm', l:85, t:45, p:'RW'},
    {id:'st1', l:35, t:15, p:'ST'}, {id:'st2', l:65, t:15, p:'ST'}
  ],
  
  buildPitch: () => {
    const el = document.getElementById('pitch');
    el.innerHTML = '';
    game.positions.forEach(pos => {
      const slot = document.createElement('div');
      slot.className = 'slot';
      slot.style.left = pos.l + '%';
      slot.style.top = pos.t + '%';
      slot.dataset.id = pos.id;
      
      if(state.squad[pos.id]) {
        slot.innerHTML = game.cardHTML(state.squad[pos.id]);
        slot.style.border = 'none';
        slot.style.background = 'transparent';
      } else {
        slot.innerText = pos.p;
      }
      
      slot.onclick = () => {
        if(state.squad[pos.id]) {
          delete state.squad[pos.id];
          game.save();
          game.buildPitch();
        } else {
          alert("Click a player in your CLUB to add them here.");
        }
      };
      el.appendChild(slot);
    });
  },
  
  addToSquad: (p) => {
    const map = {
      'GK':['gk'], 'LB':['lb'], 'RB':['rb'], 'CB':['cb1','cb2'],
      'CM':['cm1','cm2'], 'CDM':['cm1','cm2'], 'CAM':['cm1','cm2'],
      'ST':['st1','st2'], 'CF':['st1','st2'],
      'LW':['lm'], 'RW':['rm'], 'LM':['lm'], 'RM':['rm']
    };
    
    const slots = map[p.pos] || [];
    let filled = false;
    
    for(let id of slots) {
      if(!state.squad[id]) {
        state.squad[id] = p;
        filled = true;
        game.nav('squad');
        break;
      }
    }
    
    if(filled) {
      game.save();
      game.buildPitch();
    } else {
      alert(`No open ${p.pos} slots in 4-4-2! Clear a spot first.`);
    }
  },
  
  clearSquad: () => {
    state.squad = {};
    game.save();
    game.buildPitch();
  },
  
  save: () => store.set('data', state)
};

game.init();
</script>
</body>
</html>
