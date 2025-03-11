---
title: Otočit text pomocí tvaru v aplikaci Excel
linktitle: Otočit text pomocí tvaru v aplikaci Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se otáčet text s tvary v Excelu pomocí Aspose.Cells for .NET. Postupujte podle tohoto podrobného průvodce pro dokonalou prezentaci v Excelu.
weight: 12
url: /cs/net/excel-shape-text-modifications/rotate-text-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Otočit text pomocí tvaru v aplikaci Excel

## Zavedení
Ve světě Excelu je vizuální reprezentace stejně důležitá jako samotná data. Ať už vytváříte sestavu nebo navrhujete dynamický řídicí panel, způsob uspořádání informací může dramaticky ovlivnit jejich čitelnost a celkový vzhled. Chtěli jste tedy někdy otočit text, aby se stylově zarovnal s tvary? Máte štěstí! V tomto tutoriálu se ponoříme do toho, jak otáčet text s tvary pomocí Aspose.Cells pro .NET, abychom zajistili, že vaše tabulky nejen informují, ale také zapůsobí.
## Předpoklady
Než začneme, ujistěte se, že máte vše, co potřebujete:
1. Visual Studio: Ujistěte se, že máte na svém počítači nainstalované Visual Studio, protože tam budeme psát náš kód.
2.  Aspose.Cells for .NET: Budete potřebovat knihovnu Aspose.Cells. Můžete[stáhněte si nejnovější verzi zde](https://releases.aspose.com/cells/net/) nebo to vyzkoušejte zdarma s a[zkušební verze zdarma](https://releases.aspose.com/).
3. Základní znalost C#: Znalost prostředí C# a .NET bude užitečná, i když vás provedeme každým krokem.
4.  Soubor Excel: Ukázkový soubor Excel, nazvěme ho`sampleRotateTextWithShapeInsideWorksheet.xlsx`, je potřeba k otestování našeho kódu. Tento soubor byste měli umístit do adresáře, ke kterému máte snadný přístup.
Máte vše připraveno? Fantastický! Pojďme se vrhnout na zábavnější část.
## Importujte balíčky
Abychom mohli začít, musíme do našeho projektu importovat potřebné balíčky. Postupujte takto:
### Vytvořit nový projekt
1. Otevřete Visual Studio.
2. Vyberte „Vytvořit nový projekt“.
3. Zvolte "Console App" a jako preferovaný programovací jazyk vyberte C#.
### Nainstalujte Aspose.Cells
Nyní přidejte Aspose.Cells do vašeho projektu. Můžete to udělat pomocí NuGet Package Manager:
1. Otevřete "Nástroje" v horní nabídce.
2. Vyberte „Správce balíčků NuGet“ a poté „Spravovat balíčky NuGet pro řešení“.
3. Vyhledejte "Aspose.Cells."
4. Kliknutím na „Instalovat“ jej přidáte do svého projektu.
### Přidat Směrnici použití
Na začátek hlavního souboru C# musíte přidat následující direktivu:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
Nyní jsme všichni připraveni začít kódovat!
Rozeberme si proces na lehce stravitelné kroky. Zde je návod, jak otočit text s tvary v souboru aplikace Excel:
## Krok 1: Nastavte cesty k adresáři
Nejprve musíte nastavit zdrojový a výstupní adresář, kde budou uloženy vaše soubory Excel. Zde je postup:
```csharp
//Zdrojový adresář
string sourceDir = "Your Document Directory"; // Nastavte adresář dokumentů
//Výstupní adresář
string outputDir = "Your Document Directory"; // Nastavte výstupní adresář
```
 Nahradit`"Your Document Directory"` se skutečnou cestou, kde jste`sampleRotateTextWithShapeInsideWorksheet.xlsx` soubor se nachází.
## Krok 2: Načtěte ukázkový soubor Excel
Nyní načteme ukázkový soubor Excel. To je zásadní, protože chceme manipulovat se stávajícími daty.
```csharp
//Načtěte ukázkový soubor Excel.
Workbook wb = new Workbook(sourceDir + "sampleRotateTextWithShapeInsideWorksheet.xlsx");
```
## Krok 3: Otevřete sešit
Jakmile je soubor načten, musíme získat přístup ke konkrétnímu listu, který chceme upravit. V našem případě je to první pracovní list.
```csharp
//Přístup k prvnímu listu.
Worksheet ws = wb.Worksheets[0];
```
## Krok 4: Upravte buňku
Dále upravíme konkrétní buňku pro zobrazení zprávy. V našem příkladu použijeme buňku B4.
```csharp
//Otevřete buňku B4 a přidejte do ní zprávu.
Cell b4 = ws.Cells["B4"];
b4.PutValue("Text is not rotating with shape because RotateTextWithShape is false.");
```
Tento krok je celý o komunikaci – zajistit, aby kdokoli otevře tento list, pochopil, co vylaďujeme.
## Krok 5: Přístup k prvnímu tvaru
K otočení textu potřebujeme tvar, se kterým budeme pracovat. Zde se dostaneme k prvnímu tvaru v listu.
```csharp
//Přístup k prvnímu tvaru.
Shape sh = ws.Shapes[0];
```
## Krok 6: Upravte zarovnání textu tvaru
Tady se děje kouzlo. Upravíme vlastnosti zarovnání textu tvaru.
```csharp
//Přístup k zarovnání textu tvaru.
Aspose.Cells.Drawing.Texts.ShapeTextAlignment shapeTextAlignment = sh.TextBody.TextAlignment;
//Neotáčet text pomocí tvaru nastavením RotateTextWithShape na hodnotu false.
shapeTextAlignment.RotateTextWithShape = false;
```
 Nastavením`RotateTextWithShape` na false, zajistíme, že text zůstane vzpřímený a neotáčí se s tvarem, a tak vše zůstane úhledné a organizované.
## Krok 7: Uložte výstupní soubor aplikace Excel
Nakonec uložme naše změny do nového souboru Excel. To zajišťuje, že neztratíme své úpravy a budeme mít čistý výstup.
```csharp
//Uložte výstupní soubor aplikace Excel.
wb.Save(outputDir + "outputRotateTextWithShapeInsideWorksheet.xlsx");
```
A je to! Váš výstupní soubor je nyní uložen, včetně textu v buňce B4 a úprav tvaru.
## Krok 8: Spusťte kód
 Ve vašem`Main` zabalte všechny výše uvedené fragmenty kódu a spusťte svůj projekt. Podívejte se, jak se změny projeví ve vašem výstupním souboru!
```csharp
Console.WriteLine("RotateTextWithShapeInsideWorksheet executed successfully.");
```
## Závěr
Otáčení textu s tvary v Excelu pomocí Aspose.Cells for .NET se může na první pohled zdát jako složitý proces, ale jakmile to rozeberete, je to docela jednoduché. Pomocí těchto jednoduchých kroků můžete upravit své tabulky tak, aby vypadaly profesionálněji a vizuálně přitažlivější. Nyní, ať už to děláte pro klienta nebo své osobní projekty, každý bude nadšeně šílet nad kvalitou vaší práce!
## FAQ
### Mohu používat Aspose.Cells zdarma?
 Ano! Můžete použít[zkušební verze zdarma](https://releases.aspose.com/) vyzkoušet knihovnu.
### Jaké verze aplikace Excel podporuje Aspose.Cells?
Aspose.Cells podporuje různé formáty aplikace Excel, včetně XLS, XLSX, CSV a dalších.
### Je možné otáčet text s tvary ve starších verzích Excelu?
Ano, funkci lze aplikovat na starší formáty podporované Aspose.Cells.
### Kde najdu další dokumentaci o Aspose.Cells?
 Můžete prozkoumat komplexní[dokumentace](https://reference.aspose.com/cells/net/) pro více poznatků.
### Jak získám podporu pro Aspose.Cells?
 Můžete požádat o podporu návštěvou stránky[Aspose fórum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
