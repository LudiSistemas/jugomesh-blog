# Scenariji korišćenja Meshtastic rola — Iz prakse, za praksu

Kako se role koriste u stvarnom svetu? Kroz konkretne primere iz JugoMesh mreže i tipične situacije, objašnjavamo koji čvor gde ide i zašto.

---

## Scenario 1: Planinski repetitor — Kičma mreže

Najvažniji scenario za svaku mesh mrežu. Jedan ROUTER čvor na visokoj tački može da poveže desetine korisnika u dolini.

<svg viewBox="0 0 800 400" xmlns="http://www.w3.org/2000/svg" style="width:100%;max-width:800px;margin:1.5rem auto;display:block;background:linear-gradient(180deg,#0a1628 0%,#112240 100%);border-radius:12px;border:1px solid rgba(0,210,255,0.2);">
  <!-- Mountain -->
  <polygon points="250,350 400,80 550,350" fill="#1a3a5c" stroke="#2a5a8c" stroke-width="1.5"/>
  <polygon points="100,350 220,180 340,350" fill="#15304d" stroke="#2a5a8c" stroke-width="1"/>
  <polygon points="460,350 600,150 740,350" fill="#15304d" stroke="#2a5a8c" stroke-width="1"/>
  <!-- Ground -->
  <rect x="0" y="345" width="800" height="55" fill="#0d2137" rx="0"/>
  <!-- Router on peak -->
  <rect x="380" y="55" width="40" height="30" rx="5" fill="#00d2ff" fill-opacity="0.2" stroke="#00d2ff" stroke-width="2"/>
  <text x="400" y="75" text-anchor="middle" fill="#00d2ff" font-size="11" font-weight="bold">R</text>
  <text x="400" y="48" text-anchor="middle" fill="#00d2ff" font-size="10">ROUTER</text>
  <!-- Antenna -->
  <line x1="400" y1="55" x2="400" y2="30" stroke="#00d2ff" stroke-width="2"/>
  <circle cx="400" cy="27" r="3" fill="#00d2ff"/>
  <!-- Signal waves -->
  <circle cx="400" cy="70" r="30" fill="none" stroke="#00d2ff" stroke-width="0.5" opacity="0.3"/>
  <circle cx="400" cy="70" r="60" fill="none" stroke="#00d2ff" stroke-width="0.5" opacity="0.2"/>
  <circle cx="400" cy="70" r="100" fill="none" stroke="#00d2ff" stroke-width="0.5" opacity="0.1"/>
  <!-- Solar panel -->
  <rect x="420" y="60" width="20" height="12" rx="2" fill="#ffd700" fill-opacity="0.3" stroke="#ffd700" stroke-width="1"/>
  <text x="430" y="69" text-anchor="middle" fill="#ffd700" font-size="6">SOL</text>
  <!-- Client 1 - left village -->
  <rect x="110" y="310" width="36" height="24" rx="4" fill="#4ade80" fill-opacity="0.2" stroke="#4ade80" stroke-width="1.5"/>
  <text x="128" y="326" text-anchor="middle" fill="#4ade80" font-size="9" font-weight="bold">C</text>
  <text x="128" y="305" text-anchor="middle" fill="#4ade80" font-size="8">CLIENT</text>
  <!-- Client 2 - left -->
  <rect x="190" y="320" width="36" height="24" rx="4" fill="#4ade80" fill-opacity="0.2" stroke="#4ade80" stroke-width="1.5"/>
  <text x="208" y="336" text-anchor="middle" fill="#4ade80" font-size="9" font-weight="bold">C</text>
  <!-- Client 3 - right village -->
  <rect x="570" y="310" width="36" height="24" rx="4" fill="#4ade80" fill-opacity="0.2" stroke="#4ade80" stroke-width="1.5"/>
  <text x="588" y="326" text-anchor="middle" fill="#4ade80" font-size="9" font-weight="bold">C</text>
  <text x="588" y="305" text-anchor="middle" fill="#4ade80" font-size="8">CLIENT</text>
  <!-- Client 4 - right -->
  <rect x="660" y="315" width="36" height="24" rx="4" fill="#4ade80" fill-opacity="0.2" stroke="#4ade80" stroke-width="1.5"/>
  <text x="678" y="331" text-anchor="middle" fill="#4ade80" font-size="9" font-weight="bold">C</text>
  <!-- Sensor - weather station -->
  <rect x="340" y="155" width="36" height="24" rx="4" fill="#f59e0b" fill-opacity="0.2" stroke="#f59e0b" stroke-width="1.5"/>
  <text x="358" y="171" text-anchor="middle" fill="#f59e0b" font-size="9" font-weight="bold">S</text>
  <text x="358" y="150" text-anchor="middle" fill="#f59e0b" font-size="8">SENSOR</text>
  <!-- Connection lines -->
  <line x1="400" y1="85" x2="128" y2="310" stroke="#00d2ff" stroke-width="1" opacity="0.4" stroke-dasharray="4,4"/>
  <line x1="400" y1="85" x2="208" y2="320" stroke="#00d2ff" stroke-width="1" opacity="0.4" stroke-dasharray="4,4"/>
  <line x1="400" y1="85" x2="588" y2="310" stroke="#00d2ff" stroke-width="1" opacity="0.4" stroke-dasharray="4,4"/>
  <line x1="400" y1="85" x2="678" y2="315" stroke="#00d2ff" stroke-width="1" opacity="0.4" stroke-dasharray="4,4"/>
  <line x1="395" y1="75" x2="358" y2="155" stroke="#f59e0b" stroke-width="1" opacity="0.5" stroke-dasharray="3,3"/>
  <!-- Labels -->
  <text x="128" y="365" text-anchor="middle" fill="#8892a4" font-size="9">Selo A</text>
  <text x="628" y="365" text-anchor="middle" fill="#8892a4" font-size="9">Selo B</text>
  <text x="400" y="395" text-anchor="middle" fill="#8892a4" font-size="10">Planinski ROUTER povezuje dva sela na 30+ km</text>
</svg>

**Postavka:**
- **ROUTER** na vrhu planine — solarna ploča + baterija, fiksna antena
- **CLIENT** čvorovi u oba sela u dolini
- **SENSOR** meteo stanica na padini šalje temperaturu i vlažnost

**Zašto baš ove role:**
- ROUTER uvek prosleđuje i ima najkraći delay — idealan za infrastrukturni čvor
- CLIENT korisnici ne troše bateriju na nepotrebno prosleđivanje
- SENSOR optimizuje slanje telemetrije i štedi bateriju

**Iz JugoMesh prakse:** Čvor na Kopaoniku pokriva dolinu Toplice i deo Rasinskog okruga. Jedan ROUTER, desetine korisnika.

---

## Scenario 2: Urbana mreža — Grad sa više čvorova

U gradu signal odskače od zgrada i gubi se brže. Zato je potrebno više čvorova koji sarađuju.

