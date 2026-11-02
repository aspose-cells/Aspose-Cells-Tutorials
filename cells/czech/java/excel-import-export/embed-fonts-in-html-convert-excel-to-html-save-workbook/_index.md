---
category: general
date: 2026-06-27
description: Vkládejte písma do HTML při převodu Excelu na HTML. Naučte se, jak uložit
  sešit jako HTML s vloženými písmy pomocí jednoduchého Java kódu.
draft: false
keywords:
- embed fonts in html
- convert excel to html
- save workbook as html
- Java Excel to HTML conversion
- Aspose.Cells HTML export
language: cs
og_description: Vkládejte písma do HTML při převodu Excelu na HTML. Tento návod ukazuje,
  jak uložit sešit jako HTML s vloženými písmy pomocí Javy.
og_title: Vložit písma do HTML – Převést Excel do HTML a uložit sešit
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Embed fonts in HTML when you convert Excel to HTML. Learn how to save
    workbook as HTML with embedded fonts using simple Java code.
  headline: Embed Fonts in HTML – Convert Excel to HTML & Save Workbook
  type: TechArticle
- description: Embed fonts in HTML when you convert Excel to HTML. Learn how to save
    workbook as HTML with embedded fonts using simple Java code.
  name: Embed Fonts in HTML – Convert Excel to HTML & Save Workbook
  steps:
  - name: Right‑click the page → “View Page Source”.
    text: Right‑click the page → “View Page Source”.
  - name: 'Search for `@font-face`. You’ll find a CSS rule that contains a `src: url(data:font/ttf;base64,…)`
      line—this is the Base64‑encoded font data.'
    text: 'Search for `@font-face`. You’ll find a CSS rule that contains a `src: url(data:font/ttf;base64,…)`
      line—this is the Base64‑encoded font data.'
  - name: Load or create the workbook.
    text: Load or create the workbook.
  - name: Create `HtmlSaveOptions` and enable `setEmbedFonts(true)`.
    text: Create `HtmlSaveOptions` and enable `setEmbedFonts(true)`.
  - name: Call `Workbook.save` with those options.
    text: Call `Workbook.save` with those options.
  type: HowTo
tags:
- Java
- Aspose.Cells
- HTML
- Excel
title: Vložit písma do HTML – Převést Excel do HTML a uložit sešit
url: /cs/java/excel-import-export/embed-fonts-in-html-convert-excel-to-html-save-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vložit písma do HTML – převod Excelu do HTML a uložení sešitu

Už jste někdy potřebovali **vložit písma do HTML**, když *převádíte Excel do HTML*? Možná budujete portál pro reportování a výchozí webová písma vám nevyhovují. Dobrou zprávou je, že se nemusíte spokojit s nevýrazným, generickým vzhledem — Aspose.Cells vám umožní zabalit přesně ty typy písma, které jste použili v tabulce, přímo do vygenerovaného souboru HTML.

V tomto tutoriálu projdeme kompletním, připraveným k spuštění Java příkladem, který **uloží sešit jako HTML** s vloženými písmy, vysvětlí, proč byste to chtěli udělat, a upozorní na několik možných úskalí. Na konci budete mít samostatnou HTML stránku, která vypadá přesně jako původní list Excelu, bez chybějících znaků a bez potíží s externím CSS.

## Co se naučíte

- Jak načíst existující Excel sešit (nebo vytvořit nový od nuly) v Javě.  
- Jak nakonfigurovat `HtmlSaveOptions`, aby vložil písma sešitu přímo do výstupu HTML.  
- Jak zavolat `Workbook.save`, aby byl soubor uložen jako **HTML s vloženými písmy**.  
- Tipy pro práci s velkými soubory písem, vlastními adresáři písem a řešení běžných problémů.  

> **Předpoklad:** Potřebujete Aspose.Cells pro Java (nejnovější verze) ve vaší classpath a runtime Java 8+. Žádné další knihovny třetích stran nejsou vyžadovány.

---

## Krok 1: Nastavení projektu a import potřebných tříd

Než se ponoříme do kódu, ujistěte se, že vývojové prostředí je připravené. Pokud používáte Maven, přidejte závislost Aspose.Cells do vašeho `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the newest version available -->
</dependency>
```

Pokud dáváte přednost Gradlu, ekvivalent je:

