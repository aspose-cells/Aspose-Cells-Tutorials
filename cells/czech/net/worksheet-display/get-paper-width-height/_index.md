---
title: Získejte šířku a výšku papíru pro tisk listu
linktitle: Získejte šířku a výšku papíru pro tisk listu
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak získat šířku a výšku papíru pro tisk listu v Aspose.Cells pro .NET pomocí tohoto podrobného průvodce.
weight: 16
url: /cs/net/worksheet-display/get-paper-width-height/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Získejte šířku a výšku papíru pro tisk listu

## Zavedení
Přesný tisk dokumentů vyžaduje znalost rozměrů papíru. Pokud jste vývojář nebo pracujete na aplikaci, která pracuje se soubory Excel, možná budete potřebovat vědět, jak získat šířku a výšku papíru při tisku listů. Naštěstí Aspose.Cells for .NET poskytuje robustní způsob, jak programově spravovat dokumenty Excelu. V tomto článku vás provedeme procesem určování specifik velikosti papíru na jednoduchých příkladech, které ilustrují základní pojmy. 
## Předpoklady
Než se ponoříme do technických detailů, pojďme si ujasnit základy. Abyste mohli úspěšně pokračovat v tomto tutoriálu, budete potřebovat:
### 1. Základní znalost C#
Měli byste dobře ovládat programování v C#, protože budeme pracovat v prostředí .NET.
### 2. Aspose.Cells Library
Ujistěte se, že máte v projektu nainstalovanou knihovnu Aspose.Cells. Pokud jste to ještě neudělali, můžete si stáhnout nejnovější verzi z[Stránka ke stažení Aspose.Cells](https://releases.aspose.com/cells/net/).
### 3. Visual Studio IDE
Pro spouštění a správu projektů v C# je výhodné mít Visual Studio. Každá verze, která podporuje .NET, by měla fungovat skvěle.
### 4. Platná licence Aspose
 Zatímco Aspose.Cells lze vyzkoušet, zvažte zakoupení licence, pokud ji používáte pro dlouhodobé projekty. Můžete si to koupit přes[tento odkaz](https://purchase.aspose.com/buy) nebo prozkoumat a[dočasná licence](https://purchase.aspose.com/temporary-license/) pro krátké testovací fáze.
Jakmile budete mít vše připraveno, pojďme se pustit do kódu!
## Import balíčků
První krok na naší cestě zahrnuje import základních jmenných prostorů. To je zásadní, protože nám to umožňuje přístup ke třídám a metodám, které budeme používat k manipulaci se soubory aplikace Excel. Postup je následující:
```csharp
using System;
using System.IO;
using Aspose.Cells;
```
Ujistěte se, že je tento řádek uveden v horní části souboru .cs. Nyní, když máme importy připraveny, můžeme pokračovat ve vytváření našeho sešitu a přístupu k listu.
## Krok 1: Vytvořte si sešit
Začneme vytvořením instance`Workbook` třída. To tvoří základ naší manipulace se soubory Excel.
```csharp
Workbook wb = new Workbook();
```
Tento řádek říká programu, aby inicializoval nový sešit a nastavuje nás, abychom se ponořili do našich listů.
## Krok 2: Otevřete první list
Dále přistoupíme k prvnímu listu v našem nově vytvořeném sešitu. Je to docela jednoduché:
```csharp
Worksheet ws = wb.Worksheets[0];
```
Zde přistupujeme k prvnímu listu (indexovanému na 0) v našem sešitu. Zde nastavíme velikosti papíru.
## Nastavení velikosti papíru a rozměrů načítání
Nyní vstupujeme do jádra operace – nastavujeme velikost papíru a získáváme jeho rozměry! Pojďme si to rozebrat krok za krokem.
## Krok 3: Nastavte Paper Size na A2
Nejprve si nastavíme velikost papíru na A2 a vytiskneme si jeho rozměry.
```csharp
ws.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```
 Po tomto nastavení používáme`Console.WriteLine` pro zobrazení rozměrů. Když toto spustíte, uvidíte šířku a výšku v palcích pro velikost papíru A2.
## Krok 4: Nastavte Paper Size na A3
Nyní je čas na A3! Jednoduše proces opakujeme:
```csharp
ws.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```
Voila! Prohlášení vytiskne konkrétní výšku a šířku pro papír A3.
## Krok 5: Nastavte Paper Size na A4
Podle stejného vzoru se podívejme, jak se A4 měří:
```csharp
ws.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```
Tím získáme rozměry pro A4 – jeden z nejčastěji používaných formátů papíru.
## Krok 6: Nastavte Paper Size na Letter
Abychom završili náš průzkum velikosti papíru, nastavte jej na velikost Letter:
```csharp
ws.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```
Opět uvidíme konkrétní šířku a výšku pro velikost Letter.
## Závěr
A tady to máte! Právě jste se naučili, jak získat šířku a výšku papíru pro různé velikosti při přípravě pracovních listů pro tisk pomocí Aspose.Cells for .NET. Tento nástroj může být neuvěřitelně užitečný, zvláště když plánujete rozvržení tisku nebo programově spravujete nastavení tisku. Znáte-li přesné rozměry v palcích, můžete se vyhnout běžným nástrahám a zajistit, aby se vaše dokumenty vytiskly tak, jak bylo zamýšleno.
## FAQ
### Co je Aspose.Cells?
Aspose.Cells je knihovna .NET, která poskytuje řadu funkcí pro programovou práci se soubory aplikace Excel.
### Jak mohu začít s Aspose.Cells?
Začněte stažením knihovny z[Aspose webové stránky](https://releases.aspose.com/cells/net/) a podle dokumentace jej nastavte ve svém projektu.
### Mohu používat Aspose.Cells zdarma?
Aspose.Cells nabízí zkušební verzi, kterou můžete použít k prozkoumání jejích funkcí. Pro dlouhodobé používání je potřeba zakoupit licenci.
### Jaké velikosti papíru podporuje Aspose.Cells?
Aspose.Cells podporuje různé velikosti papíru včetně A2, A3, A4, Letter a mnoha dalších.
### Kde najdu další zdroje nebo podporu pro Aspose.Cells?
 Můžete zkontrolovat[Aspose fórum](https://forum.aspose.com/c/cells/9) za pomoc komunitě a[dokumentace](https://reference.aspose.com/cells/net/) pro výukové programy a referenční materiály.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
