---
title: Odebrat existující nastavení tiskárny z listů
linktitle: Odebrat existující nastavení tiskárny z listů
second_title: Aspose.Cells .NET Excel Processing API
description: V tomto podrobném podrobném průvodci se dozvíte, jak odstranit stávající nastavení tiskárny z listů aplikace Excel pomocí Aspose.Cells for .NET.
weight: 19
url: /cs/net/worksheet-page-setup-features/remove-existing-printer-settings/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Odebrat existující nastavení tiskárny z listů

## Zavedení
Pokud jste někdy pracovali se soubory aplikace Excel, víte, jak důležité je mít dokumenty správně nastavené – zejména pokud jde o tisk. Věděli jste, že nastavení tiskárny se někdy může přenést z jednoho listu do druhého, což může potenciálně narušit rozvržení tisku? V tomto tutoriálu se ponoříme do toho, jak můžete snadno odstranit stávající nastavení tiskárny z listů pomocí výkonné knihovny Aspose.Cells pro .NET. Ať už jste zkušený vývojář nebo teprve začínáte, tento článek je navržen tak, aby vás provedl každým krokem. Začněme!
## Předpoklady
Než se ponoříme do kouzla kódování, je potřeba nastavit několik věcí:
1. Visual Studio: Ujistěte se, že máte na svém počítači nainstalované Visual Studio.
2. Aspose.Cells for .NET Library: Knihovnu Aspose.Cells si můžete stáhnout z[zde](https://releases.aspose.com/cells/net/).
3. Základní porozumění C#: Vzhledem k tomu, že tento tutoriál zahrnuje kódování v C#, bude užitečné základní pochopení jazyka.
4. Ukázkový soubor Excel: Budete potřebovat existující soubor Excel s nastavením tiskárny, které chcete odstranit. Neváhejte a vytvořte si vzorový dokument nebo použijte existující dokument.
Jakmile budete mít své prostředí nastavené, můžeme začít s rozkrýváním kódu.
## Importujte balíčky
Než se pustíme do skutečného kódu pro odstranění nastavení tiskárny, musíme se ujistit, že máme v našem projektu C# importovány správné balíčky. Zde je to, co potřebujete v horní části souboru kódu:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Nyní, když máme vše, co potřebujeme, pojďme se pustit do toho nejhrubšího kódu.
## Krok 1: Definujte svůj zdrojový a výstupní adresář
Prvním krokem je určit, kde se nachází váš původní dokument Excel a kam chcete uložit upravenou verzi.
```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory\\";
// Výstupní adresář
string outputDir = "Your Document Directory\\";
```
 Nezapomeňte vyměnit`"Your Document Directory\\"` se skutečnou cestou k vašim dokumentům.
## Krok 2: Načtěte zdrojový soubor Excel
Dále načteme sešit (soubor Excel), který obsahuje nastavení tiskárny. Budete se chtít ujistit, že cesta k souboru je správná.
```csharp
// Načtěte zdrojový soubor Excel
Workbook wb = new Workbook(sourceDir + "sampleRemoveExistingPrinterSettingsOfWorksheets.xlsx");
```
 Zde načítáme určený soubor aplikace Excel do souboru a`Workbook` objekt pojmenovaný`wb`.
## Krok 3: Získejte počet pracovních listů
Potřebujeme vědět, kolik listů je v sešitu, abychom je mohli iterovat a zkontrolovat případná nastavení tiskárny.
```csharp
// Získejte počty listů sešitu
int sheetCount = wb.Worksheets.Count;
```
Tento řádek kódu načte počet listů přítomných v sešitu.
## Krok 4: Projděte všechny pracovní listy
Nyní nastavíme scénu tak, aby procházela každý list v sešitu. Zkontrolujeme, zda pro každý list existují nějaká existující nastavení tiskárny.
```csharp
// Opakujte všechny listy
for (int i = 0; i < sheetCount; i++)
{
    // Otevřete i-tý pracovní list
    Worksheet ws = wb.Worksheets[i];
```
## Krok 5: Přístup k nastavení stránky listu
Každý list má vlastnosti nastavení stránky, které zahrnují nastavení tiskárny, které chceme zkontrolovat a případně odstranit.
```csharp
    // Přístup k nastavení stránky listu
    PageSetup ps = ws.PageSetup;
```
## Krok 6: Zkontrolujte existující nastavení tiskárny
Je čas zkontrolovat, zda pro aktuální list existují nějaká nastavení tiskárny. Pokud ano, vytiskneme zprávu a přistoupíme k jejich odstranění.
```csharp
    // Zkontrolujte, zda existují nastavení tiskárny pro tento list
    if (ps.PrinterSettings != null)
    {
        Console.WriteLine("PrinterSettings of this worksheet exist.");
```
## Krok 7: Vytiskněte podrobnosti listu
Pokud jsou nalezena nastavení tiskárny, zobrazme některé užitečné informace o listu a jeho nastavení tiskárny.
```csharp
        Console.WriteLine("Sheet Name: " + ws.Name);
        Console.WriteLine("Paper Size: " + ps.PaperSize);
```
To nám umožní ověřit, které listy mají definovaná nastavení tiskárny.
## Krok 8: Odeberte nastavení tiskárny
 Nyní přichází hlavní děj! Přiřazením odstraníme stávající nastavení tiskárny`null` k`PrinterSettings` vlastnictví.
```csharp
        // Odeberte nastavení tiskárny jejich nastavením na hodnotu null
        ps.PrinterSettings = null;
        Console.WriteLine("Printer settings of this worksheet are now removed by setting it null.");
        Console.WriteLine("");
    }
}
```
## Krok 9: Uložte upravený sešit
Nakonec sešit po provedení všech potřebných změn uložíme.
```csharp
// Uložte sešit
wb.Save(outputDir + "outputRemoveExistingPrinterSettingsOfWorksheets.xlsx");
```
## Závěr
tady to máte! Právě jste se naučili, jak odstranit stávající nastavení tiskárny z listů aplikace Excel pomocí Aspose.Cells for .NET. S tímto jednoduchým procesem můžete zajistit, že se vaše dokumenty vytisknou přesně tak, jak chcete, aniž by se vám zdržovala nějaká otravná stará nastavení. Takže až budete příště čelit problémům s nastavením tiskárny, budete vědět, co dělat!
## FAQ
### Co je Aspose.Cells?
Aspose.Cells je knihovna .NET, která umožňuje vývojářům bezproblémově pracovat se soubory aplikace Excel, aniž by museli instalovat aplikaci Microsoft Excel.
### Musím si koupit Aspose.Cells, abych je mohl používat?
 Můžete začít s bezplatnou zkušební verzí, ale pro dlouhodobé používání si budete muset zakoupit licenci. Kontrola[zde](https://purchase.aspose.com/buy) pro možnosti.
### Mohu odebrat nastavení tiskárny pro všechny listy najednou?
Ano! Jak jsme si ukázali v tutoriálu, můžete procházet každý list a odebrat nastavení.
### Existuje nějaké riziko ztráty dat při úpravě nastavení tiskárny?
Ne, odstranění nastavení tiskárny neovlivní skutečná data ve vašich listech.
### Kde najdu pomoc ohledně Aspose.Cells?
 Podporu komunity a zdroje najdete na[Aspose fórum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
