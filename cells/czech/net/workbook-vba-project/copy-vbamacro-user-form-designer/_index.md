---
"description": "Naučte se, jak efektivně kopírovat návrhář uživatelských formulářů VBA v Aspose.Cells pro .NET s naším komplexním podrobným návodem! Odemkněte potenciál Excelu."
"linktitle": "Zkopírujte úložiště návrháře uživatelských formulářů VBAMacro do sešitu pomocí Aspose.Cells"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Zkopírujte úložiště návrháře uživatelských formulářů VBAMacro do sešitu pomocí Aspose.Cells"
"url": "/cs/net/workbook-vba-project/copy-vbamacro-user-form-designer/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Zkopírujte úložiště návrháře uživatelských formulářů VBAMacro do sešitu pomocí Aspose.Cells

## Zavedení
Vítejte! Pokud chcete vylepšit své prostředí v Excelu pomocí maker VBA a uživatelských formulářů, jste na správném místě! V této příručce se ponoříme do toho, jak můžete bezproblémově kopírovat návrhář uživatelských formulářů maker VBA z jednoho sešitu do druhého pomocí Aspose.Cells pro .NET. Ať už jste zkušený vývojář, nebo teprve začínáte, provedeme vás každým klíčovým krokem. Považujte tuto příručku za svůj způsob, jak zvládnout umění programově manipulovat s excelovými soubory. Jste připraveni se do toho pustit? Pojďme na to!
## Předpoklady
Než se pustíme do detailů kódování, ujistěte se, že máte vše, co potřebujete:
1. Vývojové prostředí C#: Měli byste mít připravené pracovní prostředí pro vývoj v C#. Důrazně se doporučuje Visual Studio.
2. Knihovna Aspose.Cells pro .NET: Ujistěte se, že máte ve svém projektu integrovanou knihovnu Aspose.Cells. Můžete snadno [stáhněte si to zde](https://releases.aspose.com/cells/net/).
3. Základní znalost VBA a maker v Excelu: Dobrá znalost VBA a fungování maker v Excelu vám pomůže s lehkostí se v tomto tutoriálu orientovat.
4. Soubor aplikace Excel s uživatelským formulářem: Pro experimentování vytvořte nebo si získejte sešit aplikace Excel, který obsahuje uživatelský formulář, nejlépe s povolenými makry (například `.xlsm` soubory).
## Importovat balíčky
Ve vašem projektu v C# budete muset importovat určité jmenné prostory na začátek souboru, abyste mohli využívat funkce Aspose.Cells. Zde je návod, jak to udělat:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Vba;
```
Zahrnutí těchto jmenných prostorů vám umožní přístup ke všem výkonným nástrojům obsaženým v knihovně Aspose.Cells. 
Nyní, když máme probrány předpoklady a balíčky, je čas přejít k té zábavné části: kódování! Pojďme si to rozebrat krok za krokem.
## Krok 1: Definujte zdrojové a výstupní adresáře
Nejprve je třeba zjistit, kde se vaše soubory nacházejí:
```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory";
// Výstupní adresář
string outputDir = "Your Document Directory";
```
Zde nahraďte `"Your Document Directory"` se skutečnou cestou, kam jsou uloženy vaše soubory. Odtud bude načten náš zdrojový sešit (s UserForm) a kam bude uložen nový sešit.
## Krok 2: Vytvořte prázdný cílový sešit
Dále si vytvořme cílový sešit, kam budeme kopírovat uživatelský formulář a makra:
```csharp
// Vytvořit prázdný cílový sešit
Workbook target = new Workbook();
```
Tento řádek kódu inicializuje nový, prázdný sešit, který naplníme daty. Představte si ho jako prázdné plátno pro vaše mistrovské dílo!
## Krok 3: Načtěte si šablonu sešitu
Musíme načíst sešit, který obsahuje váš uživatelský formulář a makra:
```csharp
// Načtěte soubor Excel obsahující uživatelský formulář z návrháře maker VBA
Workbook templateFile = new Workbook(sourceDir + "sampleDesignerForm.xlsm");
```
Nezapomeňte změnit `"sampleDesignerForm.xlsm"` k názvu vašeho skutečného souboru. Tento sešit je jako vaše kuchařka – z něj budeme čerpat ingredience!
## Krok 4: Kopírování pracovních listů do cílového sešitu
Nyní začněme kopírovat listy z naší šablony do cílového sešitu:
```csharp
// Zkopírovat všechny šablony listů do cílového sešitu
foreach (Worksheet ws in templateFile.Worksheets)
{
    if (ws.Type == SheetType.Worksheet)
    {
        Worksheet s = target.Worksheets.Add(ws.Name);
        s.Copy(ws);
        // Vložte zprávu do buňky A2 cílového listu
        s.Cells["A2"].PutValue("VBA Macro and User Form copied from template to target.");
    }
}
```
V tomto kroku procházíme každý list v šabloně a kopírujeme je do našeho cílového sešitu. Když se nad tím zamyslíte, je to jako přenášet své nejlepší recepty z jedné kuchařky do druhé!
## Krok 5: Zkopírujte makra VBA ze šablony
Dále zkopírujeme makra VBA, včetně modulů UserForm Designer, do našeho nového sešitu:
```csharp
// Zkopírujte uživatelský formulář v návrháři maker VBA ze šablony do cíle
foreach (VbaModule vbaItem in templateFile.VbaProject.Modules)
{
    if (vbaItem.Name == "ThisWorkbook")
    {
        // Zkopírovat kód modulu ThisWorkbook
        target.VbaProject.Modules["ThisWorkbook"].Codes = vbaItem.Codes;
    }
    else
    {
        // Zkopírujte kód a data ostatních modulů
        System.Diagnostics.Debug.Print(vbaItem.Name);
        int vbaMod = 0;
        Worksheet sheet = target.Worksheets.GetSheetByCodeName(vbaItem.Name);
        if (sheet == null)
        {
            vbaMod = target.VbaProject.Modules.Add(vbaItem.Type, vbaItem.Name);
        }
        else
        {
            vbaMod = target.VbaProject.Modules.Add(sheet);
        }
        target.VbaProject.Modules[vbaMod].Codes = vbaItem.Codes;
        if ((vbaItem.Type == VbaModuleType.Designer))
        {
            // Získejte data z uživatelského formuláře, tj. z úložiště návrháře
            byte[] designerStorage = templateFile.VbaProject.Modules.GetDesignerStorage(vbaItem.Name);
            // Přidání úložiště návrháře do cílového projektu VBA
            target.VbaProject.Modules.AddDesignerStorage(vbaItem.Name, designerStorage);
        }
    }
}
```
Tento pořádný kus kódu se stará o kontrolu každého modulu VBA v souboru šablony. Kopírujeme návrh UserFormu a s ním spojené kódy. Je to, jako byste se ujistili, že nejenže získáte recept na slavný koláč od babičky, ale také její přesné techniky pečení!
## Krok 6: Uložení cílového sešitu
Poté, co dosáhneme všech kopií, je čas ušetřit si naši tvrdou práci:
```csharp
// Uložit cílový sešit
target.Save(outputDir + "outputDesignerForm.xlsm", SaveFormat.Xlsm);
```
Nezapomeňte podle potřeby upravit název výstupního souboru. Po uložení si v podstatě vytvoříte vlastní upravenou verzi sešitu plnou maker a uživatelských formulářů. To je ale vzrušující?
## Krok 7: Potvrzení úspěchu
Nakonec vypíšeme do konzole zprávu o úspěšném provedení:
```csharp
Console.WriteLine("CopyVBAMacroUserFormDesignerStorageToWorkbook executed successfully.\r\n");
```
Tato malá čárka vás ujistí, že celý proces proběhl hladce. Je to třešnička na dortu vašeho programátorského poháru!
## Závěr
Gratulujeme! Dokončili jste podrobný návod, jak kopírovat návrhář uživatelských formulářů maker VBA z jednoho sešitu do druhého pomocí Aspose.Cells pro .NET. Zpočátku se to může zdát trochu složité, ale s praxí zvládnete manipulaci se sešity jako profesionál. Nezapomeňte, že kódování je o cviku, takže se nebojte zkoušet různé věci v souborech Excelu. Pokud máte jakékoli dotazy nebo narazíte na nějaké problémy, neváhejte se podívat na fóra nebo dokumentaci Aspose, kde vám pomohou!
## Často kladené otázky
### Jaké verze Excelu podporuje Aspose.Cells?
Aspose.Cells podporuje širokou škálu formátů Excelu, včetně XLSX, XLSM, CSV a dalších.
### Mohu používat Aspose.Cells zdarma?
Ano! Můžete začít s bezplatnou zkušební verzí, která vám umožní otestovat knihovnu: [Bezplatná zkušební verze](https://releases.aspose.com/).
### Potřebuji Visual Studio ke spuštění tohoto kódu?
I když je velmi doporučován kvůli svým uživatelsky přívětivým funkcím, postačí jakékoli C# IDE, pokud podporuje vývoj v .NET.
### Kde najdu další příklady a dokumentaci?
Můžete prozkoumat [Dokumentace k Aspose.Cells](https://reference.aspose.com/cells/net/) pro další příklady a podrobnější vysvětlení.
### Jak vyřeším problémy s používáním Aspose.Cells?
Měli byste navštívit [Fórum podpory Aspose](https://forum.aspose.com/c/cells/9) za pomoc od komunity a podpůrného personálu Aspose.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}