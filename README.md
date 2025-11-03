
Za projekat je izračunata metrika **broj linija koda (LOC)**, pri čemu nisu uključene prazne linije i komentari.

| Fajl | Ukupan broj linija | Prazne | Komentari | Efektivne linije koda (LOC) |
|------|--------------------|---------|-------------|------------------------------|
| Calculator.java | 147 | 18 | 7 | **122** |

**Ukupno efektivnih linija koda (LOC): 122**

---

## Neformalni pregled koda

Pregled koda je urađen bez pokretanja programa (code review).  
Tabela prikazuje zapažanja po fajlu i liniji koda.

| Fajl | Linija | Zapažanje |
|------|---------|------------|
| Calculator.java | 6 | Globalna promenljiva `finalResult` može izazvati probleme ako se kod koristi u više niti (nije thread-safe). |
| Calculator.java | 10–28 | Klasa `Operations` može biti implementirana kao `enum` radi čitljivosti i sigurnosti. |
| Calculator.java | 16 | Metoda `ToString()` ne poštuje Java konvenciju imenovanja (`toString`). |
| Calculator.java | 33 | Metoda `Run()` takođe ne poštuje konvenciju imenovanja (`run`). |
| Calculator.java | 40 | Potrebno proveriti da li je `expression` `null` ili prazan pre `expression.charAt(0)` kako bi se izbegla greška. |
| Calculator.java | 66 | Ručno parsiranje operatora može se zameniti jednostavnijim korišćenjem regex izraza. |
| Calculator.java | 83 | Hvatanje generičkog `Exception` nije preporučljivo – bolje koristiti `NumberFormatException`. |
| Calculator.java | 89 | Rekurzivni poziv `Calculate()` može dovesti do `StackOverflowError` kod veoma dugih izraza. |
| Calculator.java | 96–147 | Metoda `Calculate()` ima ponavljajući kod i visoku kognitivnu složenost – pogodna za refaktorisanje. |
| Calculator.java | 99 | Promenljiva `result` uvek se postavlja na 0; operator `+=` je suvišan. |
| Calculator.java | 140 | Ne postoji provera deljenja nulom (`/0`). |
| Calculator.java | 49 | Nedostaju Javadoc komentari za metode. |

---

## 🧮 Staticka analiza

Statička analiza je izvršena korišćenjem alata **SonarLint** (moguće koristiti i Checkstyle, PMD).

### Glavni nalazi:
- ⚠️ Nepoštovanje Java konvencija imenovanja (`Run`, `ToString`, `Calculate`).
- ⚠️ Visoka složenost metode `Calculate()` – previše ponavljanja i rekurzivni pozivi.
- ⚠️ Korišćenje globalnog stanja (`finalResult`).
- ⚠️ Potencijalni `NullPointerException` kod rada sa stringom `expression`.
- ⚠️ Hvatanje generičkog `Exception` umesto specifičnih tipova.
- ⚠️ Moguće deljenje nulom bez provere.

---

## ✅ Zaključak

Kod funkcioniše za osnovne aritmetičke operacije, ali bi bio čitljiviji i održiviji uz:
- poštovanje Java konvencija imenovanja metoda i klasa,
- zamenu rekurzije iterativnim pristupom u metodi `Calculate()`,
- uklanjanje globalne statičke promenljive `finalResult`,
- dodavanje provera i obrade grešaka (`null`, deljenje nulom),
- refaktorisanje ponavljajućih delova koda.

