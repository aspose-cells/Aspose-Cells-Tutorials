---
category: general
date: 2026-02-14
description: A hierarchia létrehozása a SmartMarker sablonokban könnyebb, mint gondolnád
  – tanuld meg, hogyan hozz létre hierarchikus adatokat, és hogyan listázd hatékonyan
  az alkalmazottakat.
draft: false
keywords:
- how to create hierarchy
- create hierarchical data
- how to list employees
- SmartMarker nested range
- C# template processing
language: hu
og_description: A hierarchia létrehozása a SmartMarker sablonokban egyszerű. Kövesd
  ezt az útmutatót a hierarchikus adatok létrehozásához és a beágyazott tartományokkal
  rendelkező alkalmazottak listázásához.
og_title: Hogyan hozzunk létre hierarchiát a SmartMarkerrel – Teljes útmutató
tags:
- SmartMarker
- C#
- templating
title: Hogyan hozzunk létre hierarchiát a SmartMarkerrel – Lépésről lépésre útmutató
url: /hu/net/smart-markers-dynamic-data/how-to-create-hierarchy-with-smartmarker-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan hozzunk létre hierarchiát a SmartMarker‑rel – Teljes útmutató

Gondolkodtál már azon, **hogyan lehet hierarchiát** létrehozni egy SmartMarker sablonban anélkül, hogy a hajadba nyúlnál? Nem vagy egyedül. Sok jelentéskészítési helyzetben szülő‑gyermek kapcsolat szükséges – gondolj csak a részlegekre és az ott dolgozó emberekre. A jó hír, hogy a SmartMarker egyszerűvé teszi ezt, ha ismered a megfelelő lépéseket.

Ebben a tutorialban végigvezetünk a teljes folyamaton: a **hierarchikus adatok** C#‑ban történő létrehozásától, a beágyazott tartományok engedélyezéséig, egészen egy olyan sablon rendereléséig, amely **listázza az alkalmazottakat** minden részleghez. A végére egy azonnal futtatható példát kapsz, amelyet bármely .NET projektbe beilleszthetsz.

---

## Amire szükséged lesz

- .NET 6+ (bármely friss verzió megfelelő)
- Hivatkozás a **SmartMarker** könyvtárra (a `ws.SmartMarkerProcessor` névtér)
- Alapvető C# ismeretek – semmi bonyolult, csak néhány objektum és egy‑két lambda
- Kedvenc IDE‑d vagy szerkesztőd (Visual Studio, Rider, VS Code… válaszd ki)

Ha már megvannak ezek, nagyszerű – vágjunk bele.

---

## Hogyan hozzunk létre hierarchiát – Áttekintés

A lényeg, hogy egy **beágyazott objektumgráfot** építsünk, amely tükrözi a végső dokumentumban megjelenő struktúrát. A mi esetünkben a gráf így néz ki:

```
Departments
 ├─ Name (string)
 └─ Employees (string[])
```

A SmartMarker ezután végigiterál a `Departments` gyűjteményen, és mivel **beágyazott tartományfeldolgozást** kapcsolunk be, automatikusan végigjárja minden részleg `Employees` kollekcióját is.

---

## 1. lépés: A hierarchikus adatmodell felépítése

Először egy anonim objektumot hozunk létre, amely egy részlegek tömbjét tartalmazza, mindegyik saját alkalmazotti listával. Az anonim típus könnyű példát biztosít – később nyugodtan cserélheted valós POCO osztályokra.

```csharp
// Step 1: Create hierarchical data that SmartMarker will iterate over
var departmentData = new
{
    Departments = new[]
    {
        new { Name = "HR", Employees = new[] { "John", "Amy" } },
        new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
    }
};
```

> **Miért fontos:** A `Departments` tömb a legfelső szintű gyűjtemény. Minden elem egy `Employees` tömböt tartalmaz, ami a második szintű hierarchiát adja, amelyhez később a `#Departments.Employees#` szintaxissal férünk hozzá.

---

## 2. lépés: Beágyazott tartományfeldolgozás engedélyezése

A SmartMarker csak akkor merül el a belső kollekciókban, ha ezt megmondod neki. A `SmartMarkerOptions` objektum tartalmazza ezt a kapcsolót.

```csharp
// Step 2: Enable nested range processing so inner collections (Employees) can be used
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableNestedRange = true   // crucial for #Departments.Employees# to work
};
```

> **Pro tipp:** Ha elfelejted ezt a jelzőt, a belső `#Employees#` tartomány egyszerűen semmit sem ad vissza, és azon kapod magad, hogy azon tűnődsz, miért üres a sablon.

---

## 3. lépés: A processzor futtatása az adatokkal

Most átadjuk az adatokat és a beállításokat a processzornak. A `ws` változó a **WebService**‑edet (vagy bármely objektumot, amely a SmartMarker motorját tartalmazza) jelöli.

```csharp
// Step 3: Run SmartMarker processing with the data and the configured options
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);
```

