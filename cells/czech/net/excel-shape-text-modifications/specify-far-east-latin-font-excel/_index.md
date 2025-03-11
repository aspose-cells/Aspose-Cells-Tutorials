---
title: Zadejte písmo Dálný východ a latinka v aplikaci Excel
linktitle: Zadejte písmo Dálný východ a latinka v aplikaci Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Zjistěte, jak určit písma Dálného východu a latinky v Excelu pomocí Aspose.Cells for .NET v tomto komplexním a snadno srozumitelném tutoriálu.
weight: 17
url: /cs/net/excel-shape-text-modifications/specify-far-east-latin-font-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zadejte písmo Dálný východ a latinka v aplikaci Excel

## Zavedení
Přejete si vylepšit své excelové sestavy nebo dokumenty o specifické požadavky na písmo? Ať už máte co do činění s více jazyky nebo jednoduše usilujete o jedinečnou estetiku ve svých tabulkách, pochopení toho, jak v Excelu specifikovat písma Dálného východu a latinky, je klíčovou dovedností. Naštěstí pro vás máme řešení! V tomto tutoriálu prozkoumáme, jak používat Aspose.Cells pro .NET k bezproblémové implementaci této funkce. Pojďme se ponořit!
## Předpoklady
Než se pustíme do toho, je několik věcí, které budete muset nastavit, než začnete s Aspose.Cells:
### .NET Framework nebo .NET Core
Ujistěte se, že máte na svém počítači nainstalované rozhraní .NET Framework nebo .NET Core. Tato knihovna funguje dobře s oběma.
### Instalace Aspose.Cells
 Budete si muset stáhnout knihovnu Aspose.Cells. Můžete[stáhněte si to odtud](https://releases.aspose.com/cells/net/) . Pokud nejste obeznámeni s instalací balíčků NuGet, postupujte takto[tohoto průvodce](https://www.nuget.org/).
### Integrované vývojové prostředí (IDE)
Mít IDE, jako je Visual Studio nebo JetBrains Rider, může zjednodušit kódování, ladění a spouštění vašeho projektu.
### Základní znalost C#
Znalost programování v C# bude velmi přínosná pro sledování tohoto návodu.
## Importujte balíčky
Než budeme moci pracovat s Aspose.Cells, musíme do našeho projektu importovat potřebné balíčky. Můžete to udělat takto:
### Vytvořit nový projekt
1. Otevřete své IDE a vytvořte nový projekt konzolové aplikace.
2.  Pojmenujte svůj projekt nějak popisně, např`FontSpecifyingApp`.
### Přidejte balíček NuGet Aspose.Cells
1. Klepněte pravým tlačítkem myši na svůj projekt v Průzkumníku řešení.
2.  Vybrat`Manage NuGet Packages...`.
3.  Hledat`Aspose.Cells` a nainstalujte jej.
Na konci těchto kroků byste měli mít vše připraveno, abyste mohli začít kódovat!
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Po dokončení nastavení je čas vyhrnout si rukávy a pustit se do kódování. Konkrétně vytvoříme nový excelový sešit a určíme písmo Dálného východu i latinky pro textová pole. Zde je postup, jak to udělat krok za krokem:
## Krok 1: Nastavte výstupní adresář
Začneme tím, že určíme, kam chceme soubor Excel uložit. To je zásadní, protože chceme zajistit, aby byl náš výstupní soubor uložen na místě, které je snadno dostupné.
```csharp
// Výstupní adresář
string outputDir = "Your Document Directory";
```
## Krok 2: Vytvořte prázdný sešit
Nyní, když máme nastavený adresář, vytvoříme nový sešit, kam přidáme náš obsah. Je to podobné, jako když začínáte s čerstvým plátnem před malováním.
```csharp
// Vytvořte prázdný sešit.
Workbook wb = new Workbook();
```
## Krok 3: Otevřete první pracovní list
Dále chceme pracovat s pracovním listem z našeho sešitu. Představte si pracovní list jako stránku v knize, kde se dějí všechna kouzla.
```csharp
// Přístup k prvnímu listu.
Worksheet ws = wb.Worksheets[0];
```
## Krok 4: Přidejte textové pole
Nyní do našeho listu přidáme textové pole. Zde budeme psát náš text. Představte si to jako vytvoření textového pole na snímku prezentace.
```csharp
// Přidejte textové pole do listu.
int idx = ws.TextBoxes.Add(5, 5, 50, 200);
Aspose.Cells.Drawing.TextBox tb = ws.TextBoxes[idx];
```
## Krok 5: Nastavte text textového pole
Napíšeme nějaký text. V tomto příkladu zadáme japonské znaky, abychom předvedli písmo Dálného východu. Je to stejně jednoduché jako psaní do textového pole na vašem počítači!
```csharp
// Nastavte text textového pole.
tb.Text = "こんにちは世界"; //To v japonštině znamená „Ahoj světe“.
```
## Krok 6: Zadejte písma
Nyní přichází ta vzrušující část! Pro text nastavíme jak písmo latinky, tak písma Dálného východu. Je to podobné jako výběr dokonalého písma pro luxusní svatební pozvánku!
```csharp
// Zadejte Dálný východ a latinský název písma.
tb.TextOptions.LatinName = "Comic Sans MS"; // Toto je naše zvolené latinské písmo.
tb.TextOptions.FarEastName = "KaiTi"; // Toto je naše požadované písmo Dálného východu.
```
## Krok 7: Uložte výstupní soubor aplikace Excel
Nakonec si uložme náš sešit! Tento krok uzavírá náš úkol a zajišťuje, že veškerá tvrdá práce, kterou jsme udělali, bude správně uložena. 
```csharp
// Uložte výstupní soubor aplikace Excel.
wb.Save(outputDir + "outputSpecifyFarEastAndLatinNameOfFontInTextOptionsOfShape.xlsx", SaveFormat.Xlsx);
```
## Krok 8: Potvrzující zpráva
Abychom nám dali vědět, že vše proběhlo úspěšně, vytiskneme do konzole potvrzovací zprávu:
```csharp
Console.WriteLine("SpecifyFarEastAndLatinNameOfFontInTextOptionsOfShape executed successfully.");
```
## Závěr
A tady to máte! Úspěšně jste zadali písma Dálného východu a latinky v sešitu aplikace Excel pomocí Aspose.Cells for .NET. Tato dovednost nejenže dodá vašim dokumentům profesionální nádech, ale také obohatí zážitek ze čtení pro uživatele v různých jazycích.
Nebojte se experimentovat s různými fonty a styly, abyste našli kombinaci, která vyhovuje vašim konkrétním potřebám. Šťastné kódování!
## FAQ
### Co je Aspose.Cells?
Aspose.Cells je knihovna .NET pro vytváření a správu tabulek aplikace Excel bez nutnosti instalace aplikace Microsoft Excel na vašem počítači. 
### Mohu použít Aspose.Cells pro webové aplikace?
Ano! Aspose.Cells lze použít jak pro desktopové aplikace, tak pro webové aplikace postavené s .NET.
### Existuje bezplatná verze Aspose.Cells?
 Ano, Aspose nabízí bezplatnou zkušební verzi. Můžete[stáhněte si jej zde](https://releases.aspose.com/).
### Jak získám podporu pro Aspose.Cells?
 Můžete požádat o podporu a najít cenné zdroje na webu[Aspose fóra](https://forum.aspose.com/c/cells/9).
### Kde mohu koupit Aspose.Cells?
 Aspose.Cells můžete zakoupit přímo od[Aspose webové stránky](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
