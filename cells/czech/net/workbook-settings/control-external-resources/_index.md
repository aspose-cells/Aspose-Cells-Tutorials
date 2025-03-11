---
title: Ovládání externích zdrojů pomocí nastavení sešitu
linktitle: Ovládání externích zdrojů pomocí nastavení sešitu
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se ovládat externí zdroje v Excelu pomocí Aspose.Cells for .NET s naším komplexním výukovým programem krok za krokem.
weight: 10
url: /cs/net/workbook-settings/control-external-resources/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ovládání externích zdrojů pomocí nastavení sešitu

## Zavedení
V oblasti manipulace s daty a jejich prezentace může efektivní zacházení s externími zdroji změnit hru. Pokud pracujete se soubory aplikace Excel a chcete bezproblémově spravovat externí zdroje pomocí Aspose.Cells for .NET, jste na správném místě! V tomto článku se ponoříme hluboko do ovládání externích zdrojů při práci s excelovými sešity. Na konci této příručky budete schopni bez námahy implementovat přizpůsobené řešení pro načítání obrázků a dat z externích zdrojů.
## Předpoklady
Než se pustíme do hrubky kódování, je potřeba mít několik předpokladů. Ujistěte se, že:
1. Mít Visual Studio: K psaní a testování aplikací .NET budete potřebovat IDE. Visual Studio je nejvíce doporučovanou možností díky své rozsáhlé podpoře a snadnému použití.
2.  Stáhnout Aspose.Cells pro .NET: Pokud jste tak ještě neučinili, stáhněte si knihovnu Aspose.Cells z[odkaz ke stažení](https://releases.aspose.com/cells/net/). 
3. Základní porozumění C#: Znalost konceptů C# a .NET frameworku vám tento proces usnadní.
4. Nastavte své prostředí: Ujistěte se, že váš projekt odkazuje na knihovnu Aspose.Cells. Můžete to udělat pomocí Správce balíčků NuGet v sadě Visual Studio.
5. Ukázkové soubory: Připravte si ukázkový soubor aplikace Excel, který obsahuje externí zdroj, například propojený obrázek. Tento soubor vám pomůže demonstrovat funkce, které probíráme.
Jakmile jste s nimi nastaveni, jste připraveni ponořit se do ovládání externích zdrojů pomocí Aspose.Cells.
## Importujte balíčky
Chcete-li začít s kódováním, budete muset importovat potřebné balíčky do souboru C#. Zde je to, co potřebujete:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
Tyto jmenné prostory poskytují přístup k funkcím potřebným pro manipulaci se soubory aplikace Excel a zpracování obrázků.
 Pojďme si to rozdělit do zvládnutelných kroků, které vám pomohou ovládat používání externích zdrojů`Workbook Settings`. Projdeme si vytvořením vlastního poskytovatele streamu, načtením souboru aplikace Excel a vykreslením listu do obrázku. Neváhejte a sledujte!
## Krok 1: Definujte zdrojové a výstupní adresáře
Chcete-li začít, musíme určit adresáře, ze kterých budeme číst naše soubory a kam budeme ukládat náš výstup. Je nezbytné nastavit správné cesty, aby se předešlo chybám při nenalezení souboru.
```csharp
// Zdrojový adresář
static string sourceDir = "Your Document Directory";
// Výstupní adresář
static string outputDir = "Your Document Directory";
```
 Nahradit`"Your Document Directory"` se skutečnou cestou, kde jsou umístěny vaše soubory.
## Krok 2: Implementujte rozhraní IStreamProvider
 Dále vytvoříme vlastní třídu, která implementuje`IStreamProvider` rozhraní. Tato třída bude řídit, jak se přistupuje k externím zdrojům (jako jsou obrázky).
```csharp
class SP : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        // V případě potřeby vyčistěte všechny zdroje
    }
    public void InitStream(StreamProviderOptions options)
    {
        // Otevřete souborový proud externího prostředku
        FileStream fi = new FileStream(sourceDir + "sampleControlExternalResourcesUsingWorkbookSetting_StreamProvider.png", FileMode.OpenOrCreate, FileAccess.Read);
        options.Stream = fi;
    }
}
```
 V`InitStream` otevřeme soubor, který funguje jako náš externí zdroj, a přiřadíme jej k`Stream`vlastnictví. To umožňuje sešitu přístup k prostředku při vykreslování.
## Krok 3: Načtěte soubor Excel
Nyní, když máme našeho poskytovatele streamu připraveného, načteme sešit aplikace Excel, který obsahuje externí zdroj.
```csharp
public static void Run()
{
    // Načtěte ukázkový soubor Excel
    Workbook wb = new Workbook(sourceDir + "sampleControlExternalResourcesUsingWorkbookSetting_StreamProvider.xlsx");
    
    // Poskytněte svou implementaci IStreamProvider
    wb.Settings.StreamProvider = new SP();
```
 V tomto úryvku načteme náš soubor Excel a přiřadíme vlastní`StreamProvider` implementace pro práci s externími zdroji.
## Krok 4: Otevřete sešit
Po načtení sešitu se snadno dostaneme k požadovanému listu. Vezmeme si první.
```csharp
    // Přístup k prvnímu listu
    Worksheet ws = wb.Worksheets[0];
```
Je to přímočaré, ne? K libovolnému listu můžete přistupovat zadáním jeho indexu.
## Krok 5: Nakonfigurujte možnosti obrázku nebo tisku
Nyní definujeme, jak chceme, aby výstupní obrázek vypadal. Nakonfigurujeme možnosti, jako je zajištění jedné stránky pro každý list a určení typu výstupního obrázku.
```csharp
    // Zadejte možnosti obrázku nebo tisku
    ImageOrPrintOptions opts = new ImageOrPrintOptions();
    opts.OnePagePerSheet = true;
    opts.ImageType = Drawing.ImageType.Png;
```
Výběr PNG jako výstupního formátu zajistí, že kvalita zůstane ostrá a jasná!
## Krok 6: Vykreslení listu na obrázek
Když je vše nastaveno, převedeme vybraný pracovní list do souboru obrázku! Toto je ta vzrušující část; uvidíte, jak se váš list Excelu změní na krásný obrázek.
```csharp
    // Vytvořte vykreslení listu předáním požadovaných parametrů
    SheetRender sr = new SheetRender(ws, opts);
    // Převeďte celý svůj pracovní list na obrázek ve formátu PNG
    sr.ToImage(0, outputDir + "outputControlExternalResourcesUsingWorkbookSetting_StreamProvider.png");
    
    Console.WriteLine("ControlExternalResourcesUsingWorkbookSetting_StreamProvider executed successfully.");
}
```
 The`ToImage` funkce převede veškerou těžkou práci a převede list na obrázek. Po dokončení tohoto kroku najdete obrázek uložený ve výstupním adresáři.
## Závěr
A tady to máte! Nyní máte know-how pro ovládání externích zdrojů při práci se soubory Excel pomocí Aspose.Cells v .NET. To nejen rozšíří možnosti vaší aplikace, ale také učiní práci s datovými sadami a prezentacemi hračkou. Podle uvedených kroků můžete tuto funkci snadno replikovat a přizpůsobit tak, aby vyhovovala specifickým potřebám vašeho projektu.
## FAQ
### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna navržená pro vývojáře v C# a .NET k vytváření, manipulaci a správě souborů aplikace Excel bez nutnosti instalace aplikace Microsoft Excel.
### Jak si mohu stáhnout Aspose.Cells pro .NET?
 Můžete si jej stáhnout z[Aspose webové stránky](https://releases.aspose.com/cells/net/).
### Je k dispozici bezplatná zkušební verze?
 Ano! Můžete získat přístup k bezplatné zkušební verzi Aspose.Cells z jejich[stránka vydání](https://releases.aspose.com/).
### Jaké typy souborů Aspose.Cells podporuje?
Aspose.Cells podporuje různé formáty Excelu, včetně XLS, XLSX, CSV a dalších.
### Kde najdu podporu pro Aspose.Cells?
 Fórum podpory Aspose můžete navštívit na adrese[Fórum Aspose](https://forum.aspose.com/c/cells/9) o pomoc.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
