---
category: general
date: 2026-06-21
description: Készítsen Excel munkafüzet Python oktatóanyagot, amely bemutatja, hogyan
  használjuk a MAP függvényt és a lambda kifejezést a Celsius fok gyors Fahrenheit-re
  konvertálásához.
draft: false
keywords:
- create excel workbook python
- convert celsius to fahrenheit
- use map function
- how to use map
- how to use lambda
language: hu
og_description: Készíts Excel munkafüzetet Pythonban, és tanuld meg, hogyan használhatod
  a MAP függvényt lambda kifejezéssel a Celsius fok Fahrenheit fokra való átváltáshoz
  percek alatt.
og_title: Excel munkafüzet létrehozása Pythonban – Lépésről lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create Excel workbook Python tutorial showing how to use MAP function
    and lambda to convert Celsius to Fahrenheit quickly.
  headline: Create Excel Workbook Python – Full Guide
  type: TechArticle
- description: Create Excel workbook Python tutorial showing how to use MAP function
    and lambda to convert Celsius to Fahrenheit quickly.
  name: Create Excel Workbook Python – Full Guide
  steps:
  - name: '**How to use map** for multi‑column transformations, e.g., converting temperatures
      and rounding in one go.'
    text: '**How to use map** for multi‑column transformations, e.g., converting temperatures
      and rounding in one go.'
  - name: '**How to use lambda** to embed conditional logic: `LAMBDA(c, IF(c<0, "below
      freezing", c*9/5+32))`.'
    text: '**How to use lambda** to embed conditional logic: `LAMBDA(c, IF(c<0, "below
      freezing", c*9/5+32))`.'
  - name: 'Saving the workbook to disk: `wb.save("temperatures.xlsx")`.'
    text: 'Saving the workbook to disk: `wb.save("temperatures.xlsx")`.'
  - name: Adding styling (fonts, borders) via Aspose’s rich formatting API.
    text: Adding styling (fonts, borders) via Aspose’s rich formatting API.
  - name: Initialize a workbook.
    text: Initialize a workbook.
  - name: Write raw data.
    text: Write raw data.
  - name: Apply a MAP‑based formula.
    text: Apply a MAP‑based formula.
  - name: Force calculation.
    text: Force calculation.
  - name: Pull the results back into Python.
    text: Pull the results back into Python.
  type: HowTo
- questions:
  - answer: Just extend the range in the `put_value` call and adjust the list comprehension
      range accordingly. The MAP formula will automatically expand if you reference
      a larger range.
    question: What if I have more than four rows?
  - answer: Absolutely. Replace the lambda body with any arithmetic you need, e.g.,
      `LAMBDA(c, c*2)` for a simple doubling operation.
    question: Can I use MAP with other conversions?
  - answer: The library offers a free evaluation mode, but for production use you’ll
      want a proper license to avoid watermarks.
    question: Do I need a license for Aspose.Cells?
  - answer: No, MAP is part of the dynamic array functions introduced in Excel 365.
      If you target legacy Excel, you’d fall back to traditional copy‑down formulas.
    question: Is the MAP function available in older Excel versions?
  type: FAQPage
tags:
- python
- excel
- aspose-cells
- data conversion
title: Excel munkafüzet létrehozása Pythonban – Teljes útmutató
url: /hu/python/import-and-export/create-excel-workbook-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel munkafüzet létrehozása Python‑ban – Teljes útmutató

Gondolkodtál már azon, hogyan **create excel workbook python**‑stílusban hozhatsz létre Excel fájlt anélkül, hogy magát az Excelt megnyitnád? Lehet, hogy egy Celsius‑fokok listáját szeretnéd Fahrenheit‑re konvertálni „on the fly”, és nem akarsz kézzel másolni‑beilleszteni képleteket. Ebben a tutorialban pontosan ezt oldjuk meg: megmutatjuk, hogyan hozhatsz létre egy Excel fájlt, helyezhetsz el benne egy Celsius adatos oszlopot, majd **convert celsius to fahrenheit** egyetlen elegáns képlettel, amely a **MAP function**‑t és egy **lambda**‑t használ.