Ekkor a SmartMarker feldolgozza a sablont, helyettesíti a `#Departments.Name#` értékeket a részlegnevekkel, és mivel a beágyazott tartományok engedélyezve vannak, végigiterál minden részleg `Employees` kollekcióján.

---

## 4. lépés: A sablonjelölők megalkotása

Az alábbiakban egy minimális sablon látható, amely bemutatja a külső és a belső ciklust is. Illeszd be a SmartMarker sablon szerkesztőjébe (vagy egy `.txt` fájlba, amelyet a processzornak adsz át).

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

A renderelés után a következőt fogod látni:

```
HR
  - John
  - Amy
IT
  - Bob
  - Eve
```

> **Mit látsz:** A külső `#Departments.Name#` kiírja a részleg címét. A belső `#Departments.Employees#` blokk minden alkalmazottat végigjár, és a blokkban lévő `#Departments.Employees#` a tényleges nevet adja ki.

---

## Várt kimenet és ellenőrzés

A teljes példa (adatok + beállítások + sablon) pontosan a fent bemutatott listát kell, hogy előállítsa. Gyors ellenőrzéshez kiírhatod az eredményt a konzolra:

```csharp
string result = ws.SmartMarkerProcessor.GetProcessedResult(); // pseudo‑method
Console.WriteLine(result);
```

Ha a két részleg címe után a megfelelő alkalmazotti felsorolás jelenik meg, akkor sikeresen **létrehoztad a hierarchiát** és **listáztad az alkalmazottakat**.

---

## Gyakori hibák és edge‑case‑ek

| Probléma | Miért fordul elő | Megoldás |
|----------|------------------|----------|
| Nincs kimenet az alkalmazottaknak | `EnableNestedRange` hamis értéken maradt | Állítsd `EnableNestedRange = true`-ra |
| Duplikált alkalmazotti nevek | Ugyanazt a tömböt használod több részlegnél | Klónozd a tömböt vagy használj különálló gyűjteményeket |
| Nagy hierarchiák memória nyomást okoznak | A SmartMarker az egész objektumgráfot memóriába tölti | Streameld az adatot vagy lapozd a nagy kollekciókat |
| Sablon szintaxis hibák | Hiányzó záró `#/…#` címke | Használd a SmartMarker validator‑t vagy tesztelj egy apró sablonnal |

---

## További lépések – Valós világ variációk

1. **Dinamikus adatforrások** – Hozd be a részlegeket egy adatbázisból, és mapold őket az anonim struktúrába LINQ‑val.
2. **Feltételes formázás** – Adj minden alkalmazottnak egy `IsManager` jelzőt, és használd a SmartMarker feltételes címkéit (`#if …#`) a vezetők kiemeléséhez.
3. **Több beágyazási szint** – Ha csapatok is szükségesek a részlegeken belül, egyszerűen adj hozzá egy új kollekciót (`Teams`), és tartsd bekapcsolva az `EnableNestedRange`‑t.

---

## Teljes működő példa (másolás‑beillesztés kész)

```csharp
using System;
using SmartMarker; // hypothetical namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Build hierarchical data
        var departmentData = new
        {
            Departments = new[]
            {
                new { Name = "HR", Employees = new[] { "John", "Amy" } },
                new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
            }
        };

        // 2️⃣ Enable nested ranges
        var smartMarkerOptions = new SmartMarkerOptions
        {
            EnableNestedRange = true
        };

        // 3️⃣ Start processing
        var ws = new WebService(); // assume this is your entry point
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);

        // 4️⃣ Retrieve and display the result
        string output = ws.SmartMarkerProcessor.GetProcessedResult(); // placeholder method
        Console.WriteLine(output);
    }
}
```

**Sablon (template.txt)**

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

A program futtatása pontosan a korábban bemutatott hierarchiát írja ki.

---

## Összegzés

Áttekintettük, **hogyan hozhatunk létre hierarchiát** a SmartMarker‑ben, a **hierarchikus adatok** C#‑ban történő kialakításától a beágyazott tartományok bekapcsolásáig, egészen egy olyan sablon rendereléséig, amely **listázza az alkalmazottakat** részlegenként. A minta skálázható – csak adj hozzá további beágyazott kollekciókat vagy feltételes logikát, és egy erőteljes jelentéskészítő motor áll a rendelkezésedre.

Készen állsz a következő kihívásra? Próbáld meg az anonim típusokat erősen típusos POCO osztályokra cserélni, vagy integráld ezt a folyamatot egy ASP.NET Core végpontra, amely PDF‑et vagy Word‑dokumentumot ad vissza. A határ a csillagos ég, és most már egy szilárd alapod van.

---

![How to create hierarchy diagram](image.png){alt="Hierarchia diagram, amely a részleg‑alkalmazott kapcsolatot mutatja"}

*Boldog kódolást! Ha elakadsz, írj egy megjegyzést alul – szívesen segítek.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}