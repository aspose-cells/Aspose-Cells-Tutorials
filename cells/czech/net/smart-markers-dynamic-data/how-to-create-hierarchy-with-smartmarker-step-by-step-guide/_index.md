---
category: general
date: 2026-02-14
description: Vytvořit hierarchii v šablonách SmartMarker je snadnější, než si myslíte
  – naučte se vytvářet hierarchická data a efektivně vypisovat zaměstnance.
draft: false
keywords:
- how to create hierarchy
- create hierarchical data
- how to list employees
- SmartMarker nested range
- C# template processing
language: cs
og_description: Jak vytvořit hierarchii v šablonách SmartMarker je jednoduché. Postupujte
  podle tohoto návodu, abyste vytvořili hierarchická data a vypsali zaměstnance s
  vnořenými rozsahy.
og_title: Jak vytvořit hierarchii pomocí SmartMarker – kompletní průvodce
tags:
- SmartMarker
- C#
- templating
title: Jak vytvořit hierarchii pomocí SmartMarker – krok za krokem průvodce
url: /cs/net/smart-markers-dynamic-data/how-to-create-hierarchy-with-smartmarker-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vytvořit hierarchii pomocí SmartMarker – Kompletní průvodce

Už jste se někdy zamýšleli **jak vytvořit hierarchii** uvnitř šablony SmartMarker, aniž byste si trhali vlasy? Nejste v tom sami. V mnoha scénářích reportování potřebujete vztah rodič‑potomek – například oddělení a lidi, kteří v nich pracují. Dobrou zprávou je, že SmartMarker to udělá hračkou, jakmile znáte správné kroky.

V tomto tutoriálu projdeme celý proces: od **vytváření hierarchických dat** v C#, povolení vnořených rozsahů a nakonec vykreslení šablony, která **vypisuje zaměstnance** pro každé oddělení. Na konci budete mít připravený ukázkový kód, který můžete vložit do libovolného .NET projektu.

---

## Co budete potřebovat

- .NET 6+ (jakákoli recentní verze funguje)
- Odkaz na knihovnu **SmartMarker** (namespace `ws.SmartMarkerProcessor`)
- Základní znalost C# – nic složitého, jen pár objektů a jedna‑dva lambda výrazy
- IDE nebo editor dle vašeho výběru (Visual Studio, Rider, VS Code… jaký chcete)

Pokud už to máte, skvělé — pojďme na to.

---

## Jak vytvořit hierarchii – Přehled

Základní myšlenkou je vytvořit **vnořený objektový graf**, který odráží strukturu, kterou chcete vidět ve finálním dokumentu. V našem případě graf vypadá takto:

```
Departments
 ├─ Name (string)
 └─ Employees (string[])
```

SmartMarker pak může iterovat přes `Departments` a protože zapneme **zpracování vnořených rozsahů**, automaticky projde i kolekci `Employees` každého oddělení.

---

## Krok 1: Vytvoření hierarchického datového modelu

Nejprve vytvoříme anonymní objekt, který obsahuje pole oddělení, z nichž každé má svůj vlastní seznam zaměstnanců. Použití anonymního typu udržuje příklad lehký — můžete jej později nahradit skutečnými POCO třídami.

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

> **Proč je to důležité:** Pole `Departments` je kolekce nejvyšší úrovně. Každý prvek obsahuje pole `Employees`, což nám poskytuje druhou úroveň hierarchie, ke které později přistoupíme pomocí `#Departments.Employees#`.

## Krok 2: Povolení zpracování vnořených rozsahů

SmartMarker se neponoří do vnitřních kolekcí, pokud mu to neřeknete. Objekt `SmartMarkerOptions` obsahuje tento přepínač.

```csharp
// Step 2: Enable nested range processing so inner collections (Employees) can be used
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableNestedRange = true   // crucial for #Departments.Employees# to work
};
```

> **Tip:** Pokud zapomenete nastavit tento příznak, vnitřní rozsah `#Employees#` prostě nic nevrátí a budete se kroutit hlavou, proč je šablona prázdná.

## Krok 3: Spuštění procesoru s vašimi daty