Miért fontos ez? A táblázatok automatizálása időt takarít meg, csökkenti az emberi hibákat, és egyszerűvé teszi az Excel integrálását nagyobb adatcsővezetékekbe. Ráadásul az Aspose.Cells for Python teljes Excel‑funkcionalitást biztosít a nehéz COM‑interoperáció nélkül. Készen állsz? Merüljünk el.

## Amire szükséged lesz

- Python 3.9+ (bármely friss verzió)
- `aspose-cells` csomag telepítve (`pip install aspose-cells`)
- Alapvető Python listák és függvények ismerete
- Nincs szükség előzetes Excel‑tapasztalatra; a munkafüzet létrehozását mi kezeljük

Ha ezek a pontok kipipálva vannak, már készen állsz. Ha nem, szánj egy pillanatot a könyvtár telepítésére – biztosan megéri.

![create excel workbook python example](excel_workbook.png)

*Image alt text: create excel workbook python example showing a filled spreadsheet*

## 1. lépés: Excel munkafüzet létrehozása Python‑ban

Az első dolog, amit meg kell tennünk, **create excel workbook python** az Aspose.Cells segítségével. Tekintsd a munkafüzetet egy friss jegyzetfüzetnek, ahol minden munkalap egy oldal, amelyre írni lehet.

```python
import aspose.cells as cells

# Initialize a new workbook – this is our blank Excel file
wb = cells.Workbook()

# Grab the first worksheet (index 0) to start populating data
ws = wb.worksheets[0]
```

*Why this matters*: Az `Workbook()` példányosítása egy memóriában létező `.xlsx` fájl reprezentációt ad. Még nincs lemez‑I/O, ami gyorsabbá teszi a folyamatot.

## 2. lépés: Az A oszlop feltöltése Celsius hőmérsékletekkel

Most, hogy van egy lapunk, helyezzünk néhány Celsius‑értéket az **A** oszlopba. A `put_value` metódust fogjuk használni, amely egy Python listát fogad, és közvetlenül a megadott cellatartományba írja.

```python
# Write a list of Celsius temperatures into cells A1:A4
ws.cells["A1:A4"].put_value([0, 20, 100, -10])
```

*Pro tip*: A `"A1:A4"` tartománykarakterlánc rugalmas – ha később bővíted a listát, csak állítsd be a tartományt, vagy használj dinamikus címet.

## 3. lépés: MAP alkalmazása LAMBDA‑val minden Celsius érték Fahrenheit‑re konvertálásához

Itt történik a varázslat. A **MAP function** (új az Excel 365‑ben) lehetővé teszi, hogy egy **lambda**‑t alkalmazzunk egy tömb minden elemére. Ebben az esetben a tömb `A1:A4`, a lambda pedig a klasszikus konverziót hajtja végre: `c * 9/5 + 32`.

```python
# Set the formula in B1 that maps each Celsius value to Fahrenheit
ws.cells["B1"].formula = "=MAP(A1:A4, LAMBDA(c, c*9/5 + 32))"
```

*How it works*:  
- `MAP(array, LAMBDA(parameter, expression))` végigiterál az `array`‑n.  
- `c` a helyettesítő minden egyes Celsius értékre.  
- A `c*9/5 + 32` kifejezés visszaadja a Fahrenheit megfelelőjét.

Ha új vagy a **how to use map** használatában Excelben, gondolj rá úgy, mint a Python beépített `map()` függvényére, de munkalap‑képletként. Ez megszünteti a képletek manuális lefelé húzásának szükségességét.

## 4. lépés: A képlet kiszámítása, hogy az eredmények megjelenjenek

Az Aspose.Cells nem értékeli ki automatikusan a képleteket, hacsak nem mondod meg neki. A `calculate_formula()` hívás arra kényszeríti a motorot, hogy kiszámolja a MAP eredményt, és az értékeket a **B** oszlopba tárolja.

```python
# Force calculation – this writes the computed Fahrenheit values into the cells
wb.calculate_formula()
```

*Edge case*: Ha később módosítod a Celsius oszlopot, újra futtatnod kell a `calculate_formula()`‑t, vagy állítsd a munkafüzet `calc_mode`‑ját automatikusra.

## 5. lépés: A Fahrenheit értékek lekérése és megjelenítése a B oszlopból

