---
"description": "Naučte se, jak ovládat externí zdroje v Excelu pomocí Aspose.Cells pro .NET s naším komplexním podrobným tutoriálem."
"linktitle": "Ovládání externích zdrojů pomocí nastavení sešitu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Ovládání externích zdrojů pomocí nastavení sešitu"
"url": "/cs/net/workbook-settings/control-external-resources/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ovládání externích zdrojů pomocí nastavení sešitu

## Zavedení
oblasti manipulace s daty a jejich prezentace může být efektivní nakládání s externími zdroji zásadní. Pokud pracujete s excelovými soubory a chcete bezproblémově spravovat externí zdroje pomocí Aspose.Cells pro .NET, jste na správném místě! V tomto článku se podrobně ponoříme do správy externích zdrojů při práci s excelovými sešity. Po čtení této příručky budete schopni implementovat přizpůsobené řešení pro snadné načítání obrázků a dat z externích zdrojů.
## Předpoklady
Než se pustíme do detailů kódování, je třeba splnit několik předpokladů. Ujistěte se, že:
1. Mějte nainstalované Visual Studio: Pro psaní a testování .NET aplikací budete potřebovat IDE. Visual Studio je nejvíce doporučovanou volbou díky své rozsáhlé podpoře a snadnému použití.
2. Stáhněte si Aspose.Cells pro .NET: Pokud jste tak ještě neučinili, stáhněte si knihovnu Aspose.Cells z [odkaz ke stažení](https://releases.aspose.com/cells/net/). 
3. Základní znalost C#: Znalost konceptů C# a .NET frameworku vám celý proces usnadní.
4. Nastavení prostředí: Ujistěte se, že váš projekt odkazuje na knihovnu Aspose.Cells. To můžete provést pomocí Správce balíčků NuGet v aplikaci Visual Studio.
5. Ukázkové soubory: Mějte připravený ukázkový soubor aplikace Excel, který obsahuje externí zdroj, například odkazovaný obrázek. Tento soubor pomůže demonstrovat funkce, o kterých budeme diskutovat.
Jakmile si je nastavíte, můžete se ponořit do ovládání externích zdrojů pomocí Aspose.Cells.
## Importovat balíčky
Abyste mohli začít s kódováním, budete muset importovat potřebné balíčky do souboru C#. Zde je to, co budete potřebovat:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
Tyto jmenné prostory poskytují přístup k funkcím potřebným pro manipulaci s excelovými soubory a obrázky.
Rozdělme si to na zvládnutelné kroky, které vám pomohou kontrolovat externí zdroje pomocí `Workbook Settings`Projdeme si vytvořením vlastního poskytovatele streamu, načtením souboru aplikace Excel a vykreslením pracovního listu do obrázku. Neváhejte a sledujte nás!
## Krok 1: Definování zdrojového a výstupního adresáře
Pro začátek musíme specifikovat adresáře, ze kterých budeme číst soubory a kam budeme ukládat výstup. Je nezbytné nastavit správné cesty, abychom se vyhnuli chybám „soubor nebyl nalezen“.
```csharp
// Zdrojový adresář
static string sourceDir = "Your Document Directory";
// Výstupní adresář
static string outputDir = "Your Document Directory";
```
Nahradit `"Your Document Directory"` se skutečnou cestou, kde se vaše soubory nacházejí.
## Krok 2: Implementace rozhraní IStreamProvider
Dále vytvoříme vlastní třídu, která implementuje `IStreamProvider` rozhraní. Tato třída bude spravovat, jak se přistupuje k externím zdrojům (například obrázkům).
```csharp
class SP : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        // V případě potřeby vyčistěte veškeré zdroje
    }
    public void InitStream(StreamProviderOptions options)
    {
        // Otevřete datový proud externího zdroje
        FileStream fi = new FileStream(sourceDir + "sampleControlExternalResourcesUsingWorkbookSetting_StreamProvider.png", FileMode.OpenOrCreate, FileAccess.Read);
        options.Stream = fi;
    }
}
```
V `InitStream` metodou otevřeme soubor, který slouží jako náš externí zdroj, a přiřadíme ho k `Stream` vlastnost. To umožňuje sešitu přístup k prostředku při vykreslování.
## Krok 3: Načtěte soubor Excel
Nyní, když máme připraveného poskytovatele streamu, načtěme sešit aplikace Excel, který obsahuje externí zdroj.
```csharp
public static void Run()
{
    // Načíst ukázkový soubor Excel
    Workbook wb = new Workbook(sourceDir + "sampleControlExternalResourcesUsingWorkbookSetting_StreamProvider.xlsx");
    
    // Poskytněte svou implementaci IStreamProvider
    wb.Settings.StreamProvider = new SP();
```
V tomto úryvku kódu načteme náš soubor Excel a přiřadíme mu vlastní `StreamProvider` implementace pro práci s externími zdroji.
## Krok 4: Přístup k pracovnímu listu
Po načtení sešitu se snadno dostaneme k požadovanému listu. Vezměme si první z nich.
```csharp
    // Přístup k prvnímu listu
    Worksheet ws = wb.Worksheets[0];
```
Je to jednoduché, že? K libovolnému listu se dostanete zadáním jeho indexu.
## Krok 5: Konfigurace možností obrázku nebo tisku
Nyní definujeme, jak má výstupní obrázek vypadat. Nakonfigurujeme možnosti, jako je zajištění jedné stránky pro každý list a určení typu výstupního obrázku.
```csharp
    // Zadejte možnosti obrázku nebo tisku
    ImageOrPrintOptions opts = new ImageOrPrintOptions();
    opts.OnePagePerSheet = true;
    opts.ImageType = Drawing.ImageType.Png;
```
Výběr PNG jako výstupního formátu zajistí, že kvalita zůstane ostrá a jasná!
## Krok 6: Vykreslení pracovního listu do obrázku
Jakmile je vše nastaveno, pojďme vykreslit vybraný pracovní list do obrazového souboru! Tohle je ta vzrušující část; uvidíte, jak se váš excelový list promění v krásný obrázek.
```csharp
    // Vytvořte render listu předáním požadovaných parametrů
    SheetRender sr = new SheetRender(ws, opts);
    // Převeďte celý pracovní list do formátu PNG
    sr.ToImage(0, outputDir + "outputControlExternalResourcesUsingWorkbookSetting_StreamProvider.png");
    
    Console.WriteLine("ControlExternalResourcesUsingWorkbookSetting_StreamProvider executed successfully.");
}
```
Ten/Ta/To `ToImage` Funkce provede veškerou těžkou práci a převede list na obrázek. Jakmile je tento krok dokončen, najdete obrázek uložený ve výstupním adresáři.
## Závěr
A tady to máte! Nyní máte know-how pro správu externích zdrojů při práci s excelovými soubory pomocí Aspose.Cells v .NET. To nejen vylepší možnosti vaší aplikace, ale také zjednoduší práci s datovými sadami a prezentacemi. Dodržováním uvedených kroků můžete tuto funkcionalitu snadno replikovat a přizpůsobit specifickým potřebám vašeho projektu.
## Často kladené otázky
### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna určená pro vývojáře v C# a .NET, která umožňuje vytvářet, manipulovat a spravovat soubory aplikace Excel bez nutnosti instalace aplikace Microsoft Excel.
### Jak si mohu stáhnout Aspose.Cells pro .NET?
Můžete si ho stáhnout z [Webové stránky Aspose](https://releases.aspose.com/cells/net/).
### Je k dispozici bezplatná zkušební verze?
Ano! Zkušební verzi Aspose.Cells si můžete zdarma stáhnout od nich. [stránka s vydáním](https://releases.aspose.com/).
### Jaké typy souborů Aspose.Cells podporuje?
Aspose.Cells podporuje různé formáty Excelu, včetně XLS, XLSX, CSV a dalších.
### Kde najdu podporu pro Aspose.Cells?
Fórum podpory Aspose můžete navštívit na adrese [Fórum Aspose](https://forum.aspose.com/c/cells/9) o pomoc.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}