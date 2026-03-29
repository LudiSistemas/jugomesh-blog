# Jugomesh Blog

Blog članci za [Jugomesh](https://jugomesh.com) — Meshtastic mrežni monitor za Srbiju.

## Struktura

Direktorijumi su kategorije:

```
vodiči/          — Vodiči i tutorijali za Meshtastic
vesti/           — Vesti sa mreže
tehnika/         — Tehnički članci
```

## Format članaka

Svaki članak je **čist Markdown fajl**. Metadata se automatski čita:

- **Naslov** — iz prvog `# Naslov` u fajlu
- **Autor** — iz git historije (ko je commitovao fajl)
- **Datum** — iz git historije (kad je fajl prvi put dodat)
- **Opis** — iz prvog paragrafa posle naslova

```markdown
# Naslov članka

Kratak opis koji se prikazuje na listi članaka.

## Prvi podnaslov

Sadržaj članka...
```

URL članka je naziv fajla bez `.md` ekstenzije: `vodiči/moj-clanak.md` → `jugomesh.com/blog/moj-clanak`

## Kako doprineti

1. Forkuj ovaj repo
2. Dodaj novi `.md` fajl u odgovarajuću kategoriju
3. Otvori Pull Request
4. Posle merge-a na `main`, članak se automatski objavljuje na sajtu

## Deploy

Automatski preko GitHub Actions — svaki push na `main` sinhronizuje sadržaj na server. Nije potrebna nikakva dodatna konfiguracija za autore.

## Pravila

- Članci moraju biti na Srpskom jeziku
- Naziv fajla koristi samo ASCII karaktere i crtice (`moj-clanak.md`)
- Jedan `# Naslov` na vrhu fajla je obavezan
