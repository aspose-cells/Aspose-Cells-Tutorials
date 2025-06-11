---
"date": "2025-04-05"
"description": "Naučte se, jak přizpůsobit popisky kontingenčních tabulek pomocí Aspose.Cells pro .NET. Tato příručka se zabývá přepsáním výchozích nastavení, implementací funkcí globalizace a ukládáním do PDF."
"title": "Úprava popisků kontingenčních tabulek v .NET pomocí Aspose.Cells – Komplexní průvodce"
"url": "/cs/net/data-analysis/customize-pivot-table-labels-aspose-cells-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Přizpůsobení popisků kontingenčních tabulek v .NET pomocí Aspose.Cells

## Zavedení

datové analýze je srozumitelná prezentace informací klíčová. Přizpůsobení popisků kontingenčních tabulek specifickým cílovým skupinám nebo regionálním potřebám zvyšuje přehlednost. Tato příručka ukazuje, jak přizpůsobit popisky kontingenčních tabulek pomocí Aspose.Cells pro .NET, robustní knihovny pro programově vytvářet a manipulovat se soubory Excelu.

### Co se naučíte
- Přepsat výchozí nastavení popisků kontingenční tabulky v Aspose.Cells.
- Implementujte vlastní nastavení globalizace pro kontingenční tabulky.
- Integrujte tato nastavení do pracovního postupu sešitu.
- Uložte si přizpůsobené kontingenční tabulky jako PDF s konkrétními možnostmi.

Na konci vytvoříte uživatelsky přívětivé a pro dané místo specifické pivotní tabulky. Začněme diskusí o předpokladech.

## Předpoklady

### Požadované knihovny
Chcete-li pokračovat:
- Nainstalujte knihovnu Aspose.Cells pro .NET.
- Nastavte vývojové prostředí pomocí .NET CLI nebo Správce balíčků (NuGet).

### Požadavky na nastavení prostředí
- Porozumět jazyku C# a frameworku .NET.
- Znát soubory Excelu a kontingenční tabulky.

## Nastavení Aspose.Cells pro .NET

### Instalace

**Použití .NET CLI:**
```bash
dotnet add package Aspose.Cells
```

**Používání Správce balíčků:**
```powershell
PM> Install-Package Aspose.Cells
```

### Získání licence
Aspose nabízí různé možnosti licencování:
- **Bezplatná zkušební verze:** Vyzkoušejte si všechny funkce bez omezení.
- **Dočasná licence:** Získejte bezplatnou licenci na prodloužené zkušební období.
- **Nákup:** Kupte si trvalou licenci pro dlouhodobé užívání.

#### Základní inicializace
Začněte používat Aspose.Cells inicializací sešitu a nastavením potřebných konfigurací:

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

// Inicializace nového sešitu
Workbook wb = new Workbook();
```

## Průvodce implementací

### Nastavení globalizace vlastních kontingenčních tabulek

Popisky v kontingenčních tabulkách můžete přizpůsobit pomocí následujících kroků.

#### 1. Definujte si vlastní třídu globalizace
Vytvořte třídu rozšiřující `PivotGlobalizationSettings` a přepsat potřebné metody:

```csharp
using Aspose.Cells.Pivot;
using System;

public class CustomPivotTableGlobalizationSettings : PivotGlobalizationSettings
{
    public override string GetTextOfTotal() => "AsposeGetPivotTotalName";
    
    public override string GetTextOfGrandTotal() => "AsposeGetPivotGrandTotalName";

    public override string GetTextOfMultipleItems() => "AsposeGetMultipleItemsName";

    public override string GetTextOfAll() => "AsposeGetAllName";

    public override string GetTextOfColumnLabels() => "AsposeGetColumnLabelsOfPivotTable";

    public override string GetTextOfRowLabels() => "AsposeGetRowLabelsNameOfPivotTable";

    public override string GetTextOfEmptyData() => "(blank)AsposeGetEmptyDataName";

