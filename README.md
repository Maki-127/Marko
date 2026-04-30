# 🚀 Inženjerska Analiza Telemetrije: Misija Jezero Crater

## A. Izvršni sažetak (Executive Summary)
Ovaj projekt predstavlja profesionalno inženjersko rješenje za obradu, filtriranje i vizualizaciju podataka prikupljenih s istraživačkog rovera u krateru **Jezero** na Marsu. Sustav automatizira identifikaciju ključnih biomarkera (metan i vlaga) te generira precizne navigacijske naloge u JSON formatu. Dokumentacija služi kao primarni komunikacijski kanal prema nadzornom odboru misije i znanstvenoj zajednici.

---

## B. Metodologija obrade podataka (Data Wrangling)
U procesu pripreme podataka primijenjene su sljedeće algoritamske odluke:
*   **Čišćenje senzorskog šuma:** Implementirani su logički uvjeti za uklanjanje anomalija u pH vrijednostima i ekstremnim temperaturama.
*   **Relacijsko spajanje:** Koristeći biblioteku Pandas, izvršeno je spajanje tablica `mars_lokacije.csv` i `mars_uzorci.csv` radi korelacije kemijskih nalaza s preciznim GPS koordinatama.
*   **Automatizacija:** Umjesto ručne obrade, sustav koristi Python skripte unutar `src/` mape za osiguravanje ponovljivosti rezultata.

---

## C. Geoprostorna analiza i vizualizacija
Vizualni dokazi su ključni za razumijevanje terena i planiranje rute rovera.

### 1. Satelitsko "Extent" mapiranje
![Satelitska mapa](assets/satelit.jpg)
*Interpretacija: Primjena tehničkog koncepta mapiranja granica (extent) omogućuje precizno pozicioniranje kretanja rovera na satelitsku snimku delte Neretva Vallis.*

### 2. Filtrirani podaci i ciljne lokacije
![Filtrirani podaci](assets/zvijezde.png)
*Interpretacija: Prikaz očišćenih podataka (crvene zvjezdice) u odnosu na sirovi šum. Ovaj postupak izolira prioritetne točke za znanstveno istraživanje.*

### 3. Detekcija sustavnih anomalija
![Anomalije](assets/anomalije.png)
*Interpretacija: Jasna distinkcija između nominalnih mjerenja (plavo) i detektiranih pogrešaka senzora (crveno), što sprječava donošenje krivih odluka na temelju šuma.*

### 4. Toplinska karta dubine bušenja
![Dubina bušenja](assets/toplinska.png)
*Interpretacija: Prostorna distribucija dubine bušenja. Žute zone označavaju područja gdje su sedimentne naslage omogućile maksimalan prodor sonde.*

### 5. Korelacija biomarkera (Metan i Vlaga)
![Korelacija metana](assets/metan.png)
*Interpretacija: Ključni znanstveni nalaz koji pokazuje grupiranje pozitivnih nalaza metana (narančasto) pri povišenom postotku vlage (H2O) i stabilnim temperaturama.*

---

## D. Komunikacijski protokol (JSON Uplink)
Sustav generira mrežne pakete za komunikaciju s bazom. Korištenjem petlji postignuta je automatizacija generiranja naredbi, čime se eliminira rizik od ljudske pogreške.

```json
{
  "mission_control": "Jezero_Base",
  "uplink_data": [
    {
      "command": "NAV_TO",
      "target_coords": {"lat": 18.485, "long": 77.391},
      "action": "drilling",
      "priority": "high"
    }
  ]
}
```

---

## E. Inženjerski dnevnik (Troubleshooting Log)
Tijekom razvoja sustava riješene su sljedeće tehničke prepreke:
1.  **Merge Error (Data Mismatch):** Problem kod relacijskog spajanja tablica zbog različitih tipova podataka (string/float). Riješeno funkcijom `pd.to_numeric()`.
2.  **Greška separatora:** Inicijalno rušenje skripte zbog miješanja zareza i točka-zareza u CSV datotekama. Riješeno eksplicitnim definiranjem separatora u `read_csv` metodi.

---

### 📂 Arhitektura repozitorija
*   `data/` - Izvorni CSV telemetrijski podaci.
*   `src/` - Python izvorni kod za analitiku.
*   `assets/` - Grafički prikazi i satelitske snimke.
*   `README.md` - Središnja dokumentacija projekta.
