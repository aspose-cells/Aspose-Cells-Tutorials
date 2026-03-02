---
category: general
date: 2026-03-01
description: Naučte se, jak vložit písma do HTML a dalších formátů. Podrobný návod
  krok za krokem, který zahrnuje vložení písem v HTML, převod Excelu do HTML, jak
  exportovat OLE a převod Excelu do XPS.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- convert excel to html
- how to export ole
- convert excel to xps
language: cs
og_description: Jak vložit fonty do HTML, XPS a OLE exportů. Naučte se celý pracovní
  postup, podívejte se na spustitelný Java kód a ovládněte vkládání fontů do HTML
  pro konverze do Excelu.
og_title: Jak vložit fonty – kompletní Java tutoriál
tags:
- Aspose.Cells
- Java
- Document Export
title: Jak vložit písma – Kompletní průvodce pro export HTML, XPS a OLE
url: /cs/java/ole-objects-embedded-content/how-to-embed-fonts-complete-guide-for-html-xps-and-ole-expor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vložit písma – Kompletní průvodce pro HTML, XPS a OLE export

Už jste se někdy zamýšleli **jak vložit písma**, když převádíte sešit Excelu na webovou stránku nebo tisknutelný dokument? Nejste v tom sami. Mnoho vývojářů narazí na problém, kdy výstup vypadá na jejich počítači dobře, ale na jiném selže, protože požadovaná písma chybí.

V tomto tutoriálu projdeme reálný scénář s použitím Aspose.Cells pro Java: vložíme písma do HTML, zachováme výběrové znaky emoji při převodu na XPS a dokonce udržíme OLE objekt editovatelný při exportu do PPTX. Na konci budete mít pevné řešení připravené ke kopírování a vložení, které odpovídá na otázku „jak vložit písma“ a také se dotýká **embed fonts in html**, **convert excel to html**, **how to export ole** a **convert excel to xps**.

## Požadavky

- Java 17 (nebo jakýkoli aktuální JDK)  
- Aspose.Cells pro Java 25.x nebo novější  
- Vývojové IDE (IntelliJ IDEA, Eclipse nebo VS Code)  
- Základní znalost datových struktur Excelu  

Žádné externí služby nejsou vyžadovány – vše běží lokálně.

## Přehled řešení

1. **Vytvořte sešit** a použijte funkci `WRAPCOLS` k převodu vertikálního rozsahu na rozvržení se třemi sloupci.  
2. **Uložte sešit jako XPS** a zapněte výběrové znaky písma, aby emoji zůstaly zachovány.  
3. **Exportujte do HTML** s vloženými písmy, což zaručuje, že stránka bude vypadat stejně všude.  
4. **Exportujte sešit obsahující OLE objekt do PPTX**, přičemž zachováte editovatelnost.  
5. **Použijte šablonu Smart Marker**, která demonstruje vazbu master‑detail.

Každý krok je oddělen ve své vlastní sekci H2, což usnadňuje rychlé procházení průvodce jak pro vyhledávače, tak pro AI asistenty.

![Ilustrace, jak vložit písma](image.png "jak vložit písma")

*Text alternativního popisu obrázku: diagram, jak vložit písma, zobrazující pracovní postup od Excelu k HTML, XPS a PPTX.*

---

## Krok 1 – Vytvořte sešit a použijte WRAPCOLS (Proč je to důležité pro embed fonts in html)

Než budeme mluvit o vkládání písem, potřebujeme sešit, který skutečně obsahuje data. Funkce `WRAPCOLS` je praktický způsob, jak rozdělit jeden sloupec na více sloupců, což často činí výsledné HTML čitelnějším.

```java
import com.aspose.cells.*;

public class EmbedFontsDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Populate A2:A10 with sample data
        for (int i = 2; i <= 10; i++) {
            sheet.getCells().get("A" + i).putValue("Item " + (i - 1));
        }

        // Use WRAPCOLS to create a 3‑column block starting at A1
        Cell resultCell = sheet.getCells().get("A1");
        resultCell.setFormula("=WRAPCOLS(A2:A10,3)");
        workbook.calculateFormula();

        System.out.println("WRAPCOLS result: " + resultCell.getStringValue());
        // -----------------------------------------------------------------
        // The rest of the steps are demonstrated after this point.
        // -----------------------------------------------------------------
```

