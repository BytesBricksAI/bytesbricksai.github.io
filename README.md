<!DOCTYPE html>
<html lang="es" data-lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>BytesBricks · SimPlant — Pitch Deck (ES/EN)</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Bricolage+Grotesque:opsz,wght@12..96,300..800&family=Atkinson+Hyperlegible:wght@400;700&display=swap" rel="stylesheet">
<style>
/* ════════════════════════════════════════════════════════════════
   BYTESBRICKS · SIMPLANT — PITCH DECK «HIPERLEGIBLE»
   Señalética suiza de planta: blanco puro, reglas de 1.5px,
   cero radios, rojo-señal + franja de peligro. Sin SVG: toda la
   carga visual es tipografía y CSS — 100% vectorial.

   SISTEMA DE COMPONENTES
   Cada parte de una slide es un componente discreto y animable,
   marcado con data-cmp="…" y la clase .rv (reveal). El stagger
   se controla con la variable --i (delay = --i × 80ms).
   Para agregar una animación propia a un componente:
     [data-cmp="stat"] { … }                     ← estado final
     .slide.visible [data-cmp="stat"] { … }      ← al entrar
   El estado .visible lo pone el IntersectionObserver del final.

   IDIOMA
   <html data-lang="es|en"> + spans .es/.en. Toggle con los
   botones ES/EN o la tecla L. La elección persiste (localStorage).
   ════════════════════════════════════════════════════════════════ */
:root{
  --bg:#ffffff;
  --ink:#141414;
  --muted:#454545;
  --line:#141414;             /* regla dura */
  --soft:#d9d9d9;             /* regla suave */
  --accent:#e03a00;           /* rojo-señal */
  --hazard:#ffb100;           /* ámbar de franja */
  --paper-dim:#f4f4f2;        /* fondo de celda alternativa */
  --display:'Bricolage Grotesque',sans-serif;
  --body:'Atkinson Hyperlegible',sans-serif;
  --ease:cubic-bezier(.16,1,.3,1);

  /* Escala fluida — todo clamp(), nada fijo */
  --t-hero:clamp(1.9rem,5.4vw,5rem);
  --t-h2:clamp(1.25rem,3.2vw,2.7rem);
  --t-h3:clamp(.9rem,1.5vw,1.25rem);
  --t-big:clamp(1rem,2.2vw,1.8rem);
  --t-sub:clamp(.85rem,1.5vw,1.15rem);
  --t-body:clamp(.72rem,1.15vw,.95rem);
  --t-small:clamp(.62rem,.95vw,.8rem);
  --t-tiny:clamp(.56rem,.85vw,.7rem);
  --pad-x:clamp(18px,3.2vw,52px);
  --pad-y:clamp(12px,2.4vh,32px);
  --gap:clamp(10px,2vh,24px);
}
*{margin:0;padding:0;box-sizing:border-box}
html,body{height:100%;overflow-x:hidden}
html{scroll-snap-type:y mandatory;scroll-behavior:smooth;background:var(--bg)}
body{background:var(--bg);color:var(--ink);font-family:var(--body)}

