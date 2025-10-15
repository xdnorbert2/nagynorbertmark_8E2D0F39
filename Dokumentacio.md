# Szőnyegtisztító Cég Weboldal - Dokumentáció

*Az ékezetek AI alapúak (Angol billentyűzettel rendelkezem)*

---

## Az oldalról

### Szőnyegtisztító cég

Az oldal egy cégnek a **bemutatását**, **szolgáltatásait** mutatja be amin különböző **segéd funkciók**, több oldalas és füles szövegek találhatóak. Ezen kívül **árkalkulátor**, belinkelt térkép, és egy **névnap** naptár is található rajta.

Az oldal nyomokban tartalmazni fog segítséget nem kizárt, hogy *AI* alapút is **(v0.dev, Google Gemini)**.

---

# Fontos tudni való ay oldal elkészitésével kapcsolatban



---

## Technológiák

A weboldal elkészítéséhez a következő technológiákat használtam:

- **HTML5** - Az oldal szerkezetének kialakítása, szemantikus elemek használata
- **CSS3** - Stílusok, animációk, reszponzív design (Tailwind CSS alapú)
- **JavaScript (ES6+)** - Interaktív funkciók, kalkulátorok, dinamikus tartalom

---

## Az oldal felépítése

### 1. Főoldal *(index.html)*
- **Navigációs menü** - Három oldal közötti váltás
- **Hero szekció** - Cég bemutatása, főcím
- **Szolgáltatások szekció** - Füles navigációval (tabs), különböző szolgáltatások bemutatása
- **Szolgáltatás szűrő** - Interaktív szűrés kategóriák szerint
- **Térkép** - Beágyazott Google Maps a cég elérhetőségével
- **Kapcsolat szekció** - Elérhetőségi információk

### 2. Árkalkulátor oldal *(arkalkulator.html)*
- **Interaktív kalkulátor** - Szőnyeg mérete és típusa alapján árszámítás
- **Név bekérés** - Megrendelő nevének megadása
- **Dinamikus eredmény megjelenítés** - Valós idejű árkalkuláció
- **Intelligens kedvezmény számítás** - 25 m² felett VAGY névnap esetén automatikus kedvezmény
- **Statisztika** - Legnagyobb eddigi rendelés megjelenítése

### 3. Névnap naptár oldal **(nevnap.html)*
- **Havi névnap lista** - Aktuális hónap névnapjai
- **Keresés funkció** - Név alapján keresés a teljes évben
- **Hónap váltó** - Előző/következő hónap böngészése

---

## JavaScript függvények

### 1. `szamitasAr(terulet, tipus, nev)` - Paraméteres függvény
**Funkció:** Kiszámítja a szőnyegtisztítás árát a terület, típus és megrendelő neve alapján.

**Paraméterek:**
- `terulet` (number) - A szőnyeg területe négyzetméterben
- `tipus` (string) - A szőnyeg típusa ('normal', 'premium', 'delux')
- `nev` (string) - A megrendelő neve

**Tartalmaz:**
- Aritmetikai műveletek (szorzás, százalék számítás)
- Elágazás (if-else) - típus alapján különböző árak
- Logikai műveletek (nagyobb mint, egyenlő, VAGY kapcsolat)
- Dátum kezelés (mai dátum lekérése)
- Tömb kezelés (névnap adatbázis)
- Ciklus (for loop) - névnap ellenőrzés
- **Kedvezmény logika:** 10% kedvezmény, ha `terulet > 25` **VAGY** `nev egyezik a mai névnappal`

**Programozási tétel:** Összegzés (ár + kedvezmény számítás) és Keresés (névnap ellenőrzés)

**Visszatérési érték:** Objektum az ár részleteivel és a kedvezmény okával

---

### 2. `keresNevnapot(nev)` - Paraméteres függvény
**Funkció:** Megkeresi egy adott név névnapját a teljes évben.

**Paraméterek:**
- `nev` (string) - A keresett név

**Tartalmaz:**
- Tömb (névnap adatok tárolása)
- Ciklus (for loop) - végigmegy az összes hónapon és napon
- Logikai műveletek (tartalmazza-e a név)
- Elágazás (if) - találat esetén visszaadja az eredményt