**Proč tento krok?**  
Volání `WRAPCOLS` vytvoří více‑sloupcový rozsah, který se později v HTML zobrazí jako tabulka. Když později **embed fonts in html**, stylování tabulky bude záviset na písmu, která vložíme, což zajišťuje konzistentní vykreslování napříč prohlížeči.

## Krok 2 – Uložte sešit jako XPS a zachovejte emoji (convert excel to xps)

Pokud potřebujete formát připravený k tisku, XPS je solidní volba. Moderní dokumenty však často obsahují emoji nebo symboly, které používají výběrové znaky. Zapnutí `EnableFontVariationSelectors` zajistí, že tyto znaky přežijí převod.

```java
        // --------------------------------------------------------------
        // Step 2: Save as XPS with font variation selectors enabled
        // --------------------------------------------------------------
        WorkbookSettings settings = workbook.getSettings();
        settings.setEnableFontVariationSelectors(true); // crucial for emoji

        String xpsPath = "output/withVariations.xps";
        workbook.save(xpsPath, SaveFormat.XPS);
        System.out.println("Workbook saved as XPS at: " + xpsPath);
```

**Co získáte:**  
XPS soubor, který zobrazuje jakékoli vložené emoji přesně tak, jak jsou ve zdrojovém sešitu. To splňuje požadavek **convert excel to xps** a ukazuje, že práce s písmy není omezena jen na HTML.

## Krok 3 – Export do HTML s vloženými písmy (how to embed fonts & embed fonts in html)

Nyní přicházíme k jádru tutoriálu: **how to embed fonts** při převodu Excelu do HTML. Aspose.Cells nám umožňuje vložit písma přímo do vygenerovaného HTML souboru, čímž eliminuje potřebu externích souborů písem.

```java
        // --------------------------------------------------------------
        // Step 3: Export to HTML with embedded fonts
        // --------------------------------------------------------------
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setEmbedFonts(true); // this is the key line for embed fonts in html
        htmlOptions.setExportImagesAsBase64(true); // optional, keeps all assets in one file

        String htmlPath = "output/embeddedFonts.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML with embedded fonts saved at: " + htmlPath);
```

**Jak to funguje:**  
`setEmbedFonts(true)` říká rendereru, aby načetl soubory písem použité v sešitu a vložil je jako Base64‑kódované `@font-face` pravidla uvnitř tagu `<style>`. Výsledné HTML je samostatné, takže jej můžete nasadit na jakýkoli server a písma se vykreslí správně – přesně to, co vývojáři hledají, když zadávají **how to embed fonts**.

**Očekávaný úryvek výstupu (v souboru `embeddedFonts.html`):**

```html
<style>
@font-face{font-family:"Arial";src:url(data:font/ttf;base64,AAEAAA... ) format('truetype');}
</style>
<table>
  <tr><td>Item 1</td><td>Item 4</td><td>Item 7</td></tr>
  <tr><td>Item 2</td><td>Item 5</td><td>Item 8</td></tr>
  <tr><td>Item 3</td><td>Item 6</td><td>Item 9</td></tr>
</table>
```

Všimněte si pravidla `@font-face` – to je konkrétní odpověď na **embed fonts in html**.

## Krok 4 – Export sešitu obsahujícího OLE objekt do PPTX (how to export ole)

Mnoho obchodních reportů vkládá dokumenty Word, PDF nebo jiné sešity Excelu jako OLE objekty. Při exportu takového sešitu do PowerPointu často ztratíte možnost objekt upravovat. Aspose.Cells zachovává editovatelnost přímo z krabice.

```java
        // --------------------------------------------------------------
        // Step 4: Export a workbook with an OLE object to PPTX
        // --------------------------------------------------------------
        // Load a workbook that already contains an OLE object.
        Workbook oleWorkbook = new Workbook("input/oleObject.xlsx");

        String pptxPath = "output/oleEditable.pptx";
        oleWorkbook.save(pptxPath, SaveFormat.PPTX);
        System.out.println("PPTX with editable OLE object saved at: " + pptxPath);
```

