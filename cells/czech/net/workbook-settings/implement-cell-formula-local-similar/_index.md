---
"description": "Zjistěte, jak implementovat vzorec buňky, který je podobný lokální funkci vzorce rozsahu v Aspose.Cells pro .NET. Naučte se přizpůsobovat názvy vestavěných funkcí Excelu a další."
"linktitle": "Implementace lokálního vzorce buňky podobně jako lokální vzorec rozsahu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Implementace lokálního vzorce buňky podobně jako lokální vzorec rozsahu"
"url": "/cs/net/workbook-settings/implement-cell-formula-local-similar/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Implementace lokálního vzorce buňky podobně jako lokální vzorec rozsahu

## Zavedení
Aspose.Cells pro .NET je výkonné a flexibilní API pro manipulaci s tabulkami, které umožňuje programově vytvářet, manipulovat a převádět soubory aplikace Excel. Jednou z mnoha funkcí, které Aspose.Cells nabízí, je možnost přizpůsobit chování vestavěných funkcí aplikace Excel, včetně možnosti vytvářet si vlastní lokální názvy funkcí. V tomto tutoriálu vás provedeme kroky k implementaci vzorce buňky, který je podobný lokální funkci vzorce pro rozsah v Aspose.Cells pro .NET.
## Předpoklady
Než začnete, ujistěte se, že máte následující:
1. V systému je nainstalován Microsoft Visual Studio 2010 nebo novější.
2. Nejnovější verze knihovny Aspose.Cells pro .NET nainstalovaná ve vašem projektu. Knihovnu si můžete stáhnout z [Stránka ke stažení Aspose.Cells pro .NET](https://releases.aspose.com/cells/net/).
## Importovat balíčky
Chcete-li začít, budete muset do svého projektu C# importovat potřebné balíčky. Na začátek souboru s kódem přidejte následující příkazy using:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Krok 1: Vytvoření vlastní třídy nastavení globalizace
Prvním krokem je vytvoření vlastního `GlobalizationSettings` třída, která vám umožní přepsat výchozí chování funkcí aplikace Excel. V tomto příkladu změníme názvy `SUM` a `AVERAGE` funkce pro `UserFormulaLocal_SUM` a `UserFormulaLocal_AVERAGE`, v uvedeném pořadí.
```csharp
class GS : GlobalizationSettings
{
    public override string GetLocalFunctionName(string standardName)
    {
        //Změňte název funkce SUM podle svých potřeb.
        if (standardName == "SUM")
        {
            return "UserFormulaLocal_SUM";
        }
        //Změňte název funkce AVERAGE podle svých potřeb.
        if (standardName == "AVERAGE")
        {
            return "UserFormulaLocal_AVERAGE";
        }
        return "";
    }
}
```
## Krok 2: Vytvořte nový sešit a přiřaďte mu vlastní nastavení globalizace
Dále vytvořte novou instanci sešitu a přiřaďte jí vlastní `GlobalizationSettings` implementační třída do sešitu `Settings.GlobalizationSettings` vlastnictví.
```csharp
//Vytvořit sešit
Workbook wb = new Workbook();
//Přiřadit implementační třídu GlobalizationSettings
wb.Settings.GlobalizationSettings = new GS();
```
## Krok 3: Přístup k prvnímu pracovnímu listu a buňce
Nyní se podívejme na první list v sešitu a na konkrétní buňku v tomto listu.
```csharp
//Přístup k prvnímu listu
Worksheet ws = wb.Worksheets[0];
//Přístup k nějaké buňce
Cell cell = ws.Cells["C4"];
```
## Krok 4: Přiřazení vzorců a výpis místního vzorce
Nakonec přiřaďme `SUM` a `AVERAGE` vzorce do buňky a vytiskněte výsledek `FormulaLocal` hodnoty.
```csharp
//Přiřaďte vzorec SUMA a vytiskněte jeho FormulaLocal
cell.Formula = "SUM(A1:A2)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
//Přiřaďte vzorec AVERAGE a vytiskněte jeho FormulaLocal
cell.Formula = "=AVERAGE(B1:B2, B5)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
```
## Závěr
V tomto tutoriálu jste se naučili, jak implementovat vzorec buňky, který je podobný lokální funkci vzorce rozsahu v Aspose.Cells pro .NET. Vytvořením vlastního `GlobalizationSettings` třídy můžete přepsat výchozí chování funkcí aplikace Excel a přizpůsobit lokální názvy funkcí svým potřebám. To může být obzvláště užitečné při práci s lokalizovanými nebo internacionalizovanými dokumenty aplikace Excel.
## Často kladené otázky
### Jaký je účel `GlobalizationSettings` třída v Aspose.Cells?
Ten/Ta/To `GlobalizationSettings` Třída v Aspose.Cells umožňuje přizpůsobit chování vestavěných funkcí aplikace Excel, včetně možnosti změnit lokální názvy funkcí.
### Mohu přepsat chování jiných funkcí než `SUM` a `AVERAGE`?
Ano, chování libovolné vestavěné funkce aplikace Excel můžete přepsat úpravou `GetLocalFunctionName` metoda ve vašem vlastním `GlobalizationSettings` třída.
### Existuje způsob, jak obnovit výchozí hodnoty názvů funkcí?
Ano, názvy funkcí můžete resetovat buď odstraněním vlastních `GlobalizationSettings` třídy nebo vrácením prázdného řetězce z `GetLocalFunctionName` metoda.
### Mohu tuto funkci použít k vytváření vlastních funkcí v Aspose.Cells?
Ne, ten `GlobalizationSettings` Třída je navržena tak, aby přepsala chování vestavěných funkcí aplikace Excel, nikoliv k vytváření vlastních funkcí. Pokud potřebujete vytvořit vlastní funkce, můžete použít `UserDefinedFunction` třída v Aspose.Cells.
### Je tato funkce dostupná ve všech verzích Aspose.Cells pro .NET?
Ano, `GlobalizationSettings` Třída a možnost úpravy názvů funkcí je k dispozici ve všech verzích Aspose.Cells pro .NET.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}