/* ═══ IDIOMA ═══ */
html[data-lang="es"] .en{display:none!important}
html[data-lang="en"] .es{display:none!important}
.lang-switch{
  position:fixed;top:0;right:0;z-index:100;display:flex;
  border-left:1.5px solid var(--line);border-bottom:1.5px solid var(--line);
  font-size:12px;font-weight:700;background:var(--bg);
}
.lang-switch button{all:unset;cursor:pointer;padding:9px 15px;color:var(--muted)}
.lang-switch button.active{background:var(--ink);color:#fff}
.lang-switch button:focus-visible{outline:2px solid var(--accent);outline-offset:-2px}

/* ═══ PROGRESO + PUNTOS DE NAVEGACIÓN (cuadrados, no círculos) ═══ */
.progress{
  position:fixed;top:0;left:0;height:3px;width:100%;z-index:99;
  background:var(--accent);transform-origin:0 0;transform:scaleX(0);
}
.nav-dots{
  position:fixed;right:clamp(8px,1.2vw,16px);top:50%;transform:translateY(-50%);
  z-index:99;display:flex;flex-direction:column;gap:7px;
}
.nav-dots button{
  all:unset;cursor:pointer;width:7px;height:7px;
  border:1.5px solid var(--ink);background:transparent;opacity:.4;
}
.nav-dots button.active{background:var(--accent);border-color:var(--accent);opacity:1}
.nav-dots button:focus-visible{outline:2px solid var(--accent);outline-offset:2px}

/* ═══ SLIDE: encaje exacto en viewport ═══ */
.slide{
  width:100vw;height:100vh;height:100dvh;overflow:hidden;
  scroll-snap-align:start;display:flex;flex-direction:column;
  position:relative;background:var(--bg);
}
/* Cabecera de cada slide */
[data-cmp="topbar"]{
  display:flex;justify-content:space-between;align-items:center;flex-shrink:0;gap:12px;
  border-bottom:1.5px solid var(--line);
  padding:clamp(8px,1.5vh,15px) var(--pad-x);
  /* aire extra a la derecha para no chocar con el toggle ES/EN fijo */
  padding-right:calc(var(--pad-x) + 88px);
  font-weight:700;font-size:clamp(10px,1.15vw,13.5px);
}
[data-cmp="topbar"] .chip{
  background:var(--accent);color:#fff;padding:3px 10px;font-family:var(--display);
  font-weight:700;white-space:nowrap;
}
[data-cmp="topbar"] .sect{color:var(--muted);font-weight:700}
/* Cuerpo */
.content{
  flex:1;display:flex;flex-direction:column;justify-content:center;
  gap:var(--gap);padding:var(--pad-y) var(--pad-x);
  min-height:0;overflow:hidden;
}
/* Pie de cada slide */
[data-cmp="foot"]{
  flex-shrink:0;border-top:1.5px solid var(--line);
  display:flex;justify-content:space-between;align-items:center;gap:16px;
  padding:clamp(6px,1.2vh,12px) var(--pad-x);
  font-size:clamp(9px,1vw,12px);color:var(--muted);
}
[data-cmp="foot"] b{color:var(--ink)}
[data-cmp="foot"] .num{font-family:var(--display);font-weight:700;color:var(--ink);white-space:nowrap}

/* ═══ TIPOGRAFÍA ═══ */
h1,h2,h3,p{margin:0}
h1{font-family:var(--display);font-weight:800;font-size:var(--t-hero);line-height:.98;letter-spacing:-.025em;max-width:15ch;text-wrap:balance}
h2{font-family:var(--display);font-weight:800;font-size:var(--t-h2);line-height:1.02;letter-spacing:-.02em;max-width:26ch;text-wrap:balance}
h3{font-family:var(--display);font-weight:700;font-size:var(--t-h3);line-height:1.15;letter-spacing:-.01em}
h1 em,h2 em{font-style:normal;color:var(--accent)}
.sub{font-size:var(--t-sub);line-height:1.5;color:var(--muted);max-width:60ch;text-wrap:pretty}
.sub b,.sub strong{color:var(--ink)}
p{font-size:var(--t-body);line-height:1.45;color:var(--muted)}
p strong,p b{color:var(--ink)}
.src{display:block;font-size:var(--t-tiny);color:#767676;margin-top:5px;line-height:1.3}

/* ═══ COMPONENTE: kicker (una sola vez por slide, nunca decorativo) ═══ */
[data-cmp="kicker"]{
  font-family:var(--display);font-weight:700;font-size:clamp(10px,1.2vw,13px);
  text-transform:uppercase;letter-spacing:.06em;color:var(--accent);
}

/* ═══ COMPONENTE: franja de peligro (firma del estilo) ═══ */
[data-cmp="hazard"]{
  height:clamp(7px,1.2vh,11px);width:min(400px,55%);flex-shrink:0;
  background:repeating-linear-gradient(-45deg,var(--hazard) 0 13px,var(--ink) 13px 26px);
  animation:stripes 16s linear infinite;
}
@keyframes stripes{to{background-position:-520px 0}}

/* ═══ COMPONENTE: grilla con reglas (celdas, no tarjetas) ═══
   El gap de 1.5px sobre fondo tinta dibuja las reglas — crisp y vectorial. */
.rulegrid{
  display:grid;gap:1.5px;background:var(--line);
  border:1.5px solid var(--line);min-height:0;
}
.rulegrid>*{background:var(--bg);padding:clamp(9px,1.7vh,20px) clamp(11px,1.6vw,22px);min-width:0;min-height:0}
.cols2{grid-template-columns:repeat(2,1fr)}
.cols3{grid-template-columns:repeat(3,1fr)}
.cols4{grid-template-columns:repeat(4,1fr)}
.split{grid-template-columns:1.15fr .85fr}
/* celda destacada: bloque tinta */
.rulegrid .hl{background:var(--ink);color:#fff}
.rulegrid .hl h3,.rulegrid .hl strong{color:#fff}
.rulegrid .hl p,.rulegrid .hl span{color:rgba(255,255,255,.78)}
.rulegrid .hl b{color:var(--hazard)}
/* celda atenuada */
.rulegrid .dim{background:var(--paper-dim)}

/* ═══ COMPONENTE: celda de dato (número grande + descriptor) ═══ */
[data-cmp="stat"] b{
  font-family:var(--display);font-weight:800;display:block;
  font-size:clamp(1.3rem,3vw,2.7rem);letter-spacing:-.02em;line-height:1;
}
[data-cmp="stat"] span{display:block;font-size:var(--t-small);color:var(--muted);margin-top:6px;line-height:1.4}
[data-cmp="stat"] span strong{color:var(--ink)}

/* ═══ COMPONENTE: etiqueta de estado (código de honestidad) ═══ */
[data-cmp="tag"]{
  display:inline-block;width:max-content;max-width:100%;
  font-family:var(--display);font-weight:700;font-size:clamp(8.5px,1vw,11px);
  text-transform:uppercase;letter-spacing:.05em;
  padding:3px 8px;border:1.5px solid var(--ink);margin-bottom:clamp(6px,1.2vh,12px);
}
[data-cmp="tag"].today{background:var(--ink);color:#fff}
[data-cmp="tag"].dev{background:var(--hazard);border-color:var(--hazard);color:var(--ink)}
[data-cmp="tag"].sim{background:var(--bg);color:var(--ink)}
[data-cmp="tag"].vision{border-style:dashed;border-color:var(--muted);color:var(--muted);background:var(--bg)}
[data-cmp="tag"].prospect{background:var(--paper-dim);border-color:var(--soft);color:var(--muted)}
[data-cmp="tag"].alert{background:var(--accent);border-color:var(--accent);color:#fff}

/* ═══ COMPONENTE: banda de reclamo (borde duro + franja superior) ═══ */
[data-cmp="claim"]{
  border:1.5px solid var(--ink);position:relative;
  padding:clamp(12px,2.2vh,24px) clamp(14px,2vw,26px);
  padding-top:calc(clamp(12px,2.2vh,24px) + 8px);
}
[data-cmp="claim"]::before{
  content:"";position:absolute;top:0;left:0;right:0;height:8px;
  background:repeating-linear-gradient(-45deg,var(--hazard) 0 11px,var(--ink) 11px 22px);
  animation:stripes 16s linear infinite;
}
[data-cmp="claim"] p{font-size:clamp(.78rem,1.3vw,1.05rem);color:var(--ink);line-height:1.5}
[data-cmp="claim"] .fine{font-size:var(--t-tiny);color:#767676;margin-top:8px;line-height:1.45}

/* ═══ COMPONENTE: flujo tipográfico (nodo → nodo → nodo) ═══ */
[data-cmp="flow"]{display:grid;grid-template-columns:1fr auto 1fr auto 1fr;gap:clamp(6px,1vw,14px);align-items:stretch}
[data-cmp="flow"] .node{border:1.5px solid var(--ink);padding:clamp(9px,1.6vh,18px) clamp(10px,1.4vw,18px)}
[data-cmp="flow"] .node strong{font-family:var(--display);font-weight:700;font-size:var(--t-h3);display:block}
[data-cmp="flow"] .node span{display:block;font-size:var(--t-small);color:var(--muted);margin-top:6px;line-height:1.4}
[data-cmp="flow"] .arrow{
  align-self:center;font-family:var(--display);font-weight:800;color:var(--accent);
  font-size:clamp(1.3rem,2.6vw,2.2rem);line-height:1;
  animation:nudge 2.4s var(--ease) infinite;
}
[data-cmp="flow"] .arrow:nth-of-type(4){animation-delay:1.2s}
@keyframes nudge{0%,100%{transform:translateX(0)}12%{transform:translateX(6px)}24%{transform:translateX(0)}}

/* ═══ COMPONENTE: fila de definición (término | descripción) ═══ */
[data-cmp="row"]{
  display:grid;grid-template-columns:clamp(100px,12vw,170px) 1fr;
  gap:clamp(10px,1.6vw,20px);align-items:start;
  border-top:1.5px solid var(--line);padding:clamp(7px,1.4vh,14px) 0;
}
[data-cmp="row"] strong{font-family:var(--display);font-weight:700;font-size:var(--t-body);color:var(--ink)}
[data-cmp="row"] p{font-size:var(--t-small);line-height:1.45}
.rows-tight [data-cmp="row"]{padding:clamp(5px,1vh,10px) 0}

/* ═══ COMPONENTE: lista con viñeta cuadrada (vectorial) ═══ */
ul{list-style:none;display:grid;gap:clamp(4px,.9vh,9px);margin-top:clamp(6px,1.2vh,12px)}
li{font-size:var(--t-small);line-height:1.45;color:var(--muted);padding-left:16px;position:relative}
li::before{content:"";position:absolute;left:0;top:.42em;width:7px;height:7px;background:var(--accent)}
li strong,li b{color:var(--ink)}

/* ═══ COMPONENTE: línea grande de cierre ═══ */
[data-cmp="bigline"]{
  font-family:var(--display);font-weight:700;font-size:var(--t-big);
  line-height:1.15;letter-spacing:-.015em;max-width:52ch;color:var(--ink);text-wrap:balance;
}
[data-cmp="bigline"] em{font-style:normal;color:var(--accent)}

/* ═══ COMPONENTE: persona (bloque de iniciales + bio) ═══ */
[data-cmp="person"]{display:flex;gap:clamp(10px,1.6vw,20px);align-items:flex-start}
[data-cmp="person"] .init{
  flex-shrink:0;width:clamp(42px,5vw,60px);height:clamp(42px,5vw,60px);
  background:var(--ink);color:#fff;display:flex;align-items:center;justify-content:center;
  font-family:var(--display);font-weight:800;font-size:clamp(.85rem,1.6vw,1.3rem);
}
[data-cmp="person"] h3{margin-bottom:4px}
[data-cmp="person"] p{margin-top:6px}

/* ═══ CABECERA DE SECCIÓN (kicker + h2 + sub) ═══ */
.head{display:grid;gap:clamp(6px,1.2vh,12px)}

/* ═══ LAYOUTS ═══ */
.l-cover{flex-direction:row;display:grid;grid-template-columns:1.5fr 1fr;padding:0;gap:0}
.l-cover .main{
  padding:var(--pad-y) var(--pad-x);border-right:1.5px solid var(--line);
  display:flex;flex-direction:column;justify-content:center;gap:clamp(12px,2.6vh,28px);min-width:0;
}
.l-cover .side{display:flex;flex-direction:column;min-width:0}
.l-cover .side>div{
  flex:1;display:flex;flex-direction:column;justify-content:center;
  padding:clamp(8px,1.6vh,20px) clamp(14px,2vw,30px);
  border-bottom:1.5px solid var(--line);min-height:0;
}
.l-cover .side>div:last-child{border-bottom:0}
.l-cover .side .sign{background:var(--ink);color:#fff}
.l-cover .side .sign b{color:var(--hazard)}
.l-cover .side .sign span{color:rgba(255,255,255,.75)}
.grid2{display:grid;grid-template-columns:1fr 1fr;gap:clamp(10px,1.6vw,22px);min-height:0}
.stack{display:grid;gap:clamp(8px,1.4vh,16px);align-content:start;min-height:0}

/* ═══ REVELADO POR COMPONENTE ═══
   Visible por defecto (sin JS no se pierde nada). Con JS, cada .rv
   parte oculto y entra al hacerse visible la slide, escalonado por --i. */
html.js .rv{opacity:0;transform:translateY(16px);
  transition:opacity .7s var(--ease),transform .7s var(--ease);
  transition-delay:calc(var(--i,0)*80ms)}
html.js .slide.visible .rv{opacity:1;transform:none}

/* ═══ ENCAJE EN VIEWPORTS BAJOS ═══ */
@media(max-height:760px){
  :root{--t-hero:clamp(1.7rem,4.8vw,3.8rem);--t-h2:clamp(1.1rem,2.9vw,2.1rem);--gap:clamp(8px,1.6vh,16px)}
  .src{display:none}
}
@media(max-height:640px){
  :root{--t-sub:clamp(.78rem,1.3vw,.95rem);--t-body:clamp(.68rem,1.05vw,.85rem)}
  [data-cmp="stat"] span{font-size:var(--t-tiny)}
  [data-cmp="flow"] .node span{display:none}
  .nav-dots{display:none}
}
@media(max-height:520px){
  [data-cmp="hazard"]{display:none}
  li{font-size:var(--t-tiny)}
}
/* ═══ MÓVIL: colapso a una columna ═══ */
@media(max-width:900px){
  .slide{height:auto;min-height:100dvh}
  .content{padding:clamp(16px,4vw,28px)}
  .l-cover{grid-template-columns:1fr}
  .l-cover .main{border-right:0;border-bottom:1.5px solid var(--line)}
  .cols2,.cols3,.cols4,.split,.grid2{grid-template-columns:1fr}
  [data-cmp="flow"]{grid-template-columns:1fr}
  [data-cmp="flow"] .arrow{transform:rotate(90deg);justify-self:center;animation:none}
  [data-cmp="row"]{grid-template-columns:1fr;gap:4px}
  .nav-dots{display:none}
  h1{max-width:100%}
}
@media(prefers-reduced-motion:reduce){
  *,*::before,*::after{animation:none!important;transition-duration:.01ms!important}
  html{scroll-behavior:auto}
  html.js .rv{opacity:1;transform:none}
}
</style>
</head>
<body>

<div class="progress" role="presentation"></div>
<div class="lang-switch" role="group" aria-label="Idioma / Language">
  <button data-set="es" class="active">ES</button>
  <button data-set="en">EN</button>
</div>
<nav class="nav-dots" aria-label="Navegación de slides"></nav>

<!-- ═══════════ 01 · PORTADA ═══════════ -->
<section class="slide" id="s1">
  <header data-cmp="topbar">
    <div>BytesBricks<span style="color:var(--accent)">.</span></div>
    <div class="chip">SimPlant</div>
    <div class="sect">Seed 2026</div>
  </header>
  <div class="content l-cover">
    <div class="main">
      <h1 class="rv" data-cmp="title" style="--i:0">
        <span class="es">Autonomía <em>restringida</em> para infraestructura industrial crítica.</span>
        <span class="en">Restricted <em>autonomy</em> for critical industrial infrastructure.</span>
      </h1>
      <div data-cmp="hazard" class="rv" style="--i:1" role="presentation"></div>
      <p class="sub rv" data-cmp="sub" style="--i:2">
        <span class="es">Empezamos optimizando el gas de antorcha en refinerías: menos desperdicio, menos emisiones, la misma seguridad operativa.</span>
        <span class="en">We start by optimizing refinery flare gas: less waste, fewer emissions, same operational safety.</span>
      </p>
    </div>
    <div class="side">
      <div data-cmp="stat" class="rv" style="--i:1">
        <b>151 bcm</b>
        <span class="es">Gas quemado en antorchas a nivel global · 2024</span>
        <span class="en">Gas flared globally · 2024</span>
      </div>
      <div data-cmp="stat" class="rv" style="--i:2">
        <b>US$63B</b>
        <span class="es">Valor energético perdido por año — alimentación desperdiciada</span>
        <span class="en">Energy value lost per year — wasted feedstock</span>
      </div>
      <div data-cmp="stat" class="sign rv" style="--i:3">
        <b>0</b>
        <span class="es">Violaciones del envolvente de seguridad en 260 episodios simulados</span>
        <span class="en">Safety-envelope violations across 260 simulated episodes</span>
      </div>
    </div>
  </div>
  <footer data-cmp="foot">
    <div>
      <span class="es"><b>Validación en gemelo digital completa</b> · GTM liderado por comunidad · El primer piloto sombra pago es el hito que financia esta ronda</span>
      <span class="en"><b>Twin validation complete</b> · Community-led GTM · First paid shadow pilot is the milestone this raise funds</span>
    </div>
    <div class="num">01 / 17</div>
  </footer>
</section>

<!-- ═══════════ 02 · PROBLEMA ECONÓMICO ═══════════ -->
<section class="slide" id="s2">
  <header data-cmp="topbar">
    <div>BytesBricks<span style="color:var(--accent)">.</span></div>
    <div class="chip"><span class="es">01 · Problema económico</span><span class="en">01 · Economic problem</span></div>
    <div class="sect"><span class="es">Dolor</span><span class="en">Pain</span></div>
  </header>
  <div class="content">
    <div class="head">
      <h2 class="rv" data-cmp="title" style="--i:0">
        <span class="es">Las refinerías queman margen, presupuesto de carbono y capacidad operativa en la <em>antorcha</em>.</span>
        <span class="en">Refineries burn margin, carbon budget, and operating capacity at the <em>flare stack</em>.</span>
      </h2>
      <p class="sub rv" data-cmp="sub" style="--i:1">
        <span class="es">La antorcha se trata como un punto de seguridad. En la práctica es una palanca continua de rentabilidad, emisiones y cumplimiento.</span>
        <span class="en">The flare is treated as a safety point. In practice it is a continuous lever for profitability, emissions, and compliance.</span>
      </p>
    </div>
    <div class="rulegrid cols3 rv" data-cmp="stats" style="--i:2">
      <div data-cmp="stat">
        <b>151 bcm</b>
        <span class="es">Gas quemado en antorchas a nivel global en 2024. Magnitud del mercado — no un modelo de ingresos directo.<span class="src">Fuente: World Bank Global Gas Flaring Tracker, 2024</span></span>
        <span class="en">Gas flared globally in 2024. Market magnitude — not a direct revenue model.<span class="src">Source: World Bank Global Gas Flaring Tracker, 2024</span></span>
      </div>
      <div data-cmp="stat">
        <b>389 MtCO₂e</b>
        <span class="es">Emisiones de la quema en antorcha convencional. La regulación ya no es opcional.<span class="src">Fuente: World Bank GGFR / estimaciones de metano IEA</span></span>
        <span class="en">Emissions from conventional flaring. Regulation is no longer optional.<span class="src">Source: World Bank GGFR / IEA methane estimates</span></span>
      </div>
      <div data-cmp="stat">
        <b>US$63B</b>
        <span class="es">Valor energético anual perdido estimado. Alimentación desperdiciada — no solo narrativa ESG.<span class="src">Fuente: World Bank Global Gas Flaring Reduction Partnership</span></span>
        <span class="en">Estimated annual energy value lost. Wasted feedstock — not just ESG narrative.<span class="src">Source: World Bank Global Gas Flaring Reduction Partnership</span></span>
      </div>
    </div>
    <div data-cmp="claim" class="rv" style="--i:3">
      <span data-cmp="tag" class="sim"><span class="es">SOM · de abajo hacia arriba</span><span class="en">SOM · bottoms-up</span></span>
      <p>
        <span class="es"><strong>~25 refinerías con antorcha en el beachhead LATAM</strong> × <strong>US$200–800K de ARR realista por sitio</strong> × <strong>5–10% de penetración alcanzable en 5 años</strong> = <strong>US$25–200M de mercado obtenible</strong>. Construido desde la base — no desde el titular de US$63B.</span>
        <span class="en"><strong>~25 flare-equipped refineries in LATAM beachhead</strong> × <strong>US$200–800K realistic ARR/site</strong> × <strong>5–10% achievable penetration over 5 years</strong> = <strong>US$25–200M serviceable obtainable market</strong>. Built from the ground up — not from the US$63B headline.</span>
      </p>
    </div>
  </div>
  <footer data-cmp="foot">
    <div><span class="es">SimPlant · Autonomía restringida</span><span class="en">SimPlant · Restricted autonomy</span></div>
    <div class="num">02 / 17</div>
  </footer>
</section>

<!-- ═══════════ 03 · POR QUÉ FALLAN LOS SISTEMAS ACTUALES ═══════════ -->
<section class="slide" id="s3">
  <header data-cmp="topbar">
    <div>BytesBricks<span style="color:var(--accent)">.</span></div>
    <div class="chip"><span class="es">02 · Por qué falla el stack actual</span><span class="en">02 · Why current systems fail</span></div>
    <div class="sect">Status quo</div>
  </header>
  <div class="content">
    <h2 class="rv" data-cmp="title" style="--i:0">
      <span class="es">El stack de hoy detecta, reporta o estabiliza. <em>No optimiza de forma autónoma</em> dentro de límites de seguridad.</span>
      <span class="en">Today's stack detects, reports, or stabilizes. It does <em>not autonomously optimize</em> within safety limits.</span>
    </h2>
    <div class="rulegrid cols4 rv" data-cmp="matrix" style="--i:1">
      <div>
        <h3>LDAR / <span class="es">cámaras</span><span class="en">cameras</span></h3>
        <p style="margin-top:8px"><span class="es">Encuentran fugas y eventos. No cambian la política de control.</span><span class="en">Find leaks and events. Do not change control policy.</span></p>
      </div>
      <div>
        <h3>DCS / PID</h3>
        <p style="margin-top:8px"><span class="es">Mantienen la planta estable. No aprenden trade-offs económicos.</span><span class="en">Keep the plant stable. Do not learn economic trade-offs.</span></p>
      </div>
      <div>
        <h3>APC / MPC</h3>
        <p style="margin-top:8px"><span class="es">Potentes en rangos conocidos. Frágiles en transitorios y límites de seguridad.</span><span class="en">Powerful in known ranges. Fragile on transients and safety limits.</span></p>
      </div>
      <div class="hl">
        <span data-cmp="tag" class="alert"><span class="es">Nosotros</span><span class="en">Us</span></span>
        <h3>SimPlant</h3>
        <p style="margin-top:8px"><span class="es">Capa de control autónomo restringido: entrenada en gemelo digital, desplegada en el edge, acotada por reglas de seguridad.</span><span class="en">Restricted autonomous control layer: trained on digital twin, deployed at edge, bounded by safety rules.</span></p>
      </div>
    </div>
    <p data-cmp="bigline" class="rv" style="--i:2">
      <span class="es"><em>La brecha:</em> nadie es dueño de la capa de control autónomo restringido para sistemas de antorcha.</span>
      <span class="en"><em>The gap:</em> no one owns the restricted autonomous control layer for flare systems.</span>
    </p>
  </div>
  <footer data-cmp="foot">
    <div><span class="es">SimPlant · Autonomía restringida</span><span class="en">SimPlant · Restricted autonomy</span></div>
    <div class="num">03 / 17</div>
  </footer>
</section>

<!-- ═══════════ 04 · POR QUÉ AHORA ═══════════ -->
<section class="slide" id="s4">
  <header data-cmp="topbar">
    <div>BytesBricks<span style="color:var(--accent)">.</span></div>
    <div class="chip"><span class="es">03 · Por qué ahora</span><span class="en">03 · Why now</span></div>
    <div class="sect">Timing</div>
  </header>
  <div class="content">
    <h2 class="rv" data-cmp="title" style="--i:0">
      <span class="es">Tres fuerzas hacen <em>invertible hoy</em> la autonomía industrial restringida.</span>
      <span class="en">Three forces make restricted industrial autonomy <em>investable today</em>.</span>
    </h2>
    <div class="rulegrid cols3 rv" data-cmp="forces" style="--i:1">
      <div>
        <span data-cmp="tag" class="today"><span class="es">Tracción económica</span><span class="en">Economic pull</span></span>
        <h3><span class="es">El gas recuperado es alimentación con valor inmediato en el P&amp;L — el caso del comprador es económico primero.</span><span class="en">Recovered flare gas is feedstock with immediate P&amp;L value — the buyer's case is economic first.</span></h3>
        <p style="margin-top:8px"><span class="es">En LATAM, los operadores recuperan margen de gas que de otro modo se quemaría. El ROI no depende solo de créditos de carbono.</span><span class="en">In LATAM, operators recover margin from gas that would otherwise be burned. The ROI case does not depend on carbon credits alone.</span></p>
      </div>
      <div>
        <span data-cmp="tag" class="sim"><span class="es">Presión regulatoria</span><span class="en">Regulatory pull</span></span>
        <h3><span class="es">La rendición de cuentas por metano se endurece — pasa del reporte a la prueba.</span><span class="en">Methane accountability is tightening — moving from reporting to proof.</span></h3>
        <p style="margin-top:8px"><span class="es">EU 2024/1787, OGMP 2.0, EPA y regímenes regionales de carbono empujan hacia reducciones medibles — también donde vendemos.</span><span class="en">EU 2024/1787, OGMP 2.0, EPA, and regional carbon regimes push operators toward measurable reductions — including where we sell.</span></p>
      </div>
      <div>
        <span data-cmp="tag" class="sim"><span class="es">Madurez técnica</span><span class="en">Technical maturity</span></span>
        <h3><span class="es">La IA segura, los gemelos digitales y la inferencia en el edge cruzaron el umbral de despliegue.</span><span class="en">Safe AI, digital twins, and edge inference crossed the deployment threshold.</span></h3>
        <p style="margin-top:8px"><span class="es">Ya no es un modelo de laboratorio: una política de control acotada que puede operar cerca de sistemas OT — con el SIS intacto.</span><span class="en">No longer a lab model: a bounded control policy that can operate near OT systems — with the SIS untouched.</span></p>
      </div>
    </div>
  </div>
  <footer data-cmp="foot">
    <div><span class="es">SimPlant · Autonomía restringida</span><span class="en">SimPlant · Restricted autonomy</span></div>
    <div class="num">04 / 17</div>
  </footer>
</section>

<!-- ═══════════ 05 · QUÉ HACE SIMPLANT ═══════════ -->
<section class="slide" id="s5">
  <header data-cmp="topbar">
    <div>BytesBricks<span style="color:var(--accent)">.</span></div>
    <div class="chip"><span class="es">04 · Qué hace SimPlant</span><span class="en">04 · What SimPlant does</span></div>
    <div class="sect"><span class="es">Producto</span><span class="en">Product</span></div>
  </header>
  <div class="content">
    <h2 class="rv" data-cmp="title" style="--i:0">
      <span class="es">SimPlant convierte la antorcha de la refinería en un <em>lazo de optimización restringido</em>.</span>
      <span class="en">SimPlant turns the refinery flare into a <em>restricted optimization loop</em>.</span>
    </h2>
    <div data-cmp="flow" class="rv" style="--i:1">
      <div class="node">
        <strong><span class="es">Sensores</span><span class="en">Sensors</span></strong>
        <span class="es">Tags de proceso, historia operativa, eventos de antorcha, señales de alivio.</span>
        <span class="en">Process tags, operating history, flare events, relief signals.</span>
      </div>
      <div class="arrow" aria-hidden="true">→</div>
      <div class="node">
        <strong><span class="es">Gemelo digital</span><span class="en">Digital twin</span></strong>
        <span class="es">Entorno calibrado por sitio para entrenar y validar antes de la planta real.</span>
        <span class="en">Site-calibrated environment to train and validate before live plant.</span>
      </div>
      <div class="arrow" aria-hidden="true">→</div>
      <div class="node">
        <strong><span class="es">Política segura</span><span class="en">Safe policy</span></strong>
        <span class="es">Control continuo acotado por límites de proceso, HSE y SIS — que nunca tocamos.</span>
        <span class="en">Continuous control bounded by process, HSE, and SIS limits — which we never touch.</span>
      </div>
    </div>
    <div data-cmp="claim" class="rv" style="--i:2">
      <span data-cmp="tag" class="today"><span class="es">Seguridad y responsabilidad</span><span class="en">Safety &amp; liability</span></span>
      <p>
        <span class="es"><strong>El SIS nunca se toca.</strong> SimPlant influye; el Sistema Instrumentado de Seguridad sigue siendo una red de seguridad independiente. Camino de confianza: recomendación → asesoría supervisada → control restringido — la confianza del operador se gana antes de cualquier autonomía.</span>
        <span class="en"><strong>The SIS is never touched.</strong> SimPlant influences; the Safety Instrumented System remains an independent safety net. Trust path: recommendation → supervised advisory → constrained control — operator confidence earned before any autonomy.</span>
      </p>
    </div>
    <div class="rulegrid cols2 rv" data-cmp="states" style="--i:3">
      <div>
        <span data-cmp="tag" class="today"><span class="es">Construido y operativo</span><span class="en">Built &amp; operational</span></span>
        <h3><span class="es">Plataforma SimPlant, gemelo digital y prototipo de política validado.</span><span class="en">SimPlant platform, digital twin, and validated policy prototype.</span></h3>
        <p style="margin-top:8px"><span class="es">Paquete de evidencia: corridas controladas, log de seguridad, métricas de emisiones y recuperación de gas — todo en simulación.</span><span class="en">Evidence package: controlled runs, safety log, emissions and gas-recovery metrics — all in simulation.</span></p>
      </div>
      <div>
        <span data-cmp="tag" class="dev"><span class="es">Diseñado, aún no construido</span><span class="en">Designed, not yet built</span></span>
        <h3><span class="es">Modo sombra e integración con planta real.</span><span class="en">Shadow mode and live-plant integration.</span></h3>
        <p style="margin-top:8px"><span class="es">Próximo hito: datos históricos reales, recomendaciones en sombra, gateway OT y flujo de aceptación del operador.</span><span class="en">Next milestone: real historical data, shadow recommendations, OT gateway, and operator acceptance workflow.</span></p>
      </div>
    </div>
  </div>
  <footer data-cmp="foot">
    <div>
      <span class="es">Historia simple: sensores → gemelo → política segura → restricciones → recomendaciones / control</span>
      <span class="en">Simple story: sensors → twin → safe policy → safety constraints → recommendations / control</span>
    </div>
    <div class="num">05 / 17</div>
  </footer>
</section>

<!-- ═══════════ 06 · ARQUITECTURA DE DESPLIEGUE ═══════════ -->
<section class="slide" id="s6">
  <header data-cmp="topbar">
    <div>BytesBricks<span style="color:var(--accent)">.</span></div>
    <div class="chip"><span class="es">05 · Arquitectura de despliegue</span><span class="en">05 · Deployment architecture</span></div>
    <div class="sect">Sim-to-real</div>
  </header>
  <div class="content">
    <div class="head">
      <h2 class="rv" data-cmp="title" style="--i:0">
        <span class="es">Qué está construido, qué está diseñado y qué está validado <em>solo en simulación</em>.</span>
        <span class="en">What is built, what is designed, and what is validated <em>only in simulation</em>.</span>
      </h2>
      <p class="sub rv" data-cmp="sub" style="--i:1">
        <span class="es">Gemelo digital destilado de dos proyectos reales de ingeniería. No es un simulador académico.</span>
        <span class="en">Digital twin distilled from two real engineering projects. Not an academic simulator.</span>
      </p>
    </div>
    <div class="rulegrid cols3 rv" data-cmp="status" style="--i:2">
      <div>
        <span data-cmp="tag" class="today"><span class="es">Construido y operativo</span><span class="en">Built &amp; operational</span></span>
        <p><span class="es">Plataforma SimPlant, pipeline de entrenamiento reproducible, política restringida entrenada y gemelo calibrado con dos proyectos reales de planta.</span><span class="en">SimPlant platform, reproducible training pipeline, trained constrained policy, and a digital twin calibrated from two real plant projects.</span></p>
      </div>
      <div>
        <span data-cmp="tag" class="dev"><span class="es">Diseñado, aún no construido</span><span class="en">Designed, not yet built</span></span>
        <p><span class="es">Gateway edge OPC-UA e integración OT: arquitectura definida, inferencia &lt;100 ms como restricción de diseño. <strong>Aún no desplegado contra OT en vivo.</strong></span><span class="en">OPC-UA edge gateway and OT integration: architecture defined, &lt;100 ms inference as a design constraint. <strong>Not yet deployed against live OT.</strong></span></p>
      </div>
      <div>
        <span data-cmp="tag" class="sim"><span class="es">Validado solo en simulación</span><span class="en">Validated in simulation only</span></span>
        <p><span class="es">Todas las métricas de desempeño de la slide 07 provienen del gemelo calibrado. Sin validación en planta real todavía.</span><span class="en">All performance metrics on slide 07 come from the calibrated twin. No live-plant validation yet.</span></p>
      </div>
    </div>
    <div class="grid2 rv" data-cmp="detail" style="--i:3">
      <div class="stack">
        <div data-cmp="claim">
          <span data-cmp="tag" class="today"><span class="es">Calibración fundacional · foso de datos propietario</span><span class="en">Foundational calibration · proprietary data moat</span></span>
          <p style="font-size:var(--t-small)">
            <span class="es"><strong>#1 Refinería:</strong> modernización de antorcha — presión de colector, caudales, trade-offs gas/emisiones. <strong>#2 Puerto:</strong> antorcha integrada con requisitos completos de SIL, emisiones y HSE. Dos proyectos reales de ingeniería — no pilotos — usados para calibrar el gemelo. <strong>Son datos que otros no pueden comprar.</strong></span>
            <span class="en"><strong>#1 Refinery:</strong> flare modernization — header pressure, flow rates, gas/emission trade-offs. <strong>#2 Port:</strong> integrated flare with full SIL, emissions, and HSE requirements. Two real engineering projects — not pilots — used to calibrate the twin. <strong>This is data others cannot buy.</strong></span>
          </p>
        </div>
        <div>
          <span data-cmp="tag" class="dev"><span class="es">Próximo hito técnico</span><span class="en">Next technical milestone</span></span>
          <p style="font-size:var(--t-small)"><span class="es">Calibración grado HYSYS + datos históricos del design partner. Esperamos 20–30% de degradación sim-to-real; el modo sombra cierra esa brecha. La robustez OOD (ruido de sensores, transitorios no entrenados) es el hito técnico siguiente.</span><span class="en">HYSYS-grade calibration + design-partner historical data. We expect 20–30% sim-to-real degradation; shadow mode closes that gap. OOD robustness (sensor noise, untrained transients) is the following technical milestone.</span></p>
        </div>
      </div>
      <div class="stack">
        <div class="rulegrid" style="grid-template-columns:1fr">
          <div class="dim">
            <p style="font-size:var(--t-small)"><span class="es"><strong>Construido desde cero por el founder:</strong> Soft Actor-Critic en PyTorch (replay buffer acotado, actor squashed-Gaussian, críticos gemelos, temperatura aprendible). Write-up técnico compartido en <strong>CACHE (Computer Aids for Chemical Engineering)</strong>.</span><span class="en"><strong>Built from scratch by the founder:</strong> Soft Actor-Critic in PyTorch (bounded replay buffer, squashed-Gaussian actor, twin critics, learnable temperature). Technical write-up shared in <strong>CACHE (Computer Aids for Chemical Engineering)</strong>.</span></p>
          </div>
        </div>
        <div>
          <span data-cmp="tag" class="sim"><span class="es">Procedencia de datos</span><span class="en">Data provenance</span></span>
          <p style="font-size:var(--t-small)"><span class="es">Datos de calibración de dos proyectos reales de ingeniería, usados bajo derechos de ingeniería del founder y obligaciones de confidencialidad.</span><span class="en">Calibration data from two real engineering projects, used under founder engineering rights and confidentiality obligations.</span></p>
        </div>
      </div>
    </div>
  </div>
  <footer data-cmp="foot">
    <div>
      <span class="es"><b>200 episodios de entrenamiento + 60 de despliegue · 0 violaciones del envolvente</b> · Ingeniería liderada por el founder</span>
      <span class="en"><b>200 training + 60 deployment episodes · 0 safety-envelope violations</b> · Founder-led engineering</span>
    </div>
    <div class="num">06 / 17</div>
  </footer>
</section>

<!-- ═══════════ 07 · EVIDENCIA DE VALIDACIÓN ═══════════ -->
<section class="slide" id="s7">
  <header data-cmp="topbar">
    <div>BytesBricks<span style="color:var(--accent)">.</span></div>
    <div class="chip"><span class="es">06 · Evidencia de validación</span><span class="en">06 · Validation evidence</span></div>
    <div class="sect"><span class="es">Resultados</span><span class="en">Results</span></div>
  </header>
  <div class="content">
    <div class="head">
      <h2 class="rv" data-cmp="title" style="--i:0">
        <span class="es">La política mejora la economía de la antorcha <em>sin fallas de seguridad</em> en el gemelo.</span>
        <span class="en">The policy improves flare economics <em>without safety failures</em> in the twin.</span>
      </h2>
      <p class="sub rv" data-cmp="sub" style="--i:1;font-size:var(--t-small)">
        <span class="es">Métricas de simulación sobre un gemelo calibrado con dos proyectos reales de planta — todavía no son resultados de planta real. Etiquetado con transparencia para inversores.</span>
        <span class="en">Simulation metrics on a twin calibrated from two real plant projects — not live-plant results yet. Labeled transparently for investors.</span>
      </p>
    </div>
    <div class="grid2">
      <div class="stack">
        <div data-cmp="claim" class="rv" style="--i:2">
          <p>
            <span class="es"><strong>Valor modelado por sitio: ~US$1,0M/año</strong> — gas incremental recuperado: SimPlant recupera <strong>~231% más gas de antorcha</strong> que el controlador base (≈15.000 kg/día incrementales), valuado a un conservador <strong>~US$3,5/MMBtu</strong> (ancla Plan Gas.Ar / Henry Hub, mediados de 2026). Recuperación total del sistema ≈US$1,5M/año; neto de OPEX. <strong>La validación en sombra en planta es el próximo punto de prueba.</strong></span>
            <span class="en"><strong>Modeled value per site: ~US$1.0M/yr</strong> — incremental recovered gas: SimPlant recovers <strong>~231% more flare gas</strong> than the baseline controller (≈15,000 kg/day incremental), valued at a conservative <strong>~US$3.5/MMBtu</strong> (Plan Gas.Ar / Henry Hub anchor, mid-2026). Total system recovery ≈US$1.5M/yr; net of system OPEX. <strong>Plant shadow validation is the next proof point.</strong></span>
          </p>
          <p class="fine">
            <span class="es">Supuestos visibles: volumen incremental (~15.000 kg/día del gemelo) × precio conservador ~US$3,5/MMBtu · gas ≈ calidad metano (NHV de antorcha ~899 BTU/scf en sim) · neto de OPEX · solo simulación, no datos auditados de planta.</span>
            <span class="en">Assumptions visible: incremental recovered-gas volume (~15,000 kg/day from the twin) × conservative gas price ~US$3.5/MMBtu · gas ≈ methane-quality (flare NHV ~899 BTU/scf in sim) · net of system OPEX · simulation only, not audited plant data.</span>
          </p>
        </div>
        <p class="rv" style="--i:3;font-size:var(--t-tiny);color:#767676;line-height:1.45">
          <span class="es"><strong style="color:var(--ink)">Emisiones (cumplimiento, no monetizado):</strong> en el gemelo la política reduce CO₂eq ~72% y limita la quema a ~10% del tiempo operativo. Brecha honesta: en esos intervalos, la eficiencia de combustión y el NHV caen debajo de los objetivos de 98% / 40 CFR 60.18 — próximo ítem de trabajo, separado del caso en dólares (sin precio de carbono en LATAM).</span>
          <span class="en"><strong style="color:var(--ink)">Emissions (compliance, not monetized):</strong> in the twin the policy cuts CO₂eq ~72% and keeps flaring to ~10% of operating time. Honest gap: during those flaring intervals, combustion efficiency and flare NHV fall below the 98% / 40 CFR 60.18 targets — a known next-work item, kept separate from the dollar case (no carbon price in LATAM).</span>
        </p>
      </div>
      <div class="stack">
        <div class="rulegrid cols2 rv" data-cmp="stats" style="--i:2">
          <div data-cmp="stat">
            <b>0</b>
            <span class="es"><strong>Violaciones del envolvente de seguridad</strong> en 200 + 60 episodios — valida la capa de restricciones duras (la IA nunca anula el SIS), <strong>no</strong> la robustez fuera de distribución.</span>
            <span class="en"><strong>Safety-envelope violations</strong> across 200 + 60 episodes — validates the hard-constraint layer (the AI never overrides the SIS), <strong>not</strong> out-of-distribution robustness.</span>
          </div>
          <div data-cmp="stat">
            <b>+231%</b>
            <span class="es"><strong>Evidencia direccional solamente:</strong> mejora de recuperación de gas vs. baseline de control legado en el escenario simulado (requiere validación en sombra en planta).</span>
            <span class="en"><strong>Directional evidence only:</strong> gas-recovery uplift vs. legacy-control baseline in the simulated scenario (requires plant shadow validation).</span>
          </div>
        </div>
        <div class="rulegrid cols2 rv" data-cmp="notes" style="--i:3">
          <div>
            <span data-cmp="tag" class="today"><span class="es">Seguridad</span><span class="en">Safety</span></span>
            <p style="font-size:var(--t-small)"><span class="es">El SIS nunca se toca. Camino de confianza: recomendación → asesoría supervisada → control restringido.</span><span class="en">The SIS is never touched. Trust path: recommendation → supervised advisory → constrained control.</span></p>
          </div>
          <div>
            <span data-cmp="tag" class="dev"><span class="es">Próxima prueba</span><span class="en">Next proof point</span></span>
            <p style="font-size:var(--t-small)"><span class="es">Cerrar la brecha sim-to-real con datos históricos, calibración HYSYS y recomendaciones en sombra medidas contra el baseline del operador.</span><span class="en">Close sim-to-real gap with historical data, HYSYS calibration, and shadow recommendations measured against operator baseline.</span></p>
          </div>
        </div>
      </div>
    </div>
  </div>
  <footer data-cmp="foot">
    <div><span class="es">Gemelo calibrado con dos proyectos reales de planta · sin datos de planta viva aún</span><span class="en">Twin calibrated from two real plant projects · no live-plant data yet</span></div>
    <div class="num">07 / 17</div>
  </footer>
</section>

<!-- ═══════════ 08 · SEÑALES TEMPRANAS Y MOTION DE ENTRADA ═══════════ -->
<section class="slide" id="s8">
  <header data-cmp="topbar">
    <div>BytesBricks<span style="color:var(--accent)">.</span></div>
    <div class="chip"><span class="es">07 · Señales y entrada</span><span class="en">07 · Early signals &amp; motion</span></div>
    <div class="sect">Go-to-market</div>
  </header>
  <div class="content">
    <div class="head">
      <h2 class="rv" data-cmp="title" style="--i:0">
        <span class="es"><em>Pre-revenue</em> — dicho sin vueltas. Señales tempranas reales y una estrategia de adquisición creíble.</span>
        <span class="en"><em>Pre-revenue</em> — stated plainly. Real early signals and a credible acquisition strategy.</span>
      </h2>
      <p class="sub rv" data-cmp="sub" style="--i:1">
        <span class="es">Sin clientes firmados todavía. Mostramos tracción de comunidad, motion de entrada y objetivos etiquetados con honestidad — no logos inflados.</span>
        <span class="en">No signed customers yet. We show community traction, entry motion, and honestly labeled targets — not inflated logos.</span>
      </p>
    </div>
    <div class="rulegrid split rv" data-cmp="gtm" style="--i:2">
      <div>
        <span data-cmp="tag" class="sim"><span class="es">Motion de entrada</span><span class="en">Entry motion</span></span>
        <p><span class="es">La barrera de confianza es la restricción real — las refinerías no compran software cercano al control en frío. Nuestro motion la rodea:</span><span class="en">The trust barrier is the real constraint — refineries don't buy control-adjacent software cold. Our motion routes around it:</span></p>
        <ul>
          <li><span class="es"><strong>Cuña de baja barrera</strong> — herramienta de análisis/simulación que no toca OT ni control; la comunidad de ingeniería química la adopta libremente</span><span class="en"><strong>Low-barrier wedge</strong> — analytics/simulation tool that touches no OT and no control; chem-eng community adopts freely</span></li>
          <li><span class="es"><strong>Motor de credibilidad</strong> — publicaciones en CACHE, construcción en público, advisor de O&amp;G con credenciales</span><span class="en"><strong>Credibility engine</strong> — CACHE publishing, building in public, credentialed O&amp;G advisor</span></li>
          <li><span class="es"><strong>Canales sancionados</strong> — brazos de I+D corporativos (p. ej. Y-TEC de YPF), desafíos de innovación abierta, red de aceleradoras, eventos de industria</span><span class="en"><strong>Sanctioned channels</strong> — corporate R&amp;D arms (e.g., YPF's Y-TEC), open-innovation challenges, accelerator network, industry events</span></li>
          <li><span class="es"><strong>Inbound</strong> — el primer pedido es casi cero: charla técnica de 30 min, análisis gratuito de datos de antorcha o NDA de datos — nunca un piloto pago en frío</span><span class="en"><strong>Inbound</strong> — first ask is near-zero: 30-min technical chat, free flaring-data analysis, or data NDA — never a cold paid pilot</span></li>
        </ul>
      </div>
      <div>
        <span data-cmp="tag" class="today"><span class="es">Señales tempranas</span><span class="en">Early signals</span></span>
        <ul>
          <li><span class="es">Trabajo técnico compartido en CACHE con recepción positiva</span><span class="en">Technical work shared in CACHE with positive reception</span></li>
          <li><span class="es">Interés inbound generado desde el trabajo en GitHub</span><span class="en">Inbound interest generated from the GitHub work</span></li>
        </ul>
        <div style="margin-top:clamp(10px,2vh,18px)">
          <span data-cmp="tag" class="prospect"><span class="es">Comprador objetivo · piloto pago futuro</span><span class="en">Target buyer · future paid pilot</span></span>
          <p style="font-size:var(--t-small)"><span class="es">Sponsor económico: VP Ops / CFO. Sponsor técnico: Ingeniería de Procesos. Gatekeepers: HSE y Seguridad OT. <strong>ICP:</strong> refinerías downstream, 100–500 kbpd, presión por metano, presupuestos de modernización. <strong>Objetivo de LOI: Q4 2026.</strong></span><span class="en">Economic sponsor: VP Ops / CFO. Technical sponsor: Process Engineering. Gatekeepers: HSE &amp; OT Security. <strong>ICP:</strong> downstream refineries, 100–500 kbpd, methane pressure, modernization budgets. <strong>LOI target: Q4 2026.</strong></span></p>
        </div>
      </div>
    </div>
  </div>
  <footer data-cmp="foot">
    <div><span class="es">NOC-first, por puertas sancionadas — no venta fría</span><span class="en">NOC-first, through sanctioned doors — not cold sales</span></div>
    <div class="num">08 / 17</div>
  </footer>
</section>

<!-- ═══════════ 09 · OBJETIVOS Y CAMINO DE ENTRADA ═══════════ -->
<section class="slide" id="s9">
  <header data-cmp="topbar">
    <div>BytesBricks<span style="color:var(--accent)">.</span></div>
    <div class="chip"><span class="es">07 · Objetivos de entrada</span><span class="en">07 · Targets &amp; entry path</span></div>
    <div class="sect">Go-to-market</div>
  </header>
  <div class="content">
    <h2 class="rv" data-cmp="title" style="--i:0">
      <span class="es">Objetivos con <em>puerta de entrada definida</em> — sin relaciones firmadas, sin logos inflados.</span>
      <span class="en">Targets with a <em>defined entry path</em> — no signed relationships, no inflated logos.</span>
    </h2>
    <div class="rulegrid split rv" data-cmp="targets" style="--i:1">
      <div>
        <span data-cmp="tag" class="prospect"><span class="es">Beachhead primario — YPF</span><span class="en">Primary beachhead — YPF</span></span>
        <p>
          <span class="es"><strong>NOC integrada</strong>, ~57% del crudo refinado en Argentina, gran CAPEX, presión ESG + digitalización.<br><strong>Puerta de entrada: Y-TEC</strong> (brazo de I+D de YPF, 51% YPF / 49% CONICET) — alineado en control de procesos, eficiencia energética y plantas piloto. Acceso vía convocatorias abiertas de Y-TEC y el canal académico/CONICET (universidad del founder + red CACHE), apuntando a una colaboración de I+D de bajo riesgo. <strong>Puerta sancionada — no venta fría.</strong> El hackathon de innovación de YPF vuelve en 2027 como puerta secundaria.</span>
          <span class="en"><strong>Integrated NOC</strong>, ~57% of refined crude in Argentina, large CAPEX, ESG + digitalization pressure.<br><strong>Entry path: Y-TEC</strong> (YPF's R&amp;D arm, 51% YPF / 49% CONICET) — domain-aligned in process control, energy efficiency, and pilot plants. Access via Y-TEC open calls and the academic/CONICET channel (founder's university + CACHE network), targeting a low-risk R&amp;D collaboration. <strong>Sanctioned door — not cold sales.</strong> The YPF innovation hackathon returns in 2027 as a secondary door.</span>
        </p>
      </div>
      <div class="stack" style="gap:0">
        <div style="border-bottom:1.5px solid var(--line);padding-bottom:clamp(8px,1.4vh,14px)">
          <span data-cmp="tag" class="prospect">Pan American Energy — Campana</span>
          <p style="font-size:var(--t-small)"><span class="es">La refinería más moderna de la región, expansión reciente, foco en eficiencia + HSE, cultura de pilotos. <strong>Entrada:</strong> cuña + inbound + intro del advisor; comprador más ágil que una NOC pura.</span><span class="en">Region's most modern refinery, recent expansion, efficiency + HSE focus, pilot culture. <strong>Entry:</strong> wedge + inbound + advisor intro; faster-moving buyer than a pure NOC.</span></p>
        </div>
        <div style="border-bottom:1.5px solid var(--line);padding:clamp(8px,1.4vh,14px) 0">
          <span data-cmp="tag" class="prospect">Petrobras</span>
          <p style="font-size:var(--t-small)"><span class="es">NOC grande, cultura de medición de metano, presión regulatoria, escala. <strong>Entrada:</strong> credibilidad acumulada (CACHE, advisor, inbound) + canales institucionales. Más fría; expansión de año 2.</span><span class="en">Large NOC, methane-measurement culture, regulatory pressure, scale. <strong>Entry:</strong> accumulated credibility (CACHE, advisor, inbound) + institutional channels. Colder; year-2 expansion.</span></p>
        </div>
        <div style="padding-top:clamp(8px,1.4vh,14px)">
          <span data-cmp="tag" class="vision"><span class="es">Corea — mercado global</span><span class="en">Korea — global market</span></span>
          <p style="font-size:var(--t-small)"><span class="es">Uno de los clusters de refinación más grandes del mundo (Ulsan, Yeosu — SK, GS, S-Oil, HD Hyundai Oilbank). Refleja ambición global y TAM. <strong>Entrada:</strong> habilitada por el Fast Track remoto de Antler + red de aceleradoras.</span><span class="en">One of the world's largest refining clusters (Ulsan, Yeosu — SK, GS, S-Oil, HD Hyundai Oilbank). Reflects global ambition and TAM. <strong>Entry:</strong> enabled by Antler's remote Fast Track + accelerator network.</span></p>
        </div>
      </div>
    </div>
  </div>
  <footer data-cmp="foot">
    <div><span class="es">Cada objetivo tiene una puerta definida · NOC-first, por canales sancionados</span><span class="en">Each target has a defined entry path · NOC-first, through sanctioned channels</span></div>
    <div class="num">09 / 17</div>
  </footer>
</section>

<!-- ═══════════ 10 · PRIMER PILOTO ═══════════ -->
<section class="slide" id="s10">
  <header data-cmp="topbar">
    <div>BytesBricks<span style="color:var(--accent)">.</span></div>
    <div class="chip"><span class="es">08 · Primer piloto</span><span class="en">08 · First pilot plan</span></div>
    <div class="sect"><span class="es">Despliegue</span><span class="en">Deployment</span></div>
  </header>
  <div class="content">
    <div class="head">
      <h2 class="rv" data-cmp="title" style="--i:0">
        <span class="es">De la validación simulada a la referencia industrial — <em>un plan de piloto honesto</em>.</span>
        <span class="en">From simulated validation to industrial reference — <em>one honest pilot plan</em>.</span>
      </h2>
      <p class="sub rv" data-cmp="sub" style="--i:1">
        <span class="es"><strong>Pilotos completados a la fecha: 0 — este es el hito que financia la ronda.</strong></span>
        <span class="en"><strong>Pilots completed to date: 0 — this is the milestone the raise funds.</strong></span>
      </p>
    </div>
    <div class="rulegrid split rv" data-cmp="pilot" style="--i:2">
      <div>
        <span data-cmp="tag" class="dev"><span class="es">Primer piloto — estructura (modo sombra)</span><span class="en">First pilot — structure (shadow mode)</span></span>
        <h3><span class="es">Modo sombra en refinería ancla de LATAM</span><span class="en">Shadow mode at anchor LATAM refinery</span></h3>
        <p style="margin-top:8px"><span class="es"><strong>Alcance:</strong> acceso a datos OT, calibración grado HYSYS, instalación de gateway edge, ingesta en tiempo real <strong>sin control en lazo cerrado</strong>.</span><span class="en"><strong>Scope:</strong> OT data access, HYSYS-grade calibration, edge gateway install, real-time ingestion <strong>without closed-loop control</strong>.</span></p>
        <p style="margin-top:6px"><span class="es"><strong>KPI único:</strong> reducción del tiempo de antorcha activa vs. baseline del operador (auto-reportado; la medición independiente es el paso siguiente). KPI elegido por ser una variable que la política demuestra controlar.</span><span class="en"><strong>Single KPI:</strong> reduction in active flare time vs. operator baseline (self-reported; independent measurement is the following step). KPI chosen to be a variable the policy demonstrably controls.</span></p>
        <p style="margin-top:6px"><span class="es"><strong>Ticket:</strong> US$100K–300K, pago. <strong>Duración:</strong> 12–16 semanas post-acceso a datos.</span><span class="en"><strong>Ticket:</strong> US$100K–300K, paid. <strong>Duration:</strong> 12–16 weeks post-data-access.</span></p>
      </div>
      <div>
        <span data-cmp="tag" class="today"><span class="es">Cómo se gana la confianza del operador</span><span class="en">How a cautious operator gets comfortable</span></span>
        <p><span class="es">El piloto se gana río abajo de la relación — no en frío. De-riesgamos el lado del operador: el SIS nunca se toca; primero solo-sombra; un único KPI medible; un ticket chico.</span><span class="en">The pilot is earned downstream of the relationship — not cold. We de-risk the operator's side: the SIS is never touched; shadow-only first; a single measurable KPI; a small ticket.</span></p>
        <p style="margin-top:8px"><span class="es"><strong>Secuencia:</strong> relación (vía cuña/canal) → análisis/backtest gratuito o de bajo costo sobre sus datos → piloto sombra pago → asesoría supervisada → control restringido.</span><span class="en"><strong>Sequence:</strong> relationship (via wedge/channel) → free or low-cost analysis/backtest on their data → paid shadow pilot → supervised advisory → constrained control.</span></p>
      </div>
    </div>
    <div class="rulegrid cols4 rv" data-cmp="timeline" style="--i:3">
      <div>
        <span data-cmp="tag" class="dev">Q4 2026</span>
        <h3><span class="es">Design partner + LOI</span><span class="en">Design partner + LOI</span></h3>
        <p style="margin-top:6px;font-size:var(--t-small)"><span class="es">1 design partner con datos, KPI y sponsor ejecutivo.</span><span class="en">1 design partner with data, KPI, and executive sponsor.</span></p>
      </div>
      <div>
        <span data-cmp="tag" class="dev">Q1 2027</span>
        <h3><span class="es">Kickoff de piloto pago</span><span class="en">Paid pilot kickoff</span></h3>
        <p style="margin-top:6px;font-size:var(--t-small)"><span class="es">PoC con fee pago; aprobación HSE.</span><span class="en">PoC with paid fee; HSE approval.</span></p>
      </div>
      <div>
        <span data-cmp="tag" class="dev">Q2 2027</span>
        <h3><span class="es">Modo sombra</span><span class="en">Shadow mode</span></h3>
        <p style="margin-top:6px;font-size:var(--t-small)"><span class="es">Recomendaciones medidas vs. baseline; ingesta OT en vivo.</span><span class="en">Recommendations measured vs. baseline; live OT ingestion.</span></p>
      </div>
      <div>
        <span data-cmp="tag" class="vision">2027+</span>
        <h3><span class="es">Asesoría → SaaS</span><span class="en">Advisory → SaaS</span></h3>
        <p style="margin-top:6px;font-size:var(--t-small)"><span class="es">ROI documentado → contrato recurrente US$200K–800K ARR.</span><span class="en">Documented ROI → recurring contract US$200K–800K ARR.</span></p>
      </div>
    </div>
  </div>
  <footer data-cmp="foot">
    <div><span class="es"><b>Camino:</b> evaluación paga → sombra → asesoría supervisada → control autónomo restringido</span><span class="en"><b>Path:</b> paid evaluation → shadow → supervised advisory → constrained autonomous control</span></div>
    <div class="num">10 / 17</div>
  </footer>
</section>

<!-- ═══════════ 11 · MODELO ECONÓMICO ═══════════ -->
<section class="slide" id="s11">
  <header data-cmp="topbar">
    <div>BytesBricks<span style="color:var(--accent)">.</span></div>
    <div class="chip"><span class="es">09 · Modelo económico</span><span class="en">09 · Economic model</span></div>
    <div class="sect"><span class="es">Negocio</span><span class="en">Business</span></div>
  </header>
  <div class="content">
    <h2 class="rv" data-cmp="title" style="--i:0">
      <span class="es">Empezamos con despliegue pago. Escalamos a <em>software de control recurrente</em> de alto margen.</span>
      <span class="en">We start with paid deployment. We scale to high-margin <em>recurring control software</em>.</span>
    </h2>
    <div class="rulegrid cols4 rv" data-cmp="pricing" style="--i:1">
      <div>
        <span data-cmp="tag" class="sim"><span class="es">Piloto / Sombra</span><span class="en">Pilot / Shadow</span></span>
        <h3>US$100K–300K</h3>
        <p style="margin-top:6px;font-size:var(--t-small)"><span class="es">Entrada de baja fricción. Cubre gateway, calibración del gemelo y validación en sombra antes del lazo cerrado.</span><span class="en">Low-friction entry. Covers gateway, twin calibration, and shadow validation before closed-loop.</span></p>
      </div>
      <div>
        <span data-cmp="tag" class="sim">Setup</span>
        <h3>US$0,4M–2M</h3>
        <p style="margin-top:6px;font-size:var(--t-small)"><span class="es">Gemelo por sitio, integración OT, calibración de datos, workflow HSE. Intensivo en servicios, estratégico.</span><span class="en">Per-site twin, OT integration, data calibration, HSE workflow. Service-heavy, strategic.</span></p>
      </div>
      <div>
        <span data-cmp="tag" class="sim"><span class="es">Recurrente</span><span class="en">Recurring</span></span>
        <h3>US$200K–800K ARR</h3>
        <p style="margin-top:6px;font-size:var(--t-small)"><span class="es">Software de optimización, monitoreo, actualizaciones de política, gobernanza de modelos y soporte.</span><span class="en">Optimization software, monitoring, policy updates, model governance, and support.</span></p>
      </div>
      <div>
        <span data-cmp="tag" class="vision"><span class="es">Expansión</span><span class="en">Expansion</span></span>
        <h3><span class="es">Antorcha → off-gas → APC</span><span class="en">Flare → off-gas → APC</span></h3>
        <p style="margin-top:6px;font-size:var(--t-small)"><span class="es">Aterrizar en la cuña crítica de seguridad; expandir a unidades adyacentes y sitios corporativos.</span><span class="en">Land on safety-critical wedge; expand to adjacent units and corporate sites.</span></p>
      </div>
    </div>
    <div class="rulegrid cols2 rv" data-cmp="notes" style="--i:2">
      <div>
        <span data-cmp="tag" class="today"><span class="es">Valor modelado por sitio</span><span class="en">Modeled value per site</span></span>
        <p><span class="es"><strong>~US$1,0M/año incremental</strong> (derivado de simulación: ~15.000 kg/día recuperados × ~US$3,5/MMBtu; recuperación total del sistema ~US$1,5M) · payback a confirmar vs. costo del sistema · el rango depende del tamaño de planta y el precio del gas.</span><span class="en"><strong>~US$1.0M/yr incremental</strong> (simulation-derived: ~15,000 kg/day recovered × ~US$3.5/MMBtu; total system recovery ~US$1.5M) · payback to confirm vs. system cost · range driven by plant size and gas price.</span></p>
      </div>
      <div>
        <span data-cmp="tag" class="sim"><span class="es">Producto vs. servicios</span><span class="en">Product vs. services</span></span>
        <p><span class="es"><strong>Reutilizable entre sitios (producto):</strong> toolkit de restricciones, framework de políticas, playbook de aceptación.<br><strong>Reconstruido por sitio (servicios):</strong> calibración del gemelo e integración OT específicas. El margen se compone a medida que crece la capa reutilizable.</span><span class="en"><strong>Reused across sites (product):</strong> constraint toolkit, policy framework, acceptance playbook.<br><strong>Rebuilt per site (services):</strong> site-specific twin calibration and OT integration. Margin compounds as the reusable layer grows.</span></p>
      </div>
    </div>
  </div>
  <footer data-cmp="foot">
    <div><span class="es">SimPlant · Autonomía restringida</span><span class="en">SimPlant · Restricted autonomy</span></div>
    <div class="num">11 / 17</div>
  </footer>
</section>

<!-- ═══════════ 12 · DEFENSIBILIDAD ═══════════ -->
<section class="slide" id="s12">
  <header data-cmp="topbar">
    <div>BytesBricks<span style="color:var(--accent)">.</span></div>
    <div class="chip"><span class="es">10 · Defensibilidad</span><span class="en">10 · Moat</span></div>
    <div class="sect">Moat</div>
  </header>
  <div class="content">
    <h2 class="rv" data-cmp="title" style="--i:0">
      <span class="es">Los incumbentes pueden copiar modelos. No pueden copiar rápido <em>el paquete de confianza</em>.</span>
      <span class="en">Incumbents can copy models. They cannot quickly copy <em>the trust package</em>.</span>
    </h2>
    <div class="rulegrid cols3 rv" data-cmp="moats" style="--i:1">
      <div>
        <span data-cmp="tag" class="today"><span class="es">Moat de hoy</span><span class="en">Today's moat</span></span>
        <h3><span class="es">Autoridad de dominio del founder + foso de datos de calibración propietarios + ventaja de tiempo.</span><span class="en">Founder domain authority + proprietary calibration-data moat + time advantage.</span></h3>
        <p style="margin-top:8px"><span class="es">Dos proyectos reales de ingeniería calibran el gemelo — datos que los competidores no pueden comprar. Lógica PHA/LOPA, límites SIS, camino SIL, evidencia MOC.</span><span class="en">Two real engineering projects calibrate the twin — data competitors cannot buy. PHA/LOPA logic, SIS limits, SIL pathway, MOC evidence.</span></p>
      </div>
      <div>
        <span data-cmp="tag" class="dev"><span class="es">Moat futuro</span><span class="en">Forward moat</span></span>
        <h3><span class="es">El foso de datos se compone por despliegue — no existe hoy.</span><span class="en">The data moat compounds per deployment — not present today.</span></h3>
        <p style="margin-top:8px"><span class="es">Cada sitio suma transitorios, historial de eventos, comportamiento de válvulas, modos de falla y restricciones aceptadas que los competidores no pueden comprar.</span><span class="en">Each site adds transients, event history, valve behavior, failure modes, and accepted constraints that competitors cannot purchase.</span></p>
      </div>
      <div>
        <span data-cmp="tag" class="sim"><span class="es">Moat de despliegue</span><span class="en">Deployment moat</span></span>
        <h3><span class="es">La integración OT es la barrera, no la UI.</span><span class="en">OT integration is the barrier, not the UI.</span></h3>
        <p style="margin-top:8px"><span class="es">Semántica OPC-UA, postura IEC 62443, runtime de edge y ciclos de aceptación de planta.</span><span class="en">OPC-UA semantics, IEC 62443 posture, edge runtime, and plant acceptance cycles.</span></p>
      </div>
    </div>
    <p data-cmp="bigline" class="rv" style="--i:2">
      <span class="es"><em>¿Por qué no Honeywell / Siemens / Emerson / AspenTech?</em> Su stack optimiza control instalado y APC. Qué frena a AspenTech en 18 meses: nada estructural — nuestra defensa es la ventaja de dominio del founder y los datos propietarios de despliegue acumulándose desde el día uno.</span>
      <span class="en"><em>Why not Honeywell / Siemens / Emerson / AspenTech?</em> Their stack optimizes installed control and APC. What stops AspenTech in 18 months: nothing structural — our defense is the founder's domain head-start and proprietary deployment data accumulating from day one.</span>
    </p>
  </div>
  <footer data-cmp="foot">
    <div><span class="es">SimPlant · Autonomía restringida</span><span class="en">SimPlant · Restricted autonomy</span></div>
    <div class="num">12 / 17</div>
  </footer>
</section>

<!-- ═══════════ 13 · GO-TO-MARKET ═══════════ -->
<section class="slide" id="s13">
  <header data-cmp="topbar">
    <div>BytesBricks<span style="color:var(--accent)">.</span></div>
    <div class="chip"><span class="es">11 · Go-to-market</span><span class="en">11 · Go-to-Market</span></div>
    <div class="sect"><span class="es">Distribución</span><span class="en">Distribution</span></div>
  </header>
  <div class="content">
    <h2 class="rv" data-cmp="title" style="--i:0">
      <span class="es">Vendemos por riesgo operativo y ahorro medible — <em>no por entusiasmo con la IA</em>.</span>
      <span class="en">We sell on operational risk and measurable savings — <em>not AI enthusiasm</em>.</span>
    </h2>
    <div class="grid2 rows-tight rv" data-cmp="gtmrows" style="--i:1">
      <div>
        <div data-cmp="row">
          <strong>ICP</strong>
          <p><span class="es">Refinerías downstream de LATAM, 100K–500K bpd, presión por metano, presupuestos de modernización, operadores concentrados.</span><span class="en">LATAM downstream refineries, 100K–500K bpd, methane pressure, modernization budgets, concentrated operators.</span></p>
        </div>
        <div data-cmp="row">
          <strong><span class="es">Mapa de compra</span><span class="en">Buyer map</span></strong>
          <p><span class="es">Sponsor económico: VP Ops / CFO. Sponsor técnico: Ingeniería de Procesos. Gatekeepers: HSE y Seguridad OT.</span><span class="en">Economic sponsor: VP Ops / CFO. Technical sponsor: Process Engineering. Gatekeepers: HSE &amp; OT Security.</span></p>
        </div>
        <div data-cmp="row">
          <strong><span class="es">Cuña</span><span class="en">Wedge</span></strong>
          <p><span class="es">Herramienta de simulación comunitaria → análisis/backtest gratuito → piloto sombra pago → asesoría supervisada → control restringido.</span><span class="en">Community simulation tool → free analysis/backtest → paid shadow pilot → supervised advisory → constrained control.</span></p>
        </div>
      </div>
      <div>
        <div data-cmp="row">
          <strong><span class="es">Ciclo de venta</span><span class="en">Sales cycle</span></strong>
          <p><span class="es">3–6 meses de discovery y acceso a datos · 6 meses de piloto pago · 6 meses de sombra/asesoría · expansión multi-sitio.</span><span class="en">3–6 months discovery and data access · 6 months paid pilot · 6 months shadow/advisory · multi-site expansion.</span></p>
        </div>
        <div data-cmp="row">
          <strong><span class="es">Canales</span><span class="en">Channels</span></strong>
          <p><span class="es">Cuña comunitaria + canales sancionados primero (brazos de I+D como Y-TEC, desafíos de innovación abierta, aceleradora, CACHE); integradores y EPCs después del playbook repetible.</span><span class="en">Community wedge + sanctioned channels first (corporate R&amp;D arms like Y-TEC, open-innovation challenges, accelerator, CACHE); integrators and EPCs after repeatable playbook.</span></p>
        </div>
        <div data-cmp="row">
          <strong><span class="es">Tracción cercana</span><span class="en">Near-term traction</span></strong>
          <p><span class="es">Recepción en CACHE + inbound de GitHub · lanzamiento de la herramienta de simulación · objetivo de LOI Q4 2026 · kickoff del primer piloto sombra pago Q1 2027.</span><span class="en">CACHE reception + GitHub inbound · simulation tool launch · LOI target Q4 2026 · first paid shadow pilot kickoff Q1 2027.</span></p>
        </div>
      </div>
    </div>
  </div>
  <footer data-cmp="foot">
    <div><span class="es">SimPlant · Autonomía restringida</span><span class="en">SimPlant · Restricted autonomy</span></div>
    <div class="num">13 / 17</div>
  </footer>
</section>

<!-- ═══════════ 14 · ROADMAP ═══════════ -->
<section class="slide" id="s14">
  <header data-cmp="topbar">
    <div>BytesBricks<span style="color:var(--accent)">.</span></div>
    <div class="chip">12 · Roadmap</div>
    <div class="sect">De-risking</div>
  </header>
  <div class="content">
    <h2 class="rv" data-cmp="title" style="--i:0">
      <span class="es">Secuencia de de-riesgo: prueba técnica → prueba en planta → <em>repetibilidad comercial</em>.</span>
      <span class="en">De-risking sequence: technical proof → plant proof → <em>commercial repeatability</em>.</span>
    </h2>
    <div class="rulegrid cols4 rv" data-cmp="timeline" style="--i:1">
      <div>
        <span data-cmp="tag" class="today"><span class="es">Hoy · mediados de 2026</span><span class="en">Today · mid-2026</span></span>
        <h3><span class="es">Prueba en gemelo</span><span class="en">Twin proof</span></h3>
        <p style="margin-top:6px"><span class="es">Prototipo de política, métricas de simulación, envolvente de seguridad definido, calibración fundacional de 2 proyectos reales.</span><span class="en">Policy prototype, simulation metrics, safety envelope defined, foundational calibration from 2 real projects.</span></p>
      </div>
      <div>
        <span data-cmp="tag" class="dev"><span class="es">0–6 meses</span><span class="en">0–6 months</span></span>
        <h3><span class="es">Cuña comunitaria + design partner</span><span class="en">Community wedge + design partner</span></h3>
        <p style="margin-top:6px"><span class="es">Herramienta de simulación en vivo, tracción en CACHE, backtest con datos reales del design partner, objetivo de LOI Q4 2026.</span><span class="en">Simulation tool live, CACHE traction, real-data backtest with design partner, LOI target Q4 2026.</span></p>
      </div>
      <div>
        <span data-cmp="tag" class="dev"><span class="es">6–18 meses</span><span class="en">6–18 months</span></span>
        <h3><span class="es">Despliegue en sombra</span><span class="en">Shadow deployment</span></h3>
        <p style="margin-top:6px"><span class="es">Gateway edge, workflow del operador, recomendaciones vs. baseline medido.</span><span class="en">Edge gateway, operator workflow, recommendations vs. measured baseline.</span></p>
      </div>
      <div>
        <span data-cmp="tag" class="vision"><span class="es">18–30 meses</span><span class="en">18–30 months</span></span>
        <h3><span class="es">Autonomía controlada</span><span class="en">Controlled autonomy</span></h3>
        <p style="margin-top:6px"><span class="es">De asesoría supervisada a control restringido en ventanas operativas acotadas.</span><span class="en">From supervised advisory to restricted control in bounded operating windows.</span></p>
      </div>
    </div>
  </div>
  <footer data-cmp="foot">
    <div><span class="es">SimPlant · Autonomía restringida</span><span class="en">SimPlant · Restricted autonomy</span></div>
    <div class="num">14 / 17</div>
  </footer>
</section>

<!-- ═══════════ 15 · LA RONDA ═══════════ -->
<section class="slide" id="s15">
  <header data-cmp="topbar">
    <div>BytesBricks<span style="color:var(--accent)">.</span></div>
    <div class="chip"><span class="es">13 · La ronda</span><span class="en">13 · Investment ask</span></div>
    <div class="sect"><span class="es">Uso de fondos</span><span class="en">Use of funds</span></div>
  </header>
  <div class="content">
    <div class="head">
      <h2 class="rv" data-cmp="title" style="--i:0">
        <span class="es">Levantamos <em>US$500K vía SAFE</em> para 18 meses de runway. El capital convierte la validación en gemelo en la primera referencia industrial.</span>
        <span class="en">Raising <em>US$500K via SAFE</em> for 18 months of runway. Capital converts twin validation into the first industrial reference.</span>
      </h2>
      <p class="sub rv" data-cmp="sub" style="--i:1">
        <span class="es">Burn austero con ingeniería senior local; la contratación de ventas enterprise se difiere. El capital financia profundidad de ingeniería, la cuña comunitaria y el primer piloto sombra — no tres contrataciones senior.</span>
        <span class="en">Lean burn on local senior engineering; the enterprise sales hire is deferred. Capital funds engineering depth, the community wedge, and the first shadow pilot — not three senior hires.</span>
      </p>
    </div>
    <div class="rulegrid split rv" data-cmp="funds" style="--i:2">
      <div class="rows-tight" style="padding-top:4px;padding-bottom:4px">
        <div data-cmp="row" style="border-top:0">
          <strong style="font-family:var(--display);font-size:var(--t-h3)">55–60%</strong>
          <p><span class="es">Equipo: ingeniero senior de Safe-RL/ML, advisor de O&amp;G con credenciales, soporte de seguridad funcional. Ventas enterprise diferido.</span><span class="en">Team: senior Safe-RL/ML engineer, credentialed O&amp;G advisor, functional safety support. Enterprise sales hire deferred.</span></p>
        </div>
        <div data-cmp="row">
          <strong style="font-family:var(--display);font-size:var(--t-h3)">20%</strong>
          <p><span class="es">Piloto e integración OT: gateway edge, trabajo con datos de planta, viajes, soporte de despliegue.</span><span class="en">Pilot &amp; OT integration: edge gateway, plant data work, travel, deployment support.</span></p>
        </div>
        <div data-cmp="row">
          <strong style="font-family:var(--display);font-size:var(--t-h3)">10%</strong>
          <p><span class="es">Ciber y seguridad: postura IEC 62443, documentación del camino SIL, revisión externa.</span><span class="en">Cyber &amp; safety: IEC 62443 posture, SIL pathway documentation, external review.</span></p>
        </div>
        <div data-cmp="row">
          <strong style="font-family:var(--display);font-size:var(--t-h3)">10–15%</strong>
          <p><span class="es">Legal, IP, seguros, estructura corporativa, buffer operativo.</span><span class="en">Legal, IP, insurance, corporate structure, operating buffer.</span></p>
        </div>
      </div>
      <div>
        <span data-cmp="tag" class="today"><span class="es">Qué compra US$500K</span><span class="en">What US$500K buys</span></span>
        <ul>
          <li><span class="es">Tracción comunitaria + herramienta de simulación con usuarios ingenieros de procesos</span><span class="en">Community traction + simulation tool with process-engineer users</span></li>
          <li><span class="es">Backtest con datos reales de un design partner (mes 6)</span><span class="en">Real-data backtest with a design partner (Month 6)</span></li>
          <li><span class="es">Kickoff de piloto sombra firmado (mes 9–12)</span><span class="en">Signed shadow pilot kickoff (Month 9–12)</span></li>
          <li><span class="es">Gemelo de antorcha reutilizable y toolkit de restricciones</span><span class="en">Reusable flare twin and constraint toolkit</span></li>
          <li><span class="es"><strong>El delta auditado en planta viva es la ronda siguiente</strong> — no se promete en 18 meses</span><span class="en"><strong>Audited live-plant delta is the round after this one</strong> — not promised in 18 months</span></li>
        </ul>
      </div>
    </div>
  </div>
  <footer data-cmp="foot">
    <div><span class="es">SimPlant · Autonomía restringida</span><span class="en">SimPlant · Restricted autonomy</span></div>
    <div class="num">15 / 17</div>
  </footer>
</section>

<!-- ═══════════ 16 · EQUIPO ═══════════ -->
<section class="slide" id="s16">
  <header data-cmp="topbar">
    <div>BytesBricks<span style="color:var(--accent)">.</span></div>
    <div class="chip"><span class="es">14 · Equipo</span><span class="en">14 · Team</span></div>
    <div class="sect"><span class="es">Autoridad</span><span class="en">Authority</span></div>
  </header>
  <div class="content">
    <h2 class="rv" data-cmp="title" style="--i:0">
      <span class="es">Autoridad técnica y de dominio para <em>desplegar con seguridad</em>.</span>
      <span class="en">Domain and technical authority to <em>deploy safely</em>.</span>
    </h2>
    <div class="rulegrid cols2 rv" data-cmp="people" style="--i:1">
      <div data-cmp="person">
        <div class="init" aria-hidden="true">JM</div>
        <div>
          <h3>José Martín Rodriguez Mortaloni</h3>
          <span data-cmp="tag" class="today" style="margin-bottom:0"><span class="es">CEO y cofundador · Lead Safe RL Engineer</span><span class="en">CEO &amp; Co-Founder · Lead Safe RL Engineer</span></span>
          <p><span class="es">Construyó desde cero el stack de Safe RL de SimPlant y la arquitectura edge OPC-UA. Publica trabajo técnico en CACHE. Ingeniería en Sistemas de Información (último año). Ingeniería liderada por el founder; contratación senior de ML/seguridad planificada.</span><span class="en">Built the SimPlant Safe RL stack and OPC-UA edge architecture from scratch. Publishes technical work in CACHE. Information Systems Engineering (final year). Founder-led engineering; senior ML/safety hire planned.</span></p>
        </div>
      </div>
      <div data-cmp="person">
        <div class="init" aria-hidden="true">HR</div>
        <div>
          <h3>Ing. Humberto A. Rodriguez</h3>
          <span data-cmp="tag" class="dev" style="margin-bottom:0"><span class="es">Autoridad de procesos y gemelo · Cofundador</span><span class="en">Process Authority &amp; Twin · Co-Founder</span></span>
          <p><span class="es">28+ años en ingeniería de O&amp;G. Traduce PHA/LOPA en restricciones CMDP estrictas. Fuente de los dos proyectos reales de ingeniería que calibran el gemelo (foso de datos propietario).</span><span class="en">28+ years in O&amp;G engineering. Translates PHA/LOPA into strict CMDP constraints. Source of the two real engineering projects that calibrate the twin (proprietary data moat).</span></p>
        </div>
      </div>
    </div>
    <div data-cmp="claim" class="rv" style="--i:2">
      <span data-cmp="tag" class="dev"><span class="es">Plan de contratación</span><span class="en">Hiring plan</span></span>
      <p style="font-size:var(--t-small)">
        <span class="es"><strong>Prioridad de corto plazo:</strong> ingeniero senior de Safe-RL/ML + advisor de O&amp;G con credenciales (operaciones o proveedor de APC) — para profundizar el único pilar técnico y abrir el canal de design partners. La contratación de ventas enterprise se difiere hasta probar una cuña repetible.</span>
        <span class="en"><strong>Near-term priority:</strong> senior Safe-RL/ML engineer + a credentialed O&amp;G advisor (operations or APC-vendor background) — to deepen the single technical pillar and open the design-partner channel. Enterprise sales hire deferred until a repeatable wedge is proven.</span>
      </p>
    </div>
  </div>
  <footer data-cmp="foot">
    <div>
      <span class="es">Relación familiar declarada entre cofundadores · gobernanza con vesting de 4 años / cliff de 1 año</span>
      <span class="en">Family relationship declared between co-founders · governance with 4-year vesting / 1-year cliff</span>
    </div>
    <div class="num">16 / 17</div>
  </footer>
</section>

<!-- ═══════════ 17 · CIERRE ═══════════ -->
<section class="slide" id="s17">
  <header data-cmp="topbar">
    <div>BytesBricks<span style="color:var(--accent)">.</span></div>
    <div class="chip"><span class="es">Reclamo de categoría</span><span class="en">Category claim</span></div>
    <div class="sect"><span class="es">Cierre</span><span class="en">Close</span></div>
  </header>
  <div class="content" style="max-width:1200px">
    <h1 class="rv" data-cmp="title" style="--i:0">
      <span class="es">La autonomía industrial será <em>restringida, auditada</em> y desplegada en el edge.</span>
      <span class="en">Industrial autonomy will be <em>restricted, audited</em>, and deployed at the edge.</span>
    </h1>
    <div data-cmp="hazard" class="rv" style="--i:1" role="presentation"></div>
    <p class="sub rv" data-cmp="sub" style="--i:2">
      <span class="es">SimPlant empieza donde el dolor es urgente y el foso es real: sistemas de gas de antorcha de refinería en infraestructura crítica.</span>
      <span class="en">SimPlant starts where the pain is urgent and the moat is real: refinery flare-gas systems in critical infrastructure.</span>
    </p>
  </div>
  <footer data-cmp="foot">
    <div>
      <span class="es">La autonomía de control para infraestructura industrial es una categoría de plataforma — no una solución puntual. Rev 5 · Julio 2026.</span>
      <span class="en">Control autonomy for industrial infrastructure is a platform category — not a point solution. Rev 5 · July 2026.</span>
    </div>
    <div class="num">17 / 17</div>
  </footer>
</section>

<script>
/* ════════════════════════════════════════════════════════════════
   CONTROLADOR DE PRESENTACIÓN
   — Idioma: botones ES/EN o tecla L (persiste en localStorage)
   — Navegación: ↑↓ ←→ · Espacio · PgUp/PgDn · Home/End · puntos
   — Reveals: IntersectionObserver agrega .visible por slide
   — Barra de progreso: scaleX según el scroll
   ════════════════════════════════════════════════════════════════ */
document.documentElement.classList.add('js');

(function(){
  'use strict';
  const slides=[...document.querySelectorAll('.slide')];
  const dotsNav=document.querySelector('.nav-dots');
  const progress=document.querySelector('.progress');

  /* ── Idioma ── */
  const langBtns=[...document.querySelectorAll('.lang-switch button')];
  function setLang(lang){
    document.documentElement.dataset.lang=lang;
    document.documentElement.lang=lang;
    langBtns.forEach(b=>b.classList.toggle('active',b.dataset.set===lang));
    try{localStorage.setItem('deck-lang',lang)}catch(e){}
  }
  langBtns.forEach(b=>b.addEventListener('click',()=>setLang(b.dataset.set)));
  try{const saved=localStorage.getItem('deck-lang');if(saved==='es'||saved==='en')setLang(saved)}catch(e){}

  /* ── Puntos de navegación (cuadrados) ── */
  dotsNav.innerHTML='';
  slides.forEach((s,i)=>{
    const b=document.createElement('button');
    b.setAttribute('aria-label','Slide '+(i+1));
    b.addEventListener('click',()=>slides[i].scrollIntoView({behavior:'smooth'}));
    dotsNav.appendChild(b);
  });
  const dots=[...dotsNav.children];

  /* ── Observer: reveals + punto activo ── */
  let current=0;
  const io=new IntersectionObserver(entries=>{
    entries.forEach(e=>{
      if(e.isIntersecting){
        e.target.classList.add('visible');
        current=slides.indexOf(e.target);
        dots.forEach((d,i)=>d.classList.toggle('active',i===current));
      }
    });
  },{threshold:.55});
  slides.forEach(s=>io.observe(s));

  /* ── Barra de progreso ── */
  let ticking=false;
  function paint(){
    const max=document.documentElement.scrollHeight-innerHeight;
    progress.style.transform='scaleX('+(max>0?scrollY/max:0)+')';
    ticking=false;
  }
  addEventListener('scroll',()=>{if(!ticking){requestAnimationFrame(paint);ticking=true}},{passive:true});
  paint();

  /* ── Teclado ── */
  function go(i){
    const n=Math.max(0,Math.min(slides.length-1,i));
    slides[n].scrollIntoView({behavior:'smooth'});
  }
  addEventListener('keydown',e=>{
    if(e.target.matches('input,textarea,[contenteditable]'))return;
    switch(e.key){
      case'ArrowDown':case'ArrowRight':case'PageDown':case' ':e.preventDefault();go(current+1);break;
      case'ArrowUp':case'ArrowLeft':case'PageUp':e.preventDefault();go(current-1);break;
      case'Home':e.preventDefault();go(0);break;
      case'End':e.preventDefault();go(slides.length-1);break;
      case'l':case'L':setLang(document.documentElement.dataset.lang==='es'?'en':'es');break;
    }
  });
})();
</script>
</body>
</html>

