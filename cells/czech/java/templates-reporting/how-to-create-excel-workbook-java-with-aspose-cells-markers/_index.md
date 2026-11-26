---
category: general
date: 2026-11-25
description: Vytvořte příklad kódu v Javě pro vytvoření sešitu Excel pomocí smart
  markerů Aspose.Cells, který sváže pole JSON jako jednotlivé hodnoty.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- Aspose.Cells smart marker
- Java JSON to Excel
- setSmartMarkerData
- Excel export Java
language: cs
lastmod: 2026-11-25
og_description: Vytvořte Excel sešit v Javě s Aspose.Cells, abyste snadno exportovali
  pole JSON jako jednotlivé buňky. Postupujte podle krok‑za‑krokem průvodce.
og_image_alt: Screenshot of an Excel workbook created in Java using Aspose.Cells smart
  markers
og_title: Vytvoření Excel sešitu v Javě – průvodce chytrými značkami Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Create Excel workbook Java code example using Aspose.Cells smart markers
    to bind JSON arrays as single values.
  headline: How to create Excel workbook Java with Aspose.Cells markers
  type: TechArticle
- description: Create Excel workbook Java code example using Aspose.Cells smart markers
    to bind JSON arrays as single values.
  name: How to create Excel workbook Java with Aspose.Cells markers
  steps:
  - name: '**Creates a fresh workbook** – `new Workbook()` gives you an in‑memory
      Excel file with a default sheet.'
    text: '**Creates a fresh workbook** – `new Workbook()` gives you an in‑memory
      Excel file with a default sheet.'
  - name: '**Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` tells
      Aspose.Cells to replace the marker with the *entire* array, joined by commas.'
    text: '**Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` tells
      Aspose.Cells to replace the marker with the *entire* array, joined by commas.'
  - name: '**Builds a `Map` data source** – The key `"jsonArray"` matches the marker
      name; the value is a `String[]`.'
    text: '**Builds a `Map` data source** – The key `"jsonArray"` matches the marker
      name; the value is a `String[]`.'
  - name: '**Calls `setSmartMarkerData`** – This binds the map to the marker and performs
      the replacement.'
    text: '**Calls `setSmartMarkerData`** – This binds the map to the marker and performs
      the replacement.'
  - name: '**Saves the file** – `workbook.save(...)` writes `JsonSingleValue.xlsx`
      to disk.'
    text: '**Saves the file** – `workbook.save(...)` writes `JsonSingleValue.xlsx`
      to disk.'
  - name: Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc, or Google
      Sheets.
    text: Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc, or Google
      Sheets.
  - name: Confirm that cell **A1** reads `One, Two, Three`.
    text: Confirm that cell **A1** reads `One, Two, Three`.
  - name: Check that no extra rows or columns were added – the smart marker performed
      an in‑place replacement.
    text: Check that no extra rows or columns were added – the smart marker performed
      an in‑place replacement.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Jak vytvořit Excel sešit v Javě se značkami Aspose.Cells
url: /cs/java/templates-reporting/how-to-create-excel-workbook-java-with-aspose-cells-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vytvořit Excel sešit v Javě pomocí značek Aspose.Cells

Pokud potřebujete **vytvořit Excel sešit v Javě** kód, který zapíše JSON pole do jedné buňky, tento tutoriál vám přesně ukáže, jak na to. Pomocí inteligentních značek Aspose.Cells můžete zacházet s celým polem jako s jednou hodnotou, čímž se vyhnete ručním smyčkám a zápisům buňka po buňce.

Dozvíte se, jak nastavit sešit, definovat inteligentní značku, navázat zdroj dat `Map`, který obsahuje pole ve stylu JSON, a nakonec soubor uložit. Příklad funguje s Java 17+, Maven a bezplatnou zkušební knihovnou Aspose.Cells for Java.

---

![Screenshot of an Excel workbook created in Java using Aspose.Cells smart markers](excel-workbook-java.png){: .center-image alt="Snímek obrazovky Excel sešitu vytvořeného v Javě pomocí inteligentních značek Aspose.Cells"}

## Požadavky

| Požadavek | Proč je důležité |
|-------------|----------------|
| Java 17 nebo novější | Nejnovější jazykové funkce a bezpečnostní aktualizace |
| Maven 3.6+ | Zjednodušuje správu závislostí |
| Aspose.Cells for Java (v23.12 nebo novější) | Poskytuje API `Workbook`, `Worksheet` a inteligentních značek použité ve vzorku |
| Základní znalost kolekcí v Javě | Vytvoříte `Map<String, Object>`, která funguje jako zdroj dat |

Přidejte závislost Aspose.Cells do svého `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Vytvoření Excel sešitu v Javě – kompletní příklad

Následující program je **úplné, spustitelné** řešení. Zkopírujte jej do souboru pojmenovaného `ExcelSmartMarkerDemo.java`, zkompilujte a spusťte.

```java
package com.example.excel;

import com.aspose.cells.*;
import java.util.HashMap;
import java.util.Map;

/**
 * Demonstrates how to create Excel workbook Java using Aspose.Cells smart markers.
 * The smart marker "{{jsonArray:ArrayAsSingle}}" treats the whole array as a single cell value.
 */