**Programozási tétel:** Keresés (lineáris keresés a névnap tömbben)

---

### 3. `valtFul(fulId)` - Paraméteres függvény
**Funkció:** Füles navigáció kezelése a szolgáltatások szekcióban.

**Paraméterek:**
- `fulId` (string) - A megjelenítendő fül azonosítója

**Tartalmaz:**
- Ciklus (forEach) - végigmegy az összes fülen
- Logikai műveletek (egyenlő, nem egyenlő)
- Elágazás (if-else) - aktív/inaktív állapot beállítása
- DOM manipuláció

---

### 4. `szuroSzolgaltatasok(kategoria)` - Paraméteres függvény
**Funkció:** Szolgáltatások szűrése kategória szerint.

**Paraméterek:**
- `kategoria` (string) - A szűrő kategória ('mind', 'otthoni', 'uzleti')

**Tartalmaz:**
- Tömb (szolgáltatások listája)
- Ciklus (forEach) - végigmegy az összes szolgáltatáson
- Logikai műveletek (tartalmazza-e a kategóriát)
- Elágazás (if-else) - megjelenítés/elrejtés
- Számlálás (hány elem látható)

**Programozási tétel:** Számlálás és Kiválasztás (kategóriának megfelelő elemek)

---

### 5. `frissitNevnapHonap(honap)` - Paraméteres függvény
**Funkció:** Megjeleníti a kiválasztott hónap névnapjait.

**Paraméterek:**
- `honap` (number) - A hónap száma (0-11)

**Tartalmaz:**
- Tömb (hónapok és névnapok)
- Ciklus (for loop) - végigmegy a hónap napjain
- Aritmetikai műveletek (nap számítás)
- DOM manipuláció

---

### 6. `keresMaxTerulet()` - Segédfüggvény
**Funkció:** Megkeresi a legnagyobb területű szőnyeget a korábbi rendelések közül.

**Tartalmaz:**
- Tömb (korábbi rendelések)
- Ciklus (for loop)
- Logikai műveletek (nagyobb mint)

**Programozási tétel:** Maximum kiválasztás

---

## Programozási tételek alkalmazása

1. **Összegzés** - Árkalkulátorban az ár és kedvezmény összegzése
2. **Számlálás** - Szolgáltatás szűrőben a megjelenített elemek számlálása
3. **Kiválasztás** - Kategória alapján megfelelő szolgáltatások kiválasztása
4. **Keresés** - Névnap keresés a teljes adatbázisban (2 helyen: árkalkulátor és névnap oldal)
5. **Maximum** - Legnagyobb területű rendelés megkeresése

---

## Speciális funkciók

### Intelligens kedvezmény rendszer
Az árkalkulátor egy összetett kedvezmény logikát használ:
- **Feltétel 1:** Ha a terület nagyobb mint 25 m²
- **Feltétel 2:** Ha a megrendelő neve egyezik a mai névnappal
- **Eredmény:** Ha **bármelyik** feltétel teljesül (VAGY kapcsolat), 10% kedvezményt kap
- **Megjelenítés:** A rendszer jelzi, hogy milyen okból kapott kedvezményt

### Névnap adatbázis
- Teljes éves névnap adatbázis (365 nap)
- Több név is lehet egy napon
- Keresés és ellenőrzés funkciók

---

## Dizájn és UX

- **Reszponzív design** - Mobilon, tableten és asztali gépen is jól használható
- **Modern megjelenés** - Tiszta, professzionális design
- **Könnyen használható** - Intuitív navigáció és interakciók
- **Színvilág** - Lila-kék gradiens (modern, megbízható)
- **Animációk** - Smooth átmenetek és hover effektek

---

## Fejlesztési lehetőségek

- Űrlap validáció és adatküldés backend felé
- Több nyelv támogatása
- Online időpontfoglalás
- Képgaléria korábbi munkákról
- Ügyfél vélemények szekció
- Adatbázis integráció a rendelések tárolására

---

*Készítette: [Nagy Norbert Márk]*  

