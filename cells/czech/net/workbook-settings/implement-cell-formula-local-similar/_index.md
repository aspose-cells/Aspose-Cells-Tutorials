---
title: Implementujte vzorec buňky Local Podobné jako Vzorec rozsahu Local
linktitle: Implementujte vzorec buňky Local Podobné jako Vzorec rozsahu Local
second_title: Aspose.Cells .NET Excel Processing API
description: Zjistěte, jak implementovat vzorec buňky, který je podobný místní funkčnosti vzorce rozsahu v Aspose.Cells for .NET. Naučte se přizpůsobit vestavěné názvy funkcí aplikace Excel a další.
weight: 13
url: /cs/net/workbook-settings/implement-cell-formula-local-similar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Implementujte vzorec buňky Local Podobné jako Vzorec rozsahu Local

## Zavedení
Aspose.Cells for .NET je výkonné a flexibilní rozhraní API pro manipulaci s tabulkami, které umožňuje programově vytvářet, manipulovat a převádět soubory aplikace Excel. Jednou z mnoha funkcí, které Aspose.Cells nabízí, je možnost přizpůsobit chování vestavěných funkcí aplikace Excel, včetně možnosti vytvářet vlastní názvy místních funkcí. V tomto tutoriálu vás provedeme kroky k implementaci vzorce buňky, který je podobný místní funkčnosti vzorce rozsahu v Aspose.Cells for .NET.
## Předpoklady
Než začnete, ujistěte se, že máte následující:
1. Microsoft Visual Studio 2010 nebo novější nainstalované ve vašem systému.
2.  Nejnovější verze knihovny Aspose.Cells for .NET nainstalovaná ve vašem projektu. Knihovnu si můžete stáhnout z[Stránka ke stažení Aspose.Cells for .NET](https://releases.aspose.com/cells/net/).
## Importujte balíčky
Chcete-li začít, budete muset importovat potřebné balíčky do svého projektu C#. Přidejte následující příkazy pomocí příkazů v horní části souboru kódu:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Krok 1: Vytvořte vlastní třídu nastavení globalizace
 Prvním krokem je vytvořit vlastní`GlobalizationSettings`třídy, která vám umožní přepsat výchozí chování funkcí aplikace Excel. V tomto příkladu změníme názvy`SUM` a`AVERAGE` funkce k`UserFormulaLocal_SUM` a`UserFormulaLocal_AVERAGE`, resp.
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
        //Změňte název funkce PRŮMĚR podle svých potřeb.
        if (standardName == "AVERAGE")
        {
            return "UserFormulaLocal_AVERAGE";
        }
        return "";
    }
}
```
## Krok 2: Vytvořte nový sešit a přiřaďte vlastní nastavení globalizace
 Dále vytvořte novou instanci sešitu a přiřaďte vlastní`GlobalizationSettings` implementační třídy do sešitu`Settings.GlobalizationSettings` vlastnictví.
```csharp
//Vytvořte sešit
Workbook wb = new Workbook();
//Přiřaďte implementační třídu GlobalizationSettings
wb.Settings.GlobalizationSettings = new GS();
```
## Krok 3: Přístup k prvnímu listu a buňce
Nyní zpřístupníme první list v sešitu a konkrétní buňku v tomto listu.
```csharp
//Přístup k prvnímu listu
Worksheet ws = wb.Worksheets[0];
//Přístup k nějaké buňce
Cell cell = ws.Cells["C4"];
```
## Krok 4: Přiřaďte vzorce a vytiskněte FormulaLocal
 Nakonec přiřadíme`SUM` a`AVERAGE` vzorce do buňky a vytisknout výsledek`FormulaLocal` hodnoty.
```csharp
//Přiřaďte vzorec SUM a vytiskněte jeho FormulaLocal
cell.Formula = "SUM(A1:A2)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
//Přiřaďte AVERAGE vzorec a vytiskněte jeho FormulaLocal
cell.Formula = "=AVERAGE(B1:B2, B5)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
```
## Závěr
 tomto kurzu jste se naučili, jak implementovat vzorec buňky, který je podobný místní funkčnosti vzorce rozsahu v Aspose.Cells for .NET. Vytvořením zvyku`GlobalizationSettings` třídy, můžete přepsat výchozí chování funkcí aplikace Excel a upravit názvy místních funkcí tak, aby vyhovovaly vašim potřebám. To může být užitečné zejména při práci s lokalizovanými nebo internacionalizovanými dokumenty aplikace Excel.
## FAQ
###  Jaký je účel`GlobalizationSettings` class in Aspose.Cells?
 The`GlobalizationSettings` třída v Aspose.Cells umožňuje přizpůsobit chování vestavěných funkcí aplikace Excel, včetně možnosti změnit názvy místních funkcí.
###  Mohu přepsat chování jiných funkcí než`SUM` and `AVERAGE`?
 Ano, můžete přepsat chování jakékoli vestavěné funkce aplikace Excel úpravou`GetLocalFunctionName` způsob ve vašem zvyku`GlobalizationSettings` třída.
### Existuje způsob, jak obnovit názvy funkcí zpět na jejich výchozí hodnoty?
 Ano, názvy funkcí můžete resetovat buď odebráním vlastního`GlobalizationSettings` třídy nebo vrácením prázdného řetězce z`GetLocalFunctionName` metoda.
### Mohu tuto funkci použít k vytvoření vlastních funkcí v Aspose.Cells?
 Ne,`GlobalizationSettings`třída je navržena tak, aby potlačila chování vestavěných funkcí aplikace Excel, nikoli k vytvoření vlastních funkcí. Pokud potřebujete vytvořit vlastní funkce, můžete použít`UserDefinedFunction` třídy v Aspose.Cells.
### Je tato funkce dostupná ve všech verzích Aspose.Cells pro .NET?
 Ano,`GlobalizationSettings` třída a možnost přizpůsobit názvy funkcí je k dispozici ve všech verzích Aspose.Cells pro .NET.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
