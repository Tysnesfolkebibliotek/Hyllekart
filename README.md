# Hyllekart — Tysnes folkebibliotek

Kart over biblioteket som syner kvar dei ulike delane av samlinga står. Laga for
infoskjermane, etter same mønster som [infoskjerm](https://github.com/Tysnesfolkebibliotek/infoskjerm).

## Filene

| Fil | Kva ho gjer |
|---|---|
| `index.html` | Kartsida for skjermane. Lyser opp éin del av samlinga om gongen (Krim, Biletbøker, Engelsk …) og syner kvar på kartet han står. Opne <https://tysnesfolkebibliotek.github.io/Hyllekart/> |
| `kart.json` | Sjølve kartet: hyllene, møblane og innhaldet på kvar hylleside, og kvar skjermane står |

Rom, veggar, dører og vindauge er teikna etter planteikninga `302_A201` frå 2003
og ligg fast i `index.html`. Det som står i rommet, ligg i `kart.json`.

## På infoskjermane

Legg kartsida inn i `oppsett.json` i infoskjerm-repoet som ei vanleg side:

```json
{ "namn": "Hyllekart", "url": "https://tysnesfolkebibliotek.github.io/Hyllekart/#her=skjerm1&tema=fjord&sek=7", "sekund": 140 }
```

Innstillingane står i adressa etter `#`:

- **`her`**: `skjerm1` eller `skjerm2`. Teiknar «Du er her» og snur kartet slik at
  veggen du ser mot når du står framfor skjermen, er øvst. Utan `her` står nord øvst.
- **`tema`**: eit tema frå `infoskjerm/tema.js` (`kveld`, `fjord`, `skog`, `lys`, `haust`, `libry` …).
- **`skrift`**: ei skrift frå `infoskjerm/skrifter.js`. Utan: skrifta til temaet.
- **`sek`**: kor mange sekund kvar del står lyst opp. Standard 7.
- **`berre`**: berre nokre delar, skilde med `|`, til dømes `berre=Krim|Manga|Engelsk`.

Ein runde gjennom alle delane tek om lag `sek` × talet på delar (no 18). Set
`sekund` i oppsettet til det, eller kortare om det er greitt at runden ikkje blir ferdig.

Sida snakkar med `rotasjon.html` på same måte som karusellane: ho seier «klar»
når ho er lasta, startar frå byrjinga ved «vis» og tek pause ved «skjul».

## Endre kartet

Kartet blir redigert i hyllekart-redigeraren (Claude-artifact) og lagra hit
som `kart.json`. Alle mål er i cm frå det indre hjørnet nordvest i rom 134:
`x` aukar mot aust, `y` mot sør.

- Dobbelhyller (`"type": "dobbel"`) har innhaldet på kvar side i `sideA` og `sideB`.
  Kva side som er kva, kjem an på rotasjonen: utan rotasjon er `sideA` nordsida.
- Vegghyller, kubar og krybber (`"type": "hylle"`) har innhaldet i `sideA`.
- Like innhald blir lyst opp saman, til dømes «Krim» på hylle 9 og 10.
  «Skjønnlitteratur» og «Skjønnlitteratur vaksen» blir rekna som det same.
- `skjermar` seier kvar skjermane står (`x`, `y`) og kva veg du ser
  når du står framfor dei (`ser`: `nord`, `aust`, `sør` eller `vest`).

Teksten på kartet står slik du les han når du står i biblioteket og ser på hylla.