<svg viewBox="0 0 800 400" xmlns="http://www.w3.org/2000/svg" style="width:100%;max-width:800px;margin:1.5rem auto;display:block;background:linear-gradient(180deg,#0a1628 0%,#112240 100%);border-radius:12px;border:1px solid rgba(0,210,255,0.2);">
  <!-- Buildings -->
  <rect x="80" y="150" width="60" height="200" fill="#152a4a" stroke="#2a4a6a" stroke-width="1" rx="2"/>
  <rect x="160" y="200" width="50" height="150" fill="#152a4a" stroke="#2a4a6a" stroke-width="1" rx="2"/>
  <rect x="280" y="120" width="70" height="230" fill="#152a4a" stroke="#2a4a6a" stroke-width="1" rx="2"/>
  <rect x="420" y="180" width="55" height="170" fill="#152a4a" stroke="#2a4a6a" stroke-width="1" rx="2"/>
  <rect x="530" y="140" width="65" height="210" fill="#152a4a" stroke="#2a4a6a" stroke-width="1" rx="2"/>
  <rect x="650" y="190" width="50" height="160" fill="#152a4a" stroke="#2a4a6a" stroke-width="1" rx="2"/>
  <!-- Windows -->
  <rect x="90" y="165" width="12" height="10" fill="#1a3d6d" rx="1"/><rect x="110" y="165" width="12" height="10" fill="#1a3d6d" rx="1"/>
  <rect x="90" y="185" width="12" height="10" fill="#1a3d6d" rx="1"/><rect x="110" y="185" width="12" height="10" fill="#1a3d6d" rx="1"/>
  <rect x="290" y="135" width="14" height="10" fill="#1a3d6d" rx="1"/><rect x="316" y="135" width="14" height="10" fill="#1a3d6d" rx="1"/>
  <rect x="540" y="155" width="14" height="10" fill="#1a3d6d" rx="1"/><rect x="566" y="155" width="14" height="10" fill="#1a3d6d" rx="1"/>
  <!-- Ground -->
  <rect x="0" y="348" width="800" height="52" fill="#0d2137"/>
  <!-- Router 1 - tall building -->
  <rect x="297" y="95" width="36" height="24" rx="4" fill="#00d2ff" fill-opacity="0.2" stroke="#00d2ff" stroke-width="2"/>
  <text x="315" y="111" text-anchor="middle" fill="#00d2ff" font-size="9" font-weight="bold">R</text>
  <text x="315" y="88" text-anchor="middle" fill="#00d2ff" font-size="8">ROUTER</text>
  <!-- Router Late - MQTT GW -->
  <rect x="544" y="115" width="36" height="24" rx="4" fill="#a78bfa" fill-opacity="0.2" stroke="#a78bfa" stroke-width="2"/>
  <text x="562" y="131" text-anchor="middle" fill="#a78bfa" font-size="9" font-weight="bold">RL</text>
  <text x="562" y="108" text-anchor="middle" fill="#a78bfa" font-size="7">ROUTER_LATE</text>
  <text x="562" y="153" text-anchor="middle" fill="#a78bfa" font-size="7">MQTT GW</text>
  <!-- Client on roof -->
  <rect x="92" y="125" width="36" height="24" rx="4" fill="#4ade80" fill-opacity="0.2" stroke="#4ade80" stroke-width="1.5"/>
  <text x="110" y="141" text-anchor="middle" fill="#4ade80" font-size="9" font-weight="bold">C</text>
  <text x="110" y="120" text-anchor="middle" fill="#4ade80" font-size="8">CLIENT</text>
  <!-- Client on street -->
  <rect x="360" y="330" width="36" height="24" rx="4" fill="#4ade80" fill-opacity="0.2" stroke="#4ade80" stroke-width="1.5"/>
  <text x="378" y="346" text-anchor="middle" fill="#4ade80" font-size="9" font-weight="bold">C</text>
  <text x="378" y="370" text-anchor="middle" fill="#4ade80" font-size="8">ulica</text>
  <!-- Client Mute - monitoring -->
  <rect x="657" y="165" width="36" height="24" rx="4" fill="#f87171" fill-opacity="0.2" stroke="#f87171" stroke-width="1.5"/>
  <text x="675" y="181" text-anchor="middle" fill="#f87171" font-size="8" font-weight="bold">CM</text>
  <text x="675" y="160" text-anchor="middle" fill="#f87171" font-size="7">CLIENT_MUTE</text>
  <!-- Connection lines -->
  <line x1="315" y1="119" x2="110" y2="125" stroke="#00d2ff" stroke-width="1.2" opacity="0.4" stroke-dasharray="4,4"/>
  <line x1="315" y1="119" x2="562" y2="127" stroke="#00d2ff" stroke-width="1.2" opacity="0.4" stroke-dasharray="4,4"/>
  <line x1="315" y1="119" x2="378" y2="330" stroke="#00d2ff" stroke-width="1" opacity="0.3" stroke-dasharray="4,4"/>
  <line x1="562" y1="139" x2="675" y2="165" stroke="#a78bfa" stroke-width="1" opacity="0.4" stroke-dasharray="4,4"/>
  <!-- Internet cloud from MQTT GW -->
  <ellipse cx="700" cy="70" rx="55" ry="25" fill="#a78bfa" fill-opacity="0.08" stroke="#a78bfa" stroke-width="1" stroke-dasharray="3,3"/>
  <text x="700" y="74" text-anchor="middle" fill="#a78bfa" font-size="10">MQTT ☁</text>
  <line x1="575" y1="115" x2="660" y2="78" stroke="#a78bfa" stroke-width="1" opacity="0.4" stroke-dasharray="3,3"/>
  <!-- Legend -->
  <text x="400" y="395" text-anchor="middle" fill="#8892a4" font-size="10">Urbana mreža: ROUTER na najvišoj zgradi, MQTT gateway za internet vezu</text>
</svg>

**Postavka:**
- **ROUTER** na krovu najviše zgrade — uvek prosleđuje, najkraći delay
- **ROUTER_LATE** sa MQTT gateway-om — prosleđuje pakete na internet, ali daje prednost pravom ROUTER-u
- **CLIENT** korisnici — na krovovima i u ulicama
- **CLIENT_MUTE** — neko ko samo prati mrežu bez generisanja saobraćaja

**Zašto ROUTER_LATE za MQTT gateway:**
Gateway je spojen na internet i sve pakete šalje na MQTT broker. Ali ne želimo da on bude primarni ruter u mreži — pravi ROUTER na visokoj tački to radi bolje. ROUTER_LATE prosleđuje samo ako niko drugi nije.

**Iz JugoMesh prakse:** Gateway u Beogradu koristi ROUTER_LATE — paketi prvo idu preko planinskih ROUTER čvorova, a gateway ih samo hvata za internet.

---

## Scenario 3: Praćenje vozila — Tracker u pokretu