public class ExcelSmartMarkerDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();                       // empty workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // first (default) sheet

        // Step 2: Define a smart marker that treats a JSON array as a single value
        // The "ArrayAsSingle" option concatenates the array elements with commas.
        String smartMarker = "{{jsonArray:ArrayAsSingle}}";
        worksheet.getCells().get("A1").putValue(smartMarker);

        // Step 3: Prepare the data source – a simple string array
        Map<String, Object> dataSource = new HashMap<>();
        dataSource.put("jsonArray", new String[] { "One", "Two", "Three" });

        // Step 4: Bind the data to the smart marker and save the workbook
        worksheet.getCells().get("A1").setSmartMarkerData(dataSource);
        workbook.save("JsonSingleValue.xlsx");   // workbook saved to project root
        System.out.println("Workbook created successfully.");
    }
}
```

### Co kód dělá

1. **Vytvoří nový sešit** – `new Workbook()` vám poskytne Excel soubor v paměti s výchozím listem.  
2. **Umístí inteligentní značku do buňky A1** – `{{jsonArray:ArrayAsSingle}}` říká Aspose.Cells, aby nahradil značku *celým* polem, spojeným čárkami.  
3. **Vytvoří zdroj dat `Map`** – klíč `"jsonArray"` odpovídá názvu značky; hodnota je `String[]`.  
4. **Volá `setSmartMarkerData`** – toto naváže mapu na značku a provede nahrazení.  
5. **Uloží soubor** – `workbook.save(...)` zapíše `JsonSingleValue.xlsx` na disk.

Když otevřete vygenerovaný Excel soubor, buňka **A1** obsahuje:

```
One, Two, Three
```

Pole je vykresleno jako jediný řetězec oddělený čárkami díky možnosti `ArrayAsSingle`.

---

## Použití inteligentní značky Aspose.Cells pro navázání JSON dat

Inteligentní značky Aspose.Cells jsou výkonný způsob, jak přímo mapovat složité objekty (včetně struktur podobných JSON) na listy. Syntaxe `{{fieldName:Option}}` funguje podobně jako šablonovací engine:

* **fieldName** – klíč ve vašem zdroji dat (`Map`, POJO nebo `DataTable`).  
* **Option** – určuje, jak jsou kolekce zpracovány. `ArrayAsSingle` zachází s celou kolekcí jako s jednou hodnotou; jiné možnosti jako `Array` rozšíří pole přes řádky.

**Proč použít inteligentní značku místo smyčky?**  
Smyčka vyžaduje ruční výpočty adres buněk, náchylné k chybám indexování a další kód pro formátování. Inteligentní značky vám umožní psát deklarativní zástupné symboly, udržet Java kód stručný a nechat knihovnu zvládnout detaily rozvržení.

---

## Nastavení datového zdroje Java Map

`Map<String, Object>` je nejjednodušší kontejner dat pro Aspose.Cells:

```java
Map<String, Object> dataSource = new HashMap<>();
dataSource.put("jsonArray", new String[] { "One", "Two", "Three" });
```

*Klíč (`jsonArray`) musí přesně odpovídat názvu značky.*  
Můžete také použít `List<String>`, vlastní POJO nebo dokonce vnořený `Map` pro složitější JSON struktury. Aspose.Cells automaticky projde objektový graf.

**Tip:** Pokud potřebujete formátovat spojený řetězec jinak (např. pomocí středníků), před přiřazením do mapy pole v Javě předzpracujte:

```java
String joined = String.join(";", new String[] {"One","Two","Three"});
dataSource.put("jsonArray", new String[] { joined });
```

---

## Uložení sešitu a ověření výstupu

```java
workbook.save("JsonSingleValue.xlsx");
```

Metoda `save` podporuje mnoho formátů (`.xlsx`, `.xls`, `.csv`, `.pdf`). Pro tento tutoriál ponecháváme výchozí formát Excel Open XML.

**Ověřovací kroky**

1. Otevřete `JsonSingleValue.xlsx` v Microsoft Excel, LibreOffice Calc nebo Google Sheets.  
2. Potvrďte, že buňka **A1** obsahuje `One, Two, Three`.  
3. Zkontrolujte, že nebyly přidány žádné další řádky nebo sloupce – inteligentní značka provedla nahrazení na místě.

Pokud buňka zobrazuje surový text značky (`{{jsonArray:ArrayAsSingle}}`), zkontrolujte:

* Název značky přesně odpovídá klíči v mapě (rozlišuje velká a malá písmena).  
* `setSmartMarkerData` je voláno **po** umístění značky.  
* Verze Aspose.Cells podporuje možnost `ArrayAsSingle` (k dispozici od verze v20.3).

---

## Běžné varianty a okrajové případy

| Scénář | Úprava |
|----------|------------|
| **Různý oddělovač** | Použijte `ArrayAsSingle` spolu s vlastním spojením v Javě (viz tip výše). |
| **Více polí v jednom listu** | Umístěte další značky jako `{{anotherArray:ArrayAsSingle}}` do jiných buněk a přidejte odpovídající položky do mapy. |
| **Vnořené JSON objekty** | Poskytněte vnořený `Map<String, Object>`; odkazujte na pole pomocí tečkové notace (`{{parent.child}}`). |
| **Velké datové sady** | Pro tisíce řádků upřednostněte možnost `Array`, aby Aspose.Cells automaticky rozšířil řádky, což |

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vlastních projektech.

- [Jak vytvořit a exportovat Excel do HTML pomocí Aspose.Cells Java \| Průvodce operacemi se sešitem](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Export Excel sešitu jako obrázku pomocí Aspose.Cells for Java: Krok za krokem](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Jak vytvořit a uložit Excel sešit jako SVG pomocí Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}