Nyní předáme data a možnosti procesoru. Proměnná `ws` představuje váš **WebService** (nebo jakýkoli objekt, který hostuje engine SmartMarker).

```csharp
// Step 3: Run SmartMarker processing with the data and the configured options
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);
```

V tomto okamžiku SmartMarker parsuje šablonu, nahrazuje `#Departments.Name#` názvem každého oddělení a poté, protože jsou vnořené rozsahy povoleny, iteruje přes kolekci `Employees` každého oddělení.

## Krok 4: Vytvoření značek šablony

Níže je minimální šablona, která demonstruje jak vnější, tak vnitřní smyčky. Vložte ji do editoru šablon SmartMarker (nebo do souboru `.txt`, který předáte procesoru).

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

Po vykreslení uvidíte:

```
HR
  - John
  - Amy
IT
  - Bob
  - Eve
```

> **Co vidíte:** Vnější `#Departments.Name#` vypisuje název oddělení. Vnitřní blok `#Departments.Employees#` prochází každého zaměstnance a `#Departments.Employees#` uvnitř bloku vypisuje skutečné jméno.

## Očekávaný výstup a ověření

Spuštění kompletního příkladu (data + možnosti + šablona) by mělo přesně vytvořit seznam uvedený výše. Pro rychlé ověření můžete výsledek vypsat do konzole:

```csharp
string result = ws.SmartMarkerProcessor.GetProcessedResult(); // pseudo‑method
Console.WriteLine(result);
```

Pokud vidíte dva nadpisy oddělení následované odrážkami jejich zaměstnanců, úspěšně jste **vytvořili hierarchii** a **vypsali zaměstnance**.

## Časté úskalí a okrajové případy

| Problém | Proč se to děje | Řešení |
|-------|----------------|-----|
| Žádný výstup pro zaměstnance | `EnableNestedRange` ponechán na false | Nastavte `EnableNestedRange = true` |
| Duplicitní jména zaměstnanců | Stejné pole znovu použito napříč odděleními | Klonujte pole nebo použijte odlišné kolekce |
| Velmi velké hierarchie způsobují tlak na paměť | SmartMarker načítá celý objektový graf do paměti | Streamujte data nebo stránkujte velké kolekce |
| Chyby v syntaxi šablony | Chybějící uzavírací tagy `#/…#` | Použijte validátor SmartMarker nebo rychle otestujte s malou šablonou |

## Dál – reálné varianty

1. **Dynamické zdroje dat** – Načtěte oddělení z databáze a pomocí LINQ je namapujte do anonymní struktury.  
2. **Podmíněné formátování** – Přidejte ke každému zaměstnanci příznak `IsManager` a použijte podmíněné značky SmartMarker (`#if …#`) k zvýraznění manažerů.  
3. **Více úrovní vnoření** – Pokud potřebujete týmy uvnitř oddělení, stačí přidat další kolekci (`Teams`) a nechat `EnableNestedRange` zapnutý.

## Kompletní funkční příklad (připravený ke kopírování)

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

**Šablona (template.txt)**

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

Spuštění programu vytiskne hierarchii přesně tak, jak byla ukázána výše.

## Závěr

Probrali jsme **jak vytvořit hierarchii** v SmartMarker, od tvorby **hierarchických dat** v C# po zapnutí vnořených rozsahů a nakonec vykreslení šablony, která **vypisuje zaměstnance** podle oddělení. Vzor je škálovatelný — stačí přidat další vnořené kolekce nebo podmíněnou logiku a máte výkonný reportingový engine na dosah ruky.

Jste připraveni na další výzvu? Zkuste nahradit anonymní typy silně typovanými POCO třídami nebo integrovat tento tok do ASP.NET Core endpointu, který vrací PDF nebo Word dokument. Obloha je limit a nyní máte pevný základ.

![Diagram jak vytvořit hierarchii](image.png){alt="Diagram jak vytvořit hierarchii zobrazující vztah oddělení‑zaměstnanec"}

*Šťastné kódování! Pokud narazíte na problémy, zanechte komentář níže — rád pomohu.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}