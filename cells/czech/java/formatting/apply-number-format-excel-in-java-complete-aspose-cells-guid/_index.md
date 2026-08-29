---
category: general
date: 2026-07-20
description: Použijte formát čísel v Excelu pomocí Javy a Aspose.Cells. Naučte se,
  jak aplikovat měnový styl v Excelu, vytvořit sešit Excel v Javě a efektivně importovat
  datovou tabulku do Excelu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- apply currency style excel
- create excel workbook java
- import datatable to excel
language: cs
lastmod: 2026-07-20
og_description: Použijte formát čísel v Excelu pomocí Javy. Tento průvodce vám ukáže,
  jak použít měnový styl v Excelu, vytvořit sešit Excel v Javě a krok za krokem importovat
  datovou tabulku do Excelu.
og_image_alt: Screenshot of an Excel workbook where apply number format excel has
  been applied to a currency column
og_title: Použití číselného formátu v Excelu v Javě – Kompletní tutoriál Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Apply number format excel using Java and Aspose.Cells. Learn how to
    apply currency style excel, create excel workbook java, and import datatable to
    excel efficiently.
  headline: Apply Number Format Excel in Java – Complete Aspose.Cells Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Open the workbook with `new Workbook("Existing.xlsx")`, fetch
      the target worksheet, and follow steps 3‑5 to apply the style array to new data.
    question: Can I apply the number format to an existing workbook?
  - answer: Use a different built‑in number index (`14` for short date, `22` for long
      date) or a custom format like `yyyy‑mm‑dd`. The workflow stays the same.
    question: What if I need to format dates instead of currency?
  - answer: 'Yes. Just change the file extension in `workbook.save("MyFile.xls")`.
      Aspose will automatically switch to the binary format. ## Wrap‑Up – What We
      Achieved We have **applied number format excel** to a column of monetary values,
      demonstrated how to **apply currency style excel**, shown the simplest wa'
    question: Does this work with older Excel versions (.xls)?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Použití číselného formátu v Excelu v Javě – Kompletní průvodce Aspose.Cells
url: /cs/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Použití formátu čísel v Excelu v Javě – Kompletní průvodce Aspose.Cells

Už jste se někdy zamýšleli, jak **aplikovat formát čísel v Excelu** přímo z Java kódu? Možná vytváříte finanční zprávy nebo potřebujete rychle naformátovat sloupec částek, aniž byste museli ručně otevírat Excel. Dobrá zpráva? S Aspose.Cells to můžete udělat během několika řádků a zároveň se naučíte, jak **aplikovat styl měny v Excelu**, **vytvořit Excel sešit v Javě** a **importovat datatable do Excelu** v jedné přehledné rutině.

V tomto tutoriálu projdeme reálný příklad: seznam částek uložených v Java `List<Map<String,Object>>` se importuje do nového sešitu, první sloupec získá vestavěný formát měny a soubor se uloží připravený k distribuci. Připravení vidět, jak je to jednoduché? Pojďme na to.

## Požadavky – Co budete potřebovat

Než začneme, ujistěte se, že máte:

- **Java Development Kit (JDK) 8+** – kód běží na jakémkoli aktuálním JDK.
- **Aspose.Cells for Java** knihovnu (Maven artefakt `com.aspose:aspose-cells`) – to je engine, který umožňuje manipulovat se soubory Excel bez nainstalovaného Office.
- **Oblíbené IDE** (IntelliJ IDEA, Eclipse, VS Code…) – jakýkoli editor stačí, ale IDE urychlí ladění.
- Základní znalost **Java collections** – použijeme `List` map, abychom napodobili DataTable.

A to je vše. Žádné externí služby, žádná instalace Excelu, jen čistá Java.

## Krok 1: Vytvoření Excel sešitu v Javě – Instanciace Workbooku

