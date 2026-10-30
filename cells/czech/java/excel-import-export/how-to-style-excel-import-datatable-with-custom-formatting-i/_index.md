---
category: general
date: 2026-07-03
description: Jak stylovat soubory Excel pomocí Javy. Naučte se formátovat datum ve
  sloupci v Excelu, použít číselný formát v Excelu, exportovat DataTable do XLSX a
  importovat DataTable do Excelu pomocí Aspose Cells.
draft: false
keywords:
- how to style excel
- format column date excel
- apply number format excel
- export datatable to xlsx
- import datatable into excel
language: cs
og_description: Jak stylovat soubory Excel v Javě. Tento tutoriál ukazuje, jak formátovat
  datum ve sloupci v Excelu, použít číselný formát v Excelu, exportovat DataTable
  do XLSX a importovat DataTable do Excelu.
og_title: Jak stylovat Excel – Java průvodce pro vlastní formátování sloupců
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to style Excel files using Java. Learn to format column date Excel,
    apply number format Excel, export DataTable to XLSX and import DataTable into
    Excel with Aspose Cells.
  headline: How to Style Excel – Import DataTable with Custom Formatting in Java
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: Jak stylovat Excel – importovat DataTable s vlastním formátováním v Javě
url: /cs/java/excel-import-export/how-to-style-excel-import-datatable-with-custom-formatting-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak stylovat Excel – Import DataTable s vlastním formátováním v Javě

Už jste se někdy zamýšleli **jak stylovat Excel** listy programově, aniž byste soubor otevírali ručně? Nejste sami. Mnoho vývojářů potřebuje generovat zprávy, kde je první sloupec tučný, druhý zobrazuje data a zbytek má čisté rozvržení. V tomto průvodci projdeme kompletním, spustitelným příkladem, který **importuje DataTable do Excelu**, aplikuje tučný záhlaví, formátuje sloupec s daty a nakonec **exportuje DataTable do XLSX**.  

Použijeme Aspose.Cells for Java, ale koncepty lze použít i s libovolnou knihovnou, která umožňuje pracovat se styly. Na konci budete mít znovupoužitelný vzor pro **apply number format Excel** buňky, **format column date Excel**, a nasadíte vylepšený sešit svým uživatelům.

## Požadavky

- Java 17 (nebo jakýkoli novější JDK)  
- Aspose.Cells for Java 23.9 nebo novější (bezplatná zkušební verze funguje)  
- Struktura podobná `DataTable` (v příkladu používáme jednoduchý mock)  
- Váš oblíbený IDE (IntelliJ IDEA, Eclipse, VS Code…)

Nejsou potřeba žádné další Maven pluginy; stačí přidat Aspose.Cells JAR do classpathu.

---

## Krok 1: Získání zdrojového DataTable – Příprava „Export DataTable do XLSX“

Než budeme moci **importovat datatable do excel**, potřebujeme objekt `DataTable`, který představuje data, jež chcete exportovat. Ve skutečných projektech jej můžete načíst z databáze, CSV souboru nebo API. Pro tento tutoriál vytvoříme malý mockovaný tabulku:

```java
import java.util.*;
import com.aspose.cells.*;

public class DemoData {
    public static DataTable getDataTable() {
        // Create a simple table with three columns: ID, Date, Amount
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", DataType.INTEGER);
        dt.getColumns().add("OrderDate", DataType.DATE_TIME);
        dt.getColumns().add("Total", DataType.DOUBLE);

        // Add a few rows
        dt.getRows().add(new Object[]{1, new Date(), 125.50});
        dt.getRows().add(new Object[]{2, new Date(System.currentTimeMillis() - 86400000L), 99.99});
        dt.getRows().add(new Object[]{3, new Date(System.currentTimeMillis() - 2*86400000L), 250.00});
        return dt;
    }
}
```

> **Proč je to důležité:** Získání správných dat hned na začátku znamená, že zbytek logiky stylování se může soustředit čistě na prezentaci, ne na manipulaci s daty.

---

## Krok 2: Vytvoření pole pro uložení definic stylů pro každý sloupec

Aspose.Cells vám umožňuje předat **Style[]** pole při importu `DataTable`. Každý prvek odpovídá jednomu sloupci a určuje, jak bude po importu vypadat. Alokujme pole podle počtu sloupců:

```java
DataTable dataTable = DemoData.getDataTable();
Style[] columnStyles = new Style[dataTable.getColumns().size()];
```

> **Tip:** Pokud máte mnoho sloupců, zvažte vytvoření pole ve smyčce a opakované použití jediného objektu `Style`, kde je formátování identické. Tím snížíte paměťovou zátěž.

---

## Krok 3: Definování stylů – Tučný záhlaví a formátování data

Nyní odpovíme na klasickou otázku **format column date excel** a také ukážeme **apply number format excel** pro ostatní sloupce.

```java
// --- Style for the first column (header bold) ---
columnStyles[0] = new Style();
columnStyles[0].getFont().setBold(true);          // Makes header text bold

// --- Style for the second column (date formatting) ---
columnStyles[1] = new Style();
columnStyles[1].setNumber(StyleNumberFormat.DATE); // Uses the built‑in DATE format

// --- Optional: Style for the third column (currency) ---
columnStyles[2] = new Style();
columnStyles[2].setNumber(StyleNumberFormat.CURRENCY_USD);
```

**Co se zde děje?**  
- `StyleNumberFormat.DATE` říká Excelu, aby buňku považoval za krátké datum (např. *01/31/2024*).  
- `StyleNumberFormat.CURRENCY_USD` automaticky přidá symbol `$` a dvě desetinná místa.  
- Nastavení písma na tučné v prvním sloupci zvýrazní záhlaví, což je častý požadavek, když **jak stylovat excel** tabulky pro čitelnost.

