---
category: general
date: 2026-03-29
description: Hogyan cseréljünk változókat JSON-ban a SmartMarker használatával – tanuljuk
  meg az if kifejezés használatát, alkalmazzuk a feltételes logikát, szorozzuk meg
  az értékeket, és generáljunk JSON-t könnyedén.
draft: false
keywords:
- how to substitute variables
- use if expression
- how to apply conditional
- how to multiply values
- how to generate json
language: hu
og_description: Hogyan helyettesítsünk változókat JSON-ban a SmartMarker segítségével.
  Fedezze fel, hogyan használja az if kifejezést, alkalmazzon feltételes logikát,
  szorozzon értékeket, és generáljon JSON-t percek alatt.
og_title: Hogyan helyettesítsük a változókat JSON-ban a SmartMarkerrel – Lépésről
  lépésre
tags:
- C#
- SmartMarker
- JSON templating
title: Hogyan cseréljünk változókat JSON-ban a SmartMarker segítségével – Teljes útmutató
url: /hu/net/smart-markers-dynamic-data/how-to-substitute-variables-in-json-with-smartmarker-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan helyettesítsünk változókat JSON-ban a SmartMarker segítségével – Teljes útmutató

Gondolkodtál már azon, **hogyan helyettesítsünk változókat** egy JSON payloadben anélkül, hogy saját parsert írnál? Nem vagy egyedül. Sok integrációs szituációban – gondolj csak a számlákra, árazási motorokra vagy dinamikus konfigurációs fájlokra – szükség van futásidőben értékek befecskendezésére, egyszerű feltételek alkalmazására, sőt akár egy gyors szorzásra is. Ez a tutorial pontosan megmutatja, **hogyan helyettesítsünk változókat** a SmartMarker könyvtár segítségével, miközben a JSON tiszta és olvasható marad.

Egy valós példán keresztül vezetünk végig, amely lefedi a **use if expression**, **how to apply conditional**, **how to multiply values**, és **how to generate json** témaköröket. A végére egy kész, futtatható C# kódrészletet kapsz, amelyet bármely .NET projektbe beilleszthetsz.

## Mit fogsz megtanulni

- `SmartMarkerOptions` beállítása újrahasználható változók tárolására.  
- JSON sablon írása, amely `if` kifejezést tartalmaz a feltételes logikához.  
- Érték szorzása egy változóval a sablonon belül.  
- A sablon feldolgozása a `SmartMarkerProcessor`‑rel és a végleges JSON string lekérése.  
- Gyakori hibák elhárítása, például hiányzó változók vagy hibás kifejezések.

Nincs szükség külső szolgáltatásokra, nehéz függőségekre – csak tiszta C# és a SmartMarker NuGet csomag.

---

## Hogyan helyettesítsünk változókat – Lépésről‑lépésre áttekintés

Az alábbi ábra a munkafolyamat magas szintű képét mutatja. Tekintsd úgy, mint egy csővezetéket, ahol a nyers JSON sablon balról érkezik, a SmartMarker motor varázsol, és a teljesen renderelt JSON jobb oldalon távozik.