Prvním krokem potřebujeme objekt workbooku. Představte si ho jako prázdné plátno, kam vše umístíme.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook(); // creates an in‑memory Excel file
```

Proč vytvořit workbook jako první? Aspose.Cells pracuje kompletně v paměti, takže můžete přidávat listy, styly i data, aniž byste se dotkli disku. Tento přístup je rychlý a udržuje váš kód testovatelný.

## Krok 2: Příprava dat – Import Datatable do Excelu pomocí Listu map

V mnoha podnikových aplikacích data přicházejí z databází jako tabulky. Zde to simulujeme pomocí `List<Map<String,Object>>`. Každá mapa představuje řádek a klíč `"Amount"` mapuje na číselnou hodnotu.

```java
// Step 2: Build a DataTable‑like structure (list of maps)
List<Map<String, Object>> dataRows = new ArrayList<>();

// Row 1
dataRows.add(new HashMap<>() {{
    put("Amount", 1234.56);
}});
// Row 2
dataRows.add(new HashMap<>() {{
    put("Amount", 7890.12);
}});
```

Možná se ptáte: „Proč nepoužít `ResultSet` nebo POJO?“ Metoda `importDataTable` přijímá jakoukoli kolekci, která se chová jako DataTable, a seznam map je nejjednodušší způsob, jak koncept demonstrovat bez dalších závislostí.

## Krok 3: Definice formátu čísel – Aplikace stylu měny v Excelu

Nyní přichází jádro tutoriálu: **aplikovat formát čísel v Excelu**. Aspose.Cells obsahuje vestavěné formáty čísel; formát měny má index 5. Vezmeme výchozí styl z prvního listu, upravíme jeho formát čísel a uložíme ho pro pozdější použití.

```java
// Step 3: Get the default style and set a currency number format
Style currencyStyle = workbook.getWorksheets().get(0).getCells().getDefaultStyle();
currencyStyle.setNumber(5); // 5 = built‑in currency format ($#,##0.00)
```

Proč použít výchozí styl jako základ? Ten již obsahuje výchozí písmo, zarovnání a další nastavení sešitu, takže stačí změnit jen to, co je podstatné – v tomto případě formát čísel. Pokud byste potřebovali vlastní formát (např. “€#,##0.00”), můžete místo toho zavolat `currencyStyle.setCustom("#,##0.00 €")`.

## Krok 4: Nastavení možností importu – Propojení pole stylů

Aspose.Cells umožňuje předat pole objektů `Style`, které odpovídají importovaným sloupcům. Protože naše data mají jen jeden sloupec, předáme jednoprvkové pole obsahující styl měny.

```java
// Step 4: Configure import options with the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(new Style[] { currencyStyle });
```

Pokud budete chtít stylovat více sloupců různě, stačí pole rozšířit: `new Style[] { styleForCol1, styleForCol2, … }`. Pořadí stylů odpovídá pořadí sloupců ve zdrojových datech.

## Krok 5: Import dat – Přenesení Datatable do listu

S připraveným workbookem, daty i styly můžeme konečně **importovat datatable do Excelu**. Začneme v buňce `A1`, zahrneme záhlaví sloupců (`true`) a předáme `ImportTableOptions`.

```java
// Step 5: Perform the import
Worksheet worksheet = workbook.getWorksheets().get(0);
worksheet.getCells().importDataTable(dataRows, true, "A1", importOptions);
```

Všimněte si příznaku `true` – Aspose.Cells automaticky vygeneruje řádek záhlaví na základě klíčů map (`"Amount"`). Pokud jej nastavíte na `false`, záhlaví bude vynecháno a získáte větší kontrolu nad finálním rozvržením.

## Krok 6: Uložení souboru – Vytvoření Excel sešitu v Javě na disku

Poslední částí skládačky je uložení workbooku z paměti do fyzického souboru. Můžete zvolit libovolný formát, který Aspose podporuje (`.xlsx`, `.xls`, `.csv`, …). Zde uložíme jako soubor XLSX.

```java
// Step 6: Save the workbook to disk
String outputPath = "DataTableWithCurrencyStyle.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Po spuštění programu otevřete vygenerovaný soubor. Uvidíte sloupec `"Amount"` naformátovaný s dolarovým znakem, dvěma desetinnými místy a správnými oddělovači tisíců – přesně to, co očekáváte při **aplikaci formátu čísel v Excelu** pro měnové hodnoty.

