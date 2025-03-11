---
title: Zkopírujte úložiště VBAMacro User Form Designer do sešitu pomocí Aspose.Cells
linktitle: Zkopírujte úložiště VBAMacro User Form Designer do sešitu pomocí Aspose.Cells
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak efektivně kopírovat VBA Macro User Form Designer v Aspose.Cells pro .NET s naším komplexním návodem krok za krokem! Odemkněte potenciál Excelu.
weight: 11
url: /cs/net/workbook-vba-project/copy-vbamacro-user-form-designer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zkopírujte úložiště VBAMacro User Form Designer do sešitu pomocí Aspose.Cells

## Zavedení
Vítejte! Pokud chcete vylepšit své zkušenosti s Excelem pomocí maker VBA a uživatelských formulářů, jste na správném místě! V této příručce se ponoříme do toho, jak můžete hladce zkopírovat VBA Macro UserForm Designer z jednoho sešitu do druhého pomocí Aspose.Cells for .NET. Ať už jste zkušený vývojář nebo teprve začínáte, provedeme vás každým zásadním krokem. Považujte to za svou příručku pro zvládnutí umění programového zpracování souborů aplikace Excel. Jste připraveni se ponořit? Jdeme na to!
## Předpoklady
Než se pustíme do hrubky kódování, ujistěte se, že máte vše, co potřebujete:
1. Vývojové prostředí C#: Měli byste mít připravené pracovní prostředí pro vývoj v C#. Visual Studio je vysoce doporučeno.
2.  Aspose.Cells for .NET Library: Ujistěte se, že máte knihovnu Aspose.Cells integrovanou do vašeho projektu. Můžete snadno[stáhněte si jej zde](https://releases.aspose.com/cells/net/).
3. Základní znalost VBA a Excel maker: Dobrá znalost jazyka VBA a fungování maker Excelu vám pomůže snadno procházet tímto výukovým programem.
4. Excelový soubor s uživatelským formulářem: Chcete-li experimentovat, vytvořte nebo získejte excelový sešit, který obsahuje uživatelský formulář, nejlépe s povolenými makry (např.`.xlsm` soubory).
## Importujte balíčky
Ve svém projektu C# budete muset importovat určité jmenné prostory v horní části souboru, abyste mohli využívat funkce Aspose.Cells. Postup je následující:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Vba;
```
Zahrnutí těchto jmenných prostorů vám umožní přístup ke všem výkonným nástrojům zabudovaným v knihovně Aspose.Cells. 
Nyní, když máme pokryty naše předpoklady a balíčky, je čas přejít na zábavnější část: kódování! Pojďme si to rozebrat krok za krokem.
## Krok 1: Definujte zdrojový a výstupní adresář
Nejprve musíte zjistit, kde se vaše soubory nacházejí:
```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory";
// Výstupní adresář
string outputDir = "Your Document Directory";
```
 Tady, vyměňte`"Your Document Directory"` se skutečnou cestou, kde jsou soubory uloženy. Odtud bude získán náš zdrojový sešit (s UserForm) a kde bude uložen nový sešit.
## Krok 2: Vytvořte prázdný cílový sešit
Dále vytvoříme náš cílový sešit, do kterého budeme kopírovat náš uživatelský formulář a makra:
```csharp
// Vytvořte prázdný cílový sešit
Workbook target = new Workbook();
```
Tento řádek kódu inicializuje nový prázdný sešit, který můžeme naplnit daty. Představte si to jako prázdné plátno pro vaše mistrovské dílo!
## Krok 3: Načtěte sešit šablon
Potřebujeme načíst sešit, který obsahuje váš uživatelský formulář a makra:
```csharp
// Načtěte soubor aplikace Excel obsahující uživatelský formulář VBA-Macro Designer
Workbook templateFile = new Workbook(sourceDir + "sampleDesignerForm.xlsm");
```
 Nezapomeňte změnit`"sampleDesignerForm.xlsm"` na název vašeho skutečného souboru. Tento sešit je jako váš sešit receptů – z něj budeme čerpat ingredience!
## Krok 4: Zkopírujte listy do cílového sešitu
Nyní začněme kopírovat listy z naší šablony do cílového sešitu:
```csharp
// Zkopírujte všechny šablony listů do cílového sešitu
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
V tomto kroku procházíme každý list v šabloně a zkopírujeme je do našeho cílového sešitu. Když se nad tím zamyslíte, je to jako přenášet své nejlepší recepty z jedné kuchařky do druhé!
## Krok 5: Zkopírujte makra VBA ze šablony
Dále zkopírujeme makra VBA, včetně modulů UserForm Designer, do našeho nového sešitu:
```csharp
// Zkopírujte UserForm VBA-Macro Designer ze šablony do cíle
foreach (VbaModule vbaItem in templateFile.VbaProject.Modules)
{
    if (vbaItem.Name == "ThisWorkbook")
    {
        // Zkopírujte kód modulu ThisWorkbook
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
            // Získejte data uživatelského formuláře, tj. úložiště návrháře
            byte[] designerStorage = templateFile.VbaProject.Modules.GetDesignerStorage(vbaItem.Name);
            // Přidejte úložiště návrháře do cílového projektu Vba
            target.VbaProject.Modules.AddDesignerStorage(vbaItem.Name, designerStorage);
        }
    }
}
```
Tento velký kus kódu zpracovává kontrolu každého modulu VBA v souboru šablony. Kopírujeme návrh UserForm a jeho přidružené kódy. Je to jako zajistit, abyste získali nejen babiččin slavný recept na koláč, ale také její přesné techniky pečení!
## Krok 6: Uložte cílový sešit
Poté, co získáme všechny naše kopie, je čas zachránit naši tvrdou práci:
```csharp
// Uložte cílový sešit
target.Save(outputDir + "outputDesignerForm.xlsm", SaveFormat.Xlsm);
```
Ujistěte se, že jste podle potřeby upravili výstupní název souboru. Jakmile jej uložíte, efektivně vytváříte vlastní přizpůsobenou verzi sešitu plnou maker a uživatelských formulářů. Jak vzrušující to je?
## Krok 7: Potvrďte úspěch
Nakonec vytiskněme zprávu o úspěchu do konzole:
```csharp
Console.WriteLine("CopyVBAMacroUserFormDesignerStorageToWorkbook executed successfully.\r\n");
```
Tato malá čára vás ujišťuje, že váš proces proběhl hladce. Je to třešnička na vrcholu vašeho kódovacího poháru!
## Závěr
Gratuluji! Dokončili jste krok za krokem průvodce kopírováním VBA Macro User Form Designer z jednoho sešitu do druhého pomocí Aspose.Cells for .NET. Zpočátku se to může zdát trochu zdrcující, ale s praxí zvládnete manipulaci se sešitem jako profík. Pamatujte, že kódování je o praxi, takže se nemusíte vyhýbat zkoušení různých věcí ve svých souborech Excel. Pokud máte nějaké otázky nebo narazíte na nějaké problémy, neváhejte se podívat na fóra nebo dokumentaci Aspose pro podporu!
## FAQ
### Jaké verze aplikace Excel podporuje Aspose.Cells?
Aspose.Cells podporuje širokou škálu formátů aplikace Excel včetně XLSX, XLSM, CSV a dalších.
### Mohu používat Aspose.Cells zdarma?
 Ano! Můžete začít s bezplatnou zkušební verzí, která vám umožní ohodnotit knihovnu:[Bezplatná zkušební verze](https://releases.aspose.com/).
### Potřebuji ke spuštění tohoto kódu Visual Studio?
když je to vysoce doporučeno kvůli jeho uživatelsky přívětivým funkcím, bude fungovat jakékoli IDE C#, pokud podporuje vývoj .NET.
### Kde najdu další příklady a dokumentaci?
 Můžete prozkoumat[Dokumentace Aspose.Cells](https://reference.aspose.com/cells/net/) pro více příkladů a podrobných vysvětlení.
### Jak vyřeším problémy při používání Aspose.Cells?
 Měli byste navštívit[Aspose Support Forum](https://forum.aspose.com/c/cells/9) za pomoc od komunity a podpůrného personálu Aspose.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