> **Okrajový případ:** Pokud vaše zdrojová data již obsahují formátované řetězce, možná je budete muset převést na objekty `java.util.Date` před importem; jinak je Excel bude považovat za prostý text.

---

## Krok 4: Vytvoření nového sešitu a přístup k prvnímu listu

Čerstvý sešit nám poskytuje čisté plátno. Získáme první list, kam bude import umístěn.

```java
Workbook workbook = new Workbook();               // New empty workbook
Worksheet worksheet = workbook.getWorksheets().get(0); // First sheet (index 0)
```

> **Proč nový sešit?** Začínání od nuly zaručuje, že žádné zbylé styly nebo skryté řádky nebudou zasahovat do konečného výstupu — což je zásadní, když **jak stylovat excel** soubory konzistentně napříč více běhy.

---

## Krok 5: Import DataTable s definicemi stylů sloupců

Zde je jádro operace: předání `DataTable` do listu při aplikaci dříve vytvořeného pole stylů.

```java
// The third argument (true) tells Aspose.Cells to include column headers.
worksheet.getCells().importDataTable(dataTable, true, columnStyles);
```

**Vysvětlení:**  
- `importDataTable` kopíruje jak řádek záhlaví, tak datové řádky.  
- Pole `columnStyles` se zarovnává ke každému sloupci, takže záhlaví prvního sloupce se stane tučným, druhý sloupec zobrazí data a třetí sloupec se zobrazí jako měna.  
- Tento jediný řádek nahrazuje desítky ručních formátovacích kroků buňka‑po‑buňce a ukazuje čistý způsob, jak **apply number format excel** programově.

---

## Krok 6: Uložení stylovaného sešitu – Dokončení „Export DataTable do XLSX“

Nakonec uložíme sešit na disk. Upravit cestu na zapisovatelnou složku ve vašem počítači.

```java
String outputPath = "C:/temp/styledImport.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Otevřete soubor v Excelu a měli byste vidět:

- Záhlaví sloupce **ID** tučně.  
- Sloupec **OrderDate** formátovaný jako datum (např. *04/27/2024*).  
- Sloupec **Total** zobrazený se znakem dolaru a dvěma desetinnými místy.

> **Pro tip:** Pokud potřebujete podporovat starší verze Excelu, zavolejte `workbook.save(outputPath, SaveFormat.XLS)` místo výchozího XLSX.

---

## Krok 7: Ověření výsledku a volitelné úpravy

Je dobré praxí dvakrát zkontrolovat vygenerovaný soubor, zejména při automatizaci zpráv pro stakeholdery.

```java
// Quick verification: read the first cell's style
Cell firstHeader = worksheet.getCells().get(0, 0);
boolean isBold = firstHeader.getStyle().getFont().isBold();
System.out.println("Header bold? " + isBold);
```

Pokud `isBold` vypíše `true`, vaše **jak stylovat excel** rutina fungovala podle očekávání. Odtud můžete:

- Přidat podmíněné formátování (např. zvýraznit součty > $200).  
- Uzamknout horní řádek pro snadnější posouvání.  
- Vložit graf, který odkazuje na importovaná data.

Všechny tyto rozšíření následují stejný vzor: definovat `Style`, aplikovat jej a uložit.

---

## Časté otázky a okrajové případy

| Question | Answer |
|----------|--------|
| **Mohu stylovat více sloupců stejným způsobem?** | Ano — znovu použijte jedinou instanci `Style` pro všechny sloupce, které sdílejí formátování. |
| **Co když má můj DataTable více sloupců než stylů?** | Každý sloupec bez odpovídající položky v `columnStyles` použije výchozí styl. |
| **Jak změním formát data na „dd‑MMM‑yyyy“?** | Použijte `columnStyles[1].setCustom("#dd-MMM-yyyy#");` místo vestavěného `DATE`. |
| **Existuje způsob, jak automaticky nastavit šířku sloupců po importu?** | Zavolejte `worksheet.autoFitColumns();` po `importDataTable`. |
| **Bude to fungovat na Linuxu/macOS?** | Rozhodně — Aspose.Cells je platformně nezávislý, pokud máte kompatibilní JDK. |

---

## Závěr

Nyní máte solidní, end‑to‑end příklad **jak stylovat Excel** sešitu pomocí **importování datatable do excel**, **format column date excel** a **apply number format excel** v Javě. Kód ukazuje celý tok od **export datatable do xlsx** po otevření souboru v Excelu, pokrývající jak *co*, tak *proč* za každým krokem.  

Vyzkoušejte to: upravte pole stylů, přidejte další sloupce nebo zapojte skutečný databázový dotaz. Stejný vzor vám umožní generovat profesionálně vypadající zprávy na jedno kliknutí, bez nutnosti ručního formátování.

---

![Styled Excel worksheet generated by the tutorial code](https://example.com/images/styled-worksheet.png "Screenshot of styled Excel worksheet created using Java and Aspose.Cells")

*Obrázek: “Stylovaný list Excel vytvořený pomocí Javy a Aspose.Cells, zobrazující tučné záhlaví a formátovaný sloupec s datem.”*

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Jak vytvořit a formátovat buňky Excel pomocí Aspose.Cells for Java: Průvodce krok za krokem](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Jak stylovat buňky Excel a přidávat hypertextové odkazy pomocí Aspose.Cells for Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)
- [Aspose.Cells for Java: Jak efektivně vytvářet a formátovat sešity Excel](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}