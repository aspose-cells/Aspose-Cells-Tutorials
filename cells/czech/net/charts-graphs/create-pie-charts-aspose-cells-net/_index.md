---
"date": "2025-04-05"
"description": "Naučte se, jak vytvářet dynamické koláčové grafy s vodicími čarami pomocí Aspose.Cells pro .NET. Postupujte podle tohoto průvodce a zlepšete si své dovednosti v oblasti vizualizace dat."
"title": "Vytváření koláčových grafů s vodicími čarami v Aspose.Cells .NET – Komplexní průvodce"
"url": "/cs/net/charts-graphs/create-pie-charts-aspose-cells-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Vytváření koláčových grafů s vodicími čarami pomocí Aspose.Cells .NET

## Zavedení
Vylepšete vizualizaci dat vytvářením informativnějších koláčových grafů pomocí Aspose.Cells pro .NET. Tento podrobný návod vám ukáže, jak přidat vodicí čáry k segmentům koláčového grafu, což usnadní identifikaci odpovídajících kategorií dat na první pohled. Dodržováním tohoto tutoriálu budou vaše vizualizace vizuálně přitažlivé i vysoce funkční.

**Co se naučíte:**
- Nastavení Aspose.Cells pro .NET ve vašem prostředí
- Vytváření vlastních koláčových grafů s vodicími čarami pomocí C#
- Uložení grafu jako obrázku nebo do sešitu aplikace Excel

Ujistěte se, že máte vše připravené, abyste mohli efektivně pokračovat.

## Předpoklady
Než začnete, ujistěte se, že splňujete tyto předpoklady:

- **Knihovny a verze**Nainstalujte Aspose.Cells pro .NET. Ujistěte se, že váš projekt je nastaven na nejnovější verzi.
- **Nastavení prostředí**Tato příručka předpokládá kompatibilní prostředí .NET pro Aspose.Cells.
- **Předpoklady znalostí**Základní znalost programování v C# a operací v Excelu je výhodou.

## Nastavení Aspose.Cells pro .NET
Pro začátek nainstalujte Aspose.Cells do svého projektu pomocí:

**Rozhraní příkazového řádku .NET**
```bash
dotnet add package Aspose.Cells
```

**Správce balíčků**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