Tracker u kolima ili na biciklu šalje poziciju dok se kreće kroz mrežu.

<svg viewBox="0 0 800 350" xmlns="http://www.w3.org/2000/svg" style="width:100%;max-width:800px;margin:1.5rem auto;display:block;background:linear-gradient(180deg,#0a1628 0%,#112240 100%);border-radius:12px;border:1px solid rgba(0,210,255,0.2);">
  <!-- Road -->
  <rect x="50" y="220" width="700" height="40" fill="#1a2d4a" rx="5"/>
  <line x1="100" y1="240" x2="150" y2="240" stroke="#3a4d6a" stroke-width="2" stroke-dasharray="10,10"/>
  <line x1="200" y1="240" x2="250" y2="240" stroke="#3a4d6a" stroke-width="2" stroke-dasharray="10,10"/>
  <line x1="300" y1="240" x2="350" y2="240" stroke="#3a4d6a" stroke-width="2" stroke-dasharray="10,10"/>
  <line x1="400" y1="240" x2="450" y2="240" stroke="#3a4d6a" stroke-width="2" stroke-dasharray="10,10"/>
  <line x1="500" y1="240" x2="550" y2="240" stroke="#3a4d6a" stroke-width="2" stroke-dasharray="10,10"/>
  <line x1="600" y1="240" x2="650" y2="240" stroke="#3a4d6a" stroke-width="2" stroke-dasharray="10,10"/>
  <!-- Car with tracker -->
  <rect x="340" y="195" width="70" height="30" rx="8" fill="#f59e0b" fill-opacity="0.15" stroke="#f59e0b" stroke-width="1.5"/>
  <circle cx="355" cy="228" r="7" fill="#1a2d4a" stroke="#f59e0b" stroke-width="1"/>
  <circle cx="395" cy="228" r="7" fill="#1a2d4a" stroke="#f59e0b" stroke-width="1"/>
  <text x="375" y="213" text-anchor="middle" fill="#f59e0b" font-size="9" font-weight="bold">TRACKER</text>
  <!-- GPS signal dots (breadcrumbs) -->
  <circle cx="180" cy="210" r="4" fill="#f59e0b" opacity="0.2"/>
  <circle cx="220" cy="210" r="4" fill="#f59e0b" opacity="0.3"/>
  <circle cx="260" cy="210" r="4" fill="#f59e0b" opacity="0.4"/>
  <circle cx="300" cy="210" r="4" fill="#f59e0b" opacity="0.6"/>
  <!-- Arrow showing movement -->
  <line x1="415" y1="210" x2="460" y2="210" stroke="#f59e0b" stroke-width="1.5" opacity="0.6"/>
  <polygon points="460,205 470,210 460,215" fill="#f59e0b" opacity="0.6"/>
  <!-- Tower/Router 1 -->
  <line x1="150" y1="60" x2="150" y2="130" stroke="#445" stroke-width="3"/>
  <line x1="130" y1="130" x2="170" y2="130" stroke="#445" stroke-width="2"/>
  <line x1="135" y1="100" x2="165" y2="100" stroke="#445" stroke-width="1.5"/>
  <rect x="132" y="42" width="36" height="22" rx="4" fill="#00d2ff" fill-opacity="0.2" stroke="#00d2ff" stroke-width="2"/>
  <text x="150" y="57" text-anchor="middle" fill="#00d2ff" font-size="9" font-weight="bold">R</text>
  <text x="150" y="36" text-anchor="middle" fill="#00d2ff" font-size="8">ROUTER</text>
  <!-- Tower/Router 2 -->
  <line x1="650" y1="60" x2="650" y2="130" stroke="#445" stroke-width="3"/>
  <line x1="630" y1="130" x2="670" y2="130" stroke="#445" stroke-width="2"/>
  <line x1="635" y1="100" x2="665" y2="100" stroke="#445" stroke-width="1.5"/>
  <rect x="632" y="42" width="36" height="22" rx="4" fill="#00d2ff" fill-opacity="0.2" stroke="#00d2ff" stroke-width="2"/>
  <text x="650" y="57" text-anchor="middle" fill="#00d2ff" font-size="9" font-weight="bold">R</text>
  <text x="650" y="36" text-anchor="middle" fill="#00d2ff" font-size="8">ROUTER</text>
  <!-- CLIENT_BASE at home -->
  <rect x="380" y="80" width="40" height="40" rx="3" fill="#152a4a" stroke="#2a4a6a" stroke-width="1"/>
  <polygon points="370,82 400,55 430,82" fill="#1a3050" stroke="#2a4a6a" stroke-width="1"/>
  <rect x="388" y="68" width="24" height="16" rx="3" fill="#22d3ee" fill-opacity="0.15" stroke="#22d3ee" stroke-width="1.5"/>
  <text x="400" y="80" text-anchor="middle" fill="#22d3ee" font-size="7" font-weight="bold">CB</text>
  <text x="400" y="50" text-anchor="middle" fill="#22d3ee" font-size="7">CLIENT_BASE</text>
  <!-- Connection lines -->
  <line x1="375" y1="195" x2="150" y2="64" stroke="#f59e0b" stroke-width="1" opacity="0.3" stroke-dasharray="4,4"/>
  <line x1="375" y1="195" x2="400" y2="120" stroke="#22d3ee" stroke-width="1.2" opacity="0.5" stroke-dasharray="4,4"/>
  <line x1="375" y1="195" x2="650" y2="64" stroke="#f59e0b" stroke-width="1" opacity="0.2" stroke-dasharray="4,4"/>
  <line x1="400" y1="120" x2="150" y2="64" stroke="#00d2ff" stroke-width="1" opacity="0.3" stroke-dasharray="3,3"/>
  <line x1="400" y1="120" x2="650" y2="64" stroke="#00d2ff" stroke-width="1" opacity="0.3" stroke-dasharray="3,3"/>
  <!-- Label -->
  <text x="400" y="295" text-anchor="middle" fill="#8892a4" font-size="9">Tracker u autu šalje GPS poziciju → CLIENT_BASE kod kuće ima prioritet za prosleđivanje</text>
  <!-- Phone at home -->
  <rect x="440" y="95" width="16" height="24" rx="3" fill="#4ade80" fill-opacity="0.2" stroke="#4ade80" stroke-width="1"/>
  <text x="448" y="110" text-anchor="middle" fill="#4ade80" font-size="6">📱</text>
  <text x="470" y="110" text-anchor="start" fill="#4ade80" font-size="7">telefon</text>
</svg>

**Postavka:**
- **TRACKER** u vozilu — šalje GPS poziciju svaka 2 minuta, štedi bateriju
- **CLIENT_BASE** kod kuće — favorizuje tracker, uvek prosleđuje njegove pakete
- **ROUTER** čvorovi duž puta — obezbeđuju pokrivenost