    public override string GetTextOfSubTotal(PivotFieldSubtotalType subTotalType)
    {
        return subTotalType switch
        {
            PivotFieldSubtotalType.Sum => "AsposeSum",
            PivotFieldSubtotalType.Count => "AsposeCount",
            PivotFieldSubtotalType.Average => "AsposeAverage",
            PivotFieldSubtotalType.Max => "AsposeMax",
            PivotFieldSubtotalType.Min => "AsposeMin",
            PivotFieldSubtotalType.Product => "AsposeProduct",
            PivotFieldSubtotalType.CountNums => "AsposeCount",
            PivotFieldSubtotalType.Stdev => "AsposeStdDev",
            PivotFieldSubtotalType.Stdevp => "AsposeStdDevp",
            PivotFieldSubtotalType.Var => "AsposeVar",
            PivotFieldSubtotalType.Varp => "AsposeVarp",
            _ => "AsposeSubTotalName"
        };
    }
}
```

#### 2. Použití vlastních nastavení globalizace na sešit
Zde je návod, jak můžete tato nastavení použít v pracovním postupu sešitu:

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;
using System.IO;

public class ApplyCustomGlobalizationSettings
{
    public static void Run()
    {
        string SourceDir = "YOUR_SOURCE_DIRECTORY";
        string outputDir = "YOUR_OUTPUT_DIRECTORY";

        string dataDir = Path.Combine(SourceDir, "samplePivotTableGlobalizationSettings.xlsx");

        // Načíst sešit
        Workbook wb = new Workbook(dataDir);

        // Nastavení vlastních nastavení globalizace
        GlobalizationSettings settings = new GlobalizationSettings();
        settings.PivotSettings = new CustomPivotTableGlobalizationSettings();
        wb.Settings.GlobalizationSettings = settings;

        // Skrýt list se zdrojovými daty a zobrazit kontingenční tabulku
        wb.Worksheets[0].IsVisible = false;
        Worksheet ws = wb.Worksheets[1];
        PivotTable pt = ws.PivotTables[0];

        // Obnovení a výpočet dat pro kontingenční tabulku
        pt.RefreshDataFlag = true;
        pt.RefreshData();
        pt.CalculateData();
        pt.RefreshDataFlag = false;

        // Uložit jako PDF s konkrétními možnostmi
        PdfSaveOptions options = new PdfSaveOptions { OnePagePerSheet = true };
        string outputPath = Path.Combine(outputDir, "outputPivotTableGlobalizationSettings.pdf");
        wb.Save(outputPath, options);
    }
}
```

#### Tipy pro řešení problémů
- Ujistěte se, že je cesta ke zdrojovému souboru Excelu správná.
- Ověřte indexy kontingenčních tabulek při programovém přístupu k nim.

### Praktické aplikace
Zde je několik reálných případů použití pro úpravu popisků kontingenčních tabulek:
1. **Lokalizace:** Přizpůsobte zprávy regionálním podmínkám a terminologii.
2. **Firemní branding:** Slaďte štítky s pokyny pro branding společnosti.
3. **Vzdělávací nástroje:** Používejte v kontingenčních tabulkách alternativní termíny pro vzdělávací účely.

### Úvahy o výkonu
- **Optimalizace využití paměti:** Aspose.Cells efektivně zpracovává paměť, ale optimalizuje zpracování dat, kde je to možné.
- **Efektivní aktualizace dat:** Aktualizujte data pouze v případě potřeby, aby se snížila výpočetní režie.

## Závěr

Úpravy popisků kontingenčních tabulek pomocí Aspose.Cells pro .NET zlepšují čitelnost a specifičnost sestav. Tato příručka vám pomůže výrazně zlepšit použitelnost vašich kontingenčních tabulek. Prozkoumejte další funkce nabízené službou Aspose.Cells pro propracovanější řešení pro analýzu dat.

### Další kroky
- Experimentujte s různými úpravami štítků.
- Prostudujte si dokumentaci k Aspose, kde najdete pokročilé funkce.

## Sekce Často kladených otázek

**Q1: Mohu přizpůsobit popisky pro všechny prvky aplikace Excel pomocí Aspose.Cells?**
A1: Ano, Aspose.Cells umožňuje rozsáhlé přizpůsobení napříč různými komponentami Excelu, jako jsou grafy a tabulky.

**Q2: Jak mám řešit chyby při použití vlastních nastavení?**
A2: Zkontrolujte cesty k souborům, indexy kontingenčních tabulek a ujistěte se, že máte správnou licenci, abyste předešli problémům za běhu.

**Q3: Lze tato nastavení použít dynamicky ve webové aplikaci?**
A3: Aspose.Cells se dobře integruje s webovými aplikacemi založenými na .NET pro dynamické přizpůsobení.

**Q4: Existují nějaká omezení ohledně délky nebo obsahu štítku?**
A4: Zajistěte, aby popisky odpovídaly omezením zobrazení v Excelu, aby byla zachována čitelnost.

**Q5: Jak aktualizuji svou stávající licenci pro nové funkce?**
A5: Kontaktujte podporu Aspose s údaji o vaší aktuální licenci a proberte s nimi možnosti aktualizace.

## Zdroje
- **Dokumentace:** [Dokumentace k Aspose.Cells .NET](https://reference.aspose.com/cells/net/)
- **Stáhnout:** [Soubory ke stažení Aspose.Cells](https://releases.aspose.com/cells/net/)
- **Nákup:** [Koupit Aspose.Cells](https://purchase.aspose.com/buy)
- **Bezplatná zkušební verze:** [Zahájit bezplatnou zkušební verzi](https://www.aspose.com/purchase/pricing.aspx?k=aspose.cells)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}