Získejte licenci pro plnou funkčnost výběrem z následujících možností:
- **Bezplatná zkušební verze**Začněte svou bezplatnou zkušební verzi na [Stránka ke stažení Aspose](https://releases.aspose.com/cells/net/).
- **Dočasná licence**Získejte dočasnou licenci [zde](https://purchase.aspose.com/temporary-license/).
- **Nákup**Pro plné funkce si zakupte licenci [zde](https://purchase.aspose.com/buy).

Inicializujte Aspose.Cells ve vašem projektu vytvořením instance třídy `Workbook` třída.

## Průvodce implementací

### Vytvoření sešitu a pracovního listu
1. **Inicializace sešitu**
   Vytvořte nový sešit ve formátu XLSX:
   ```csharp
   Workbook workbook = new Workbook(FileFormatType.Xlsx);
   ```

2. **Přístup k prvnímu pracovnímu listu**
   Pro zadání dat použijte první pracovní list:
   ```csharp
   Worksheet worksheet = workbook.Worksheets[0];
   ```

3. **Přidávání dat pro koláčový graf**
   Naplňte svůj pracovní list kategoriemi a hodnotami:
   ```csharp
   worksheet.Cells["A1"].PutValue("Retail");
   // Přidat zbývající názvy kategorií...
   worksheet.Cells["B1"].PutValue(10.4);
   // Přidejte odpovídající hodnoty...
   ```

### Přidání koláčového grafu do pracovního listu
1. **Vytvořte koláčový graf**
   Vygenerujte koláčový graf a přidejte ho do kolekce grafů na pracovním listu:
   ```csharp
   int id = worksheet.Charts.Add(ChartType.Pie, 3, 3, 23, 13);
   ```

2. **Konfigurace dat sérií a kategorií**
   Propojte data pro série a kategorie:
   ```csharp
   Chart chart = worksheet.Charts[id];
   chart.NSeries.Add("B1:B16", true);
   chart.NSeries.CategoryData = "A1:A16";
   ```

3. **Přizpůsobení popisků dat**
   Vypnout zobrazení legendy, nastavit popisky dat tak, aby zobrazovaly názvy kategorií a procenta:
   ```csharp
   chart.ShowLegend = false;
   DataLabels dataLabels = chart.NSeries[0].DataLabels;
   dataLabels.ShowCategoryName = true;
   dataLabels.ShowPercentage = true;
   dataLabels.Position = LabelPositionType.OutsideEnd;
   ```

### Implementace vodicích čar
1. **Zapnout vodicí čáry**
   Povolte vodicí čáry pro jasnější vizuální propojení:
   ```csharp
   chart.NSeries[0].HasLeaderLines = true;
   ```

2. **Úprava polohy popisků dat**
   Zajistěte viditelnost úpravou pozic štítků:
   ```csharp
   int DELTA = 100;
   foreach (var point in chart.NSeries[0].Points)
   {
       int X = point.DataLabels.X;
       if (X > 2000) 
           point.DataLabels.X += DELTA;
       else 
           point.DataLabels.X -= DELTA;
   }
   ```

### Uložení grafu a sešitu
1. **Uložit jako obrázek**
   Vykreslení grafu do obrazového souboru:
   ```csharp
   ImageOrPrintOptions options = new ImageOrPrintOptions { ImageType = Drawing.ImageType.Png, HorizontalResolution = 200, VerticalResolution = 200 };
   chart.ToImage("output_out.png", options);
   ```

2. **Uložit sešit**
   Uložte si sešit, abyste si mohli graf zobrazit v Excelu:
   ```csharp
   workbook.Save("output_out.xlsx");
   ```

## Praktické aplikace
- **Finanční zprávy**Jasně reprezentují rozpočtové alokace.
- **Marketingová analytika**Efektivně vizualizujte data o podílu na trhu v prezentacích nebo zprávách.
- **Analýza prodeje**Snadné zobrazení rozdělení prodeje mezi různé regiony/produkty.

Možnosti integrace zahrnují export těchto vizualizací do webových aplikací nebo jejich vložení do automatizovaných nástrojů pro tvorbu reportů.

## Úvahy o výkonu
Při používání Aspose.Cells zvažte pro optimální výkon následující:
- Minimalizujte velké datové sady načítané do paměti najednou.
- Používejte efektivní smyčky a vyhýbejte se zbytečným výpočtům uvnitř smyček.
- Pravidelně čistěte prostředky, jako jsou objekty sešitu, abyste zabránili úniku paměti.

## Závěr
Naučili jste se, jak vytvářet koláčové grafy s vodicími čarami pomocí Aspose.Cells pro .NET. Tato funkce zvyšuje přehlednost vizualizací dat, díky čemuž jsou přístupnější a působivější. 

**Další kroky:**
Prozkoumejte další možnosti úprav vzhledu grafů nebo experimentujte s dalšími typy grafů dostupnými v Aspose.Cells.

## Sekce Často kladených otázek
1. **Co je to vodicí čára v koláčovém grafu?**
   Vodicí čáry spojují popisky dat s příslušnými segmenty, což zlepšuje čitelnost.

2. **Mohu používat Aspose.Cells zdarma?**
   Ano, můžete začít s bezplatnou zkušební verzí, ale pro všechny funkce je vyžadována licence.

3. **Je možné exportovat grafy jako obrázky?**
   Rozhodně! Použijte `ImageOrPrintOptions` uložit graf do obrazových formátů, jako je PNG nebo JPEG.

4. **Jak mohu ručně upravit pozice datových popisků?**
   Upravte souřadnice X a Y popisků dat v rámci smyčky bodů řady.

5. **Může se Aspose.Cells integrovat s jinými systémy?**
   Ano, lze jej použít ve spojení s databázemi, webovými službami a dalšími pro automatizovaná řešení pro tvorbu reportů.

## Zdroje
- [Dokumentace k Aspose.Cells](https://reference.aspose.com/cells/net/)
- [Stáhnout Aspose.Cells](https://releases.aspose.com/cells/net/)
- [Zakoupit licenci](https://purchase.aspose.com/buy)
- [Bezplatná zkušební verze](https://releases.aspose.com/cells/net/)
- [Dočasná licence](https://purchase.aspose.com/temporary-license/)
- [Fórum podpory](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}