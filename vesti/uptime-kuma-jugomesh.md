# JugoMesh Uptime API + Uptime Kuma vodič

Kako da pratiš online/offline status Meshtastic nodova preko JugoMesh API-ja i prikažeš ga u Uptime Kuma monitoringu.

---

## Šta je ovo?

JugoMesh nudi API za proveru statusa nodova:

- `online` ako je nod imao aktivnost u poslednja 2 sata
- `offline` ako nije bilo aktivnosti unutar tog perioda

Status se osvežava periodično (na sat vremena), pa je idealan za lagani health monitoring.

---

## API endpointi

### Status jednog noda

`GET https://jugomesh.com/api/node/{node_id}/uptime`

**HTTP odgovori:**

- `200` - nod je online
- `503` - nod je offline
- `404` - nod nije pronađen

**Primer poziva:**

`https://jugomesh.com/api/node/2998283580/uptime`

**Primer JSON odgovora:**

```json
{
  "status": "online",
  "node_id": 2998283580,
  "hex_id": "!b2b0113c",
  "long_name": "VelikiMokriLug",
  "last_updated": 1776171004.63,
  "seconds_ago": 342,
  "threshold": 7200
}
```

### Status svih nodova (bulk)

`GET https://jugomesh.com/api/nodes/uptime`

Vraća listu svih nodova sa statusom. Ovaj endpoint vraća `200`.

---

## Podešavanje u Uptime Kuma

1. Dodaj novi monitor i izaberi tip `HTTP(s)`.
2. U polje URL unesi: `https://jugomesh.com/api/node/{node_id}/uptime`.
3. Zameni `{node_id}` ID-em noda koji želiš da pratiš.
4. Podesi `Heartbeat Interval` na `3600` sekundi (1 sat).
5. `Accepted Status Codes` ostavi na `200`.
6. Sačuvaj monitor - Uptime Kuma će prikazivati `UP` / `DOWN`.

---

## Gde naći `node_id`?

- Otvori stranicu noda na `jugomesh.com` (npr. `/node/2998283580`)
- Ili pozovi bulk endpoint `https://jugomesh.com/api/nodes/uptime`

---

## Rate limit

| Endpoint | Ograničenje |
|---|---|
| `/api/node/{id}/uptime` | 60 zahteva/min po IP |
| `/api/nodes/uptime` | 10 zahteva/min po IP |

Pri prekoračenju limita server vraća `429`.

---

## Napomene

- Nod se smatra online ako je poslednja aktivnost unutar `7200` sekundi
- Status se računa u pozadini na svakih 1 sat
- `node_id` može biti decimalni (`2998283580`) ili hex (`!b2b0113c`)
