# Analiza comenzilor GustoExpress

Proiect Python (pandas, numpy, matplotlib, seaborn) pentru analiza comenzilor de livrare mancare plasate in 2025 prin GustoExpress.

## Structura proiectului

| Fisier                              | Descriere                                                      |
| ----------------------------------- | -------------------------------------------------------------- |
| `proiect_gustoexpress.ipynb`        | Notebook-ul cu intreaga analiza                                |
| `gustoexpress_date/comenzi.csv`     | Date brute: comenzile (~1975 inregistrari)                     |
| `gustoexpress_date/restaurante.csv` | Date despre restaurante: nume, tip bucatarie, rating           |
| `comenzi_curat.csv`                 | Date curatate, exportate din notebook (`utf-8-sig`)            |
| `rezumat_orase.xlsx`                | Tabel cu rezumatul pe orase (generat la rularea notebook-ului) |

## Continutul notebook-ului

### Partea 1 - Pregatirea datelor

- Incarcarea si inspectarea datelor (`head`, `shape`, `info`, `describe`).
- Eliminarea duplicatelor.
- Standardizarea coloanelor `oras` (5 orase, cu diacritice) si `metoda_plata` (`Card` / `Cash`).
- Tratarea valorilor lipsa: `timp_livrare_min` completat cu mediana orasului, `rating_client` completat cu media.
- Eliminarea comenzilor cu `valoare_produse` <= 0.
- Coloane noi: `luna`, `zi_saptamana`, `ora`, `valoare_totala`.
- Unirea cu `restaurante.csv` pe `id_restaurant` (left join).

### Partea 2 - Functii Python

- `categorie_comanda(valoare)`: Mica / Medie / Mare.
- `rezumat_oras(date, oras)`: numar comenzi, valoare medie si timp mediu de livrare pe oras.

### Partea 3 - Intrebari de analiza

1. Tipuri de bucatarie comandate: Pizza si Burgeri sunt cele mai populare.
2. Vanzari pe orase: Bucuresti are cele mai mari incasari, datorita numarului de comenzi, nu valorii medii (~68 lei).
3. Evolutia pe luni: varfuri in Februarie, Noiembrie si Decembrie; cea mai slaba luna este August.
4. Orele si zilele de varf: 19:00-20:00, iar Vineri, Sambata si Duminica sunt cele mai aglomerate zile.
5. Timp de livrare vs. rating: livrarile lente primesc ratinguri mai mici (corelatie ~ -0.30); Bucuresti are cel mai mare timp mediu de livrare (~36.9 min).

### Partea 4 - Concluzii si export

- Concluzii finale si recomandari (mai multi curieri in orele de varf, campanii de marketing vara).
- Export `comenzi_curat.csv` si `rezumat_orase.xlsx`.

### Bonus

- Top 10 produse comandate (`ast.literal_eval` + `explode`): Cola, Cartofi prajiti, Tiramisu.
- Heatmap zile x ore (`pivot_table` + `sns.heatmap`).
- Dashboard 2x2 cu patru grafice din proiect.

## Rulare

1. Instaleaza dependintele: `pip install pandas numpy matplotlib seaborn openpyxl`.
2. Deschide `proiect_gustoexpress.ipynb` si ruleaza celulele in ordine, din folderul proiectului (caile catre date sunt relative).