**Zašto TRACKER a ne CLIENT:**
- TRACKER optimizuje slanje pozicije — češće šalje GPS, ređe nodeinfo i telemetriju
- Baterija traje danima jer ne šalje nepotrebne podatke
- CLIENT_BASE kod kuće ga tretira kao prioritetni čvor

**Primer iz prakse:** T-Beam u automobilu sa TRACKER rolom — vlasnik na telefonu kod kuće vidi gde mu je auto preko mreže, bez SIM kartice ili interneta.

---

## Scenario 4: Meteo mreža — Senzori na terenu

Mreža vremenskih stanica koje šalju podatke o temperaturi, vlažnosti i pritisku.

<svg viewBox="0 0 800 380" xmlns="http://www.w3.org/2000/svg" style="width:100%;max-width:800px;margin:1.5rem auto;display:block;background:linear-gradient(180deg,#0a1628 0%,#112240 100%);border-radius:12px;border:1px solid rgba(0,210,255,0.2);">
  <!-- Terrain -->
  <polygon points="0,300 100,220 200,260 350,180 500,240 650,200 800,280 800,380 0,380" fill="#0d2137"/>
  <polygon points="0,300 100,220 200,260 350,180 500,240 650,200 800,280" fill="none" stroke="#1a3a5c" stroke-width="1.5"/>
  <!-- Sensor 1 - hilltop -->
  <rect x="332" y="148" width="36" height="24" rx="4" fill="#f59e0b" fill-opacity="0.2" stroke="#f59e0b" stroke-width="1.5"/>
  <text x="350" y="164" text-anchor="middle" fill="#f59e0b" font-size="9" font-weight="bold">S</text>
  <text x="350" y="140" text-anchor="middle" fill="#f59e0b" font-size="8">SENSOR</text>
  <!-- Thermometer icon -->
  <text x="350" y="195" text-anchor="middle" fill="#f59e0b" font-size="10" opacity="0.7">🌡 22°C</text>
  <!-- Sensor 2 - valley -->
  <rect x="82" y="190" width="36" height="24" rx="4" fill="#f59e0b" fill-opacity="0.2" stroke="#f59e0b" stroke-width="1.5"/>
  <text x="100" y="206" text-anchor="middle" fill="#f59e0b" font-size="9" font-weight="bold">S</text>
  <text x="100" y="183" text-anchor="middle" fill="#f59e0b" font-size="8">SENSOR</text>
  <text x="100" y="235" text-anchor="middle" fill="#f59e0b" font-size="10" opacity="0.7">🌡 18°C</text>
  <!-- Sensor 3 -->
  <rect x="632" y="168" width="36" height="24" rx="4" fill="#f59e0b" fill-opacity="0.2" stroke="#f59e0b" stroke-width="1.5"/>
  <text x="650" y="184" text-anchor="middle" fill="#f59e0b" font-size="9" font-weight="bold">S</text>
  <text x="650" y="161" text-anchor="middle" fill="#f59e0b" font-size="8">SENSOR</text>
  <text x="650" y="210" text-anchor="middle" fill="#f59e0b" font-size="10" opacity="0.7">💧 85%</text>
  <!-- Central Router -->
  <rect x="382" y="55" width="36" height="24" rx="4" fill="#00d2ff" fill-opacity="0.2" stroke="#00d2ff" stroke-width="2"/>
  <text x="400" y="71" text-anchor="middle" fill="#00d2ff" font-size="9" font-weight="bold">R</text>
  <text x="400" y="48" text-anchor="middle" fill="#00d2ff" font-size="8">ROUTER</text>
  <!-- MQTT GW -->
  <rect x="540" y="55" width="42" height="24" rx="4" fill="#a78bfa" fill-opacity="0.2" stroke="#a78bfa" stroke-width="1.5"/>
  <text x="561" y="71" text-anchor="middle" fill="#a78bfa" font-size="8" font-weight="bold">MQTT</text>
  <text x="561" y="48" text-anchor="middle" fill="#a78bfa" font-size="7">ROUTER_LATE</text>
  <!-- Cloud/Server -->
  <ellipse cx="700" cy="50" rx="50" ry="22" fill="#a78bfa" fill-opacity="0.08" stroke="#a78bfa" stroke-width="1" stroke-dasharray="3,3"/>
  <text x="700" y="48" text-anchor="middle" fill="#a78bfa" font-size="8">jugomesh.com</text>
  <text x="700" y="60" text-anchor="middle" fill="#a78bfa" font-size="7">📊 dashboard</text>
  <!-- Connections -->
  <line x1="350" y1="148" x2="400" y2="79" stroke="#f59e0b" stroke-width="1" opacity="0.5" stroke-dasharray="4,4"/>
  <line x1="100" y1="190" x2="400" y2="79" stroke="#f59e0b" stroke-width="1" opacity="0.4" stroke-dasharray="4,4"/>
  <line x1="650" y1="168" x2="561" y2="79" stroke="#f59e0b" stroke-width="1" opacity="0.4" stroke-dasharray="4,4"/>
  <line x1="418" y1="67" x2="540" y2="67" stroke="#00d2ff" stroke-width="1" opacity="0.4" stroke-dasharray="3,3"/>
  <line x1="582" y1="60" x2="650" y2="50" stroke="#a78bfa" stroke-width="1" opacity="0.4" stroke-dasharray="3,3"/>
  <!-- Data flow arrows -->
  <text x="250" y="130" text-anchor="middle" fill="#f59e0b" font-size="8" opacity="0.6">telemetrija →</text>
  <text x="500" y="50" text-anchor="middle" fill="#00d2ff" font-size="8" opacity="0.6">→</text>
  <!-- Label -->
  <text x="400" y="370" text-anchor="middle" fill="#8892a4" font-size="10">Senzori šalju telemetriju → ROUTER prosleđuje → MQTT GW šalje na dashboard</text>
</svg>

**Postavka:**
- **SENSOR** čvorovi na terenu — temperatura, vlažnost, pritisak
- **ROUTER** centralni čvor — prima podatke od svih senzora i prosleđuje
- **ROUTER_LATE** sa MQTT — šalje sve na jugomesh.com dashboard

**Zašto SENSOR:**
- Prioritizuje telemetriju — podaci o vremenu stižu redovno
- Smanjuje nodeinfo i pozicione broadcast-ove — baterija traje mesecima sa solarom
- Prosleđuje tuđe pakete samo dok je budan — ne troši energiju na routing

**Iz JugoMesh prakse:** Meteo stanice na Zlatiboru i Goliji koriste SENSOR rolu. Podaci se vide na `vreme.jugomesh.com` u realnom vremenu.

---

## Scenario 5: Vanredne situacije — Komunikacija bez infrastrukture

Kad nestane struja i mobilna mreža — mesh radi dalje.