```gradle
implementation 'com.aspose:aspose-cells:23.12'
```

> **Tip:** Udržujte knihovnu aktuální. Nová vydání často zlepšují práci s písmy a snižují velikost vložených dat.

Nyní importujte třídy, které budeme potřebovat:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.HtmlSaveOptions;
import com.aspose.cells.SaveFormat;
import java.io.File;
```

Tyto importy nám poskytují přístup k modelu sešitu, možnostem exportu HTML a několika pomocným třídám.

---

## Krok 2: Načtení (nebo vytvoření) Excel sešitu

Můžete buď načíst existující soubor `.xlsx`, nebo vytvořit sešit za běhu. Pro ilustraci předpokládejme, že máme soubor `Sample.xlsx` ve složce `resources` projektu.

```java
// Load an existing workbook
String inputPath = "resources/Sample.xlsx";
Workbook wb = new Workbook(inputPath);
```

Pokud nemáte zdrojový soubor, můžete rychle vygenerovat sešit:

```java
// Create a workbook from scratch (optional)
Workbook wb = new Workbook();               // creates a new empty workbook
wb.getWorksheets().get(0).getCells().putValue("A1", "Hello, world!");
```

> **Proč je to důležité:** Když vkládáte písma, Aspose.Cells extrahuje přesné definice písem použitých v sešitu. Pokud sešit obsahuje vlastní písma, budou s HTML přenesena, což zaručuje vizuální věrnost.

---

## Krok 3: Konfigurace HtmlSaveOptions pro vložení písem

Toto je jádro tutoriálu. Ve výchozím nastavení `HtmlSaveOptions` zapisuje CSS, které odkazuje na systémová písma. Pro změnu tohoto chování povolíme příznak `setEmbedFonts(true)`.

```java
// Step 1: Create HTML save options
HtmlSaveOptions htmlOpts = new HtmlSaveOptions(SaveFormat.HTML);

// Step 2: Enable embedding of fonts in the HTML output
htmlOpts.setEmbedFonts(true);

// (Optional) Reduce the size of embedded fonts by subsetting only used glyphs
htmlOpts.setSubsetFonts(true);
```

### Co jednotlivé možnosti dělají

| Option | Default | Effect when changed |
|--------|---------|---------------------|
| `setEmbedFonts(true)` | `false` | Vloží celé soubory písem (obvykle jako Base64‑kódované data URI) do vygenerovaného HTML. |
| `setSubsetFonts(true)` | `false` | Omezí vložené písmo jen na znaky, které jsou skutečně použity, což dramaticky zmenší velikost souboru. |
| `setFontEmbeddingMode(HtmlSaveOptions.FontEmbeddingMode.EMBED_ALL)` | `EMBED_ALL` | Můžete zvolit vložení pouze konkrétních písem, pokud máte licenční omezení. |

> **Hraniční případ:** Pokud sešit používá písmo, které není nainstalováno na serveru, Aspose.Cells přejde na výchozí systémové písmo. Aby nedošlo k překvapením, ujistěte se, že všechna vlastní písma jsou dostupná v adresáři písem Java runtime nebo je zaregistrujte ručně pomocí `FontConfig`.

---

## Krok 4: Uložení sešitu jako HTML s vloženými písmy

Jakmile jsou možnosti nastaveny, jednoduše zavoláme `save`. Výstup bude jediný soubor `.html`, který obsahuje data sešitu **a** soubory písem zakódované přímo v markup.

```java
// Step 3: Save the workbook as an HTML file with embedded fonts
String outputDir = "output";
new File(outputDir).mkdirs(); // Ensure the folder exists

String outputPath = outputDir + File.separator + "page.html";
wb.save(outputPath, htmlOpts);

