---
"description": "Naučte se, jak nastavit čas vytvoření PDF v .NET pomocí Aspose.Cells. Postupujte podle našeho podrobného návodu pro bezproblémovou konverzi z Excelu do PDF."
"linktitle": "Nastavení času vytvoření PDF v .NET"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Nastavení času vytvoření PDF v .NET"
"url": "/cs/net/xps-and-pdf-operations/setting-pdf-creation-time/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Nastavení času vytvoření PDF v .NET

## Zavedení
dnešní digitální době je schopnost převádět dokumenty do různých formátů klíčová pro mnoho aplikací. Jednou z běžných potřeb je převod excelových tabulek do PDF souborů. Tím se nejen zachová formátování, ale také se to výrazně usnadňuje sdílení a tisk. Pokud jste vývojář pracující s .NET, Aspose.Cells je fantastická knihovna, která tento proces zjednodušuje. V tomto tutoriálu se ponoříme do toho, jak nastavit čas vytvoření PDF při převodu excelového souboru do PDF pomocí Aspose.Cells pro .NET.
## Předpoklady
Než se pustíme do detailů kódu, ujistěme se, že máte vše, co potřebujete k zahájení.
### Co potřebujete
1. Visual Studio: Ujistěte se, že máte na svém počítači nainstalované Visual Studio. Toto bude vaše vývojové prostředí.
2. Aspose.Cells pro .NET: Stáhněte si knihovnu Aspose.Cells z [webové stránky](https://releases.aspose.com/cells/net/)Můžete také začít s bezplatnou zkušební verzí a otestovat si jeho funkce.
3. Základní znalost C#: Znalost programování v C# vám pomůže lépe porozumět úryvkům kódu.
4. Soubor Excel: Mějte připravený soubor Excel pro převod. V tomto příkladu použijeme soubor s názvem `Book1.xlsx`.
Nyní, když máte vyřešené předpoklady, pojďme se pustit do zábavné části – importu potřebných balíčků a psaní kódu!
## Importovat balíčky
Pro začátek je potřeba importovat požadované jmenné prostory do souboru C#. To je klíčové, protože vám to umožní přístup ke třídám a metodám poskytovaným knihovnou Aspose.Cells.
### Otevřete svůj projekt v C#
Otevřete Visual Studio a buď vytvořte nový projekt, nebo otevřete existující, do kterého chcete implementovat funkci převodu PDF.
### Přidat odkaz na Aspose.Cells
Knihovnu Aspose.Cells můžete do projektu přidat tak, že v Průzkumníku řešení kliknete pravým tlačítkem myši na projekt, vyberete možnost „Spravovat balíčky NuGet“ a vyhledáte „Aspose.Cells“. Balíček nainstalujete.
### Importovat jmenné prostory
horní části souboru C# uveďte následující jmenné prostory:
```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Charts;
```
Tyto jmenné prostory vám poskytnou přístup ke třídě Workbook a dalším základním funkcím.

Nyní, když máme importované balíčky, pojďme si rozebrat proces převodu souboru Excel do PDF a zároveň nastavit čas vytvoření.
## Krok 1: Definování adresáře dokumentů
Nejprve je třeba zadat adresář, kde jsou uloženy vaše dokumenty. Zde se nachází váš soubor Excel a kam se uloží výstupní PDF.
```csharp
string dataDir = "Your Document Directory"; // Zadejte adresář dokumentů
```
Nahradit `"Your Document Directory"` se skutečnou cestou, kde se nachází vaše `Book1.xlsx` soubor se nachází. Tato cesta pomůže aplikaci najít soubor ke zpracování.
## Krok 2: Načtěte soubor Excel
Dále načtete soubor Excel do `Workbook` objekt. A právě zde vyniká Aspose.Cells, protože umožňuje bez námahy pracovat s excelovými soubory.
```csharp
string inputPath = dataDir + "Book1.xlsx"; // Cesta k vašemu souboru Excel
Workbook workbook = new Workbook(inputPath); // Načtěte soubor Excelu
```
Ten/Ta/To `Workbook` Třída se používá k načítání a manipulaci se soubory aplikace Excel. Předáním vstupní cesty sdělujete aplikaci, se kterým souborem má pracovat.
## Krok 3: Vytvořte PDFSaveOptions
Nyní je čas vytvořit instanci `PdfSaveOptions`Tato třída umožňuje zadat různé možnosti pro uložení sešitu ve formátu PDF, včetně času vytvoření.
```csharp
PdfSaveOptions options = new PdfSaveOptions(); // Vytvořit instanci PdfSaveOptions
options.CreatedTime = DateTime.Now; // Nastavte čas vytvoření na nyní
```
Nastavením `options.CreatedTime` na `DateTime.Now`, zajistíte, že PDF bude odrážet aktuální datum a čas jeho vytvoření.
## Krok 4: Uložte sešit jako PDF
Nakonec uložíte sešit jako soubor PDF s použitím právě definovaných možností.
```csharp
workbook.Save(dataDir + "output.pdf", options); // Uložit jako PDF
```
Tento řádek kódu vezme sešit a uloží ho ve formátu PDF na určené místo. `options` Parametr se předává pro zahrnutí času vytvoření do metadat PDF.

## Závěr
tady to máte! Úspěšně jste převedli soubor Excel do PDF pomocí Aspose.Cells pro .NET, včetně časového razítka vytvoření. Tato funkce může být neuvěřitelně užitečná, když potřebujete sledovat verze dokumentu nebo když chcete příjemcům poskytnout informace o tom, kdy byl dokument vytvořen.
Pokud chcete prozkoumat další funkce Aspose.Cells, neváhejte se podívat na [dokumentace](https://reference.aspose.com/cells/net/).
## Často kladené otázky
### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna pro .NET, která umožňuje vývojářům vytvářet, manipulovat a převádět soubory aplikace Excel.
### Mohu používat Aspose.Cells zdarma?
Ano, můžete začít s bezplatnou zkušební verzí dostupnou na [Webové stránky Aspose](https://releases.aspose.com/).
### Jak nastavím další vlastnosti PDF?
Různé vlastnosti PDF můžete nastavit pomocí `PdfSaveOptions` třída, jako je velikost stránky, komprese a další.
### Je možné převést více souborů Excelu najednou?
Ano, můžete procházet seznam souborů a na každý z nich použít stejný proces převodu.
### Kde mohu získat podporu pro Aspose.Cells?
Podporu od komunity Aspose můžete získat na jejich [fórum podpory](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}