<svg viewBox="0 0 800 380" xmlns="http://www.w3.org/2000/svg" style="width:100%;max-width:800px;margin:1.5rem auto;display:block;background:linear-gradient(180deg,#1a0a0a 0%,#2a1515 40%,#112240 100%);border-radius:12px;border:1px solid rgba(255,80,80,0.3);">
  <!-- "No signal" indicators -->
  <text x="700" y="30" text-anchor="end" fill="#f87171" font-size="11" opacity="0.7">📵 Nema mobilne mreže</text>
  <text x="700" y="48" text-anchor="end" fill="#f87171" font-size="11" opacity="0.7">⚡ Nema struje</text>
  <!-- Destroyed tower -->
  <line x1="680" y1="100" x2="695" y2="200" stroke="#555" stroke-width="3" opacity="0.4"/>
  <line x1="700" y1="90" x2="690" y2="200" stroke="#555" stroke-width="2" opacity="0.3"/>
  <text x="690" y="215" text-anchor="middle" fill="#f87171" font-size="20" opacity="0.4">✕</text>
  <!-- Person 1 with CLIENT -->
  <circle cx="120" cy="180" r="12" fill="none" stroke="#4ade80" stroke-width="1.5"/>
  <line x1="120" y1="192" x2="120" y2="230" stroke="#4ade80" stroke-width="1.5"/>
  <line x1="120" y1="210" x2="100" y2="225" stroke="#4ade80" stroke-width="1.5"/>
  <line x1="120" y1="210" x2="140" y2="225" stroke="#4ade80" stroke-width="1.5"/>
  <rect x="102" y="150" width="36" height="22" rx="4" fill="#4ade80" fill-opacity="0.2" stroke="#4ade80" stroke-width="1.5"/>
  <text x="120" y="165" text-anchor="middle" fill="#4ade80" font-size="8" font-weight="bold">CLIENT</text>
  <!-- Person 2 -->
  <circle cx="320" cy="200" r="12" fill="none" stroke="#4ade80" stroke-width="1.5"/>
  <line x1="320" y1="212" x2="320" y2="250" stroke="#4ade80" stroke-width="1.5"/>
  <line x1="320" y1="230" x2="300" y2="245" stroke="#4ade80" stroke-width="1.5"/>
  <line x1="320" y1="230" x2="340" y2="245" stroke="#4ade80" stroke-width="1.5"/>
  <rect x="302" y="170" width="36" height="22" rx="4" fill="#4ade80" fill-opacity="0.2" stroke="#4ade80" stroke-width="1.5"/>
  <text x="320" y="185" text-anchor="middle" fill="#4ade80" font-size="8" font-weight="bold">CLIENT</text>
  <!-- Person 3 -->
  <circle cx="530" cy="190" r="12" fill="none" stroke="#4ade80" stroke-width="1.5"/>
  <line x1="530" y1="202" x2="530" y2="240" stroke="#4ade80" stroke-width="1.5"/>
  <line x1="530" y1="220" x2="510" y2="235" stroke="#4ade80" stroke-width="1.5"/>
  <line x1="530" y1="220" x2="550" y2="235" stroke="#4ade80" stroke-width="1.5"/>
  <rect x="512" y="160" width="36" height="22" rx="4" fill="#4ade80" fill-opacity="0.2" stroke="#4ade80" stroke-width="1.5"/>
  <text x="530" y="175" text-anchor="middle" fill="#4ade80" font-size="8" font-weight="bold">CLIENT</text>
  <!-- ROUTER on car roof with battery -->
  <rect x="260" y="85" width="70" height="30" rx="8" fill="#00d2ff" fill-opacity="0.1" stroke="#00d2ff" stroke-width="1.5"/>
  <circle cx="275" cy="118" r="7" fill="#1a0a0a" stroke="#00d2ff" stroke-width="1"/>
  <circle cx="315" cy="118" r="7" fill="#1a0a0a" stroke="#00d2ff" stroke-width="1"/>
  <rect x="272" y="60" width="46" height="22" rx="4" fill="#00d2ff" fill-opacity="0.2" stroke="#00d2ff" stroke-width="2"/>
  <text x="295" y="75" text-anchor="middle" fill="#00d2ff" font-size="8" font-weight="bold">ROUTER</text>
  <text x="295" y="50" text-anchor="middle" fill="#ffd700" font-size="7">🔋 auto baterija</text>
  <!-- Mesh connections -->
  <line x1="120" y1="172" x2="295" y2="82" stroke="#4ade80" stroke-width="1.5" opacity="0.5" stroke-dasharray="4,4"/>
  <line x1="320" y1="170" x2="295" y2="82" stroke="#4ade80" stroke-width="1.5" opacity="0.5" stroke-dasharray="4,4"/>
  <line x1="530" y1="160" x2="295" y2="82" stroke="#4ade80" stroke-width="1.5" opacity="0.4" stroke-dasharray="4,4"/>
  <!-- Direct mesh between persons -->
  <line x1="138" y1="172" x2="302" y2="182" stroke="#4ade80" stroke-width="1" opacity="0.25" stroke-dasharray="3,3"/>
  <line x1="338" y1="182" x2="512" y2="172" stroke="#4ade80" stroke-width="1" opacity="0.25" stroke-dasharray="3,3"/>
  <!-- Message bubbles -->
  <rect x="60" y="260" width="120" height="30" rx="8" fill="#4ade80" fill-opacity="0.1" stroke="#4ade80" stroke-width="1"/>
  <text x="120" y="279" text-anchor="middle" fill="#4ade80" font-size="9">"Svi smo OK"</text>
  <rect x="460" y="260" width="140" height="30" rx="8" fill="#4ade80" fill-opacity="0.1" stroke="#4ade80" stroke-width="1"/>
  <text x="530" y="279" text-anchor="middle" fill="#4ade80" font-size="9">"Treba nam voda"</text>
  <!-- Label -->
  <text x="400" y="340" text-anchor="middle" fill="#c8c8c8" font-size="10">Mesh radi bez interneta, bez struje — samo baterije i radio</text>
  <text x="400" y="358" text-anchor="middle" fill="#f87171" font-size="9" opacity="0.7">Svaki CLIENT prosleđuje jer nema infrastrukturnih ROUTER-a u blizini</text>
</svg>

**Postavka:**
- Svi na **CLIENT** — svako prosleđuje poruke ako niko drugi ne prosledi
- Jedan improvizovani **ROUTER** na krovu automobila — napajan iz auto baterije
- Nema interneta, nema MQTT — čist mesh, poruka do poruke

**Zašto CLIENT za sve:**
- U vanrednoj situaciji svako treba da prima I prosleđuje
- CLIENT automatski prosleđuje kad niko drugi ne prosledi — obezbeđuje pokrivenost
- Ako neko ima bolju lokaciju, prebaci na ROUTER za stabilniji signal

**Ključna lekcija:** Meshtastic ne zavisi od interneta, mobilne mreže ili struje. Dok god imaš bateriju — možeš da komuniciraš. Zato je dobro imati uvek napunjen uređaj u kućnom setu za vanredne situacije.

---

## Scenario 6: Festival ili okupljanje — Privremena mreža