![Diagram showing how to substitute variables in JSON](https://example.com/images/smartmarker-flow.png "How to substitute variables in JSON")

*Image alt text: Diagram showing how to substitute variables in JSON.*

---

## 1. lépés: SmartMarker telepítése és importálása

Mielőtt elkezdenéd, győződj meg róla, hogy a SmartMarker csomag hivatkozásként szerepel a projektedben. Ha a .NET CLI‑t használod, futtasd:

```bash
dotnet add package SmartMarker
```

Ezután add hozzá a szükséges `using` direktívákat a C# fájlod tetejéhez:

```csharp
using SmartMarker;
using SmartMarker.Models;
using System;
```

> **Pro tip:** A legújabb verzió (2026 márciusában) a 2.4.1. Támogatja a .NET 6‑ot és újabbakat, de a .NET Framework 4.7‑tel is tökéletesen működik.

---

## 2. lépés: SmartMarker beállítások létrehozása és változók definiálása

Most létrehozzuk a `SmartMarkerOptions` példányt, amely a sablonban újrahasználni kívánt változókat tárolja. Itt válik egyértelművé a **hogyan helyettesítsünk változókat** kérdés – a változók helyőrzőként szolgálnak, amelyeket a SmartMarker később kicserél.

```csharp
// Step 2: Create SmartMarker options to hold variables used in the template
var smartMarkerOptions = new SmartMarkerOptions();

// Define a variable (Rate) that we’ll reference later in the JSON expression
smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission rate
```

Miért tároljuk a rátát a `Variables`‑ban a keménykódolás helyett? Mert ez a szám származhat adatbázisból, konfigurációs fájlból vagy felhasználói bemenetből. Az opciókban tartva a sablon újrahasználható és tesztelhető marad.

---

## 3. lépés: JSON sablon írása `if` kifejezéssel

Itt jön a **use if expression** kulcsszó ereje. A SmartMarker lehetővé teszi, hogy feltételes logikát ágyazzunk közvetlenül a JSON stringbe. A szintaxis egy kicsit hasonlít egy tulajdonság nevére, de a SmartMarker ezt direktívaként kezeli.

```csharp
// Step 3: Prepare the JSON data with a conditional field that uses the variable
string jsonTemplate = @"{
    ""Amount"": 1000,
    ""if(Amount>500)"": ""${Amount * Rate}""
}";
```

Vedd észre a `if(Amount>500)` kulcsot. A SmartMarker kiértékeli az `Amount>500` kifejezést; ha igaz, a megfelelő érték (`${Amount * Rate}`) kerül beillesztésre a kimenetbe. A `${...}` szintaxis a *változóhelyettesítő* motor – itt **hogyan szorozzuk meg az értékeket** (`Amount * Rate`) még a beszúrás előtt.

---

## 4. lépés: A sablon feldolgozása és a végleges JSON lekérése

Miután a beállítások és a sablon készen áll, mindent átadunk a processzornak. A `ProcessJson` metódus beolvassa a sablont, alkalmazza a feltételt, elvégzi a szorzást, és egy tiszta JSON stringet ad vissza.

```csharp
// Step 4: Process the JSON with SmartMarker, applying the variable substitution
string resultJson = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(resultJson);
```

A snippet futtatása a következőt írja ki:

```json
{
  "Amount": 1000,
  "Result": "80"
}
```

**Mi történt?**  
- Az `Amount` értéke 1000, ami kielégíti az `Amount>500` feltételt.  
- A SmartMarker kiértékeli a `${Amount * Rate}` → `1000 * 0.08 = 80`.  
- Az eredeti feltételes kulcs (`if(Amount>500)`) egy tiszta tulajdonságnévre (`Result`) cserélődik. Alapértelmezés szerint a SmartMarker a `"Result"`‑ot használja, de ezt testre szabhatod (tovább olvasd lejjebb).

Ha az `Amount` értékét `400`‑ra változtatod, a kimenet:

```json
{
  "Amount": 400
}
```

A feltételes blokk eltűnik, mert a kifejezés `false`‑ra értékelődik. Ez a **hogyan alkalmazzunk feltételes** logikát jelentő JSON lényege.

---

## 5. lépés: A kimeneti tulajdonság nevének testreszabása (opcionális)

Néha nem szeretnénk a generikus `"Result"` kulcsot. A SmartMarker lehetővé teszi egy egyedi név megadását a `RenameIfExpression` opcióval:

```csharp
smartMarkerOptions.RenameIfExpression = "Discount";
string customResult = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(customResult);
```

Kimenet:

```json
{
  "Amount": 1000,
  "Discount": "80"
}
```

Most a feltételes érték egy jelentősebb tulajdonságnév alatt tárolódik – tökéletes a downstream szolgáltatások számára, amelyek egy konkrét mezőt várnak.

---

## Gyakori hibák és elkerülésük módja

| Probléma | Miért fordul elő | Megoldás |
|----------|------------------|----------|
| Variable not found | Olyan változóra hivatkozol, amely nincs a `smartMarkerOptions.Variables`‑ban. | Ellenőrizd a helyesírást és győződj meg róla, hogy a változó hozzá lett adva a feldolgozás előtt. |
| Invalid `if` syntax | Hiányzó zárójelek vagy rossz operátor (`>`, `<`, `==`). | Kövesd pontosan az `if(<kifejezés>)` mintát; a SmartMarker csak egyszerű numerikus összehasonlításokat támogat. |
| JSON becomes malformed | Véletlenül egy felesleges vessző marad a feltételes blokk után. | Hagyd, hogy a SmartMarker távolítsa el; tartsd a sablont szintaktikailag helyesnek. |
| Unexpected number format | Az eredmény stringként `"80"` jelenik meg szám helyett. | Castolj vagy parse-olj később, vagy használd a `${(Amount * Rate):N0}` formátumot a numerikus formázáshoz. |

---

## Teljes működő példa (másolás‑beillesztés kész)

Az alábbi program a teljes, lefordítható és futtatható kódot tartalmazza. Bemutatja, **hogyan generáljunk json** dinamikus változókkal, feltételekkel és aritmetikával – mindössze 30 sorban.

```csharp
using System;
using SmartMarker;
using SmartMarker.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Create SmartMarker options and define a reusable variable
        var smartMarkerOptions = new SmartMarkerOptions();
        smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission
        smartMarkerOptions.RenameIfExpression = "Discount"; // optional custom name

        // 2️⃣ JSON template with an if expression and multiplication
        string jsonTemplate = @"{
            ""Amount"": 1000,
            ""if(Amount>500)"": ""${Amount * Rate}""
        }";

        // 3️⃣ Process the template
        string output = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);

        // 4️⃣ Show the result
        Console.WriteLine("Generated JSON:");
        Console.WriteLine(output);
    }
}
```

**Várt konzolkimenet**

```
Generated JSON:
{
  "Amount": 1000,
  "Discount": "80"
}
```

Nyugodtan változtasd meg az `Amount` értékét a feltételes ág teszteléséhez, vagy állítsd át a `Rate`‑et, hogy más kedvezmény számításokat láss.

---

## A minta kibővítése – További “Hogyan” szcenáriók

- **Hogyan helyettesítsünk változókat** egy konfigurációs fájlból: Tölts be egy `Dictionary<string, object>`‑t az `appsettings.json`‑ból, és add át a `smartMarkerOptions.Variables`‑nek.  
- **Hogyan használjunk if expression** több feltételt: Láncold őket így: `"if(Amount>500 && CustomerType=='VIP')"` – a SmartMarker támogatja a logikai AND/OR operátorokat.  
- **Hogyan alkalmazzunk feltételes** formázást: Használd a `${Amount:0.00}`‑t a kifejezésben a tizedesjegyek szabályozásához.  
- **Hogyan szorozzuk meg az értékeket** összetettebb matematikával: `${(Amount - Discount) * TaxRate}` ugyanúgy működik.  
- **Hogyan generáljunk json** beágyazott objektumokhoz: Helyezd a feltételes blokkot egy másik JSON objektumba, a SmartMarker megőrzi a hierarchiát.

---

## Összegzés

Áttekintettük, **hogyan helyettesítsünk változókat** JSON-ban a SmartMarker segítségével, bemutattuk a **use if expression** használatát a feltételes beillesztéshez, elmagyaráztuk a **hogyan alkalmazzunk feltételes** logikát, megmutattuk a **hogyan szorozzuk meg az értékeket** a sablonban, és végül illusztráltuk, **hogyan generáljunk json** amely készen áll a downstream fogyasztásra. A megközelítés könnyű, nem igényel külső sablonmotorokat, és bármely C# kódbázisba könnyen beilleszthető.

Próbáld ki – módosítsd a változókat, adj hozzá több feltételt, vagy csomagold be egy segédosztályba a megoldás újrahasználhatósága érdekében. Amikor gyorsan kell dinamikus JSON‑t előállítani, a SmartMarker egy stabil, production‑kész opció.

---

**Következő lépések**

- Mélyedj el a SmartMarker haladó funkcióiban, mint a ciklusok (`foreach`) és egyedi függvények.  
- Kombináld ezt a technikát ASP.NET Core endpointokkal, hogy dinamikus JSON API‑kat szolgálj ki.  
- Ismerkedj meg más sablonkönyvtárakkal (pl. Handlebars.NET) a összehasonlítás kedvéért, különösen, ha gazdagabb szintaxist igényelsz.

Van kérdésed vagy egy konkrét use‑case, amivel küzdesz? Írj egy kommentet alább, és együtt megoldjuk. Jó kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}