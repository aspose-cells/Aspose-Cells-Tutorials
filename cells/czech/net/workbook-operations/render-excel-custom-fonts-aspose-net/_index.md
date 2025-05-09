---
"date": "2025-04-05"
"description": "Naučte se, jak s Aspose.Cells pro .NET vykreslovat soubory Excelu do formátů PNG, TIFF a PDF s použitím vlastních písem. Zajistěte konzistentní typografii ve všech konverzích dokumentů."
"title": "Renderování Excelu do PNG, TIFF, PDF s vlastními fonty v .NET pomocí Aspose.Cells"
"url": "/cs/net/workbook-operations/render-excel-custom-fonts-aspose-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Renderování souborů Excelu do formátu PNG, TIFF a PDF s vlastními fonty pomocí Aspose.Cells pro .NET

## Zavedení

Zachování integrity písma během převodu souborů Excel do obrázků nebo PDF je klíčové pro konzistenci značky. Aspose.Cells pro .NET nabízí robustní řešení, které umožňuje zadat vlastní výchozí písma v převodech dokumentů.

V tomto tutoriálu vás provedeme vykreslením souborů aplikace Excel do formátů PNG, TIFF a PDF pomocí Aspose.Cells pro .NET se zadanými vlastními výchozími fonty. To je ideální, pokud:
- V renderovaných dokumentech se snažte o konzistentní typografii.
- Během konverzí je třeba upravit nastavení písma.
- Chci prozkoumat možnosti konfigurace v Aspose.Cells pro .NET.

Pojďme si nastavit prostředí a bezproblémově implementovat tyto funkce.

### Předpoklady

Než začnete, ujistěte se, že máte následující:
- **Prostředí .NET**Nastavení na vašem počítači (nejlépe .NET Core nebo .NET Framework).
- **Knihovna Aspose.Cells pro .NET**Nainstalováno ve vašem projektu.
- **Soubor Excelu**Sešit aplikace Excel s daty k převodu.

### Nastavení Aspose.Cells pro .NET

Pro začátek přidejte do projektu knihovnu Aspose.Cells:

**Použití .NET CLI:**
```bash
dotnet add package Aspose.Cells
```

**Používání Správce balíčků:**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