Kada se mnogo ljudi skupi na malom prostoru, mesh mreža zamenjuje preopterećene mobilne mreže.

<svg viewBox="0 0 800 350" xmlns="http://www.w3.org/2000/svg" style="width:100%;max-width:800px;margin:1.5rem auto;display:block;background:linear-gradient(180deg,#0a1628 0%,#112240 100%);border-radius:12px;border:1px solid rgba(0,210,255,0.2);">
  <!-- Stage -->
  <rect x="300" y="30" width="200" height="60" rx="5" fill="#a78bfa" fill-opacity="0.1" stroke="#a78bfa" stroke-width="1.5"/>
  <text x="400" y="55" text-anchor="middle" fill="#a78bfa" font-size="11">🎵 BINA</text>
  <text x="400" y="75" text-anchor="middle" fill="#a78bfa" font-size="8">ROUTER ovde</text>
  <!-- Router on stage -->
  <rect x="465" y="40" width="30" height="20" rx="4" fill="#00d2ff" fill-opacity="0.3" stroke="#00d2ff" stroke-width="1.5"/>
  <text x="480" y="54" text-anchor="middle" fill="#00d2ff" font-size="8" font-weight="bold">R</text>
  <!-- Crowd of CLIENT_MUTE -->
  <circle cx="200" cy="170" r="8" fill="#f87171" fill-opacity="0.3" stroke="#f87171" stroke-width="1"/>
  <circle cx="230" cy="160" r="8" fill="#f87171" fill-opacity="0.3" stroke="#f87171" stroke-width="1"/>
  <circle cx="260" cy="175" r="8" fill="#f87171" fill-opacity="0.3" stroke="#f87171" stroke-width="1"/>
  <circle cx="300" cy="155" r="8" fill="#f87171" fill-opacity="0.3" stroke="#f87171" stroke-width="1"/>
  <circle cx="330" cy="170" r="8" fill="#f87171" fill-opacity="0.3" stroke="#f87171" stroke-width="1"/>
  <circle cx="360" cy="160" r="8" fill="#f87171" fill-opacity="0.3" stroke="#f87171" stroke-width="1"/>
  <circle cx="390" cy="175" r="8" fill="#f87171" fill-opacity="0.3" stroke="#f87171" stroke-width="1"/>
  <circle cx="420" cy="155" r="8" fill="#f87171" fill-opacity="0.3" stroke="#f87171" stroke-width="1"/>
  <circle cx="450" cy="170" r="8" fill="#f87171" fill-opacity="0.3" stroke="#f87171" stroke-width="1"/>
  <circle cx="480" cy="160" r="8" fill="#f87171" fill-opacity="0.3" stroke="#f87171" stroke-width="1"/>
  <circle cx="510" cy="175" r="8" fill="#f87171" fill-opacity="0.3" stroke="#f87171" stroke-width="1"/>
  <circle cx="540" cy="165" r="8" fill="#f87171" fill-opacity="0.3" stroke="#f87171" stroke-width="1"/>
  <circle cx="280" cy="195" r="8" fill="#f87171" fill-opacity="0.3" stroke="#f87171" stroke-width="1"/>
  <circle cx="340" cy="200" r="8" fill="#f87171" fill-opacity="0.3" stroke="#f87171" stroke-width="1"/>
  <circle cx="400" cy="195" r="8" fill="#f87171" fill-opacity="0.3" stroke="#f87171" stroke-width="1"/>
  <circle cx="460" cy="200" r="8" fill="#f87171" fill-opacity="0.3" stroke="#f87171" stroke-width="1"/>
  <text x="370" y="140" text-anchor="middle" fill="#f87171" font-size="9">CLIENT_MUTE × mnogo</text>
  <!-- Few CLIENTS for forwarding -->
  <circle cx="150" cy="180" r="10" fill="#4ade80" fill-opacity="0.3" stroke="#4ade80" stroke-width="1.5"/>
  <text x="150" y="184" text-anchor="middle" fill="#4ade80" font-size="8" font-weight="bold">C</text>
  <circle cx="580" cy="170" r="10" fill="#4ade80" fill-opacity="0.3" stroke="#4ade80" stroke-width="1.5"/>
  <text x="580" y="174" text-anchor="middle" fill="#4ade80" font-size="8" font-weight="bold">C</text>
  <!-- Info area -->
  <rect x="100" y="260" width="250" height="55" rx="8" fill="rgba(0,210,255,0.05)" stroke="rgba(0,210,255,0.2)" stroke-width="1"/>
  <text x="225" y="280" text-anchor="middle" fill="#00d2ff" font-size="9" font-weight="bold">✅ Dobra praksa</text>
  <text x="225" y="296" text-anchor="middle" fill="#8892a4" font-size="8">Većina na CLIENT_MUTE</text>
  <text x="225" y="308" text-anchor="middle" fill="#8892a4" font-size="8">Samo 2-3 CLIENT-a prosleđuju</text>
  <rect x="450" y="260" width="250" height="55" rx="8" fill="rgba(255,80,80,0.05)" stroke="rgba(255,80,80,0.2)" stroke-width="1"/>
  <text x="575" y="280" text-anchor="middle" fill="#f87171" font-size="9" font-weight="bold">❌ Loša praksa</text>
  <text x="575" y="296" text-anchor="middle" fill="#8892a4" font-size="8">Svi na CLIENT ili ROUTER</text>
  <text x="575" y="308" text-anchor="middle" fill="#8892a4" font-size="8">= kolizije, zagušenje kanala</text>
  <!-- Label -->
  <text x="400" y="345" text-anchor="middle" fill="#8892a4" font-size="10">Na festivalu: većina na CLIENT_MUTE, samo par čvorova prosleđuje</text>
</svg>

**Postavka:**
- **ROUTER** na bini ili visokoj tački — jedini čvor koji uvek prosleđuje
- Većina publike na **CLIENT_MUTE** — primaju i šalju poruke, ali NE prosleđuju
- Par organizatora na **CLIENT** — prosleđuju ako ROUTER ne pokrije

**Zašto CLIENT_MUTE za većinu:**
- Na okupljanju sa 50+ uređaja, ako svi prosleđuju, kanal se zasiti kolizijama
- CLIENT_MUTE eliminiše nepotrebne retransmisije
- Samo infrastrukturni čvorovi (ROUTER + par CLIENT-a) se brinu o prosleđivanju

**Zlatno pravilo:** Što više ljudi, to više CLIENT_MUTE. Na malom okupljanju (5-10 ljudi) svi mogu biti CLIENT. Na velikom (50+) — većina mora biti MUTE.

---

## Scenario 7: Monitoring vikendice — Daleki čvor sa baznom stanicom

Praćenje vikendice ili imanja koje je van dometa direktnog signala.