**Proč je to důležité:**  
Pokud hledáte **how to export ole**, tento úryvek ukazuje přesné volání API. Výsledný snímek PowerPointu obsahuje OLE objekt jako živou komponentu, kterou lze dvojklikem upravit – není potřeba žádné další post‑zpracování.

## Krok 5 – Použijte šablonu Smart Marker (master‑detail) a dokončete ukázku

Smart Markery vám umožňují svázat zdroj dat (Map, JSON, DataTable) přímo s šablonou Excelu. Zde je minimální příklad, který vypisuje řádky master‑detail.

```java
        // --------------------------------------------------------------
        // Step 5: Apply Smart Marker template (master‑detail)
        // --------------------------------------------------------------
        String smartMarkerTemplate = "${Orders.Master:OrderID,Customer}\n${Orders.Detail:Product,Qty,Price}";
        // Simulated data source
        java.util.Map<String, Object> dataSource = new java.util.HashMap<>();
        java.util.List<java.util.Map<String, Object>> master = new java.util.ArrayList<>();
        java.util.Map<String, Object> masterRow = new java.util.HashMap<>();
        masterRow.put("OrderID", 1001);
        masterRow.put("Customer", "Acme Corp");
        master.add(masterRow);
        dataSource.put("Orders.Master", master);

        java.util.List<java.util.Map<String, Object>> detail = new java.util.ArrayList<>();
        java.util.Map<String, Object> detailRow = new java.util.HashMap<>();
        detailRow.put("Product", "Widget");
        detailRow.put("Qty", 5);
        detailRow.put("Price", 9.99);
        detail.add(detailRow);
        dataSource.put("Orders.Detail", detail);

        SmartMarkerProcessor processor = new SmartMarkerProcessor(new Workbook());
        processor.apply(smartMarkerTemplate, dataSource);
        processor.getWorkbook().save("output/smartMarkerResult.xlsx");
        System.out.println("Smart Marker workbook saved.");
    }
}
```

**Co vidíte:**  
Nový sešit (`smartMarkerResult.xlsx`), kde jsou zástupné symboly šablony nahrazeny daty. Tento krok se přímo netýká písem, ale doplňuje tutoriál ukázkou typického workflow reportování, který často předchází exportu **embed fonts in html**.

## Časté úskalí a tipy (Zajištění úspěšného vkládání písem)

| Problém | Proč k tomu dochází | Oprava |
|-------|----------------|-----|
| Písma chybí v HTML souboru | Sešit používá systémové písmo, které není nainstalováno na serveru. | Použijte `Workbook.getSettings().setDefaultFont("Arial")` před načtením dat, nebo vložte požadované soubory písem ručně. |
| Výstupní HTML je obrovské | Vkládání mnoha velkých písem zvětšuje velikost souboru. | Omezte vkládání pouze na písma, která skutečně používáte: `htmlOptions.setFontEmbeddingMode(HtmlFontEmbeddingMode.EmbedSubset)`. |
| Emoji zmizí po konverzi na XPS | Výběrové znaky jsou ve výchozím nastavení odstraňovány. | Povolte `settings.setEnableFontVariationSelectors(true)` jak je ukázáno v Kroku 2. |
| OLE objekt se v PPTX stane statickým obrázkem | Zdrojový sešit byl uložen s `setSuppressOLEObjects(true)`. | Ujistěte se, že **ne**potlačujete OLE objekty při ukládání do PPTX. |

## Ověření výsledků

1. Otevřete `embeddedFonts.html` v Chrome/Firefox. Tabulka by měla být zobrazena pomocí vloženého písma (např. Arial), i když toto písmo není nainstalováno na počítači.  
2. Otevřete `withVariations.xps` ve Windows XPS Viewer. Emoji jako 👍 by měly být vykresleny správně.  
3. Otevřete `oleEditable.pptx` v PowerPointu. Dvojklikněte na OLE tvar;

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}