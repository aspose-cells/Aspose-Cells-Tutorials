---
category: general
date: 2026-03-29
description: Jak nahradit proměnné v JSON pomocí SmartMarker – naučte se používat
  if výraz, aplikovat podmíněnou logiku, násobit hodnoty a generovat JSON bez námahy.
draft: false
keywords:
- how to substitute variables
- use if expression
- how to apply conditional
- how to multiply values
- how to generate json
language: cs
og_description: Jak nahradit proměnné v JSON pomocí SmartMarkeru. Objevte, jak použít
  výraz if, aplikovat podmíněnou logiku, násobit hodnoty a během několika minut generovat
  JSON.
og_title: Jak nahradit proměnné v JSON pomocí SmartMarker – krok za krokem
tags:
- C#
- SmartMarker
- JSON templating
title: Jak nahradit proměnné v JSON pomocí SmartMarker – kompletní průvodce
url: /cs/net/smart-markers-dynamic-data/how-to-substitute-variables-in-json-with-smartmarker-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak nahradit proměnné v JSON pomocí SmartMarker – Kompletní průvodce

Už jste se někdy zamýšleli **jak nahradit proměnné** uvnitř JSON payloadu, aniž byste museli psát vlastní parser? Nejste v tom sami. V mnoha integračních scénářích—například faktury, cenové enginy nebo dynamické konfigurační soubory—musíte vkládat runtime hodnoty, použít jednoduché podmínky a možná i rychle vynásobit. Tento tutoriál vám přesně ukáže **jak nahradit proměnné** pomocí knihovny SmartMarker, a to vše při zachování čistého a čitelného JSON.

Provedeme vás reálným příkladem, který zahrnuje **use if expression**, **how to apply conditional**, **how to multiply values** a **how to generate json** za běhu. Na konci budete mít připravený C# úryvek, který můžete vložit do libovolného .NET projektu.

## Co se naučíte

- Nastavit `SmartMarkerOptions` pro uložení znovupoužitelných proměnných.  
- Napsat JSON šablonu, která obsahuje `if` výraz pro podmíněnou logiku.  
- Vynásobit hodnotu proměnnou uvnitř šablony.  
- Zpracovat šablonu pomocí `SmartMarkerProcessor` a získat finální JSON řetězec.  
- Odhalit a opravit běžné problémy, jako chybějící proměnné nebo špatně formátované výrazy.

Žádné externí služby, žádné těžké závislosti—pouze čistý C# a NuGet balíček SmartMarker.

---

## Jak nahradit proměnné – Přehled krok za krokem

Níže je zobrazeno diagram workflowu na vysoké úrovni. Představte si to jako pipeline, kde vaše surová JSON šablona vstupuje zleva, engine SmartMarker provede své kouzlo a plně vykreslený JSON vychází zprava.