<svg viewBox="0 0 800 320" xmlns="http://www.w3.org/2000/svg" style="width:100%;max-width:800px;margin:1.5rem auto;display:block;background:linear-gradient(180deg,#0a1628 0%,#112240 100%);border-radius:12px;border:1px solid rgba(0,210,255,0.2);">
  <!-- House in city -->
  <rect x="60" y="140" width="80" height="70" rx="3" fill="#152a4a" stroke="#2a4a6a" stroke-width="1.5"/>
  <polygon points="50,142 100,100 150,142" fill="#1a3050" stroke="#2a4a6a" stroke-width="1"/>
  <rect x="85" y="170" width="20" height="35" rx="2" fill="#1a3d6d"/>
  <rect x="70" y="155" width="14" height="14" rx="1" fill="#1a3d6d"/>
  <text x="100" y="88" text-anchor="middle" fill="#22d3ee" font-size="9" font-weight="bold">CLIENT_BASE</text>
  <rect x="115" y="110" width="30" height="20" rx="3" fill="#22d3ee" fill-opacity="0.2" stroke="#22d3ee" stroke-width="1.5"/>
  <text x="130" y="124" text-anchor="middle" fill="#22d3ee" font-size="8" font-weight="bold">CB</text>
  <text x="100" y="230" text-anchor="middle" fill="#8892a4" font-size="9">Kuća u gradu</text>
  <!-- Mountain relay -->
  <polygon points="330,270 400,100 470,270" fill="#1a3a5c" stroke="#2a5a8c" stroke-width="1"/>
  <rect x="382" y="75" width="36" height="22" rx="4" fill="#00d2ff" fill-opacity="0.2" stroke="#00d2ff" stroke-width="2"/>
  <text x="400" y="90" text-anchor="middle" fill="#00d2ff" font-size="9" font-weight="bold">R</text>
  <text x="400" y="68" text-anchor="middle" fill="#00d2ff" font-size="8">ROUTER</text>
  <!-- Cabin -->
  <rect x="620" y="150" width="70" height="55" rx="3" fill="#152a4a" stroke="#2a4a6a" stroke-width="1.5"/>
  <polygon points="615,152 655,120 695,152" fill="#1a3050" stroke="#2a4a6a" stroke-width="1"/>
  <rect x="640" y="170" width="15" height="30" rx="2" fill="#1a3d6d"/>
  <!-- Sensor inside cabin -->
  <rect x="670" y="125" width="36" height="22" rx="4" fill="#f59e0b" fill-opacity="0.2" stroke="#f59e0b" stroke-width="1.5"/>
  <text x="688" y="140" text-anchor="middle" fill="#f59e0b" font-size="9" font-weight="bold">S</text>
  <text x="688" y="118" text-anchor="middle" fill="#f59e0b" font-size="8">SENSOR</text>
  <text x="655" y="225" text-anchor="middle" fill="#8892a4" font-size="9">Vikendica</text>
  <!-- Sensor data -->
  <text x="730" y="150" text-anchor="start" fill="#f59e0b" font-size="8" opacity="0.7">🌡 5°C</text>
  <text x="730" y="165" text-anchor="start" fill="#f59e0b" font-size="8" opacity="0.7">💧 72%</text>
  <text x="730" y="180" text-anchor="start" fill="#f59e0b" font-size="8" opacity="0.7">🚪 zatvoren</text>
  <!-- Connections -->
  <line x1="145" y1="120" x2="382" y2="86" stroke="#22d3ee" stroke-width="1.2" opacity="0.5" stroke-dasharray="4,4"/>
  <line x1="418" y1="86" x2="670" y2="136" stroke="#f59e0b" stroke-width="1.2" opacity="0.5" stroke-dasharray="4,4"/>
  <!-- Distance labels -->
  <text x="250" y="85" text-anchor="middle" fill="#8892a4" font-size="8">~15 km</text>
  <text x="550" y="95" text-anchor="middle" fill="#8892a4" font-size="8">~20 km</text>
  <!-- Phone notification -->
  <rect x="30" y="245" width="140" height="30" rx="6" fill="#4ade80" fill-opacity="0.1" stroke="#4ade80" stroke-width="1"/>
  <text x="100" y="264" text-anchor="middle" fill="#4ade80" font-size="8">📱 Vikendica: 5°C, sve OK</text>
  <!-- Label -->
  <text x="400" y="305" text-anchor="middle" fill="#8892a4" font-size="10">CLIENT_BASE favorizuje vikendicu — svaki njen paket ima prioritet</text>
</svg>

**Postavka:**
- **SENSOR** u vikendici — šalje temperaturu, vlažnost, stanje vrata
- **ROUTER** na planini između — prenosi signal
- **CLIENT_BASE** kod kuće — favorizuje vikendicu, svaki njen paket prosleđuje s prioritetom

**Zašto CLIENT_BASE:**
- Vikendica je daleko, signal je slab
- CLIENT_BASE tretira SENSOR u vikendici kao favorizovani čvor
- Čak i kad je signal na granici, CLIENT_BASE će pokušati da prosledi
- Na telefonu kod kuće vidite temperaturu i stanje vikendice u realnom vremenu

---

## Kako izabrati rolu — Dijagram odluke

