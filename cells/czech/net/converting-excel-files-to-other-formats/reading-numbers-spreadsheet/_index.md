---
title: Čtení číselné tabulky Programově v .NET
linktitle: Čtení číselné tabulky Programově v .NET
second_title: Aspose.Cells .NET Excel Processing API
description: V tomto podrobném kurzu se dozvíte, jak číst tabulky Numbers a převádět je do PDF pomocí Aspose.Cells for .NET.
weight: 18
url: /cs/net/converting-excel-files-to-other-formats/reading-numbers-spreadsheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Čtení číselné tabulky Programově v .NET

## Zavedení
V dnešním digitálním světě je správa dat zásadní dovedností a tabulky jsou v popředí organizace dat. Co když ale potřebujete pracovat s tabulkou Numbers – se soubory vytvořenými aplikací Apple Numbers – pomocí .NET? Nebojte se; nejsi sám! V tomto tutoriálu projdeme procesem čtení tabulky Numbers programově pomocí Aspose.Cells pro .NET. Naučíte se, jak načíst soubor Numbers a převést jej do PDF.
## Předpoklady
Než začneme, je třeba mít připraveno několik věcí:
1. Aspose.Cells for .NET: Ujistěte se, že máte nainstalovanou knihovnu Aspose.Cells. Můžete si jej stáhnout[zde](https://releases.aspose.com/cells/net/).
2. Visual Studio: Doporučuje se mít na počítači nainstalováno Visual Studio (nebo jakékoli jiné IDE kompatibilní s .NET).
3. Základní znalost C#: Malá znalost programování v C# vám pomůže hladce pokračovat.
4. Váš adresář dokumentů: Budete potřebovat adresář, kde je uložen váš soubor Numbers, spolu s umístěním pro uložení převedeného PDF.
Jakmile splníte tyto předpoklady, můžete začít!
## Importujte balíčky
Nejprve musíme naimportovat potřebné balíčky do našeho projektu C#. Toto je zásadní krok, protože nám to umožňuje využít funkce poskytované knihovnou Aspose.Cells.
1. Otevřete svůj projekt C# ve Visual Studiu.
2. Přidejte odkaz na knihovnu Aspose.Cells:
   - Pokud používáte NuGet, jednoduše spusťte následující příkaz v konzole Správce balíčků:
```
 Install-Package Aspose.Cells
 ```
3. Importujte potřebné jmenné prostory do kódu:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Nyní, když jsme importovali potřebné balíčky, přejděme k podrobnému průvodci čtením tabulky Numbers.
## Krok 1: Zadejte zdrojový a výstupní adresář
V tomto kroku nastavíme adresáře, kde se nachází váš zdrojový soubor Numbers a kam chcete uložit výstupní PDF.
```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory"; // Aktualizujte to do svého skutečného adresáře
// Výstupní adresář
string outputDir = "Your Document Directory"; // Aktualizujte to do svého skutečného adresáře
```
 Zde definujeme dvě řetězcové proměnné,`sourceDir` a`outputDir` , k určení umístění vstupních a výstupních souborů. Nezapomeňte vyměnit`"Your Document Directory"` se skutečnými cestami ve vašem systému.
## Krok 2: Nastavte možnosti načítání pro formát čísel
Dále určíme možnosti načtení pro čtení tabulky Numbers. Tento krok je nezbytný, protože říká Aspose, jak interpretovat soubor Numbers.
```csharp
// Specifikujte možnosti zatížení; chceme načíst tabulku Numbers
LoadOptions opts = new LoadOptions(LoadFormat.Numbers);
```
 Vytváříme a`LoadOptions` objekt a zadejte formát jako`LoadFormat.Numbers`. To říká knihovně Aspose.Cells, že pracujeme se souborem Numbers. 
## Krok 3: Načtěte tabulku Numbers do sešitu
Nyní je čas načíst skutečnou tabulku Numbers do a`Workbook` objekt.
```csharp
// Načtěte tabulku Numbers do sešitu s výše uvedenými možnostmi načítání
Workbook wb = new Workbook(sourceDir + "sampleNumbersByAppleInc.numbers", opts);
```
 Vytvoříme instanci a`Workbook` objekt a předat cestu k souboru Numbers spolu s našimi možnostmi načtení. Ujistěte se, že název souboru (`sampleNumbersByAppleInc.numbers`) odpovídá skutečnému názvu vašeho souboru Numbers.
## Krok 4: Uložte sešit jako PDF
Jakmile je soubor Numbers úspěšně načten, dalším krokem je jeho uložení v jiném formátu – konkrétně PDF.
```csharp
// Uložte sešit do formátu PDF
wb.Save(outputDir + "outputNumbersByAppleInc.pdf", SaveFormat.Pdf);
```
 Zde nazýváme`Save` metoda na`Workbook` objekt, určující cestu k výstupnímu souboru a formát, ve kterém jej chceme uložit. V tomto případě jej ukládáme jako PDF. Ujistěte se, že název výstupního souboru (`outputNumbersByAppleInc.pdf`) je jedinečný a nepřepisuje žádné existující soubory.
## Krok 5: Potvrďte úspěch
Nakonec přidáme zprávu pro potvrzení, že naše operace byla úspěšná.
```csharp
Console.WriteLine("ReadNumbersSpreadsheet executed successfully.\r\n");
```
Jakmile je vše hotovo, tento řádek kódu vytiskne do konzole zprávu o úspěchu. Vždy je příjemné mít zpětnou vazbu, že?
## Závěr
A tady to máte! Úspěšně jste si přečetli tabulku Numbers a převedli ji do PDF pomocí Aspose.Cells for .NET. Tato výkonná knihovna vám umožňuje bez námahy manipulovat s tabulkami, takže úkoly správy dat budou hračkou. Ať už vyvíjíte aplikace nebo jen potřebujete efektivněji zacházet s tabulkami, Aspose.Cells je fantastický nástroj, který můžete mít ve své sadě nástrojů.
## FAQ
### Jaké typy souborů může Aspose.Cells číst?  
Aspose.Cells umí číst různé formáty souborů, včetně souborů XLS, XLSX, CSV a Numbers. 
### Mohu upravovat soubory Numbers pomocí Aspose.Cells?  
Ano, můžete číst, manipulovat a ukládat soubory Numbers pomocí Aspose.Cells.
### Je Aspose.Cells zdarma k použití?  
 Aspose.Cells nabízí bezplatnou zkušební verzi, ale pro rozšířené použití budete potřebovat licenci. Zkontrolujte cenu[zde](https://purchase.aspose.com/buy).
### Co mám dělat, když při načítání souboru Numbers narazím na chybu?  
 Ujistěte se, že používáte správné možnosti načítání a že cesta k souboru je přesná. Pro další podporu navštivte stránku[Aspose Support Forum](https://forum.aspose.com/c/cells/9).
### Jak mohu získat dočasnou licenci pro Aspose.Cells?  
 Můžete požádat o dočasnou licenci[zde](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
