# Meshtastic role — Koji tip čvora si ti?

Kompletni vodič kroz sve Meshtastic role — od CLIENT-a do ROUTER-a. Objašnjeno jednostavno, sa primerima iz prakse.

---

## Šta su role i zašto su bitne?

Svaki Meshtastic uređaj ima **rolu** — to je kao "posao" koji tvoj uređaj obavlja u mreži. Rola određuje:

- Da li tvoj uređaj **prosleđuje tuđe poruke** ili samo prima/šalje svoje
- Koliko **struje troši** (bitno za baterijsko napajanje)
- Da li je **vidljiv** ostalim korisnicima u mreži
- Koliko **brzo reaguje** na prosleđivanje paketa

Pogrešna rola može da uguši mrežu ili da ti brzo potroši bateriju. Evo vodiča za svaku.

---

## CLIENT — Osnovni korisnik

**Za koga:** Svako ko koristi Meshtastic za dopisivanje i praćenje mreže.

**Šta radi:**
- Prima i šalje tvoje poruke
- Prosleđuje tuđe poruke, ali **samo ako niko drugi već nije prosledio**
- Ako čuje da je drugi nod već prosledio paket, odustaje od prosleđivanja

**Potrošnja:** Srednja — radio se povremeno pali

**Kada koristiti:**
- Imaš telefon povezan sa uređajem
- Čitaš poruke, gledaš mapu, šalješ poruke
- Većina korisnika treba da bude na ovoj roli

> 💡 **Ako si početnik — izaberi CLIENT.** Ovo je podrazumevana rola i radi savršeno za 90% korisnika.

---

## CLIENT_MUTE — Tihi korisnik

**Za koga:** Ko želi da prati mrežu ali ne želi da mu uređaj prosleđuje tuđe pakete.

**Šta radi:**
- Prima i šalje tvoje poruke
- **NE prosleđuje** tuđe poruke — potpuno je "tih" u mreži

**Potrošnja:** Najniža od svih rola

**Kada koristiti:**
- Imaš slab signal i ne doprinosiš mreži prosleđivanjem
- Želiš maksimalnu uštedu baterije
- Želiš da pratiš mrežu bez generisanja saobraćaja
- Imaš više uređaja na istoj lokaciji (samo jedan treba da prosleđuje)

> ⚠️ **Pažnja:** Poruke neće biti prosleđivane kroz tvoj uređaj, što će smanjiti domet mreže u tvom delu.

---

## CLIENT_HIDDEN — Nevidljivi korisnik

**Za koga:** Ko želi privatnost — uređaj ne objavljuje svoju poziciju i informacije.

**Šta radi:**
- Prima i šalje poruke
- Prosleđuje pakete, ali **samo lokalne** (tvoji kanali)
- **Ne pojavljuje se** u spisku čvorova kod drugih korisnika

**Potrošnja:** Niska

**Kada koristiti:**
- Ne želiš da drugi vide da postojiš u mreži
- Koristiš mrežu ali ne želiš da ostavljaš trag

---

## CLIENT_BASE — Bazna stanica za korisnike

**Za koga:** Napredni korisnici sa stalnom strujom koji žele da podrže mrežu za specifične uređaje.

**Šta radi:**
- Za **favorizovane čvorove** — ponaša se kao ROUTER (uvek prosleđuje)
- Za ostale čvorove — ponaša se kao obični CLIENT
- Ne troši hop budžet kada prosleđuje između favorizovanih rutera

**Potrošnja:** Srednja do visoka

**Kada koristiti:**
- Imaš baznu stanicu kod kuće sa stalnom strujom
- Želiš da garantuješ dobar signal za tvoje uređaje (npr. tracker u autu)
- Imaš više svojih čvorova i želiš da ih povežeš

> 💡 **Primer:** Imaš fiksnu antenu na krovu i mobilni tracker u kolima. Stavi krovnu stanicu na CLIENT_BASE i dodaj tracker kao favorit — uvek će proslediti njegove pakete sa prioritetom.

---

## ROUTER — Mrežni ruter

**Za koga:** Infrastrukturni čvorovi na stalnoj struji, na dobrim lokacijama.

**Šta radi:**
- **Uvek prosleđuje** svaki paket koji primi — nikad ne odustaje
- Prosleđuje **pre svih ostalih** (najkraći delay)
- WiFi i ekran se automatski isključuju za uštedu
- Ne troši hop budžet između favorizovanih rutera

**Potrošnja:** Srednja (radio aktivan, sve ostalo ugašeno)

**Kada koristiti:**
- Postavljaš čvor na toranj, krov, planinu
- Čvor ima stalnu struju ili solarno napajanje
- Lokacija ima dobar pogled (line of sight) u više pravaca
- Cilj ti je da **proširiš pokrivenost mreže**

> 🔑 **Ovo je NAJVAŽNIJA rola za mrežu.** Dobar ROUTER na visokoj tački može da poveže čvorove na 50-200km udaljenosti. Jugomesh mreža zavisi od ROUTER čvorova na planinama.

> ⚠️ **Ne stavljaj ROUTER na uređaj koji nosiš sa sobom.** ROUTER uvek reemituje i troši bateriju. Za mobilnu upotrebu koristi CLIENT.

---

## ROUTER_LATE — Rezervni ruter

**Za koga:** Čvorovi koji treba da budu backup za mrežu — prosleđuju samo kad niko drugi ne prosledi.

