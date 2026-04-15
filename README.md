# BAC Informatică — Jurnal de pregătire

> Aplicație web de urmărire a progresului la examenul de Bacalaureat, profil Mate-Info

[![License: GPL v3](https://img.shields.io/badge/licen%C8%9B%C4%83-GPL%20v3-blue?style=flat-square)](https://www.gnu.org/licenses/gpl-3.0) ![Version](https://img.shields.io/badge/versiune-3.0-purple?style=flat-square) ![HTML](https://img.shields.io/badge/HTML-single--file-orange?style=flat-square) ![Offline](https://img.shields.io/badge/offline-ready-green?style=flat-square)

---

## Despre proiect

**BAC Informatică — Jurnal de pregătire** este o aplicație web single-file care centralizează toate variantele oficiale de subiecte de Bacalaureat la Informatică (profil Mate-Info) din 2018 până în 2026. Problema pe care o rezolvă este simplă: când exersezi zeci de variante, pierzi ușor firul — ce ai rezolvat, unde ai greșit, ce trebuie aprofundat. Aplicația îți oferă un spațiu structurat pentru fiecare variantă: vizualizezi subiectul PDF direct în browser, înregistrezi răspunsurile la grilă, scrii rezolvările pentru subiectele II și III, adaugi notițe și marchezi varianta ca terminată. Toate datele sunt salvate automat în `localStorage`, fără niciun server, fără cont — deschizi fișierul HTML și ești gata. Este destinată elevilor de liceu care se pregătesc pentru BAC la Informatică, dar și profesorilor care lucrează cu mai mulți elevi simultan (prin sistemul de profiluri multiple).

---

## Funcționalități

- 📅 **Arhivă completă de variante** — subiecte organizate pe ani (2018–2026), sesiuni (vară, toamnă, specială, simulare) și teste de antrenament, totalizând peste 80 de variante
- 📄 **Vizualizator PDF integrat** — subiectul se afișează direct în pagină printr-un `<embed>`, fără a deschide alt tab
- 🔗 **Link rapid la barem** — fiecare variantă are un buton de acces direct la baremul oficial (PDF de pe pbinfo.ro)
- ✅ **Grilă interactivă Subiectul I** — butoane MCQ (A/B/C/D) pentru cele 5 exerciții, cu toggle și salvare automată
- 📝 **Câmpuri de răspuns Subiectele II & III** — textarea-uri cu font monospațiat (`JetBrains Mono`) pentru cod C++, câte un câmp pe exercițiu
- 🚩 **Flaguri de revizuire** — două butoane independente per exercițiu: `?` (neclar) și `AI` (rezolvat cu ajutorul AI), pentru a filtra retrospectiv punctele slabe
- 💾 **Salvare automată în localStorage** — fiecare modificare (răspuns, notițe, flaguri, stare terminat) se persistă instant, fără buton de salvare
- 👤 **Sistem de profiluri multiple** — mai mulți elevi pot folosi același fișier HTML; profilurile se pot crea, redenumi, șterge, exporta ca `.json`, importa și combina (merge cu strategie primary/secondary)
- ✓ **Marcaj „Terminat"** — buton per variantă care marchează varianta ca finalizată; pilula din lista de ani reflectă imediat starea

---

## Tehnologii folosite

| Tehnologie | Versiune | Rol |
|---|---|---|
| HTML5 | — | Structura aplicației (single-file) |
| CSS3 (custom properties, transitions) | — | Design, teme, animații |
| JavaScript (Vanilla ES2020+) | — | Logică de aplicație, gestionare stare, localStorage |
| Google Fonts — Syne | 700, 800 | Font titluri |
| Google Fonts — JetBrains Mono | 400, 500 | Font cod și elemente monospațiate |
| Google Fonts — DM Sans | 400, 500 | Font principal UI |

---

## Instalare

Nu există build step, nu există dependențe de instalat. Aplicația rulează complet local.

1. **Clonează repository-ul:**
   ```bash
   git clone https://github.com/r0bert1337/bac_info.git
   cd bac_info
   ```

2. **Extrage arhiva cu subiecte** — dezarhivează `sources.zip` în același director cu `bac_informatica.html`. Folderul rezultat trebuie să se numească exact `sources`:
   ```
   bac_info/
   ├── bac_informatica.html
   ├── sources.zip
   └── sources/          ← folderul extras din sources.zip
       ├── 2018_vara.pdf
       └── ...
   ```
   > **Important:** Numele folderului trebuie să fie `sources`, nu `sources (1)` sau altceva — aplicația îl referențiază cu această cale exactă.

3. **Deschide aplicația** — deschide `bac_informatica.html` direct în browser (Chrome, Edge sau Firefox recomandat pentru suport `<embed>` PDF):
   ```
   # Windows
   start bac_informatica.html

   # macOS
   open bac_informatica.html

   # Linux
   xdg-open bac_informatica.html
   ```

4. **Sau server local** (recomandat dacă `<embed>` PDF nu funcționează din `file://`):
   ```bash
   # Python 3
   python -m http.server 8080
   # Apoi accesează http://localhost:8080/bac_informatica.html
   ```

> **Notă:** Nu există variabile de mediu, fișiere `.env` sau configurare adițională necesară.

---

## Utilizare

### Caz de utilizare principal — rezolvarea unei variante

1. Deschide `bac_informatica.html` în browser.
2. Creează un profil cu numele tău din widget-ul din stânga sus (prima utilizare).
3. Extinde un an (ex: **2024**) din lista de variante — click pe rândul anului.
4. Apasă pe o variantă (ex: `Sesiunea vara`) — panoul de lucru apare mai jos.
5. Citește subiectul PDF integrat, completează grilele, rezolvările și notițele.
6. Marchează varianta ca **Terminat ✓** — varianta din listă devine verde.

### Export / import progres între dispozitive

```
1. Click pe numele profilului tău (stânga sus) → ⬇ Export profil (.json)
   → Se descarcă un fișier bac_profil_NumeleTau.json

2. Pe alt dispozitiv: deschide același fișier HTML
   → Click profil → ⬆ Import profil (.json) → selectează fișierul exportat
```

### Lucru cu mai mulți elevi pe același fișier

```
1. Fiecare elev își creează propriul profil: click → ＋ Profil nou → introdu numele
2. Comutarea între profiluri se face instant din dropdown — datele nu interferează
3. Combinarea datelor din două profiluri: ⇔ Combină profiluri → selectează primary + secondary
```

---

## Structura proiectului

```
bac-informatica-jurnal/
│
├── bac_informatica.html        # Întreaga aplicație — HTML + CSS + JS într-un singur fișier
│
└── sources/                    # Fișiere PDF cu subiectele oficiale de BAC
    ├── 2018_vara.pdf           # Sesiunea vară 2018
    ├── 2018_toamna.pdf         # Sesiunea toamnă 2018
    ├── 2018_speciala.pdf       # Sesiunea specială 2018
    ├── 2019_*.pdf              # Variante 2019 (vară, toamnă, specială, simulare)
    ├── 2020_*.pdf              # Variante 2020 + 20 teste de antrenament MEC
    ├── 2021_*.pdf              # Variante 2021 + 12 teste de antrenament
    ├── 2022_*.pdf              # Variante 2022
    ├── 2023_*.pdf              # Variante 2023
    ├── 2024_*.pdf              # Variante 2024
    ├── 2025_*.pdf              # Variante 2025
    ├── 2026_modele.pdf         # Modele de subiecte 2026
    └── mec2020_test_*.pdf      # Teste de antrenament MEC 2020 (1–20)
```

---

## Contribuții

Contribuțiile sunt binevenite, mai ales adăugarea de variante noi sau corectarea link-urilor de barem.

1. **Fork** la repository și clonează-l local.
2. **Creează un branch** descriptiv:
   ```bash
   git checkout -b adauga-variante-2027
   ```
3. **Fă modificările** — adaugă PDF-urile în `sources/` și actualizează obiectele `DATA` și `BAREM` din `bac_informatica.html`.
4. **Deschide un Pull Request** cu o descriere clară a ce ai adăugat sau modificat.

---

## Licență

Distribuit sub licența [GNU GPL v3](https://www.gnu.org/licenses/gpl-3.0).
Orice versiune derivată trebuie publicată tot sub GPL v3 — codul poate fi distribuit, folosit dar nu poate fi closed-source sau integrat în software proprietar.

---

## Contact / Autor

Creat cu ❤️ de Robert — [\[r0bert1337\]](https://github.com/r0bert1337)