## Očekávaný výsledek

| Amount |
|--------|
| $1,234.56 |
| $7,890.12 |

Záhlaví „Amount“ je tučné (výchozí styl) a každá buňka pod ním zobrazuje měnový formát, který jsme nastavili. Žádné ruční formátování v Excelu není potřeba.

## Praktické tipy a časté úskalí

- **Znovupoužití stylů** – Styly jsou lehké, ale vytváření nového `Style` pro každou buňku může snížit výkon. Vždy znovupoužívejte objekt stylu, když aplikujete stejný formát na mnoho buněk, tak jak jsme to udělali s `currencyStyle`.
- **Vlastní formáty** – Pokud vaše lokalita používá jiný měnový symbol, nahraďte `currencyStyle.setNumber(5)` za `currencyStyle.setCustom("€#,##0.00")`. Otestujte formát v Excelu, abyste se ujistili, že funguje podle očekávání.
- **Velké datové sady** – Pro tisíce řádků zvažte použití `importDataTable` s příznakem `ImportTableOptions.setImportDataOnly(true)`, který přeskočí generování záhlaví a urychlí import.
- **Bezpečnost vláken** – Objekt Aspose.Cells **není** thread‑safe. Vytvořte samostatný `Workbook` pro každé vlákno, pokud generujete reporty paralelně.

## Často kladené otázky

**Q: Můžu aplikovat formát čísel na existující sešit?**  
A: Rozhodně. Otevřete sešit pomocí `new Workbook("Existing.xlsx")`, získejte cílový list a postupujte podle kroků 3‑5, abyste na nová data aplikovali pole stylů.

**Q: Co když potřebuji formátovat datum místo měny?**  
A: Použijte jiný vestavěný index čísla (`14` pro krátké datum, `22` pro dlouhé datum) nebo vlastní formát jako `yyyy‑mm‑dd`. Pracovní postup zůstává stejný.

**Q: Funguje to i se staršími verzemi Excelu (.xls)?**  
A: Ano. Stačí změnit příponu souboru v `workbook.save("MyFile.xls")`. Aspose automaticky přepne do binárního formátu.

## Závěr – Co jsme dosáhli

Úspěšně jsme **aplikovali formát čísel v Excelu** na sloupec peněžních hodnot, ukázali, jak **aplikovat styl měny v Excelu**, představili nejjednodušší způsob, jak **vytvořit Excel sešit v Javě**, a pomocí Aspose.Cells **importovali datatable do Excelu** bez nutnosti UI. Vše bylo provedeno v krátkém, samostatném programu, který můžete zkopírovat, vložit a spustit.

Co dál? Zkuste rozšířit příklad:

- Přidejte další sloupce (např. „Date“, „Description“) a přiřaďte různým sloupcům odlišné styly.
- Exportujte stejná data do CSV a porovnejte, jak se ztrácejí formáty čísel.
- Integrovejte kód do Spring Boot služby, která vrací workbook jako stahovatelnou HTTP odpověď.

Nebojte se experimentovat a pokud narazíte na problémy, zanechte komentář níže. Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobným krok‑za‑krokem vysvětlením, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [How to Apply Styles to Excel Cells Using Aspose.Cells for Java - Complete Guide](/cells/english/java/formatting/apply-styles-excel-aspose-cells-java/)
- [Merge Cells & Apply Styles in Excel using Aspose.Cells for Java - A Complete Guide](/cells/english/java/formatting/merge-cells-apply-styles-aspose-cells-java/)
- [Aspose.Cells for Java&#58; How to Create and Format Excel Workbooks Efficiently](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}