Získejte licenci pro přístup k plným funkcím:
- **Bezplatná zkušební verze**Navštivte [Bezplatná zkušební verze Aspose](https://releases.aspose.com/cells/net/) pro počáteční přístup.
- **Dočasná licence**Získejte to z [Dočasná licence Aspose](https://purchase.aspose.com/temporary-license/).
- **Nákup**Pro trvalou licenci přejděte na [Nákup Aspose](https://purchase.aspose.com/buy).

Po získání licence inicializujte Aspose.Cells ve vaší aplikaci:
```csharp
// Nastavte licenci pro Aspose.Cells.
License license = new License();
license.SetLicense("path_to_your_license_file");
```

## Průvodce implementací

### Vykreslování do PNG s vlastním výchozím písmem

Vykreslení listu aplikace Excel do formátu PNG s nastavením vlastního výchozího písma zajišťuje vizuální konzistenci. Zde je postup:

#### Krok 1: Konfigurace možností obrazu

Nakonfigurujte možnosti vykreslování pro výstupní obrázek.
```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Určete adresáře.
string SourceDir = @"YOUR_SOURCE_DIRECTORY";
string outputDir = @"YOUR_OUTPUT_DIRECTORY";

// Otevřete soubor aplikace Excel.
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// Nastavení možností vykreslování obrázků.
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false; // Pro chybějící písma v sešitu použijte vlastní písmo.
imgOpt.DefaultFont = "Times New Roman";
```

#### Krok 2: Vykreslení a uložení

Vykreslete pracovní list do obrazového souboru s použitím těchto nastavení.
```csharp
// Vykreslete první pracovní list do obrázku PNG.
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```

### Vykreslování do formátu TIFF s vlastním výchozím písmem

Formát TIFF je ideální pro vysoce kvalitní obrázky. Zde je návod, jak vykreslit celý sešit jako soubor TIFF:

#### Krok 3: Nastavení možností obrazu pro TIFF

Nakonfigurujte možnosti vykreslování speciálně pro výstup TIFF.
```csharp
// Znovu použijte dříve definované adresáře a otevřete soubor aplikace Excel.
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// Nakonfigurujte možnosti vykreslování obrázků pro formát TIFF.
imgOpt.ImageType = Drawing.ImageType.Tiff;
```

#### Krok 4: Vykreslení celého sešitu do formátu TIFF

Převeďte celý sešit do jednoho souboru TIFF.
```csharp
// Vykreslete sešit jako obrázek TIFF.
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```

### Vykreslování do PDF s vlastním výchozím písmem

Uložení sešitu aplikace Excel ve formátu PDF při zachování konzistence písma je pro profesionální dokumentaci zásadní.

#### Krok 5: Konfigurace možností ukládání PDF

Nastavte potřebné možnosti pro uložení souboru ve formátu PDF.
```csharp
using Aspose.Cells;

// Znovu otevřete sešit.
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// Nastavení možností ukládání PDF.
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false; // Pro chybějící písma v sešitu použijte vlastní písmo.
```

#### Krok 6: Uložit jako PDF

Exportujte si sešit do PDF dokumentu.
```csharp
// Uložte sešit jako soubor PDF.
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```

## Praktické aplikace

- **Obchodní zprávy**Zajistěte konzistentní branding ve všech exportovaných sestavách pomocí vlastních písem.
- **Archivace dokumentů**Převeďte starší soubory aplikace Excel do formátu PDF pro snadné sdílení a archivaci s jednotnou typografií.
- **Grafický design**Vytvářejte obrázky TIFF s vysokým rozlišením z dat aplikace Excel pro prezentace nebo designové projekty.

Integrace s jinými systémy, jako jsou platformy CRM nebo řešení pro správu dokumentů, může tyto případy použití dále vylepšit automatizací exportu na základě specifických spouštěčů nebo událostí.

## Úvahy o výkonu

Optimalizace procesu vykreslování je klíčová:
- **Správa paměti**: Zlikvidujte `Workbook`, `SheetRender`a `WorkbookRender` objekty okamžitě uvolnit zdroje.
- **Dávkové zpracování**Pokud pracujete s více soubory, implementujte dávkové zpracování pro efektivní práci.
- **Asynchronní operace**Kdekoli je to možné, používejte asynchronní metody pro zlepšení odezvy aplikací.

## Závěr

Nyní jste zvládli vykreslování sešitů aplikace Excel do formátů PNG, TIFF a PDF a zároveň nastavování vlastních výchozích písem pomocí nástroje Aspose.Cells pro .NET. Tato funkce zajišťuje, že si vaše dokumenty zachovají vizuální integritu napříč různými platformami a způsoby použití.

Prozkoumejte další funkce nabízené službou Aspose.Cells, které dále vylepší možnosti zpracování dokumentů. Další informace nebo pomoc naleznete na [Fórum Aspose](https://forum.aspose.com/c/cells/9).

## Sekce Často kladených otázek

**1. Co je Aspose.Cells pro .NET?**
   — Aspose.Cells pro .NET je knihovna, která poskytuje robustní funkce pro programovou správu a převod souborů aplikace Excel.

**2. Mohu používat Aspose.Cells ve webových aplikacích?**
   — Ano, Aspose.Cells lze integrovat do ASP.NET nebo jakékoli jiné webové aplikace založené na .NET.

**3. Jak mám řešit chybějící fonty během vykreslování?**
   — Nastavením `CheckWorkbookDefaultFont` na false a zadáním `DefaultFont`, zajistíte, že veškerý text bude používat vámi zvolené písmo, i když originál není k dispozici.

**4. Jsou podporovány i jiné formáty než PNG, TIFF a PDF?**
   — Ano, Aspose.Cells podporuje různé obrazové formáty, jako je JPEG, BMP atd., a nabízí rozsáhlé možnosti konverze dokumentů.

**5. Jaké jsou některé osvědčené postupy pro použití Aspose.Cells ve velkých aplikacích?**
   — Využívejte efektivní techniky správy paměti, dávkové zpracování pro práci s více soubory a zvažte asynchronní operace pro zvýšení výkonu aplikací.

## Zdroje
- **Dokumentace**: [Dokumentace k Aspose.Cells](https://reference.aspose.com/cells/net/)
- **Stáhnout**: [Vydání Aspose.Cells](https://releases.aspose.com/cells/net/)
- **Nákup**: [Koupit Aspose.Cells](https://purchase.aspose.com/buy)
- **Bezplatná zkušební verze**: [Vyzkoušejte Aspose.Cells zdarma](https://releases.aspose.com/cells/net/)
- **Dočasná licence**: [Získejte dočasnou licenci](https://purchase.aspose.com/temporary-license/) 


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}