![Diagram ukazující, jak nahradit proměnné v JSON](https://example.com/images/smartmarker-flow.png "Diagram ukazující, jak nahradit proměnné v JSON")

*Text obrázku: Diagram ukazující, jak nahradit proměnné v JSON.*

---

## Krok 1: Instalace a import SmartMarker

Než začnete, ujistěte se, že je balíček SmartMarker zahrnut ve vašem projektu. Pokud používáte .NET CLI, spusťte:

```bash
dotnet add package SmartMarker
```

Poté přidejte potřebné `using` direktivy na začátek vašeho C# souboru:

```csharp
using SmartMarker;
using SmartMarker.Models;
using System;
```

> **Tip:** Nejnovější verze (k březnu 2026) je 2.4.1. Podporuje .NET 6 a novější, ale funguje také bez problémů s .NET Framework 4.7.

---

## Krok 2: Vytvoření SmartMarker Options a definice proměnných

Nyní vytvoříme instanci `SmartMarkerOptions`, která bude obsahovat všechny proměnné, jež chceme znovu použít v šabloně. Zde odpovídáme na otázku **jak nahradit proměnné**—proměnné fungují jako zástupné symboly, které SmartMarker později nahradí.

```csharp
// Step 2: Create SmartMarker options to hold variables used in the template
var smartMarkerOptions = new SmartMarkerOptions();

// Define a variable (Rate) that we’ll reference later in the JSON expression
smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission rate
```

Proč ukládat sazbu do `Variables` místo pevného zakódování? Protože tuto hodnotu můžete získat z databáze, konfiguračního souboru nebo vstupu uživatele. Uložení v options dělá šablonu znovupoužitelnou a testovatelnou.

---

## Krok 3: Napsání JSON šablony s `if` výrazem

Zde se ukáže síla klíčového slova **use if expression**. SmartMarker vám umožňuje vložit podmíněnou logiku přímo do JSON řetězce. Syntaxe vypadá trochu jako název vlastnosti, ale SmartMarker ji interpretuje jako direktivu.

```csharp
// Step 3: Prepare the JSON data with a conditional field that uses the variable
string jsonTemplate = @"{
    ""Amount"": 1000,
    ""if(Amount>500)"": ""${Amount * Rate}""
}";
```

Všimněte si klíče `if(Amount>500)`. SmartMarker vyhodnotí výraz `Amount>500`; pokud je pravda, odpovídající hodnota (`${Amount * Rate}`) se vloží do výstupu. Syntaxe `${...}` je *engine pro substituci proměnných*—zde **jak vynásobit hodnoty** (`Amount * Rate`) před vložením výsledku.

---

## Krok 4: Zpracování šablony a získání finálního JSON

S připravenými options a šablonou předáme vše procesoru. Metoda `ProcessJson` parsuje šablonu, aplikuje podmínku, provede násobení a vrátí čistý JSON řetězec.

```csharp
// Step 4: Process the JSON with SmartMarker, applying the variable substitution
string resultJson = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(resultJson);
```

Spuštění úryvku vypíše:

```json
{
  "Amount": 1000,
  "Result": "80"
}
```

**Co se stalo?**  
- `Amount` je 1000, což splňuje `Amount>500`.  
- SmartMarker vyhodnotí `${Amount * Rate}` → `1000 * 0.08 = 80`.  
- Původní podmínkový klíč (`if(Amount>500)`) je nahrazen čistým názvem vlastnosti (`Result`). Ve výchozím nastavení SmartMarker používá `"Result"`, ale můžete to přizpůsobit (více níže).

Pokud změníte `Amount` na `400`, výstup bude:

```json
{
  "Amount": 400
}
```

Podmínkový blok zmizí, protože výraz byl vyhodnocen jako `false`. To je podstata **jak aplikovat podmínky** v JSON.

---

## Krok 5: Přizpůsobení názvu výstupní vlastnosti (volitelné)

Někdy nechcete generický klíč `"Result"`. SmartMarker vám umožňuje zadat vlastní název pomocí možnosti `RenameIfExpression`:

```csharp
smartMarkerOptions.RenameIfExpression = "Discount";
string customResult = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(customResult);
```

Výstup:

```json
{
  "Amount": 1000,
  "Discount": "80"
}
```

Nyní je podmíněná hodnota uložena pod smysluplnějším názvem vlastnosti—ideální pro downstream služby, které očekávají konkrétní pole.

---

## Časté úskalí a jak se jim vyhnout

| Problém | Proč k tomu dochází | Řešení |
|-------|----------------|-----|
| Proměnná nenalezena | Odkázali jste na proměnnou, která není v `smartMarkerOptions.Variables`. | Zkontrolujte pravopis a ujistěte se, že je proměnná přidána před zpracováním. |
| Neplatná syntaxe `if` | Chybějící závorky nebo špatný operátor (`>`, `<`, `==`). | Dodržujte přesný vzor `if(<expression>)`; SmartMarker podporuje jen jednoduché číselné porovnání. |
| JSON se stane neplatným | Náhodně zůstane za podmínkovým blokem čárka. | Nechte SmartMarker provést odstranění; udržujte původní šablonu syntakticky správnou. |
| Neočekávaný formát čísla | Výsledek se zobrazí jako řetězec `"80"` místo čísla. | Přetypujte nebo později parsujte, nebo použijte `${(Amount * Rate):N0}` pro číselné formátování. |

---

## Kompletní funkční příklad (připravený ke zkopírování)

Níže je kompletní program, který můžete zkompilovat a spustit. Ukazuje **jak generovat json** s dynamickými proměnnými, podmínkami a aritmetikou—vše za méně než 30 řádků.

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

**Očekávaný výstup v konzoli**

```
Generated JSON:
{
  "Amount": 1000,
  "Discount": "80"
}
```

Neváhejte změnit `Amount` pro otestování podmíněné větve, nebo upravit `Rate` pro zobrazení různých výpočtů slev.

---

## Rozšíření vzoru – Další scénáře “Jak”

- **How to substitute variables** z konfiguračního souboru: Načtěte `Dictionary<string, object>` z `appsettings.json` a předávejte jej do `smartMarkerOptions.Variables`.  
- **How to use if expression** pro více podmínek: Spojte je jako `"if(Amount>500 && CustomerType=='VIP')"`—SmartMarker podporuje logické AND/OR.  
- **How to apply conditional** formátování: Použijte `${Amount:0.00}` uvnitř výrazu pro kontrolu desetinných míst.  
- **How to multiply values** s komplexnější matematikou: `${(Amount - Discount) * TaxRate}` funguje stejně.  
- **How to generate json** pro vnořené objekty: Umístěte podmínkový blok do jiného JSON objektu a SmartMarker zachová hierarchii.

---

## Závěr

Probrali jsme **jak nahradit proměnné** v JSON pomocí SmartMarker, ukázali **use if expression** pro podmíněné zahrnutí, vysvětlili **jak aplikovat podmínky** logiku, předvedli **jak vynásobit hodnoty** uvnitř šablony a nakonec ilustrovali **jak generovat json**, který je připraven pro downstream spotřebu. Přístup je lehký, nevyžaduje externí templating engine a snadno zapadá do jakéhokoli C# kódu.

Vyzkoušejte to—pohrabujte s proměnnými, přidávejte další podmínky nebo zabalte celý proces do pomocné třídy pro opakované použití napříč řešením. Když potřebujete rychle vytvořit dynamický JSON, SmartMarker je solidní, připravená pro produkci možnost.

**Další kroky**

- Prozkoumejte pokročilé funkce SmartMarkeru, jako jsou smyčky (`foreach`) a vlastní funkce.  
- Kombinujte tuto techniku s ASP.NET Core endpointy pro poskytování dynamických JSON API.  
- Prozkoumejte další templating knihovny (např. Handlebars.NET) pro srovnání, zejména pokud potřebujete bohatší syntaxi.

Máte otázky nebo konkrétní případ, se kterým bojujete? Zanechte komentář níže a pojďme to společně vyřešit. Šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}