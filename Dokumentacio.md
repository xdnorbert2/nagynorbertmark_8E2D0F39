# Szőnyegtisztító Cég Weboldal - Dokumentáció

*Az ékezetek AI alapúak (Angol billentyűzettel rendelkezem)*

---

## Az oldalról

### Szőnyegtisztító cég

Az oldal egy cégnek a **bemutatását**, **szolgáltatásait** mutatja be amin különböző **segéd funkciók**, több oldalas és füles szövegek találhatóak. Ezen kívül **árkalkulátor**, belinkelt térkép, és egy **névnap** naptár is található rajta.

Az oldal tartalmazni fog segítséget, *AI* alapút is **(v0.dev, Google Gemini)**.

---

# Fontos tudni való az oldal elkészitésével kapcsolatban

> Ez a weboldal egy prototípus, amelyet egy korábban közösen tervezett, valós szőnyegtisztító cég weboldalának mintájára készítettem anyummal együtt.
A korábbi oldal ötleteit, elrendezését és tartalmi elemeit vettem alapul amit akkor megalkottunk, majd azokat egyszerűsítve AI (v0.dev) segitségével újraalkottam.
Eredetileg az oldal egy funkiconáló weboldalnak indult és azóta be is fejeztük az eredetit, ez az oldal már csak az árnyéka.
Sajnos az oldal készitésekor kérdezett dolgokat nem tudom felidézni pontosan, de azt megtudom adni hogy mi tartalmaz AI-t, ezt kommenteken belül mutatni is fogom.
A cégnév, telefonszám, lokáció és egyéb más személyes információk átirásra kerültek. Dokumentációban a sablonos funkció, technológia és egyéb szöveget AI készitette, én kiegészitem a funkció körül irásával ha az szükséges. Ahol nem lát AI-ra input/outputot, az azért van mert azt régen csináltuk olyan funkció. Szerettem volna ezt az oldalt használni a projekt feladathoz, hogy lássam használható az oldal amit csináltunk.

---

## Technológiák

A weboldal elkészítéséhez a következő technológiákat használtam/használtuk régen:

- **HTML** - Az oldal szerkezetének kialakítása, szemantikus elemek használata
- **CSS** - Stílusok, animációk, reszponzív design (Tailwind CSS alapú)
- **JavaScript** - Interaktív funkciók, kalkulátorok, dinamikus tartalom

---

## Az oldal felépítése

### 1. Főoldal *(index.html)*
- **Navigációs menü** - Három oldal közötti váltást hozza létre
- **Hero szekció** - Cég bemutatása, főcím
- **Szolgáltatások szekció** - Füles navigációval (tabs), különböző szolgáltatások bemutatása
- **Szolgáltatás szűrő** - Interaktív szűrés kategóriák szerint
- **Térkép** - Beágyazott Google Maps(A cim nincs megadva) a cég elérhetőségével
- **Kapcsolat szekció** - Elérhetőségi információk (Fals információk)

### 2. Árkalkulátor oldal *(arkalkulator.html)*
- **Interaktív kalkulátor** - Szőnyeg mérete és típusa alapján árszámítás
- **Név bekérés** - Megrendelő nevének megadása
- **Dinamikus eredmény megjelenítés** - Valós idejű árkalkuláció
- **Intelligens kedvezmény számítás** - 25 m² felett vagy névnap esetén automatikus kedvezmény
- **Statisztika** - Legnagyobb eddigi rendelés megjelenítése

### 3. Névnap naptár oldal **(nevnap.html)*
- **Havi névnap lista** - Aktuális hónap névnapjai
- **Keresés funkció** - Név alapján keresés a teljes évben
- **Hónap váltó** - Előző/következő hónap változtatása

> Itt plusz funkciónak raktam be, hogy névnap esetén is adjon kedvezményt és ha esetleg mindkét feltétel teljesül, akkor összesitse azokat 15%ra. A kalkulació egy nagyon basic szorzással működő egyenlet segitségével számolja ki az eredményt. A névnap naptárhoz annó kértünk segitséget hogy végig legyenek irva azok emellett most kértem segitséget AI-tól hogy azt rakja bele, mint plusz funkciót a kedvezmény adáshoz.
- Input AI-hoz
    - Csak azt a reszt kene megvaltoztasd ahol a kalkulator kalkulal: Azt valtoztasd hogy kedvezmeny akkor legyen ha tobb mint 25m2 vagy a jelenlegi nevnap egyenlo a megrendelo nevevel (kerje be a felhasznalotol hogy nevnapja van e es ha igen akkor legyen kedvezmeny)
- Output AI
     
