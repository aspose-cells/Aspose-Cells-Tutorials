---
title: Nahraďte značku textem v textovém poli v aplikaci Excel
linktitle: Nahraďte značku textem v textovém poli v aplikaci Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Bez námahy nahraďte text v textových polích v listech aplikace Excel pomocí Aspose.Cells pro .NET. Podrobný průvodce automatizací Excelu.
weight: 11
url: /cs/net/excel-shape-text-modifications/replace-tag-text-textbox-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nahraďte značku textem v textovém poli v aplikaci Excel

## Zavedení
V tomto článku se ponoříme do konkrétního úkolu: nahrazení značek textem uvnitř textových polí v listu aplikace Excel pomocí Aspose.Cells. Provedeme vás celým procesem krok za krokem a zajistíme, že pochopíte každý detail. Na konci tohoto tutoriálu si nejen prohloubíte porozumění Aspose.Cells, ale také zjednodušíte své úkoly související s Excelem!
## Předpoklady
Než začnete, musíte si připravit několik věcí:
1. Visual Studio: Ujistěte se, že máte nainstalované Visual Studio. Je to flexibilní IDE, díky kterému je kódování v C# hračkou.
2.  Knihovna Aspose.Cells: Pokud jste tak ještě neučinili, stáhněte si knihovnu Aspose.Cells pro .NET z webu[strana](https://releases.aspose.com/cells/net/)Můžete také získat bezplatnou zkušební verzi a vyzkoušet její funkce.
3. Základní znalost C#: Základní znalost programování v C# vám pomůže snadno postupovat podle tohoto průvodce.
Nyní, když je vše připraveno, přejděme k zábavnější části – psaní kódu!
## Importujte balíčky
První věci – importujme potřebné balíčky. To je zásadní, protože bez správných importů váš kód nerozpozná třídy a metody, které budeme používat.
## Spusťte svůj projekt C#
Otevřete Visual Studio a vytvořte nový projekt C#, nejlépe aplikaci konzoly, protože vám umožní snadno zobrazit výstup.
## Přidejte odkaz Aspose.Cells
- Klikněte pravým tlačítkem na svůj projekt v Průzkumníku řešení.
- Vyberte „Přidat“ > „Odkaz“.
- Přejděte do umístění, kam jste stáhli knihovnu Aspose.Cells, a zahrňte ji do svého projektu.
## Importujte potřebné jmenné prostory
 Po přidání reference přidejte následující`using` direktiva v horní části vašeho hlavního souboru:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
To vám umožní přístup ke třídám v oboru názvů Aspose.Cells.
Nyní, když jsme nastavili naše prostředí, pojďme se pustit do šťavnaté části – kódování! Naším cílem je najít konkrétní značky v textových polích v souboru aplikace Excel a nahradit je poskytnutým textem.
## Krok 1: Definujte zdrojový a výstupní adresář
Nejprve musíme určit, kde se nachází náš zdrojový soubor Excel a kam chceme upravenou verzi uložit.
```csharp
// Zdrojový a výstupní adresář
string sourceDir = "Your Document Directory"; // Přejděte do svého adresáře
string outputDir = "Your Document Directory"; // Přejděte do svého adresáře
```
## Krok 2: Načtěte sešit
Zde načteme náš excelový sešit. Pokud soubor neexistuje, vyvolá chybu. Ujistěte se tedy, že cesta k souboru je správná!
```csharp
Workbook wb = new Workbook(sourceDir + "sampleReplaceTagWithText.xlsx");
```
 Zde načítáme existující soubor aplikace Excel s názvem`sampleReplaceTagWithText.xlsx`.
## Krok 3: Definujte značky a náhradní text
Dále musíme definovat značky, které hledáme a čím je chceme nahradit.
```csharp
string tag = "TAG_2$TAG_1";
string replace = "1$ys";
```
 V tomto příkladu jsou značky rozděleny pomocí`$`. Můžete jej nahradit libovolným oddělovačem, který preferujete.
## Krok 4: Otočte značky a vyměňte je
Vytvoříme smyčku, která projde každou značku, kterou chceme nahradit. Tady se děje kouzlo!
```csharp
for (int i = 0; i < tag.Split('$').Length; i++)
{
    sheetReplace(wb, "<" + tag.Split('$')[i] + ">", replace.Split('$')[i]);
}
```
## Krok 5: Uložte sešit
Nyní, když jsme provedli naše náhrady, je čas uložit upravený sešit do požadovaného formátu. Zde je návod, jak jej převedeme do PDF.
```csharp
PdfSaveOptions opts = new PdfSaveOptions();
wb.Save(outputDir + "outputReplaceTagWithText.pdf", opts);
```
Můžete jej také uložit v různých dalších formátech, včetně XLSX.
## Krok 6: Implementujte náhradní logiku
 Zde sídlí jádro naší funkčnosti. The`sheetReplace` metoda zvládne skutečnou výměnu v excelových listech.
```csharp
public static void sheetReplace(Workbook workbook, string sFind, string sReplace)
{
    string finding = sFind;
    foreach (Worksheet sheet in workbook.Worksheets)
    {
        sheet.Replace(finding, sReplace);
        for (int j = 0; j < 3; j++)
        {
            if (sheet.PageSetup.GetHeader(j) != null)
                sheet.PageSetup.SetHeader(j, sheet.PageSetup.GetHeader(j).Replace(finding, sReplace));
                
            if (sheet.PageSetup.GetFooter(j) != null)
                sheet.PageSetup.SetFooter(j, sheet.PageSetup.GetFooter(j).Replace(finding, sReplace));
        }
    }
    foreach (Worksheet sheet in workbook.Worksheets)
    {
        sFind = sFind.Replace("<", "&lt;");
        sFind = sFind.Replace(">", "&gt;");
        foreach (Aspose.Cells.Drawing.TextBox mytextbox in sheet.TextBoxes)
        {
            if (mytextbox.HtmlText != null)
            {
                if (mytextbox.HtmlText.IndexOf(sFind) >= 0)
                {
                    mytextbox.HtmlText = mytextbox.HtmlText.Replace(sFind, sReplace);
                }
            }
        }
    }
}
```
- Nejprve procházíme každý list v sešitu.
- Hlavní tag nahrazujeme nejen v obsahu buňky, ale také v záhlaví a zápatí (pokud existují).
- Nakonec zkontrolujeme každé textové pole v listu a nahradíme text v nich na základě značky, kterou hledáme.
## Závěr
voila! Nyní jste se naučili, jak nahradit tagy textem v textových polích v dokumentech aplikace Excel pomocí Aspose.Cells for .NET. To může být skutečnou úsporou času, zejména při řešení opakujících se úkolů v tabulkách.
## FAQ
### Mohu nahradit značky ve více souborech aplikace Excel najednou?
Ano, procházením seznamu souborů můžete použít stejnou logiku na více souborů aplikace Excel.
### Potřebuji k používání Aspose.Cells placenou licenci?
 Můžete začít s bezplatnou zkušební verzí, ale pro plnou funkčnost si budete muset zakoupit licenci. Podívejte se[Možnosti nákupu Aspose](https://purchase.aspose.com/buy).
### Mohu nahradit obrázky v textových polích pomocí Aspose.Cells?
Aspose.Cells se primárně zabývá textem. V případě potřeby však můžete s obrázky manipulovat samostatně.
### V jakých formátech mohu uložit svůj upravený soubor Excel?
Můžete jej uložit v různých formátech včetně XLSX, PDF, CSV atd.
### Kde najdu podporu pro Aspose.Cells?
 Podporu a dotazy můžete najít na[Aspose fórum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
