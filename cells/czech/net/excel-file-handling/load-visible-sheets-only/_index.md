---
title: Načíst pouze viditelné listy ze souboru aplikace Excel
linktitle: Načíst pouze viditelné listy ze souboru aplikace Excel
second_title: Aspose.Cells .NET Excel Processing API
description: V tomto podrobném průvodci se dozvíte, jak načíst pouze viditelné listy ze souborů aplikace Excel pomocí Aspose.Cells for .NET.
weight: 12
url: /cs/net/excel-file-handling/load-visible-sheets-only/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Načíst pouze viditelné listy ze souboru aplikace Excel

## Zavedení
Když pracujete se soubory Excelu ve svých aplikacích .NET, problém se správou více listů se stává zřejmým, zvláště když jsou některé skryté nebo nejsou pro vaši operaci relevantní. Aspose.Cells for .NET je výkonná knihovna, která vám pomůže efektivně manipulovat se soubory aplikace Excel. V tomto článku prozkoumáme, jak načíst pouze viditelné listy ze souboru aplikace Excel a odfiltrovat veškerá skrytá data. Pokud jste se někdy cítili zahlceni procházením dat aplikace Excel, tento průvodce je pro vás!
## Předpoklady
Než se pustíte do výukového programu, ujistěte se, že máte vše, co potřebujete, abyste se řídili:
1. Základní porozumění C#: Tento tutoriál je určen pro vývojáře obeznámené s programovacím jazykem C#.
2.  Aspose.Cells for .NET: Musíte mít staženou a nastavenou knihovnu Aspose.Cells for .NET. Můžete[stáhněte si knihovnu zde](https://releases.aspose.com/cells/net/).
3. Visual Studio nebo jakékoli IDE: Měli byste mít IDE, kde můžete psát a testovat svůj kód C#.
4. .NET Framework: Ujistěte se, že máte nainstalovaný nezbytný .NET Framework pro spouštění aplikací.
5. Vzorový soubor Excel: Pro procvičení vytvořte vzorový soubor Excel nebo postupujte podle poskytnutého kódu.
Máte vše připraveno? Děsivý! Jdeme do toho!
## Importujte balíčky
Jedním z prvních kroků v jakémkoli C# projektu pracujícím s Aspose.Cells je import požadovaných balíčků. To vám umožní přístup ke všem funkcím, které knihovna poskytuje. Jak na to:
1. Otevřete svůj projekt: Začněte otevřením projektu C# v sadě Visual Studio nebo jiném preferovaném IDE.
2. Přidat reference: Klikněte pravým tlačítkem na svůj projekt v Průzkumníku řešení, vyberte "Přidat" a poté "Odkaz." 
3. Vyhledat Aspose.Cells: Vyhledejte soubor Aspose.Cells.dll, který jste stáhli dříve, a přidejte jej do referencí projektu.
Tento krok je zásadní, protože propojuje funkci Aspose.Cells s vaším projektem. 
```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Nyní, když jste naimportovali potřebné balíčky, vytvoříme vzorový excelový sešit. V tomto sešitu budeme mít více listů a jeden z nich bude pro tento tutoriál skrytý.
## Krok 1: Nastavte své prostředí
Nejprve nastavíme prostředí a určíme cesty pro ukázkový soubor.
```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
string sampleFile = "output.xlsx";
string samplePath = dataDir + sampleFile;
```
 V tomto fragmentu kódu nahraďte`"Your Document Directory"` se skutečnou cestou, kam chcete sešit uložit. 
## Krok 2: Vytvořte sešit
Dále vytvoříme sešit a přidáme nějaká data.
```csharp
// Vytvořte vzorový sešit
Workbook createWorkbook = new Workbook();
createWorkbook.Worksheets["Sheet1"].Cells["A1"].Value = "Aspose";
createWorkbook.Worksheets.Add("Sheet2").Cells["A1"].Value = "Aspose";
createWorkbook.Worksheets.Add("Sheet3").Cells["A1"].Value = "Aspose";
createWorkbook.Worksheets["Sheet3"].IsVisible = false; // Skrýt List3
createWorkbook.Save(samplePath);
```
Zde je rozpis toho, co se děje:
- Vytváříme nový sešit a přidáváme tři listy.
- „Sheet1“ a „Sheet2“ budou viditelné, zatímco „Sheet3“ bude skrytý.
- Sešit pak uložíme na zadanou cestu.
## Krok 3: Načtěte ukázkový sešit s možnostmi načtení
Nyní, když máme sešit s viditelnými a skrytými listy, je čas jej načíst a zajistit, abychom měli přístup pouze k viditelným listům.
```csharp
LoadOptions loadOptions = new LoadOptions();
loadOptions.LoadFilter = new CustomLoad();
```
Tento fragment kódu nastavuje možnosti načítání pro sešit, který přizpůsobíme tak, aby odfiltroval skryté listy.
## Krok 4: Definujte vlastní filtr zatížení
Chcete-li načíst pouze viditelné listy, musíme vytvořit vlastní filtr načítání. Zde je návod, jak jej definovat:
```csharp
class CustomLoad : LoadFilter
{
    public override void StartSheet(Worksheet sheet)
    {
        if (sheet.IsVisible)
        {
            this.LoadDataFilterOptions = LoadDataFilterOptions.All;
        }
        else
        {
            this.LoadDataFilterOptions = LoadDataFilterOptions.Structure;
        }
    }
}
```
-  The`StartSheet` metoda kontroluje, zda je každý list viditelný.
- Pokud je viditelný, načte všechna data z tohoto listu.
- Pokud není vidět, přeskočí načítání dat z tohoto listu.
## Krok 5: Načtěte sešit pomocí možností načíst
Nyní načteme sešit a zobrazíme data z viditelných listů.
```csharp
Workbook loadWorkbook = new Workbook(samplePath, loadOptions);
Console.WriteLine("Sheet1: A1: {0}", loadWorkbook.Worksheets["Sheet1"].Cells["A1"].Value);
Console.WriteLine("Sheet2: A1: {0}", loadWorkbook.Worksheets["Sheet2"].Cells["A1"].Value);
```
 Tento fragment kódu využívá`loadOptions` importovat data pouze z viditelných listů a zobrazit obsah buňky A1 z „List1“ a „List2“. 
## Závěr
tady to máte! Úspěšně jste se naučili, jak načíst pouze viditelné listy ze souboru aplikace Excel pomocí Aspose.Cells for .NET. Správa excelových listů může být hračkou, když víte, jak omezit načítaná data a pracovat pouze s tím, co potřebujete. To nejen zlepšuje efektivitu vašich aplikací, ale také činí váš kód čistším a snadněji spravovatelným. 
## FAQ
### Mohu v případě potřeby vložit skryté listy?
Ano, můžete jednoduše upravit podmínky ve vlastním filtru zatížení tak, aby zahrnoval skryté listy.
### K čemu se Aspose.Cells používá?
Aspose.Cells se používá pro manipulaci se soubory aplikace Excel bez nutnosti instalace aplikace Microsoft Excel a nabízí funkce, jako je čtení, psaní a správa listů aplikace Excel.
### Existuje zkušební verze Aspose.Cells?
 Ano, můžete[stáhnout zkušební verzi zdarma](https://releases.aspose.com/) vyzkoušet jeho vlastnosti.
### Kde najdu dokumentaci pro Aspose.Cells?
 The[dokumentace](https://reference.aspose.com/cells/net/) poskytuje komplexní informace o všech funkcích.
### Jak koupím Aspose.Cells?
 Můžete snadno[koupit Aspose.Cells](https://purchase.aspose.com/buy) z jejich nákupní stránky.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
