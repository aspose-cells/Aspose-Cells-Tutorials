---
"description": "tomto podrobném návodu se naučíte, jak číst tabulky v Numbers a převádět je do PDF pomocí Aspose.Cells pro .NET."
"linktitle": "Programové čtení čísel v tabulce v .NET"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Programové čtení čísel v tabulce v .NET"
"url": "/cs/net/converting-excel-files-to-other-formats/reading-numbers-spreadsheet/"
"weight": 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Programové čtení čísel v tabulce v .NET

## Zavedení
V dnešním digitálním světě je správa dat zásadní dovedností a tabulkové procesory jsou v popředí organizace dat. Co když ale potřebujete pracovat s tabulkou Numbers – soubory vytvořenými aplikací Numbers od Apple – pomocí .NET? Nebojte se, nejste sami! V tomto tutoriálu si projdeme procesem programově čtení tabulky Numbers pomocí Aspose.Cells pro .NET. Naučíte se, jak načíst soubor Numbers a převést ho do formátu PDF.
## Předpoklady
Než začneme, je potřeba mít připraveno několik věcí:
1. Aspose.Cells pro .NET: Ujistěte se, že máte nainstalovanou knihovnu Aspose.Cells. Můžete si ji stáhnout. [zde](https://releases.aspose.com/cells/net/).
2. Visual Studio: Doporučuje se mít na počítači nainstalované Visual Studio (nebo jakékoli jiné IDE kompatibilní s .NET).
3. Základní znalost C#: Trocha znalosti programování v C# vám pomůže plynule se orientovat.
4. Adresář s dokumenty: Budete potřebovat adresář, kde je uložen soubor Numbers, a také umístění pro uložení převedeného PDF.
Jakmile splníte tyto předpoklady, můžete začít!
## Importovat balíčky
Nejprve musíme do našeho projektu v C# importovat potřebné balíčky. To je klíčový krok, protože nám umožňuje využít funkce poskytované knihovnou Aspose.Cells.
1. Otevřete svůj projekt C# ve Visual Studiu.
2. Přidejte odkaz na knihovnu Aspose.Cells:
   - Pokud používáte NuGet, jednoduše spusťte v konzoli Správce balíčků následující příkaz:
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
Nyní, když jsme importovali potřebné balíčky, pojďme se přesunout k podrobnému návodu pro čtení tabulky Numbers.
## Krok 1: Určení zdrojového a výstupního adresáře
tomto kroku nastavíme adresáře, kde se nachází váš zdrojový soubor Numbers a kam chcete uložit výstupní PDF.
```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory"; // Aktualizujte toto na váš skutečný adresář
// Výstupní adresář
string outputDir = "Your Document Directory"; // Aktualizujte toto na váš skutečný adresář
```
Zde definujeme dvě řetězcové proměnné, `sourceDir` a `outputDir`, chcete-li určit umístění vstupních a výstupních souborů. Nezapomeňte nahradit `"Your Document Directory"` se skutečnými cestami ve vašem systému.
## Krok 2: Nastavení možností načítání pro formát čísel
Dále určíme možnosti načítání pro čtení tabulky Numbers. Tento krok je nezbytný, protože sděluje Aspose, jak má interpretovat soubor Numbers.
```csharp
// Zadejte možnosti načítání; chceme načíst tabulku Numbers
LoadOptions opts = new LoadOptions(LoadFormat.Numbers);
```
Vytvoříme `LoadOptions` objekt a zadejte formát jako `LoadFormat.Numbers`Toto říká knihovně Aspose.Cells, že pracujeme se souborem typu Numbers. 
## Krok 3: Načtěte tabulku Numbers do sešitu
Nyní je čas načíst skutečnou tabulku Numbers do `Workbook` objekt.
```csharp
// Načtěte tabulku Numbers do sešitu s výše uvedenými možnostmi načtení
Workbook wb = new Workbook(sourceDir + "sampleNumbersByAppleInc.numbers", opts);
```
Vytvoříme instanci `Workbook` objekt a předat cestu k souboru Numbers spolu s našimi možnostmi načítání. Ujistěte se, že název souboru (`sampleNumbersByAppleInc.numbers`) odpovídá skutečnému názvu vašeho souboru Numbers.
## Krok 4: Uložte sešit jako PDF
Jakmile je soubor Numbers úspěšně načten, dalším krokem je jeho uložení v jiném formátu – konkrétně v PDF.
```csharp
// Uložit sešit do formátu PDF
wb.Save(outputDir + "outputNumbersByAppleInc.pdf", SaveFormat.Pdf);
```
Zde nazýváme `Save` metoda na `Workbook` objekt, přičemž určíme cestu k výstupnímu souboru a formát, ve kterém jej chceme uložit. V tomto případě jej ukládáme jako PDF. Ujistěte se, že název výstupního souboru (`outputNumbersByAppleInc.pdf`) je jedinečný a nepřepisuje žádné existující soubory.
## Krok 5: Potvrzení úspěchu
Nakonec přidejme zprávu, která potvrdí, že naše operace proběhla úspěšně.
```csharp
Console.WriteLine("ReadNumbersSpreadsheet executed successfully.\r\n");
```
Tento řádek kódu vypíše do konzole zprávu o úspěšném dokončení, jakmile bude vše hotové. Vždycky je fajn mít zpětnou vazbu, že?
## Závěr
tady to máte! Úspěšně jste si přečetli tabulku Numbers a převedli ji do PDF pomocí Aspose.Cells pro .NET. Tato výkonná knihovna vám umožňuje bez námahy manipulovat s tabulkami, což vám usnadňuje správu dat. Ať už vyvíjíte aplikace, nebo jen potřebujete efektivněji pracovat s tabulkami, Aspose.Cells je fantastický nástroj, který byste měli mít ve své sadě nástrojů.
## Často kladené otázky
### Jaké typy souborů dokáže Aspose.Cells číst?  
Aspose.Cells dokáže číst různé formáty souborů, včetně souborů XLS, XLSX, CSV a Numbers. 
### Mohu upravovat soubory Numbers pomocí Aspose.Cells?  
Ano, soubory Numbers můžete číst, manipulovat s nimi a ukládat je pomocí Aspose.Cells.
### Je Aspose.Cells zdarma k použití?  
Aspose.Cells nabízí bezplatnou zkušební verzi, ale pro delší používání budete potřebovat licenci. Zkontrolujte ceny. [zde](https://purchase.aspose.com/buy).
### Co mám dělat, když se při načítání souboru Numbers setkám s chybou?  
Ujistěte se, že používáte správné možnosti načítání a že je cesta k souboru přesná. Další podporu naleznete na [Fórum podpory Aspose](https://forum.aspose.com/c/cells/9).
### Jak mohu získat dočasnou licenci pro Aspose.Cells?  
Můžete požádat o dočasnou licenci [zde](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}