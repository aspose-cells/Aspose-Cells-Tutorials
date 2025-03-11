---
title: Nastavení času vytvoření PDF v .NET
linktitle: Nastavení času vytvoření PDF v .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak nastavit čas vytváření PDF v .NET pomocí Aspose.Cells. Postupujte podle našeho podrobného průvodce pro bezproblémový převod Excelu do PDF.
weight: 11
url: /cs/net/xps-and-pdf-operations/setting-pdf-creation-time/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nastavení času vytvoření PDF v .NET

## Zavedení
dnešní digitální době je schopnost převádět dokumenty do různých formátů pro mnoho aplikací zásadní. Jednou z běžných potřeb je převést tabulky aplikace Excel do souborů PDF. Nejen, že se tím zachová formátování, ale také mnohem jednodušší sdílení a tisk. Pokud jste vývojář pracující s .NET, Aspose.Cells je fantastická knihovna, která tento proces zjednodušuje. V tomto tutoriálu se ponoříme do toho, jak nastavit čas vytvoření PDF při převodu souboru Excel do PDF pomocí Aspose.Cells for .NET.
## Předpoklady
Než se pustíme do hrubšího kódu, ujistěte se, že máte vše, co potřebujete, abyste mohli začít.
### Co potřebujete
1. Visual Studio: Ujistěte se, že máte na svém počítači nainstalované Visual Studio. Toto bude vaše vývojové prostředí.
2.  Aspose.Cells for .NET: Stáhněte si knihovnu Aspose.Cells z[webové stránky](https://releases.aspose.com/cells/net/). Můžete také začít s bezplatnou zkušební verzí a otestovat její funkce.
3. Základní znalost C#: Znalost programování v C# vám pomůže lépe porozumět úryvkům kódu.
4.  Soubor Excel: Připravte soubor Excel pro převod. V tomto příkladu použijeme soubor s názvem`Book1.xlsx`.
Nyní, když máte seřazené předpoklady, pojďme se pustit do té zábavné části – importu potřebných balíčků a psaní kódu!
## Importujte balíčky
Chcete-li začít, musíte importovat požadované jmenné prostory do souboru C#. To je zásadní, protože vám to umožňuje přístup ke třídám a metodám poskytovaným knihovnou Aspose.Cells.
### Otevřete svůj projekt C#
Otevřete Visual Studio a buď vytvořte nový projekt, nebo otevřete existující, kde chcete implementovat funkci převodu PDF.
### Přidejte odkaz Aspose.Cells
Knihovnu Aspose.Cells můžete přidat do svého projektu kliknutím pravým tlačítkem myši na projekt v Průzkumníku řešení, výběrem „Spravovat balíčky NuGet“ a vyhledáním „Aspose.Cells“. Nainstalujte balíček.
### Importovat jmenné prostory
V horní části souboru C# uveďte následující jmenné prostory:
```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Charts;
```
Tyto jmenné prostory vám umožní přístup ke třídě Workbook a dalším základním funkcím.

Nyní, když máme naše balíčky naimportované, pojďme si rozebrat proces převodu souboru Excel do PDF při nastavování času vytvoření.
## Krok 1: Definujte adresář dokumentů
Nejprve musíte určit adresář, kde jsou vaše dokumenty uloženy. Zde se nachází váš soubor Excel a kam se uloží výstupní PDF.
```csharp
string dataDir = "Your Document Directory"; // Zadejte adresář dokumentů
```
 Nahradit`"Your Document Directory"` se skutečnou cestou, kde jste`Book1.xlsx` soubor se nachází. Tato cesta pomůže aplikaci najít soubor ke zpracování.
## Krok 2: Načtěte soubor Excel
 Dále načtete soubor Excel do a`Workbook` objekt. To je místo, kde Aspose.Cells září, protože vám umožňuje pracovat se soubory aplikace Excel bez námahy.
```csharp
string inputPath = dataDir + "Book1.xlsx"; // Cesta k souboru aplikace Excel
Workbook workbook = new Workbook(inputPath); // Načtěte soubor Excel
```
 The`Workbook` třída se používá k načítání a manipulaci se soubory Excel. Předáním vstupní cesty sdělujete aplikaci, se kterým souborem má pracovat.
## Krok 3: Vytvořte možnosti PdfSaveOptions
 Nyní je čas vytvořit instanci`PdfSaveOptions`. Tato třída vám umožňuje určit různé možnosti pro uložení sešitu jako PDF, včetně času vytvoření.
```csharp
PdfSaveOptions options = new PdfSaveOptions(); // Vytvořte instanci PdfSaveOptions
options.CreatedTime = DateTime.Now; // Nastavte čas vytvoření na nyní
```
 Nastavením`options.CreatedTime` na`DateTime.Now`, zajistíte, že PDF bude odrážet aktuální datum a čas, kdy byl vytvořen.
## Krok 4: Uložte sešit jako PDF
Nakonec uložíte sešit jako soubor PDF pomocí možností, které jste právě definovali.
```csharp
workbook.Save(dataDir + "output.pdf", options); //Uložit jako PDF
```
 Tento řádek kódu vezme sešit a uloží jej ve formátu PDF na určené místo. The`options` je předán tak, aby zahrnoval čas vytvoření do metadat PDF.

## Závěr
A tady to máte! Úspěšně jste převedli soubor aplikace Excel do formátu PDF pomocí Aspose.Cells for .NET, včetně časového razítka vytvoření. Tato funkce může být neuvěřitelně užitečná, když potřebujete mít přehled o verzích dokumentů nebo když chcete poskytnout příjemcům informace o tom, kdy byl dokument vytvořen.
 Pokud chcete prozkoumat další funkce Aspose.Cells, neváhejte a podívejte se na[dokumentace](https://reference.aspose.com/cells/net/).
## FAQ
### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna pro .NET, která umožňuje vývojářům vytvářet, manipulovat a převádět soubory aplikace Excel.
### Mohu používat Aspose.Cells zdarma?
 Ano, můžete začít s bezplatnou zkušební verzí dostupnou na[Aspose webové stránky](https://releases.aspose.com/).
### Jak nastavím další vlastnosti PDF?
 Můžete nastavit různé vlastnosti PDF pomocí`PdfSaveOptions` třídy, jako je velikost stránky, komprese a další.
### Je možné převést více souborů aplikace Excel najednou?
Ano, můžete procházet seznam souborů a na každý z nich použít stejný proces převodu.
### Kde mohu získat podporu pro Aspose.Cells?
 Na jejich stránkách můžete získat podporu od komunity Aspose[fórum podpory](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