System.out.println("HTML file with embedded fonts created at: " + outputPath);
```

Když otevřete `page.html` v libovolném moderním prohlížeči, stránka se vykreslí se stejnou typografií, jakou jste viděli v Excelu — žádné externí soubory písem, žádné chybějící znaky.

---

## Krok 5: Ověření výsledku a pochopení výstupu

Otevřete vygenerovaný HTML soubor v prohlížeči (Chrome, Firefox, Edge — kterýkoliv vyhovuje). Měli byste vidět list vykreslený věrně. Pro dvojitou kontrolu, že jsou písma skutečně vložena:

1. Klikněte pravým tlačítkem na stránku → „Zobrazit zdroj stránky“.  
2. Vyhledejte `@font-face`. Najdete CSS pravidlo, které obsahuje řádek `src: url(data:font/ttf;base64,…)` — to jsou Base64‑kódovaná data písem.  

Pokud to vidíte, krok **vložit písma do HTML** byl úspěšný.

### Časté otázky

- **Proč je HTML soubor větší, než se očekávalo?**  
  Vložení úplných souborů písem může přidat několik set kilobajtů. Použijte `setSubsetFonts(true)` pro zmenšení, nebo zvažte převod jen potřebných listů.

- **Mohu vložit jen konkrétní písmo?**  
  Ano. Nastavte `htmlOpts.setFontEmbeddingMode(HtmlSaveOptions.FontEmbeddingMode.EMBED_SPECIFIED)` a poté specifikujte názvy písem pomocí `htmlOpts.getSpecifiedFontNames().add("MyCustomFont")`.

- **Co když je písmo licencováno a nemohu ho vložit?**  
  Vypněte příznak (`setEmbedFonts(false)`) a poskytněte web‑bezpečnou náhradu pomocí CSS, nebo hostujte písmo na CDN, kde máte povolení.

---

## Krok 6: Práce s velkými sešity a tipy na výkon

Vkládání písem funguje dobře pro středně velké tabulky, ale sešit s desítkami vlastních písem může nafouknout velikost HTML. Zde je několik doporučení zaměřených na výkon:

- **Podmnožina písem** (již ukázáno), aby se zachovala jen použita písmena.  
- **Exportovat jen potřebné listy** pomocí `htmlOpts.setExportActiveWorksheetOnly(true)`.  
- **Komprimovat HTML** po vygenerování (např. gzip na serveru) pro snížení latence sítě.  
- **Ukládat vygenerované HTML do cache**, pokud je stejný Excel soubor požadován často.

---

## Krok 7: Další kroky – Přesah základního exportu

Nyní, když ovládáte **vkládání písem do HTML**, můžete chtít prozkoumat související možnosti:

- **Převést Excel do HTML s obrázky** (`htmlOpts.setExportImagesAsBase64(true)`).  
- **Generovat PDF místo HTML** (`wb.save("output.pdf", SaveFormat.PDF)`).  
- **Vytvořit responzivní HTML** úpravou `htmlOpts.setExportActiveWorksheetOnly` a `htmlOpts.setExportGridLines`.  

Všechny tyto funkce sdílejí stejný vzor: nakonfigurujte objekt `*SaveOptions`, přepněte příslušné příznaky a zavolejte `Workbook.save`.

## Závěr

Právě jste se naučili, jak **vložit písma do HTML** při **převodu Excelu do HTML** a **uložení sešitu jako HTML** pomocí Aspose.Cells pro Java. Klíčové kroky jsou:

1. Načíst nebo vytvořit sešit.  
2. Vytvořit `HtmlSaveOptions` a povolit `setEmbedFonts(true)`.  
3. Zavolat `Workbook.save` s těmito možnostmi.

Výsledkem je jediný, přenosný HTML soubor, který vypadá přesně jako váš původní sešit — žádná chybějící písma, žádné extra CSS soubory a žádná závislost na písmech nainstalovaných u klienta.

Klidně experimentujte s podmnožinou písem, selektivním vkládáním nebo dokonce kombinací s cache na serveru pro scénáře s vysokým provozem. Pokud narazíte na nějaké podivnosti (např. nečekaně velké soubory nebo chybějící znaky), vraťte se k volitelným nastavením, která jsme probírali, a upravte je podle potřeby.

Šťastné programování a užívejte si pixel‑dokonalé HTML, které nyní můžete přímo naservírovat ze svých Java aplikací!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Převést Excel do HTML v Javě pomocí Aspose.Cells: Průvodce krok za krokem](/cells/english/java/workbook-operations/convert-excel-html-aspose-cells-java/)
- [Exportovat Excel do HTML pomocí Aspose.Cells pro Java: Kompletní průvodce](/cells/english/java/workbook-operations/export-excel-to-html-aspose-cells-java/)
- [Exportovat Excel do HTML pomocí IStreamProvider a Aspose.Cells pro Java: Obsáhlý průvodce](/cells/english/java/workbook-operations/export-excel-html-streamprovider-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}