**Šta radi:**
- **Uvek prosleđuje** svaki paket (nikad ne odustaje)
- Ali čeka **duže od svih** pre prosleđivanja
- Ako ROUTER ili CLIENT već prosledi paket, ROUTER_LATE se aktivira samo kao backup

**Potrošnja:** Srednja

**Kada koristiti:**
- Imaš čvor na dobroj lokaciji ali ne želiš da dominira mrežom
- Želiš backup prosleđivanje — ako primarni ruteri ne proslede, tvoj će! Ili imaš MQTT gateway koji treba da prosleđuje ali ne da bude primarni ruter

> 💡 **Jugomesh savet:** Naši MQTT gejtvejevi (Paxy, Knez Mihailova) koriste ROUTER_LATE — prosleđuju pakete ali daju prednost pravim ROUTER čvorovima na planinama.

---

## REPEATER — Jednostavni repetitor (ZASTARELO)

**Za koga:** Niko — ova rola je **ukinuta** od firmware verzije 2.7.11.

**Šta je radila:**
- Prosleđivala pakete bez dekriptovanja
- Bila nevidljiva u mreži
- Stvarala "rupe" u traceroute podacima

> ❌ **Ne koristi ovu rolu.** Ako ti je uređaj na REPEATER, prebaci ga na ROUTER.

---

## TRACKER — GPS tracker

**Za koga:** Uređaji koji prvenstveno šalju GPS poziciju (npr. u kolima, na biciklu, na psu).

**Šta radi:**
- Prioritetno šalje **poziciju** u kraćim intervalima
- Smanjuje ostale broadcast-ove (nodeinfo, telemetrija) da uštedi kanal
- Prosleđuje tuđe pakete samo dok je budan

**Potrošnja:** Niska do srednja (zavisi od intervala slanja)

**Kada koristiti:**
- Pratiš vozilo ili osobu
- Uređaj je na bateriji i treba da traje dugo
- Bitna ti je pozicija, ne dopisivanje

> 💡 **Primer:** T-Beam u autu — šalje poziciju svaka 2 minuta, baterija traje danima.

---

## SENSOR — Senzorska stanica

**Za koga:** Uređaji koji prvenstveno šalju telemetriju (temperatura, vlažnost, vazdušni pritisak).

**Šta radi:**
- Prioritetno šalje **telemetriju** senzora
- Smanjuje ostale broadcast-ove
- Prosleđuje tuđe pakete samo dok je budan

**Potrošnja:** Niska

**Kada koristiti:**
- Meteo stanica
- Monitoring temperatura u stakleniku, podrumu, serverskoj sobi
- Bilo koji IoT senzor koji šalje podatke preko mesh mreže

> 💡 **Jugomesh primer:** WS stanice (Weather Station) na Goliji, Kablaru, Zlatiboru koriste SENSOR rolu za slanje temperature i vlažnosti.

---

## TAK — ATAK integracija

**Za koga:** Korisnici Android Team Awareness Kit (ATAK) sistema.

**Šta radi:**
- Optimizovano za TAK plugin
- Automatski šalje PLI (Position Location Information) u TAK formatu
- Smanjuje rutinske broadcast-ove

**Potrošnja:** Srednja

**Kada koristiti:**
- Koristiš ATAK/CivTAK aplikaciju
- Potrebna ti je taktička situaciona svest

> ℹ️ Ova rola je specijalizovana. Ako ne znaš šta je ATAK, ne treba ti.

---

## TAK_TRACKER — TAK tracker

**Za koga:** TAK korisnici kojima treba automatsko praćenje pozicije.

**Šta radi:** Kombinacija TAK + TRACKER — automatski šalje PLI bez manuelnog aktiviranja.

---

## LOST_AND_FOUND — Pronađi izgubljeni uređaj

**Za koga:** Uređaji koji treba da se pronađu ako se izgube.

**Šta radi:**
- Šalje svoju poziciju kao **tekstualnu poruku** na podrazumevani kanal
- Svako u mreži može da vidi gde je uređaj

**Kada koristiti:**
- Stavio si uređaj na nešto vredno (dron, bicikl, oprema)
- Ako se izgubi, mreža će objaviti lokaciju

---

## Tabela za brz pregled

| Rola | Prosleđuje? | Prioritet | Baterija | Za koga |
|------|------------|-----------|----------|---------|
| CLIENT | Da (ako niko drugi) | Normalan | Srednja | Većina korisnika |
| CLIENT_MUTE | Ne | - | Najniža | Pasivno praćenje |
| CLIENT_HIDDEN | Lokalno | Normalan | Niska | Privatnost |
| CLIENT_BASE | Za favorite DA | Visok za fav. | Srednja | Bazna stanica |
| ROUTER | Uvek | Najviši | Srednja | Infrastruktura |
| ROUTER_LATE | Uvek (kasni) | Najniži | Srednja | Backup ruter |
| TRACKER | Dok je budan | Normalan | Niska | GPS praćenje |
| SENSOR | Dok je budan | Normalan | Niska | Meteo/IoT |

---

## Koji da izaberem?

**Počni sa CLIENT.** Ako vidiš da tvoj uređaj može da pomogne mreži (dobra lokacija, stalna struja) — prebaci na ROUTER. Ako ti treba samo praćenje — TRACKER. Ako samo gledaš — CLIENT_MUTE.

Za Jugomesh mrežu u Srbiji, najviše nam trebaju **ROUTER čvorovi na visokim tačkama** — oni su kičma cele mreže. Svaki novi ROUTER na planini ili visokoj zgradi dramatično poboljšava pokrivenost.
