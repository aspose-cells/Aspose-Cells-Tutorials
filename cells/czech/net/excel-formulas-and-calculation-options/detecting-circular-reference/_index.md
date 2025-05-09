---
"description": "Snadno detekujte kruhové odkazy v Excelu pomocí Aspose.Cells pro .NET. Postupujte podle našeho podrobného návodu a zajistěte si přesné výpočty ve vašich tabulkách."
"linktitle": "Detekce cyklických odkazů v Excelu programově"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Detekce cyklických odkazů v Excelu programově"
"url": "/cs/net/excel-formulas-and-calculation-options/detecting-circular-reference/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Detekce cyklických odkazů v Excelu programově

## Zavedení
Pokud jde o práci se soubory aplikace Excel, jedním z nejfrustrujících problémů, se kterými se můžete setkat, je cyklický odkaz. K tomu dochází, když vzorec odkazuje zpět na svou vlastní buňku, ať už přímo nebo nepřímo, a vytváří tak smyčku, která může zmást výpočetní engine aplikace Excel. Ale nebojte se! S Aspose.Cells pro .NET můžete programově detekovat tyto otravné cyklické odkazy a zajistit tak, aby vaše tabulky zůstaly funkční a přesné. V této příručce vás krok za krokem provedeme celým procesem a usnadníme vám ho jako facka.
## Předpoklady
Než se ponoříme do detailů detekce cyklických odkazů, ujistěte se, že máte vše, co potřebujete k zahájení:
1. Visual Studio: Ujistěte se, že máte na svém počítači nainstalované Visual Studio. Toto bude vaše vývojové prostředí.
2. .NET Framework: Ujistěte se, že používáte kompatibilní verzi .NET Framework (alespoň .NET Framework 4.0).
3. Knihovna Aspose.Cells: Potřebujete knihovnu Aspose.Cells. Můžete si ji stáhnout z [Webové stránky Aspose](https://releases.aspose.com/cells/net/).
4. Základní znalost C#: Znalost programování v C# bude výhodou, protože budeme psát kód v tomto jazyce.
5. Soubor Excel: Mějte připravený soubor Excel, který obsahuje cyklické odkazy pro testování. Můžete si vytvořit jednoduchý soubor nebo si stáhnout ukázku.
Teď, když máme připravené všechny předpoklady, pojďme k té zábavné části!
## Importovat balíčky
Než začnete s kódováním, musíte importovat potřebné balíčky. Zde je návod, jak to udělat:
### Vytvořit nový projekt
- Otevřete Visual Studio a vytvořte nový projekt konzolové aplikace v C#.
### Přidat odkaz na Aspose.Cells
- Klikněte pravým tlačítkem myši na svůj projekt v Průzkumníku řešení.
- Vyberte možnost „Spravovat balíčky NuGet“.
- Vyhledejte „Aspose.Cells“ a nainstalujte nejnovější verzi.
### Importovat požadované jmenné prostory
Na vrcholu tvého `Program.cs` soubor, importujte potřebné jmenné prostory:
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Nyní, když máme vše nastavené, pojďme se ponořit do kódu pro detekci cyklických odkazů v souboru aplikace Excel.
## Krok 1: Definování vstupního adresáře
Nejprve je třeba zadat adresář, kde se nachází váš soubor Excel. Zde načtete svůj soubor Excel.
```csharp
// Vstupní adresář
string sourceDir = "Your Document Directory";
```
Nahradit `"Your Document Directory"` se skutečnou cestou k vašemu souboru aplikace Excel.
## Krok 2: Načtení sešitu pomocí LoadOptions
Dále si načtete sešit aplikace Excel. Tady začíná kouzlo!
```csharp
LoadOptions loadOptions = new LoadOptions();
var objWB = new Aspose.Cells.Workbook(sourceDir + "Circular Formulas.xls", loadOptions);
```
Zde vytváříme novou instanci `LoadOptions` a načítání sešitu ze zadané cesty. Ujistěte se, že název vašeho souboru Excelu se shoduje!
## Krok 3: Povolení nastavení iterace
Chcete-li povolit cyklické odkazy, je nutné v sešitu povolit nastavení iterace.
```csharp
objWB.Settings.Iteration = true;
```
Toto říká Aspose.Cells, aby během výpočtu povolil cyklické odkazy.
## Krok 4: Vytvořte možnosti výpočtu a kruhový monitor
Nyní si vytvořme možnosti výpočtu a náš vlastní kruhový monitor.
```csharp
CalculationOptions copts = new CalculationOptions();
CircularMonitor cm = new CircularMonitor();
copts.CalculationMonitor = cm;
```
Zde vytváříme instanci `CalculationOptions` a zvyk `CircularMonitor`Tento monitor pomůže sledovat jakékoli cyklické odkazy nalezené během výpočtů.
## Krok 5: Výpočet vzorců
Nyní je čas vypočítat vzorce ve vašem sešitu.
```csharp
objWB.CalculateFormula(copts);
```
Tento řádek provede výpočet a zkontroluje cyklické odkazy.
## Krok 6: Počet cyklických odkazů
Po výpočtu můžete spočítat, kolik cyklických odkazů bylo nalezeno.
```csharp
long lngCircularRef = cm.circulars.Count;
Console.WriteLine("Circular References found - " + lngCircularRef);
```
Toto vypíše počet cyklických odkazů zjištěných ve vašem souboru Excel.
## Krok 7: Zobrazení výsledků
Nakonec si zobrazme výsledky a ověřme, že naše metoda byla úspěšně provedena.
```csharp
Console.WriteLine("DetectCircularReference executed successfully.\r\n");
```
## Krok 8: Implementace třídy CircularMonitor
Pro dokončení procesu budete muset implementovat `CircularMonitor` třída. Tato třída bude dědit z `AbstractCalculationMonitor` a zvládat detekci cyklických odkazů.
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
Tato třída zachycuje podrobnosti o každém nalezeném cyklickém odkazu, včetně názvu listu a indexu buňky.
## Závěr
Detekce cyklických odkazů v Excelu pomocí Aspose.Cells pro .NET je jednoduchý proces, jakmile si ho rozdělíte na zvládnutelné kroky. Dodržováním tohoto návodu můžete snadno identifikovat a zpracovávat cyklické odkazy v tabulkách a zajistit tak, aby vaše výpočty zůstaly přesné a spolehlivé. Ať už jste zkušený vývojář nebo teprve začínáte, Aspose.Cells poskytuje výkonné nástroje pro vylepšení vašich schopností manipulace s Excelem. 
## Často kladené otázky
### Co je to kruhový odkaz v Excelu?
Kruhový odkaz vzniká, když vzorec odkazuje zpět na svou vlastní buňku, což způsobuje nekonečnou smyčku ve výpočtech.
### Jak mohu programově detekovat cyklické odkazy?
K programové detekci cyklických odkazů můžete v rozhraní .NET použít knihovnu Aspose.Cells implementací vlastního monitoru výpočtů.
### Jaké jsou předpoklady pro používání Aspose.Cells?
Potřebujete mít nainstalované Visual Studio, .NET Framework a knihovnu Aspose.Cells.
### Mohu používat Aspose.Cells zdarma?
Ano, Aspose.Cells nabízí bezplatnou zkušební verzi, kterou můžete využít k prozkoumání jeho funkcí.
### Kde najdu více informací o Aspose.Cells?
Můžete navštívit [Dokumentace k Aspose.Cells](https://reference.aspose.com/cells/net/) pro podrobné informace a příklady.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}