Végül, vonjuk ki a kiszámított számokat vissza Pythonba, és nyomtassuk ki őket. Ez bemutatja, hogyan lehet **how to use lambda** eredményeket programozottan felhasználni.

```python
# Extract the Fahrenheit values from B1:B4 into a Python list
fahrenheit = [ws.cells[f"B{i}"].value for i in range(1, 5)]
print(fahrenheit)
```

**Várható kimenet**

```
[32.0, 68.0, 212.0, 14.0]
```

Ha ezeket a számokat látod, gratulálok – sikeresen **create excel workbook python**‑stílusban hoztad létre, feltöltötted, és a **use map function**‑t egy **lambda**‑val kombinálva **convert celsius to fahrenheit**.

## Gyakori kérdések és buktatók

- **Mi van, ha négy sornál több van?**  
  Egyszerűen bővítsd a `put_value` hívásban megadott tartományt, és állítsd be a listakomprehenció tartományát ennek megfelelően. A MAP képlet automatikusan kiterjed, ha nagyobb tartományra hivatkozol.

- **Használhatom a MAP‑ot más konverziókhoz?**  
  Természetesen. Cseréld le a lambda törzsét bármilyen aritmetikai műveletre, pl. `LAMBDA(c, c*2)` egyszerű duplázáshoz.

- **Szükség van licencre az Aspose.Cells‑hez?**  
  A könyvtár ingyenes értékelési módot kínál, de éles környezetben megfelelő licencre lesz szükség a vízjelek elkerüléséhez.

- **Elérhető a MAP függvény régebbi Excel verziókban?**  
  Nem, a MAP a dinamikus tömbfüggvények része, amelyeket az Excel 365 vezetett be. Régebbi Excel esetén hagyományos másolás‑lefelé képletekre kell visszatérned.

## Példa kiterjesztése – Következő lépések

Most, hogy az alapfolyamat világos, kísérletezhetsz a következőkkel:

1. **How to use map** több oszlopos átalakításokhoz, pl. hőmérsékletek konvertálása és egyszerre kerekítése.  
2. **How to use lambda** feltételes logika beágyazásához: `LAMBDA(c, IF(c<0, "below freezing", c*9/5+32))`.  
3. A munkafüzet mentése lemezre: `wb.save("temperatures.xlsx")`.  
4. Stílusok hozzáadása (betűtípusok, szegélyek) az Aspose gazdag formázási API‑jával.  

Ezek mind ugyanarra az alapra épülnek, amelyet most felállítottunk, így a kód rövid marad, miközben erőteljes táblázat‑automatizálást tesz lehetővé.

## Összegzés

Végigvezettük a **create excel workbook python** teljes folyamatát a semmiből, feltöltöttük Celsius adatokkal, majd **convert celsius to fahrenheit** a **MAP function** és egy **lambda** kifejezés segítségével. A lépések:

1. Munkafüzet inicializálása.  
2. Nyers adatok írása.  
3. MAP‑alapú képlet alkalmazása.  
4. Számítás kényszerítése.  
5. Eredmények visszahozása Pythonba.

Ezzel a recepttel az Excel‑központú adatcsővezetékek automatizálása gyerekjáték. Nyugodtan módosítsd a lambda‑t, láncolj több MAP hívást, vagy ágyazd be a munkafüzetet egy webszolgáltatásba. A lehetőségek határtalanok.

Van más konverzió a fejedben? Írj egy megjegyzést, és fedezzük fel együtt. Boldog kódolást!

## Mit érdemes legközelebb megtanulni?

A következő tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra építenek. Minden forrás komplett, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy könnyedén elsajátíthasd az API további funkcióit, és alternatív megvalósítási megközelítéseket próbálhass ki saját projektjeidben.

- [Hogyan hozzunk létre és mentsünk Excel munkafüzetet SVG‑ként az Aspose.Cells for Java segítségével](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Hogyan hozzunk létre és exportáljunk Excel-t HTML‑be az Aspose.Cells Java használatával | Munkafüzet műveletek útmutatója](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Hogyan hozzunk létre és mentünk Excel munkafüzetet ODS‑ként az Aspose.Cells for .NET használatával](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}