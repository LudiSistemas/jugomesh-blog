# Scenariji korišćenja Meshtastic rola — Iz prakse, za praksu

Kako se role koriste u stvarnom svetu? Kroz konkretne primere iz JugoMesh mreže i tipične situacije, objašnjavamo koji čvor gde ide i zašto.

---

## Scenario 1: Planinski repetitor — Kičma mreže

Najvažniji scenario za svaku mesh mrežu. Jedan ROUTER čvor na visokoj tački može da poveže desetine korisnika u dolini.

![Planinski ROUTER povezuje dva sela](/blog/img/scenario-planinski-router.svg)

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

![Urbana mreža sa ROUTER-om i MQTT gateway-om](/blog/img/scenario-urbana-mreza.svg)

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

![Tracker u vozilu sa CLIENT_BASE kod kuće](/blog/img/scenario-tracker-vozilo.svg)

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

![Mreža SENSOR čvorova sa centralnim ROUTER-om](/blog/img/scenario-meteo-mreza.svg)

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

![Mesh komunikacija u vanrednoj situaciji](/blog/img/scenario-vanredna-situacija.svg)

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

![Festival — većina na CLIENT_MUTE](/blog/img/scenario-festival.svg)

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

![Monitoring vikendice sa CLIENT_BASE](/blog/img/scenario-vikendica.svg)

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

![Dijagram odluke za izbor role](/blog/img/scenario-dijagram-odluke.svg)

---

## Zaključak

Role nisu samo tehnička podešavanja — one su **strategija**. Pravilno raspoređene role čine razliku između mreže koja radi i mreže koja se guši u kolizijama.

**Tri stvari za zapamtiti:**

1. **Lokacija određuje rolu** — visoko i na struji = ROUTER, u dolini = CLIENT
2. **Manje je više** — ne stavljaj ROUTER svuda, koristi CLIENT_MUTE na okupljanjima
3. **Mesh je tim** — svaki čvor ima svoju ulogu, kao igrači u timu

Pogledaj [vodič za sve role](/blog/meshtastic-role-vodic) za detaljne specifikacije svake role.
