# Jugomesh Blog

Blog članci za [Jugomesh](https://jugomesh.com) — Meshtastic mrežni monitor za Srbiju.

## Struktura

Direktorijumi su kategorije:

```
vodiči/          — Vodiči i tutorijali za Meshtastic
vesti/           — Vesti iz mreže
tehnika/        — Tehnički članci
```

## Format članaka

Svaki članak je Markdown fajl sa YAML headerom:

```markdown
---
title: Naslov članka
date: 2026-03-29
author: github-username
summary: Kratak opis za listu članaka.
icon: bi-router
---

Sadržaj članka u Markdown formatu...
```

Polje `author` je GitHub korisničko ime — na sajtu se prikazuje kao link na GitHub profil autora.

Ikone: bilo koja [Bootstrap Icons](https://icons.getbootstrap.com/) klasa.

## Kako doprineti

1. Fork ovaj repo
2. Dodaj novi `.md` fajl u odgovarajuću kategoriju
3. Otvori Pull Request
4. Posle merge-a na `main`, članak se automatski objavljuje na sajtu

## Pravila

- Članci moraju biti na srpskom jeziku
- YAML header je obavezan (title, date, author, summary)
- Slike se mogu linkati eksterno
