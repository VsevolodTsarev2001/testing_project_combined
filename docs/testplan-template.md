# Testiplaani mall

# Testiplaan – Task 2: Projekti seadistus ja avalikud API-d

**Projekti nimi:** API kvaliteedikontroll   
**Autorid ja kuupäev:** Daria, 24.11.2025  
**Versioon:** 1.0

---

## 1. Sissejuhatus
**Eesmärk** – testida FastAPI backendit, mis ühendab JSONPlaceholderi ja Rick & Morty avalike API-de andmed üheks ennustatavaks skeemiks.  
**Testimise kontekst:** veenduda, et `/api/koond` tagastab korrektse JSONi ja töötleb korrektselt väliste API-de vigu (HTTP 502).

---

## 2. Ulatus
**Kaasatud komponendid:**
- Backend FastAPI (`backend/main.py`)
- Avalikud API-d: JSONPlaceholder ja Rick & Morty
- Endpoints: `/status` ja `/api/koond`
- Logimine ja error handling

---

## 3. Nõuded ja aktsepteerimiskriteeriumid
| Nõue | Testimeetod | Oodatav tulemus |
|-------|-------------|----------------|
| `/status` tagastab `200 OK` | GET /status | {"olek": "aktiivne", "allikas": "Kvaliteedijälg API"} |
| `/api/koond` koondab mõlema API andmed | GET /api/koond | JSON sisaldab `postitus`, `tegelane`, `allikad`, `paastikuAeg` |
| Logimine | vaata serveri logisid | INFO logid väliste API päringute ja koondamise kohta |
| Viga välises API-s | muuda URL katkise või eksisteerimata | HTTP 502 koos `detail`: sonum, allikad, pohjus |

---

## 4. Riskid ja maandus
| Risk | Mõju | Tõenäosus | Maandus |
|------|------|------------|---------|
| Välise API kättesaamatus | Kõik koondatud andmed puuduvad | Keskmine | Tagada error handling 502 |
| Vale JSON skeem | Testid läbivad ebaõigesti | Madal | Kontrollida kõiki väljastatud välju |

---

## 5. Meetodid ja tööriistad
- Ühikutestid: FastAPI endpoints
- Integratsioonitestid: `/api/koond` väliste API-dega
- Automaatika: Python `pytest`, HTTP päringud käsitsi `curl` või `http`

---

## 6. Testkeskkonnad ja andmed
- OS: Windows 11
- Python: 3.13
- Testandmed: avalikud API-d (`JSONPlaceholder`, `Rick & Morty`)
- Mock-serverid võivad kasutada vigade simuleerimiseks katkiseid URL-e

---

## 7. Ajajoon ja vastutajad
| Tegevus | Vastutaja | Aeg |
|----------|-----------|-----|
| Venv loomine ja sõltuvuste paigaldus | Daria | 5 min |
| Serveri käivitamine ja `/status` testimine | Daria | 2 min |
| `/api/koond` korrektse skeemi test | Daria | 2 min |
| Vigade käsitlemise test | Daria | 10 min |

---

## 8. Raporteerimine
- Testitulemused salvestatakse: `docs/results/task2.md` ja `backend/README.md`
- Edukriteerium: kõik kriitilised testid (`/api/koond` ja 502 error handling) läbivad

