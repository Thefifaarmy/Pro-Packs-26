<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover, user-scalable=no">
<title>TFA Ultimate — Real DB</title>
<link href="https://fonts.googleapis.com/css2?family=Oswald:wght@300;400;500;700&family=Outfit:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #0e121b; --dark: #05070a;
  --accent: #3bf6ff; --accent-glow: rgba(59, 246, 255, 0.4);
  --purple: #6e45ff; --gold: #eebb44;
  --card-w: 160px; --card-h: 230px;
  --font-h: 'Oswald', sans-serif; --font-b: 'Outfit', sans-serif;
  --safe-top: env(safe-area-inset-top);
  --safe-bot: env(safe-area-inset-bottom);
}

/* --- RESET & BASE --- */
* { box-sizing: border-box; -webkit-tap-highlight-color: transparent; user-select: none; }
body { margin: 0; background: radial-gradient(circle at 50% -20%, #1a2c4e, #05070a 60%); 
       font-family: var(--font-b); color: #fff; min-height: 100vh; overflow-x: hidden; padding-bottom: 90px; }

/* --- UI COMPONENTS --- */
.flex-c { display: flex; align-items: center; justify-content: center; }
.flex-sb { display: flex; align-items: center; justify-content: space-between; }
.btn { border: none; background: rgba(255,255,255,0.1); color: #fff; padding: 10px 16px; border-radius: 8px; font-weight: 600; cursor: pointer; transition: 0.2s; font-family: var(--font-b); backdrop-filter: blur(5px); }
.btn:active { transform: scale(0.96); }
.btn.primary { background: linear-gradient(135deg, var(--accent), var(--purple)); color: #000; box-shadow: 0 4px 15px var(--accent-glow); }
.btn.danger { background: #ff4757; color: #fff; }

/* --- HEADER --- */
.topbar { position: sticky; top: 0; z-index: 50; padding: calc(10px + var(--safe-top)) 16px 10px; background: rgba(5,7,10,0.85); backdrop-filter: blur(12px); border-bottom: 1px solid rgba(255,255,255,0.05); }
.brand { font-family: var(--font-h); font-weight: 700; font-size: 20px; letter-spacing: 1px; }
.brand span { color: var(--accent); }
.currency { background: rgba(0,0,0,0.4); border: 1px solid rgba(255,255,255,0.1); padding: 4px 12px; border-radius: 20px; font-size: 14px; font-weight: 700; color: #ffd700; display: flex; align-items: center; gap: 6px; }

/* --- VIEWS --- */
.view { display: none; padding: 20px 16px; max-width: 1000px; margin: 0 auto; animation: fadeIn 0.3s ease; }
.view.active { display: block; }
@keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

/* --- STORE GRID --- */
.pack-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(160px, 1fr)); gap: 16px; }
.store-pack { background: linear-gradient(160deg, #1c2533, #111); border: 1px solid rgba(255,255,255,0.1); border-radius: 16px; padding: 16px; text-align: center; position: relative; overflow: hidden; transition: transform 0.2s; cursor: pointer; }
.store-pack:active { transform: scale(0.97); }
.pack-art { height: 100px; background: radial-gradient(circle, #444, #111); margin-bottom: 12px; border-radius: 10px; display: flex; align-items: center; justify-content: center; font-family: var(--font-h); font-size: 40px; color: rgba(255,255,255,0.1); }
.pack-title { font-weight: 700; font-size: 15px; margin-bottom: 4px; }
.pack-price { color: #ffd700; font-weight: 600; font-size: 14px; background: rgba(0,0,0,0.3); display: inline-block; padding: 4px 10px; border-radius: 12px; }

/* --- FUT CARD (The Real Deal) --- */
.fut-card {
  width: var(--card-w); height: var(--card-h);
  position: relative; margin: 10px; display: inline-block;
  background-color: #1a1a1a;
  border: 2px solid #aaa;
  clip-path: polygon(20% 0, 80% 0, 100% 20%, 100% 100%, 0 100%, 0 20%);
  border-radius: 0 0 12% 12%;
  box-shadow: 0 10px 20px rgba(0,0,0,0.5);
  transition: transform 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  cursor: pointer; flex-shrink: 0;
}
.fut-card:hover { transform: translateY(-10px) scale(1.05); z-index: 10; }
/* Rarity Colors */
.c-gold { background: radial-gradient(ellipse at center, #f5d878 0%, #a07e32 100%); border-color: #f7e199; color: #3e3012; }
.c-silver { background: radial-gradient(ellipse at center, #e6e6e6 0%, #949494 100%); border-color: #fff; color: #222; }
.c-bronze { background: radial-gradient(ellipse at center, #e8b382 0%, #7d5032 100%); border-color: #e8b382; color: #381e10; }
.c-icon { background: linear-gradient(135deg, #fbf6e8 0%, #d4c08b 100%); border-color: #bfa567; color: #57461f; }
.c-totw { background: linear-gradient(180deg, #000 0%, #1e1e1e 100%); border-color: #d4af37; color: #d4af37; }
.c-totw .c-ovr, .c-totw .c-name { color: #fff; text-shadow: 0 0 5px #d4af37; }

/* Card Content */
.c-top { position: absolute; top: 12px; left: 10px; display: flex; flex-direction: column; align-items: center; width: 30px; text-align: center; }
.c-ovr { font-family: var(--font-h); font-size: 32px; font-weight: 700; line-height: 1; margin-bottom: 2px; }
.c-pos { font-family: var(--font-b); font-size: 12px; font-weight: 700; text-transform: uppercase; }
.c-img { position: absolute; top: 35px; right: 10px; width: 90px; height: 90px; object-fit: contain; filter: drop-shadow(4px 4px 4px rgba(0,0,0,0.4)); }
.c-info { position: absolute; bottom: 0; width: 100%; height: 85px; text-align: center; }
.c-name { font-family: var(--font-h); font-weight: 700; text-transform: uppercase; font-size: 16px; border-bottom: 1px solid rgba(0,0,0,0.1); padding-bottom: 2px; margin: 0 10px; white-space: nowrap; overflow: hidden; }
.c-club-row { font-size: 11px; margin: 4px 0; opacity: 0.8; font-weight: 600; display:flex; justify-content:center; gap:5px; }
.c-stats { display: grid; grid-template-columns: 1fr 1fr; gap: 2px 8px; font-size: 10px; padding: 0 15px; font-weight: 700; text-align: left; opacity: 0.9; }
.stat-item { display: flex; justify-content: space-between; }

/* --- ANIMATION OVERLAY --- */
.overlay { position: fixed; inset: 0; background: #000; z-index: 200; display: none; flex-direction: column; align-items: center; justify-content: center; }
.overlay.active { display: flex; }
.walkout-stage { position: relative; width: 100%; height: 100%; display: flex; align-items: center; justify-content: center; overflow: hidden; }
.flare { position: absolute; width: 1px; height: 1px; box-shadow: 0 0 400px 150px var(--accent); opacity: 0; transition: 1s; }
.flare.boom { opacity: 1; }
.pack-opening-card { transform: scale(0.1); opacity: 0; transition: 0.8s cubic-bezier(0.34, 1.56, 0.64, 1); }
.pack-opening-card.reveal { transform: scale(1.5); opacity: 1; }
.pack-results { display: none; padding: 80px 20px 20px; text-align: center; overflow-y: auto; height: 100%; width: 100%; background: rgba(14,18,27,0.95); }
.pack-results.show { display: block; }
.result-grid { display: flex; flex-wrap: wrap; justify-content: center; gap: 10px; padding-bottom: 60px; }
.walkout-badges { position: absolute; bottom: 20%; display: flex; gap: 20px; opacity: 0; transition: 0.5s; }
.walkout-badges.show { opacity: 1; bottom: 25%; }
.w-badge { width: 60px; height: 60px; border-radius: 50%; background: #fff; display: flex; align-items: center; justify-content: center; font-size: 30px; box-shadow: 0 0 20px rgba(255,255,255,0.5); }

/* --- SQUAD BUILDER --- */
.pitch {
  background: repeating-linear-gradient(90deg, #2e5c32 0, #2e5c32 20px, #366b3b 20px, #366b3b 40px);
  border: 4px solid rgba(255,255,255,0.2); border-radius: 8px; height: 500px; position: relative; margin: 0 auto; max-width: 400px;
}
.squad-pos { position: absolute; width: 70px; height: 90px; transform: translate(-50%, -50%); background: rgba(0,0,0,0.3); border-radius: 6px; border: 2px dashed rgba(255,255,255,0.2); display: flex; align-items: center; justify-content: center; cursor: pointer; }
.squad-pos .pos-lbl { font-weight: 800; opacity: 0.5; }
.squad-pos .filled-card { zoom: 0.45; pointer-events: none; margin: 0; }
/* 4-4-2 */
.p-gk { left: 50%; bottom: 2%; } .p-lb { left: 15%; bottom: 20%; } .p-cb1 { left: 38%; bottom: 18%; } .p-cb2 { left: 62%; bottom: 18%; } .p-rb { left: 85%; bottom: 20%; }
.p-lm { left: 15%; bottom: 50%; } .p-cm1 { left: 38%; bottom: 50%; } .p-cm2 { left: 62%; bottom: 50%; } .p-rm { left: 85%; bottom: 50%; }
.p-st1 { left: 35%; bottom: 80%; } .p-st2 { left: 65%; bottom: 80%; }

/* --- NAV --- */
.nav-rail { position: fixed; bottom: 20px; left: 50%; transform: translateX(-50%); display: flex; gap: 8px; background: rgba(20,25,35,0.9); padding: 6px; border-radius: 24px; border: 1px solid rgba(255,255,255,0.1); backdrop-filter: blur(10px); z-index: 100; }
.nav-item { padding: 10px 18px; border-radius: 18px; color: #8a9bbd; font-weight: 600; font-size: 13px; cursor: pointer; }
.nav-item.active { background: var(--accent); color: #000; box-shadow: 0 0 15px var(--accent-glow); }
.toast { position: fixed; top: 20px; left: 50%; transform: translate(-50%, -20px); background: #fff; color: #000; padding: 12px 24px; border-radius: 30px; font-weight: 600; opacity: 0; transition: 0.3s; pointer-events: none; z-index: 999; }
.toast.show { transform: translate(-50%, 0); opacity: 1; }
</style>
</head>
<body>

<div class="topbar flex-sb">
  <div class="brand">TFA <span>ULTIMATE</span></div>
  <div class="flex-c" style="gap:10px">
    <div class="currency">🪙 <span id="ui-coins">0</span></div>
    <button class="btn" onclick="app.daily()">Daily</button>
  </div>
</div>

<div id="view-store" class="view active">
  <div class="flex-sb" style="margin-bottom:15px"><h2>Store</h2></div>
  <div class="pack-grid" id="store-grid"></div>
</div>

<div id="view-club" class="view">
  <div class="flex-sb"><h2>My Club (<span id="club-count">0</span>)</h2> <button class="btn danger" onclick="app.qsAll()">QS All</button></div>
  <input type="text" id="club-search" placeholder="Search..." onkeyup="app.renderClub()" style="width:100%; padding:10px; margin-bottom:10px; background:rgba(0,0,0,0.3); border:1px solid #333; color:#fff; border-radius:8px;">
  <div class="club-grid" id="club-list" style="display:flex; flex-wrap:wrap; justify-content:center;"></div>
</div>

<div id="view-squad" class="view">
  <div class="flex-sb"><h2>Squad (4-4-2)</h2> <span style="font-size:12px; color:#aaa" id="squad-ovr">OVR: 0</span></div>
  <div class="pitch" id="pitch-container">
    </div>
  <button class="btn" style="width:100%; margin-top:20px" onclick="app.clearSquad()">Clear Squad</button>
</div>

<div class="overlay" id="pack-overlay">
  <div class="walkout-stage" id="stage"></div>
  <div class="pack-results" id="pack-results">
    <h2 id="pack-title-disp">Pack Result</h2>
    <div class="result-grid" id="result-grid"></div>
    <div class="flex-c" style="gap:10px; position: sticky; bottom: 0; background: #0e121b; padding: 10px;">
      <button class="btn primary" onclick="app.storeToClub()">Send All to Club</button>
      <button class="btn danger" onclick="app.qsPack()">Quick Sell (<span id="qs-val">0</span>)</button>
    </div>
  </div>
</div>

<div class="nav-rail">
  <div class="nav-item active" onclick="app.nav('store')">Store</div>
  <div class="nav-item" onclick="app.nav('club')">Club</div>
  <div class="nav-item" onclick="app.nav('squad')">Squad</div>
</div>

<div class="toast" id="toast">Saved</div>

<script>
/* --- 1. REAL PLAYER DATABASE --- */
const DB_PLAYERS = [];

// Helper to generate Stats
const genStats = (ovr, pos) => {
    const r = (base, v) => Math.max(30, Math.min(99, Math.floor(base + (Math.random() * v * 2) - v)));
    let s = { pac:0, sho:0, pas:0, dri:0, def:0, phy:0 };
    if(pos==='GK') { s={ pac:r(ovr,5), sho:r(ovr,5), pas:r(ovr-10,10), dri:r(ovr,5), def:r(45,10), phy:r(ovr-5,5) }; }
    else if(['ST','LW','RW'].includes(pos)) { s={ pac:r(ovr+2,5), sho:r(ovr,5), pas:r(ovr-10,8), dri:r(ovr,5), def:r(40,10), phy:r(65,10) }; }
    else if(['CM','CAM','CDM'].includes(pos)) { s={ pac:r(75,10), sho:r(ovr-5,8), pas:r(ovr,5), dri:r(ovr-2,5), def:r(ovr-10,10), phy:r(70,10) }; }
    else { s={ pac:r(75,10), sho:r(50,10), pas:r(70,10), dri:r(65,10), def:r(ovr,5), phy:r(ovr-2,5) }; }
    return s;
};

const add = (club, league, players) => {
    players.forEach(p => {
        let type = p[4] || (p[1] >= 75 ? 'gold' : (p[1] >= 65 ? 'silver' : 'bronze'));
        DB_PLAYERS.push({
            name: p[0], ovr: p[1], pos: p[2], nat: p[3], type: type, club: club, league: league,
            stats: genStats(p[1], p[2])
        });
    });
};

/* --- LOAD REAL PLAYERS (Hardcoded for stability) --- */
const PL = "Premier League";
add("Man City", PL, [["Haaland",91,"ST","🇳🇴"],["De Bruyne",90,"CM","🇧🇪"],["Rodri",89,"CDM","🇪🇸"],["Foden",88,"RW","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Dias",88,"CB","🇵🇹"],["Ederson",88,"GK","🇧🇷"],["Silva",87,"CM","🇵🇹"],["Gvardiol",86,"LB","🇭🇷"],["Doku",85,"LW","🇧🇪"],["Savinho",83,"RW","🇧🇷"],["Lewis",80,"RB","🏴󠁧󠁢󠁥󠁮󠁧󠁿"]]);
add("Arsenal", PL, [["Odegaard",89,"CM","🇳🇴"],["Saka",89,"RW","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Saliba",88,"CB","🇫🇷"],["Rice",88,"CDM","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Gabriel",87,"CB","🇧🇷"],["Raya",86,"GK","🇪🇸"],["Havertz",85,"ST","🇩🇪"],["Calafiori",84,"LB","🇮🇹"],["Merino",83,"CM","🇪🇸"],["Sterling",82,"LW","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Martinelli",84,"LW","🇧🇷"]]);
add("Liverpool", PL, [["Salah",90,"RW","🇪🇬"],["Alisson",89,"GK","🇧🇷"],["Van Dijk",89,"CB","🇳🇱"],["Mac Allister",86,"CM","🇦🇷"],["Trent AA",86,"RB","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Diaz",85,"LW","🇨🇴"],["Szoboszlai",84,"CM","🇭🇺"],["Konate",84,"CB","🇫🇷"],["Chiesa",83,"LW","🇮🇹"],["Gravenberch",82,"CM","🇳🇱"]]);
add("Man Utd", PL, [["Fernandes",87,"CAM","🇵🇹"],["Martinez",84,"CB","🇦🇷"],["De Ligt",84,"CB","🇳🇱"],["Rashford",83,"LW","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Onana",83,"GK","🇨🇲"],["Mainoo",82,"CM","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Garnacho",82,"LW","🇦🇷"],["Zirkzee",80,"ST","🇳🇱"],["Ugarte",82,"CDM","🇺🇾"],["Yoro",79,"CB","🇫🇷","silver"]]);
add("Chelsea", PL, [["Palmer",86,"CAM","🏴󠁧󠁢󠁥󠁮󠁧󠁿","totw"],["James",84,"RB","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Nkunku",84,"CF","🇫🇷"],["Caicedo",83,"CDM","🇪🇨"],["Fernandez",83,"CM","🇦🇷"],["Neto",82,"LW","🇵🇹"],["Felix",82,"CF","🇵🇹"],["Sancho",82,"LW","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Jackson",81,"ST","🇸🇳"]]);
add("Spurs", PL, [["Son",87,"LW","🇰🇷"],["Maddison",85,"CAM","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Romero",85,"CB","🇦🇷"],["Porro",84,"RB","🇪🇸"],["Vicario",84,"GK","🇮🇹"],["Solanke",82,"ST","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Van de Ven",83,"CB","🇳🇱"],["Udogie",82,"LB","🇮🇹"],["Johnson",80,"RW","🏴󠁧󠁢󠁷󠁬󠁳󠁿"]]);
add("Newcastle", PL, [["Isak",85,"ST","🇸🇪"],["Guimaraes",85,"CM","🇧🇷"],["Gordon",84,"LW","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Botman",83,"CB","🇳🇱"],["Tonali",84,"CDM","🇮🇹"],["Pope",82,"GK","🏴󠁧󠁢󠁥󠁮󠁧󠁿"]]);
add("Aston Villa", PL, [["Martinez",87,"GK","🇦🇷"],["Watkins",85,"ST","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["McGinn",83,"CM","🏴󠁧󠁢󠁳󠁣󠁴󠁿"],["Tielemans",83,"CM","🇧🇪"],["Onana",80,"CDM","🇧🇪"]]);
add("West Ham", PL, [["Bowen",83,"RW","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Paqueta",84,"CAM","🇧🇷"],["Kudus",83,"RW","🇬🇭"],["Fullkrug",82,"ST","🇩🇪"],["Wan-Bissaka",80,"RB","🏴󠁧󠁢󠁥󠁮󠁧󠁿"]]);
add("Everton", PL, [["Pickford",83,"GK","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Tarkowski",80,"CB","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Calvert-Lewin",78,"ST","🏴󠁧󠁢󠁥󠁮󠁧󠁿","silver"],["Ndiaye",77,"CAM","🇸🇳","silver"]]);
add("Leicester", PL, [["Vardy",77,"ST","🏴󠁧󠁢󠁥󠁮󠁧󠁿","silver"],["Winks",76,"CM","🏴󠁧󠁢󠁥󠁮󠁧󠁿","silver"],["Fatawu",74,"RW","🇬🇭","silver"],["Ndidi",77,"CDM","🇳🇬","silver"]]);
add("Brighton", PL, [["Mitoma",82,"LW","🇯🇵"],["Estupinan",81,"LB","🇪🇨"],["Pedro",80,"ST","🇧🇷"],["Ferguson",77,"ST","🇮🇪","silver"],["Minteh",76,"RW","🇬🇲","silver"]]);

const ES = "La Liga";
add("Real Madrid", ES, [["Mbappe",91,"ST","🇫🇷"],["Bellingham",90,"CAM","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Vinicius",90,"LW","🇧🇷"],["Courtois",89,"GK","🇧🇪"],["Valverde",88,"CM","🇺🇾"],["Rudiger",87,"CB","🇩🇪"],["Rodrygo",86,"RW","🇧🇷"],["Modric",85,"CM","🇭🇷"],["Endrick",79,"ST","🇧🇷","silver"]]);
add("Barcelona", ES, [["Lewandowski",88,"ST","🇵🇱"],["Ter Stegen",88,"GK","🇩🇪"],["Pedri",86,"CM","🇪🇸"],["De Jong",86,"CM","🇳🇱"],["Araujo",85,"CB","🇺🇾"],["Kounde",85,"RB","🇫🇷"],["Yamal",83,"RW","🇪🇸","totw"],["Olmo",84,"CAM","🇪🇸"],["Raphinha",85,"LW","🇧🇷"],["Cubarsi",78,"CB","🇪🇸","silver"]]);
add("Atletico", ES, [["Griezmann",88,"ST","🇫🇷"],["Oblak",88,"GK","🇸🇮"],["Alvarez",86,"ST","🇦🇷"],["De Paul",84,"CM","🇦🇷"],["Le Normand",84,"CB","🇪🇸"],["Gallagher",82,"CM","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Sorloth",82,"ST","🇳🇴"]]);
add("Sevilla", ES, [["Ocampos",80,"RW","🇦🇷"],["Navas",79,"RB","🇪🇸","silver"],["Saul",79,"CM","🇪🇸","silver"],["Lukebakio",78,"RW","🇧🇪","silver"]]);
add("Valencia", ES, [["Mamardashvili",83,"GK","🇬🇪"],["Gaya",81,"LB","🇪🇸"],["Pepelu",80,"CDM","🇪🇸"],["Duro",78,"ST","🇪🇸","silver"]]);
add("Villarreal", ES, [["Moreno",83,"ST","🇪🇸"],["Parejo",82,"CM","🇪🇸"],["Baena",81,"CAM","🇪🇸"],["Ayoze",79,"LW","🇪🇸","silver"]]);
add("Sociedad", ES, [["Oyarzabal",83,"LW","🇪🇸"],["Zubimendi",84,"CDM","🇪🇸"],["Remiro",83,"GK","🇪🇸"],["Kubo",82,"RW","🇯🇵"],["Aguerd",80,"CB","🇲🇦"]]);
add("Athletic", ES, [["N Williams",85,"LW","🇪🇸","totw"],["I Williams",82,"RM","🇬🇭"],["Simon",84,"GK","🇪🇸"],["Sancet",81,"CAM","🇪🇸"]]);

const DE = "Bundesliga";
add("Bayern", DE, [["Kane",90,"ST","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Musiala",88,"CAM","🇩🇪"],["Neuer",87,"GK","🇩🇪"],["Kimmich",87,"CDM","🇩🇪"],["Sane",85,"RW","🇩🇪"],["Olise",84,"RW","🇫🇷"],["Palhinha",85,"CDM","🇵🇹"],["Davies",84,"LB","🇨🇦"],["Kim",84,"CB","🇰🇷"]]);
add("Dortmund", DE, [["Brandt",85,"CAM","🇩🇪"],["Kobel",86,"GK","🇨🇭"],["Schlotterbeck",84,"CB","🇩🇪"],["Guirassy",84,"ST","🇬🇳"],["Sabitzer",83,"CM","🇦🇹"],["Adeyemi",80,"LM","🇩🇪"]]);
add("Leipzig", DE, [["Openda",84,"ST","🇧🇪"],["Simons",85,"CAM","🇳🇱"],["Orban",83,"CB","🇭🇺"],["Sesko",80,"ST","🇸🇮"],["Raum",81,"LB","🇩🇪"]]);
add("Leverkusen", DE, [["Wirtz",88,"CAM","🇩🇪"],["Xhaka",85,"CM","🇨🇭"],["Grimaldo",86,"LB","🇪🇸"],["Frimpong",85,"RWB","🇳🇱"],["Tah",84,"CB","🇩🇪"],["Boniface",82,"ST","🇳🇬"],["Terrier",81,"LW","🇫🇷"]]);
add("Stuttgart", DE, [["Undav",82,"ST","🇩🇪"],["Fuhrich",80,"LM","🇩🇪"],["Nubal",79,"GK","🇩🇪","silver"],["Demirovic",79,"ST","🇧🇦","silver"]]);

const IT = "Serie A";
add("Juventus", IT, [["Vlahovic",84,"ST","🇷🇸"],["Bremer",85,"CB","🇧🇷"],["Luiz",84,"CM","🇧🇷"],["Koopmeiners",84,"CAM","🇳🇱"],["Di Gregorio",83,"GK","🇮🇹"],["Thuram",80,"CM","🇫🇷"],["Yildiz",79,"CF","🇹🇷","silver"]]);
add("Milan", IT, [["Leao",87,"LW","🇵🇹"],["Theo",86,"LB","🇫🇷"],["Maignan",87,"GK","🇫🇷"],["Pulisic",84,"RW","🇺🇸"],["Morata",83,"ST","🇪🇸"],["Tomori",83,"CB","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Reijnders",82,"CM","🇳🇱"]]);
add("Inter", IT, [["Lautaro",89,"ST","🇦🇷"],["Barella",87,"CM","🇮🇹"],["Bastoni",86,"CB","🇮🇹"],["Calhanoglu",86,"CDM","🇹🇷"],["Thuram",85,"ST","🇫🇷"],["Sommer",85,"GK","🇨🇭"],["Dimarco",84,"LB","🇮🇹"]]);
add("Roma", IT, [["Dybala",86,"CF","🇦🇷"],["Pellegrini",83,"CAM","🇮🇹"],["Mancini",82,"CB","🇮🇹"],["Dovbyk",82,"ST","🇺🇦"],["Hummels",83,"CB","🇩🇪"],["Soule",79,"RW","🇦🇷","silver"]]);
add("Napoli", IT, [["Kvara",86,"LW","🇬🇪"],["Lukaku",84,"ST","🇧🇪"],["Di Lorenzo",84,"RB","🇮🇹"],["McTominay",81,"CM","🏴󠁧󠁢󠁳󠁣󠁴󠁿"],["Lobotka",83,"CM","🇸🇰"],["Buongiorno",82,"CB","🇮🇹"]]);
add("Atalanta", IT, [["Lookman",84,"ST","🇳🇬"],["Scamacca",82,"ST","🇮🇹"],["Ederson",82,"CM","🇧🇷"],["Scalvini",80,"CB","🇮🇹"],["Retegui",80,"ST","🇮🇹"]]);

const FR = "Ligue 1";
add("PSG", FR, [["Dembele",86,"RW","🇫🇷"],["Donnarumma",87,"GK","🇮🇹"],["Marquinhos",87,"CB","🇧🇷"],["Hakimi",86,"RB","🇲🇦"],["Vitinha",85,"CM","🇵🇹"],["Neves",83,"CDM","🇵🇹"],["Barcola",82,"LW","🇫🇷"],["Pacho",80,"CB","🇪🇨"]]);
add("Marseille", FR, [["Rabiot",83,"CM","🇫🇷"],["Greenwood",81,"RW","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Hojbjerg",81,"CDM","🇩🇰"],["Rulli",80,"GK","🇦🇷"],["Wahi",78,"ST","🇫🇷","silver"]]);
add("Lyon", FR, [["Lacazette",82,"ST","🇫🇷"],["Tolisso",80,"CM","🇫🇷"],["Zaha",80,"LW","🇨🇮"],["Cherki",78,"CAM","🇫🇷","silver"]]);
add("Monaco", FR, [["Zakaria",83,"CDM","🇨🇭"],["Embolo",79,"ST","🇨🇭","silver"],["Golovin",81,"CAM","🇷🇺"],["Balogun",78,"ST","🇺🇸","silver"]]);
add("Lille", FR, [["David",82,"ST","🇨🇦"],["Chevalier",81,"GK","🇫🇷"],["Andre",80,"CDM","🇫🇷"],["Zhegrova",80,"RW","🇽🇰"]]);

const PT = "Liga Portugal";
add("Benfica", PT, [["Di Maria",84,"RW","🇦🇷"],["Otamendi",81,"CB","🇦🇷"],["Kokcu",82,"CM","🇹🇷"],["Pavlidis",80,"ST","🇬🇷"],["Trubin",81,"GK","🇺🇦"]]);
add("Porto", PT, [["Costa",84,"GK","🇵🇹"],["Galeno",81,"LW","🇧🇷"],["Varela",80,"CDM","🇦🇷"],["Pepe",79,"LW","🇧🇷","silver"]]);
add("Sporting", PT, [["Gyokeres",85,"ST","🇸🇪","totw"],["Goncalves",82,"LW","🇵🇹"],["Inacio",81,"CB","🇵🇹"],["Hjulmand",81,"CDM","🇩🇰"],["Trincao",80,"RW","🇵🇹"]]);
add("Braga", PT, [["Horta",80,"CAM","🇵🇹"],["Moutinho",79,"CM","🇵🇹","silver"],["Bruma",78,"LW","🇵🇹","silver"]]);

const NL = "Eredivisie";
add("Ajax", NL, [["Henderson",80,"CDM","🏴󠁧󠁢󠁥󠁮󠁧󠁿"],["Brobbey",79,"ST","🇳🇱","silver"],["Hato",78,"CB","🇳🇱","silver"],["Weghorst",77,"ST","🇳🇱","silver"],["Berghuis",79,"RW","🇳🇱","silver"]]);
add("PSV", NL, [["De Jong",81,"ST","🇳🇱"],["Bakayoko",80,"RW","🇧🇪"],["Veerman",81,"CM","🇳🇱"],["Lang",79,"LW","🇳🇱","silver"],["Dest",79,"LB","🇺🇸","silver"]]);
add("Feyenoord", NL, [["Gimenez",81,"ST","🇲🇽"],["Timber",80,"CM","🇳🇱"],["Hancko",81,"CB","🇸🇰"],["Bijlow",78,"GK","🇳🇱","silver"]]);

/* --- APP ENGINE --- */
const store = { get: k => JSON.parse(localStorage.getItem('tfa_db_v2_'+k)) || null, set: (k,v) => localStorage.setItem('tfa_db_v2_'+k, JSON.stringify(v)) };
let state = store.get('data') || { coins: 5000, club: [], squad: {}, daily: "" };

const PACKS = {
    bronze: {id:'bronze', title:"Bronze Pack", price:500, count:12, min:50, max:64},
    silver: {id:'silver', title:"Silver Pack", price:2500, count:12, min:65, max:74},
    gold: {id:'gold', title:"Gold Pack", price:7500, count:12, min:75, max:84},
    prime: {id:'prime', title:"Prime Gold", price:15000, count:12, min:78, max:88},
    promo: {id:'promo', title:"Ultimate Pack", price:100000, count:30, min:82, max:99}
};

const app = {
    tempPack: [],
    
    init: () => {
        app.updateUI();
        app.renderStore();
        app.renderSquad();
    },

    updateUI: () => {
        document.getElementById('ui-coins').innerText = state.coins.toLocaleString();
        document.getElementById('club-count').innerText = state.club.length;
        store.set('data', state);
    },

    nav: (view) => {
        document.querySelectorAll('.view').forEach(e => e.classList.remove('active'));
        document.getElementById('view-'+view).classList.add('active');
        document.querySelectorAll('.nav-item').forEach(e => e.classList.remove('active'));
        event.currentTarget.classList.add('active');
        if(view==='club') app.renderClub();
    },

    /* PACK LOGIC */
    buyPack: (id) => {
        let p = PACKS[id];
        if(state.coins < p.price) { app.toast('Not enough coins!'); return; }
        state.coins -= p.price;
        app.updateUI();

        let cards = [];
        for(let i=0; i<p.count; i++) {
            // STRICT FILTERING
            let pool = DB_PLAYERS.filter(pl => pl.ovr >= p.min && pl.ovr <= p.max);
            
            // Fallback for strict ranges (e.g. if no 75-84 exist, widen slightly)
            if(pool.length === 0) pool = DB_PLAYERS.filter(pl => pl.ovr >= p.min-5 && pl.ovr <= p.max+5);
            if(pool.length === 0) pool = DB_PLAYERS; // Final fallback

            // Weighting: Pick 3, choose lowest rating (makes high rated rare)
            let c1 = pool[Math.floor(Math.random()*pool.length)];
            let c2 = pool[Math.floor(Math.random()*pool.length)];
            let c3 = pool[Math.floor(Math.random()*pool.length)];
            
            // 95% chance to take the lowest rated of the 3 candidates
            let chosen = (Math.random() < 0.95) ? [c1,c2,c3].sort((a,b)=>a.ovr-b.ovr)[0] : [c1,c2,c3].sort((a,b)=>b.ovr-a.ovr)[0];

            cards.push({ ...chosen, uid: Date.now()+Math.random() });
        }
        
        cards.sort((a,b) => b.ovr - a.ovr);
        app.openOverlay(cards, p.title);
    },

    renderStore: () => {
        const grid = document.getElementById('store-grid');
        grid.innerHTML = '';
        Object.values(PACKS).forEach(p => {
            grid.innerHTML += `
            <div class="store-pack" onclick="app.buyPack('${p.id}')">
                <div class="pack-art">⚽</div>
                <div class="pack-title">${p.title}</div>
                <div class="pack-price">${p.price.toLocaleString()}</div>
            </div>`;
        });
    },

    /* ANIMATION */
    openOverlay: (cards, title) => {
        app.tempPack = cards;
        let best = cards[0];
        let isWalkout = best.ovr >= 86;
        
        let ov = document.getElementById('pack-overlay');
        let stage = document.getElementById('stage');
        let res = document.getElementById('pack-results');
        
        ov.classList.add('active');
        stage.style.display = 'flex';
        res.classList.remove('show');
        stage.innerHTML = `<div class="flare" id="flare"></div><div class="walkout-badges" id="w-badges"><div class="w-badge" id="wb-nat"></div><div class="w-badge" id="wb-pos" style="font-size:16px; font-weight:800; color:#000"></div><div class="w-badge" id="wb-club" style="font-size:12px"></div></div><div id="main-walkout"></div>`;

        setTimeout(() => {
            document.getElementById('flare').classList.add('boom');
            if(isWalkout) {
                // Walkout Sequence
                let b = document.getElementById('w-badges');
                document.getElementById('wb-nat').innerText = best.nat;
                document.getElementById('wb-pos').innerText = best.pos;
                document.getElementById('wb-club').innerText = '🛡️';
                b.classList.add('show');
                
                setTimeout(() => {
                     document.getElementById('main-walkout').innerHTML = app.renderCardHTML(best);
                     let c = document.querySelector('#main-walkout .fut-card');
                     c.classList.add('pack-opening-card');
                     requestAnimationFrame(()=>c.classList.add('reveal'));
                }, 1200);
                setTimeout(() => { app.showGrid(title); }, 4500);
            } else {
                app.showGrid(title);
            }
        }, 200);
    },

    showGrid: (title) => {
        document.getElementById('stage').style.display = 'none';
        let res = document.getElementById('pack-results');
        res.classList.add('show');
        document.getElementById('pack-title-disp').innerText = title;
        
        let grid = document.getElementById('result-grid');
        grid.innerHTML = '';
        let totalVal = 0;
        
        app.tempPack.forEach(p => {
            let d = document.createElement('div');
            d.innerHTML = app.renderCardHTML(p);
            grid.appendChild(d);
            totalVal += app.getQS(p);
        });
        
        document.getElementById('qs-val').innerText = totalVal.toLocaleString();
    },

    renderCardHTML: (p, small=false) => {
        // Calculate Stats for Grid
        let s = p.stats || {pac:0,sho:0,pas:0,dri:0,def:0,phy:0};
        let isGK = p.pos === 'GK';
        let lbls = isGK ? ['DIV','HAN','KIC','REF','SPD','POS'] : ['PAC','SHO','PAS','DRI','DEF','PHY'];
        let vals = isGK ? [s.pac,s.sho,s.pas,s.dri,s.def,s.phy] : [s.pac,s.sho,s.pas,s.dri,s.def,s.phy];

        let img = `https://raw.githubusercontent.com/FortAwesome/Font-Awesome/6.x/svgs/solid/user.svg`;

        return `
        <div class="fut-card c-${p.type}" ${small ? 'style="transform:scale(0.7); margin:5px"' : ''} onclick="app.cardClick(${p.ovr})">
          <div class="c-top">
            <div class="c-ovr">${p.ovr}</div>
            <div class="c-pos">${p.pos}</div>
          </div>
          <img src="${img}" class="c-img" style="${(p.type=='icon'||p.ovr>88)?'filter:sepia(1)':''}">
          <div class="c-info">
            <div class="c-name">${p.name}</div>
            <div class="c-club-row"><span>${p.nat}</span> <span>${p.club}</span></div>
            <div class="c-stats">
              <div class="stat-item"><span>${vals[0]}</span> <span style="opacity:0.6">${lbls[0]}</span></div>
              <div class="stat-item"><span>${vals[3]}</span> <span style="opacity:0.6">${lbls[3]}</span></div>
              <div class="stat-item"><span>${vals[1]}</span> <span style="opacity:0.6">${lbls[1]}</span></div>
              <div class="stat-item"><span>${vals[4]}</span> <span style="opacity:0.6">${lbls[4]}</span></div>
              <div class="stat-item"><span>${vals[2]}</span> <span style="opacity:0.6">${lbls[2]}</span></div>
              <div class="stat-item"><span>${vals[5]}</span> <span style="opacity:0.6">${lbls[5]}</span></div>
            </div>
          </div>
        </div>`;
    },

    /* CLUB & SQUAD */
    storeToClub: () => {
        state.club = [...state.club, ...app.tempPack];
        app.closeOverlay();
        app.toast('Sent to Club');
        app.updateUI();
    },
    qsPack: () => {
        let val = app.tempPack.reduce((a,b)=>a+app.getQS(b),0);
        state.coins += val;
        app.closeOverlay();
        app.toast(`Sold for ${val.toLocaleString()}`);
        app.updateUI();
    },
    getQS: (p) => p.ovr * 15 * (p.type==='gold'?3:1),
    closeOverlay: () => { document.getElementById('pack-overlay').classList.remove('active'); app.tempPack=[]; },

    renderClub: () => {
        let list = document.getElementById('club-list');
        list.innerHTML = '';
        let search = document.getElementById('club-search').value.toLowerCase();
        let arr = state.club.filter(p => p.name.toLowerCase().includes(search)).sort((a,b)=>b.ovr-a.ovr).slice(0,100);
        
        arr.forEach(p => {
            let d = document.createElement('div');
            d.innerHTML = app.renderCardHTML(p, true);
            d.onclick = () => app.addToSquad(p);
            list.appendChild(d);
        });
        if(arr.length===0) list.innerHTML='<div style="padding:20px;color:#aaa">No players found</div>';
    },

    qsAll: () => {
        if(!confirm("Quick Sell ALL?")) return;
        let val = state.club.reduce((a,b)=>a+app.getQS(b),0);
        state.coins += val;
        state.club = [];
        app.updateUI();
        app.renderClub();
    },

    /* SQUAD BUILDER */
    // 4-4-2 Coords
    posMap: [
        {id:'gk', p:'GK', x:50, y:85},
        {id:'lb', p:'LB', x:15, y:70}, {id:'cb1', p:'CB', x:38, y:70}, {id:'cb2', p:'CB', x:62, y:70}, {id:'rb', p:'RB', x:85, y:70},
        {id:'lm', p:'LM', x:15, y:45}, {id:'cm1', p:'CM', x:38, y:45}, {id:'cm2', p:'CM', x:62, y:45}, {id:'rm', p:'RM', x:85, y:45},
        {id:'st1', p:'ST', x:35, y:15}, {id:'st2', p:'ST', x:65, y:15}
    ],

    renderSquad: () => {
        const pitch = document.getElementById('pitch-container');
        pitch.innerHTML = '';
        app.posMap.forEach(slot => {
            let el = document.createElement('div');
            el.className = 'squad-pos';
            el.style.left = slot.x+'%'; el.style.top = slot.y+'%';
            
            if(state.squad[slot.id]) {
                el.innerHTML = `<div class="filled-card">${app.renderCardHTML(state.squad[slot.id])}</div>`;
                el.style.border = 'none'; el.style.background = 'transparent';
                el.onclick = () => { delete state.squad[slot.id]; app.renderSquad(); app.calcSquadOvr(); };
            } else {
                el.innerHTML = `<div class="pos-lbl">${slot.p}</div>`;
                el.onclick = () => alert("Go to CLUB and click a player to add them here.");
            }
            pitch.appendChild(el);
        });
        app.calcSquadOvr();
    },

    addToSquad: (p) => {
        // Simple auto-fill logic
        let validSlots = app.posMap.filter(s => {
            if(p.pos === s.p) return true;
            if(p.pos === 'LW' && s.p === 'LM') return true;
            if(p.pos === 'RW' && s.p === 'RM') return true;
            if(p.pos === 'CDM' || p.pos === 'CAM') return s.p === 'CM';
            if(p.pos === 'CF') return s.p === 'ST';
            return false;
        });

        let emptySlot = validSlots.find(s => !state.squad[s.id]);
        
        if(emptySlot) {
            state.squad[emptySlot.id] = p;
            app.renderSquad();
            app.nav('squad');
            app.toast(`Added to ${emptySlot.p}`);
        } else {
            app.toast(`No ${p.pos} slot available`);
        }
    },

    calcSquadOvr: () => {
        let players = Object.values(state.squad);
        if(players.length === 0) { document.getElementById('squad-ovr').innerText = "OVR: 0"; return; }
        let tot = players.reduce((a,b)=>a+b.ovr,0);
        document.getElementById('squad-ovr').innerText = "OVR: " + Math.round(tot / 11); // Always divide by 11 for FIFA style rating
    },
    
    daily: () => {
        let d = new Date().toDateString();
        if(state.daily === d) { app.toast("Already claimed!"); return; }
        state.coins += 5000;
        state.daily = d;
        app.toast("+5,000 Coins");
        app.updateUI();
    },

    toast: (msg) => {
        let t = document.getElementById('toast');
        t.innerText = msg;
        t.classList.add('show');
        setTimeout(()=>t.classList.remove('show'), 2000);
    },
    
    cardClick: (ovr) => {} // Placeholder
};

app.init();
</script>
</body>
</html>