<svg viewBox="0 0 800 500" xmlns="http://www.w3.org/2000/svg" style="width:100%;max-width:800px;margin:1.5rem auto;display:block;background:linear-gradient(180deg,#0a1628 0%,#112240 100%);border-radius:12px;border:1px solid rgba(0,210,255,0.2);">
  <!-- Start -->
  <rect x="320" y="20" width="160" height="40" rx="20" fill="#00d2ff" fill-opacity="0.2" stroke="#00d2ff" stroke-width="2"/>
  <text x="400" y="45" text-anchor="middle" fill="#00d2ff" font-size="12" font-weight="bold">Šta je cilj?</text>
  <!-- Branch 1: Infrastructure -->
  <line x1="340" y1="60" x2="150" y2="100" stroke="#00d2ff" stroke-width="1.5" opacity="0.5"/>
  <rect x="60" y="100" width="180" height="36" rx="6" fill="#1a2d4a" stroke="#00d2ff" stroke-width="1"/>
  <text x="150" y="123" text-anchor="middle" fill="#e0e0e0" font-size="10">Infrastruktura mreže</text>
  <!-- Sub-branch: Power? -->
  <line x1="150" y1="136" x2="150" y2="170" stroke="#00d2ff" stroke-width="1" opacity="0.4"/>
  <rect x="70" y="170" width="160" height="30" rx="6" fill="#1a2d4a" stroke="#445" stroke-width="1"/>
  <text x="150" y="190" text-anchor="middle" fill="#c0c0c0" font-size="9">Stalna struja?</text>
  <!-- Yes -->
  <line x1="110" y1="200" x2="80" y2="240" stroke="#4ade80" stroke-width="1" opacity="0.5"/>
  <text x="90" y="225" text-anchor="middle" fill="#4ade80" font-size="8">DA</text>
  <rect x="30" y="240" width="100" height="35" rx="6" fill="#00d2ff" fill-opacity="0.15" stroke="#00d2ff" stroke-width="1.5"/>
  <text x="80" y="262" text-anchor="middle" fill="#00d2ff" font-size="11" font-weight="bold">ROUTER</text>
  <!-- No -->
  <line x1="190" y1="200" x2="220" y2="240" stroke="#f87171" stroke-width="1" opacity="0.5"/>
  <text x="210" y="225" text-anchor="middle" fill="#f87171" font-size="8">NE</text>
  <rect x="160" y="240" width="120" height="35" rx="6" fill="#a78bfa" fill-opacity="0.15" stroke="#a78bfa" stroke-width="1.5"/>
  <text x="220" y="256" text-anchor="middle" fill="#a78bfa" font-size="10" font-weight="bold">ROUTER_LATE</text>
  <text x="220" y="270" text-anchor="middle" fill="#a78bfa" font-size="7">(backup)</text>
  <!-- Branch 2: Tracking -->
  <line x1="400" y1="60" x2="400" y2="100" stroke="#f59e0b" stroke-width="1.5" opacity="0.5"/>
  <rect x="320" y="100" width="160" height="36" rx="6" fill="#1a2d4a" stroke="#f59e0b" stroke-width="1"/>
  <text x="400" y="123" text-anchor="middle" fill="#e0e0e0" font-size="10">Praćenje / Senzori</text>
  <!-- Sub: GPS or Telemetry? -->
  <line x1="400" y1="136" x2="400" y2="170" stroke="#f59e0b" stroke-width="1" opacity="0.4"/>
  <rect x="315" y="170" width="170" height="30" rx="6" fill="#1a2d4a" stroke="#445" stroke-width="1"/>
  <text x="400" y="190" text-anchor="middle" fill="#c0c0c0" font-size="9">GPS pozicija ili telemetrija?</text>
  <!-- GPS -->
  <line x1="360" y1="200" x2="330" y2="240" stroke="#f59e0b" stroke-width="1" opacity="0.5"/>
  <text x="335" y="225" text-anchor="middle" fill="#f59e0b" font-size="8">GPS</text>
  <rect x="290" y="240" width="100" height="35" rx="6" fill="#f59e0b" fill-opacity="0.15" stroke="#f59e0b" stroke-width="1.5"/>
  <text x="340" y="262" text-anchor="middle" fill="#f59e0b" font-size="11" font-weight="bold">TRACKER</text>
  <!-- Telemetry -->
  <line x1="440" y1="200" x2="470" y2="240" stroke="#f59e0b" stroke-width="1" opacity="0.5"/>
  <text x="465" y="225" text-anchor="middle" fill="#f59e0b" font-size="8">Telem.</text>
  <rect x="420" y="240" width="100" height="35" rx="6" fill="#f59e0b" fill-opacity="0.15" stroke="#f59e0b" stroke-width="1.5"/>
  <text x="470" y="262" text-anchor="middle" fill="#f59e0b" font-size="11" font-weight="bold">SENSOR</text>
  <!-- Branch 3: Communication -->
  <line x1="460" y1="60" x2="650" y2="100" stroke="#4ade80" stroke-width="1.5" opacity="0.5"/>
  <rect x="570" y="100" width="160" height="36" rx="6" fill="#1a2d4a" stroke="#4ade80" stroke-width="1"/>
  <text x="650" y="123" text-anchor="middle" fill="#e0e0e0" font-size="10">Komunikacija</text>
  <!-- Sub: Many people? -->
  <line x1="650" y1="136" x2="650" y2="170" stroke="#4ade80" stroke-width="1" opacity="0.4"/>
  <rect x="565" y="170" width="170" height="30" rx="6" fill="#1a2d4a" stroke="#445" stroke-width="1"/>
  <text x="650" y="190" text-anchor="middle" fill="#c0c0c0" font-size="9">Puno čvorova u blizini?</text>
  <!-- Yes many -->
  <line x1="610" y1="200" x2="580" y2="240" stroke="#f87171" stroke-width="1" opacity="0.5"/>
  <text x="585" y="225" text-anchor="middle" fill="#f87171" font-size="8">DA</text>
  <rect x="520" y="240" width="120" height="35" rx="6" fill="#f87171" fill-opacity="0.15" stroke="#f87171" stroke-width="1.5"/>
  <text x="580" y="256" text-anchor="middle" fill="#f87171" font-size="10" font-weight="bold">CLIENT_MUTE</text>
  <text x="580" y="270" text-anchor="middle" fill="#f87171" font-size="7">(ne zagušuj)</text>
  <!-- No few -->
  <line x1="690" y1="200" x2="720" y2="240" stroke="#4ade80" stroke-width="1" opacity="0.5"/>
  <text x="715" y="225" text-anchor="middle" fill="#4ade80" font-size="8">NE</text>
  <rect x="670" y="240" width="100" height="35" rx="6" fill="#4ade80" fill-opacity="0.15" stroke="#4ade80" stroke-width="1.5"/>
  <text x="720" y="262" text-anchor="middle" fill="#4ade80" font-size="11" font-weight="bold">CLIENT</text>
  <!-- Bottom summary -->
  <rect x="100" y="320" width="600" height="80" rx="10" fill="rgba(0,210,255,0.03)" stroke="rgba(0,210,255,0.15)" stroke-width="1"/>
  <text x="400" y="345" text-anchor="middle" fill="#00d2ff" font-size="11" font-weight="bold">Zlatna pravila</text>
  <text x="400" y="365" text-anchor="middle" fill="#c0c0c0" font-size="9">🔹 Počni sa CLIENT — prebaci tek kad vidiš potrebu</text>
  <text x="400" y="382" text-anchor="middle" fill="#c0c0c0" font-size="9">🔹 ROUTER samo na stalnoj struji i dobroj lokaciji</text>
  <text x="400" y="399" text-anchor="middle" fill="#c0c0c0" font-size="9">🔹 Više ljudi = više CLIENT_MUTE, manje ROUTER-a</text>
  <!-- Decorative -->
  <text x="400" y="480" text-anchor="middle" fill="#556" font-size="9">Detaljan opis svake role: jugomesh.com/blog/meshtastic-role-vodic</text>
</svg>

---

## Zaključak

Role nisu samo tehnička podešavanja — one su **strategija**. Pravilno raspoređene role čine razliku između mreže koja radi i mreže koja se guši u kolizijama.

**Tri stvari za zapamtiti:**

1. **Lokacija određuje rolu** — visoko i na struji = ROUTER, u dolini = CLIENT
2. **Manje je više** — ne stavljaj ROUTER svuda, koristi CLIENT_MUTE na okupljanjima
3. **Mesh je tim** — svaki čvor ima svoju ulogu, kao igrači u timu

Pogledaj [vodič za sve role](/blog/meshtastic-role-vodic) za detaljne specifikacije svake role.