``` javascript
    let vanNevnapja = false;
        for (let i = 0; i < maiNevnapok.length; i++) {
            if (maiNevnapok[i].toLowerCase() === nevNormalizalt) {
                 vanNevnapja = true;
                break;
            }
        }
                       
        if (terulet > 25 || vanNevnapja) {
                
            kedvezmeny = alapar * 0.10;
                
                
            if (terulet > 25 && vanNevnapja) {
                kedvezmenyOka = '15% - Névnap + 25m² felett';
                 kedvezmeny = alapar * 0.15;
              } else if (terulet > 25) {
                 kedvezmenyOka = '10% - 25m² felett';
              } else if (vanNevnapja) {
                  kedvezmenyOka = '10% - Névnap';
           }
            }
```

---

## JavaScript függvények

### 1. `szamitasAr(terulet, tipus, nev)` 
**Funkció:** Kiszámítja a szőnyegtisztítás árát a szőnyeg *területe*, *típusa* és a *megrendelő neve* alapján.

**Paraméterek:**
- `terulet` - A szőnyeg területe négyzetméterben
- `tipus` - A szőnyeg típusa ('normal', 'premium', 'delux'). Különböző árak mindegyikhez.
- `nev` - A megrendelő nevét tárolja stringként, majd később felhasználja egy `paraméteresen függvénnyel` , hogy ellenőrizze, hogy az adott napon az a névnap.

- **Kedvezmény logika:** 10% kedvezmény, ha `terulet > 25` **vagy** `nev egyezik a mai névnappal` 15% ha mindkettő

**Programozási tétel - egyik requirement a feladatban:** Összegzés (ár + kedvezmény számítás) és Keresés (névnap ellenőrzés)

**Return érték:** Objektum az ár részleteivel és a kedvezmény okával, mennyiségével

---

### 2. `keresNevnapot(nev)` 
**Funkció:** Megkeresi egy adott név névnapját a teljes évben.

**Paraméterek:**
- `nev` - A keresett név

**Tartalmaz:**
- Tömb (névnap adatok tárolása)
- Ciklus (for loop) - végigmegy az összes hónapon és napon
- Logikai műveletek (tartalmazza-e a név)
- Elágazás (if) - találat esetén visszaadja az eredményt

> AI alapú keresés (lásd fentebb **Oldal felépitése 3. pontban**)
---

### 3. `valtFul(fulId)` 
**Funkció:** Navigáció kezelése 

**Paraméterek:**
- `fulId` - A megjelenítendő fül azonosítója

**Tartalmaz:**
- Ciklus `forEach` - végigmegy az összes fülen
- Logikai műveletek (egyenlő, nem egyenlő)
- Elágazás `if-else` - aktív/inaktív állapot beállítása

---

### 4. `szuroSzolgaltatasok(kategoria)` 
**Funkció:** Szolgáltatások szűrése kategória szerint.

**Paraméterek:**
- `kategoria` - A szűrő kategória ('mind', 'otthoni', 'uzleti')

> Lényege, hogy adott kategóriákban kihozza a különböző tipusú tisztitásokat és azok árait. A funkció eléréséhez volt AI használva.

---

### 5. `frissitNevnapHonap(honap)` 
**Funkció:** Megjeleníti a kiválasztott hónap névnapjait.

**Paraméterek:**
- `honap` - A hónap száma (0-11)

> Lényege, hogy amikor lépegetünk a hónapok között a `következő` és `Előző` gomb segitségével, akkor az megjelenitse azon hónapok napjait és névnapjait külön-külön. A névnap naptárhoz egyetlen dolog amiben az AI segitett, hogy végig irta az összes napot és bele illesztette a már meglévő `const`-ba.

---

### 6. `keresMaxTerulet()` 
**Funkció:** Megkeresi a legnagyobb területű szőnyeget a korábbi rendelések közül.

> Az árkalkulátor részlegen található egy eddigi legnagyobb rendelés rész, ahol az eddig legnagyobb rendelést jeleniti meg (alapból 45m2)

---

## Speciális funkciók

### Intelligens kedvezmény rendszer

- **Feltétel 1:** Ha a terület nagyobb mint 25 m²
- **Feltétel 2:** Ha a megrendelő neve egyezik az aznapi névnappal
- **Eredmény:** Ha **bármelyik** feltétel teljesül, 10% kedvezményt kap vagy ha mindkettő akkor 15%
- **Megjelenítés:** A rendszer jelzi, hogy milyen okból kapott kedvezményt és mennyit

### Névnap adatbázis
- Teljes éves névnap adatbázis (365 nap)
- Több név is lehet egy napon
- Keresés és ellenőrzés funkciók

---

### Design

> A design fullban AI alapú segitséggel van (sok div a html-ben), annyi hogy pár apró adjust volt a helyezkedés, szinekkel kapcsolatban. A szövegtől még itt megvolt kimélve az oldal és inkább a funkciókat próbáltuk, hogy mi az ami bele illene az oldalba. 

### Zárszó

Ha elolvasta idáig a tanárúr és esetleg érdekli, szivesen megmutatom az iskolában a weboldal jelenlegi helyzetét.


*Készítette: [Nagy Norbert Márk és anyja(**régen**)]*  

