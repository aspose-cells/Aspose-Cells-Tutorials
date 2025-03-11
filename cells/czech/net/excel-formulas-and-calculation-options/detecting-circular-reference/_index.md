---
title: Programově zjišťování kruhových odkazů v Excelu
linktitle: Programově zjišťování kruhových odkazů v Excelu
second_title: Aspose.Cells .NET Excel Processing API
description: Snadno zjistěte kruhové odkazy v aplikaci Excel pomocí Aspose.Cells pro .NET. Postupujte podle našeho podrobného průvodce, abyste zajistili přesné výpočty ve svých tabulkách.
weight: 13
url: /cs/net/excel-formulas-and-calculation-options/detecting-circular-reference/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Programově zjišťování kruhových odkazů v Excelu

## Zavedení
Pokud jde o práci se soubory aplikace Excel, jedním z nejvíce frustrujících problémů, se kterými se můžete setkat, je kruhový odkaz. K tomu dochází, když vzorec odkazuje zpět na svou vlastní buňku, ať už přímo nebo nepřímo, a vytváří smyčku, která může zmást výpočetní stroj Excelu. Ale nebojte se! S Aspose.Cells for .NET můžete programově detekovat tyto otravné kruhové odkazy a zajistit, že vaše tabulky zůstanou funkční a přesné. V této příručce vás provedeme procesem krok za krokem, takže bude jednoduchý jako facka.
## Předpoklady
Než se ponoříme do toho nejhrubšího zjišťování kruhových referencí, ujistěte se, že máte vše, co potřebujete, abyste mohli začít:
1. Visual Studio: Ujistěte se, že máte na svém počítači nainstalované Visual Studio. Toto bude vaše vývojové prostředí.
2. .NET Framework: Ujistěte se, že používáte kompatibilní verzi rozhraní .NET Framework (alespoň .NET Framework 4.0).
3.  Knihovna Aspose.Cells: Musíte mít knihovnu Aspose.Cells. Můžete si jej stáhnout z[Aspose webové stránky](https://releases.aspose.com/cells/net/).
4. Základní znalost C#: Výhodou bude znalost programování v C#, protože budeme psát kód v tomto jazyce.
5. Soubor Excel: Připravte si soubor Excel, který obsahuje cyklické odkazy pro testování. Můžete si vytvořit jednoduchý nebo si stáhnout ukázku.
Nyní, když máme své předpoklady na místě, přejděme k zábavnější části!
## Importujte balíčky
Než začnete kódovat, musíte naimportovat potřebné balíčky. Jak na to:
### Vytvořit nový projekt
- Otevřete Visual Studio a vytvořte nový projekt C# Console Application.
### Přidejte odkaz Aspose.Cells
- Klepněte pravým tlačítkem myši na svůj projekt v Průzkumníku řešení.
- Vyberte „Spravovat balíčky NuGet“.
- Vyhledejte „Aspose.Cells“ a nainstalujte nejnovější verzi.
### Importujte požadované jmenné prostory
 V horní části vašeho`Program.cs` soubor, importujte potřebné jmenné prostory:
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Nyní, když máme vše nastaveno, pojďme se ponořit do kódu pro detekci cyklických odkazů v souboru aplikace Excel.
## Krok 1: Definujte vstupní adresář
Nejprve musíte určit adresář, kde se nachází váš soubor Excel. Zde načtete soubor Excel.
```csharp
// Vstupní adresář
string sourceDir = "Your Document Directory";
```
 Nahradit`"Your Document Directory"` se skutečnou cestou k souboru Excel.
## Krok 2: Načtěte sešit pomocí LoadOptions
Dále načtete sešit aplikace Excel. Tady začíná kouzlo!
```csharp
LoadOptions loadOptions = new LoadOptions();
var objWB = new Aspose.Cells.Workbook(sourceDir + "Circular Formulas.xls", loadOptions);
```
 Zde vytváříme novou instanci`LoadOptions` a načtení sešitu ze zadané cesty. Ujistěte se, že se název souboru Excel shoduje!
## Krok 3: Povolte nastavení iterace
Chcete-li povolit cyklické odkazy, musíte v sešitu povolit nastavení iterace.
```csharp
objWB.Settings.Iteration = true;
```
To říká Aspose.Cells, aby povolilo kruhové odkazy během výpočtu.
## Krok 4: Vytvořte možnosti výpočtu a kruhový monitor
Nyní vytvoříme možnosti výpočtu a náš vlastní kruhový monitor.
```csharp
CalculationOptions copts = new CalculationOptions();
CircularMonitor cm = new CircularMonitor();
copts.CalculationMonitor = cm;
```
 Zde vytváříme instanci`CalculationOptions` a zvyk`CircularMonitor`Tento monitor pomůže sledovat všechny kruhové reference nalezené během výpočtů.
## Krok 5: Vypočítejte vzorce
Nyní je čas vypočítat vzorce ve vašem sešitu.
```csharp
objWB.CalculateFormula(copts);
```
Tento řádek provede výpočet a zkontroluje kruhové reference.
## Krok 6: Počítání kruhových odkazů
Po výpočtu můžete spočítat, kolik kruhových referencí bylo nalezeno.
```csharp
long lngCircularRef = cm.circulars.Count;
Console.WriteLine("Circular References found - " + lngCircularRef);
```
Tím se zobrazí počet cyklických odkazů zjištěných v souboru aplikace Excel.
## Krok 7: Zobrazení výsledků
Nakonec si zobrazme výsledky a potvrďte, že naše metoda byla úspěšně provedena.
```csharp
Console.WriteLine("DetectCircularReference executed successfully.\r\n");
```
## Krok 8: Implementujte třídu CircularMonitor
 Chcete-li dokončit proces, budete muset implementovat`CircularMonitor` třída. Tato třída bude dědit od`AbstractCalculationMonitor` a zvládnout detekci kruhových referencí.
```csharp
public class CircularMonitor : AbstractCalculationMonitor
{
    public ArrayList circulars = new ArrayList();
    public ArrayList Circulars { get { return circulars; } }
    public override bool OnCircular(IEnumerator circularCellsData)
    {
        CalculationCell cc = null;
        ArrayList cur = new ArrayList();
        while (circularCellsData.MoveNext())
        {
            cc = (CalculationCell)circularCellsData.Current;
            cur.Add(cc.Worksheet.Name + "!" + CellsHelper.CellIndexToName(cc.CellRow, cc.CellColumn));
        }
        circulars.Add(cur);
        return true;
    }
}
```
Tato třída zachycuje podrobnosti o každém nalezeném kruhovém odkazu, včetně názvu listu a indexu buňky.
## Závěr
Detekce cyklických odkazů v aplikaci Excel pomocí Aspose.Cells for .NET je jednoduchý proces, jakmile jej rozdělíte do zvládnutelných kroků. Podle této příručky můžete snadno identifikovat a zpracovat kruhové odkazy ve svých tabulkách, čímž zajistíte, že vaše výpočty zůstanou přesné a spolehlivé. Ať už jste zkušený vývojář nebo teprve začínáte, Aspose.Cells poskytuje výkonné nástroje pro vylepšení vašich možností manipulace s Excelem. 
## FAQ
### Co je to kruhový odkaz v Excelu?
Kruhový odkaz nastává, když vzorec odkazuje zpět na svou vlastní buňku, což způsobuje nekonečnou smyčku ve výpočtech.
### Jak mohu programově detekovat cyklické odkazy?
Knihovnu Aspose.Cells v .NET můžete použít k programové detekci cyklických odkazů implementací vlastního monitoru výpočtů.
### Jaké jsou předpoklady pro používání Aspose.Cells?
Potřebujete nainstalovat Visual Studio, .NET Framework a knihovnu Aspose.Cells.
### Mohu používat Aspose.Cells zdarma?
Ano, Aspose.Cells nabízí bezplatnou zkušební verzi, kterou můžete použít k prozkoumání jeho funkcí.
### Kde najdu více informací o Aspose.Cells?
 Můžete navštívit[Dokumentace Aspose.Cells](https://reference.aspose.com/cells/net/) pro podrobné informace a příklady.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
