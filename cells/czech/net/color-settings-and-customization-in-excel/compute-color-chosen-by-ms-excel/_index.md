---
title: Vypočítat barvu zvolenou programem MS Excel
linktitle: Vypočítat barvu zvolenou programem MS Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak vypočítat barvu zvolenou MS Excel pomocí Aspose.Cells pro .NET. Podle tohoto podrobného průvodce získáte programový přístup k barvě podmíněného formátování aplikace Excel.
weight: 10
url: /cs/net/color-settings-and-customization-in-excel/compute-color-chosen-by-ms-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vypočítat barvu zvolenou programem MS Excel

## Zavedení
Už jste někdy pracovali se soubory Excel a přemýšleli jste, jak jsou určité barvy automaticky vybírány pro formátování? Nejsi sám. Podmíněné formátování Excelu může být trochu záhadou, zvláště když se pokoušíte extrahovat přesnou barvu, kterou Excel přiřadí. Ale nebojte se, my jsme vám pomohli! V tomto tutoriálu se ponoříme hluboko do toho, jak programově vypočítat barvu zvolenou MS Excel pomocí Aspose.Cells pro .NET. Rozebereme to krok za krokem, takže je můžete snadno sledovat a aplikovat na své vlastní projekty. Začněme!
## Předpoklady
Než se ponoříme do kódu, proberme si, co budete potřebovat, abyste mohli postupovat podle tohoto návodu:
-  Aspose.Cells for .NET nainstalován. Pokud ho ještě nemáte, můžete[stáhněte si jej zde](https://releases.aspose.com/cells/net/).
- Pracovní znalost C# a .NET frameworku.
- Ukázkový soubor aplikace Excel (Sešit1.xlsx) s použitým podmíněným formátováním.
Pokud ještě nemáte licenci, můžete si také vyzkoušet bezplatnou zkušební verzi Aspose.Cells for .NET. Vezměte si zkušební verzi[zde](https://releases.aspose.com/).
## Importujte balíčky
Než začneme kódovat, musíme naimportovat potřebné balíčky, abychom zajistili hladký chod. Ujistěte se, že jste do projektu zahrnuli následující jmenné prostory:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using System;
```
Tyto importy poskytují přístup k hlavním třídám Aspose.Cells a nativní systémové knihovně výkresů .NET pro práci s barvami.

Nyní, když máme vše na svém místě, rozdělme tento úkol na stravitelné kroky:
## Krok 1: Nastavte objekt sešitu
 První věc, kterou musíme udělat, je vytvořit instanci a`Workbook` objekt a načteme soubor Excel, se kterým chceme pracovat. Tady cesta začíná!
```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
// Vytvořte instanci objektu sešitu a otevřete soubor šablony
Workbook workbook = new Workbook(dataDir + "Book1.xlsx");
```
 V tomto kroku vytváříme novou instanci`Workbook` třídy od Aspose.Cells. The`Workbook`class představuje soubor Excel a poskytnutím cesty k našemu souboru jej můžeme snadno načíst pro další manipulaci.
## Krok 2: Otevřete první list
Jakmile je sešit načten, musíme získat přístup ke konkrétnímu listu, kde chceme extrahovat barvu. V tomto příkladu budeme pracovat s prvním listem.
```csharp
// Získejte první pracovní list
Worksheet worksheet = workbook.Worksheets[0];
```
 Zde načítáme první pracovní list v sešitu pomocí`Worksheets[0]` index. Aspose.Cells umožňuje přístup k libovolnému listu v souboru aplikace Excel podle jeho indexu nebo názvu.
## Krok 3: Vyberte buňku zájmu
Dále vybereme konkrétní buňku v listu. V tomto tutoriálu se zaměříme na buňku "A1", ale můžete vybrat libovolnou buňku s aplikovaným podmíněným formátováním.
```csharp
// Získejte buňku A1
Cell a1 = worksheet.Cells["A1"];
```
 Používáme`Cells` vlastnost odkazovat na konkrétní buňku její adresou. V tomto případě vybíráme buňku „A1“, protože chceme extrahovat výsledky podmíněného formátování použité na tuto buňku.
## Krok 4: Získejte výsledek podmíněného formátování
Tady se děje kouzlo! Použijeme Aspose.Cells k zachycení výsledku podmíněného formátování pro vybranou buňku. Takto Excel dynamicky vypočítá formátování včetně barev.
```csharp
// Získejte výsledný objekt podmíněného formátování
ConditionalFormattingResult cfr1 = a1.GetConditionalFormattingResult();
```
 The`GetConditionalFormattingResult()` metoda je v tomto kroku klíčová. Vrátí objekt, který obsahuje výsledky jakéhokoli podmíněného formátování použitého na buňku. Zde začínáme využívat informace o barvách, které Excel používá.
## Krok 5: Otevřete ColorScaleResult
Jakmile máme výsledek podmíněného formátování, můžeme se ponořit hlouběji a získat přístup k barevné škále, kterou Excel použil pro tuto konkrétní buňku.
```csharp
// Získejte výsledný barevný objekt ColorScale
Color c = cfr1.ColorScaleResult;
```
Podmíněné formátování v Excelu často spoléhá na barevné škály. Tento řádek nám umožňuje extrahovat výslednou barvu, která byla použita na základě pravidel podmíněného formátování.
## Krok 6: Výstup informací o barvě
Nakonec chceme vidět použitou barvu Excelu. Vytiskněme barevné detaily ve formátu, který je snadno srozumitelný, včetně jeho hodnoty ARGB a jeho názvu.
```csharp
// Přečtěte si barvu
Console.WriteLine(c.ToArgb().ToString());
Console.WriteLine(c.Name);
```
 The`ToArgb()` metoda nám dává barvu ve formátu ARGB (Alpha, Red, Green, Blue), zatímco`Name` vlastnost poskytuje název barvy ve formátu, který je pro člověka lépe čitelný. Tyto detaily barev můžete použít k jejich shodě v jiných aplikacích nebo programově upravit soubory aplikace Excel.

## Závěr
A tady to máte! Podle těchto kroků jste se právě naučili, jak programově vypočítat barvu zvolenou aplikací MS Excel pomocí Aspose.Cells for .NET. Tento přístup může být neuvěřitelně užitečný pro automatizaci úloh založených na Excelu, zejména při řešení složitého podmíněného formátování. Nyní, až se v Excelu příště setkáte s tajemnou barvou, budete přesně vědět, jak odhalit její tajemství.
## FAQ
### Mohu použít podmíněné formátování programově pomocí Aspose.Cells?
Ano, Aspose.Cells vám umožňuje používat, upravovat a dokonce odstraňovat podmíněné formátování v souborech Excelu programově.
### Podporuje Aspose.Cells všechny verze Excelu?
Absolutně! Aspose.Cells podporuje Excel 97-2003 (XLS), Excel 2007-2019/365 (XLSX) a další formáty, včetně PDF, HTML a CSV.
### Je Aspose.Cells k dispozici pro jiné platformy než .NET?
Ano, Aspose.Cells je k dispozici pro různé platformy, včetně Java, C++a Android přes Javu.
### Jak mohu získat bezplatnou zkušební verzi Aspose.Cells?
 Můžete si stáhnout bezplatnou zkušební verzi Aspose.Cells pro .NET z[zde](https://releases.aspose.com/).
### Jak zpracuji velké soubory aplikace Excel pomocí Aspose.Cells?
Aspose.Cells je optimalizován pro výkon i při práci s velkými soubory. K efektivnímu zpracování velkých dat můžete využít rozhraní API pro streamování.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
