---
category: general
date: 2026-06-30
description: Nastavte vlastní číselný formát v Excelu pomocí Javy. Naučte se, jak
  vytvořit Excel sešit v Javě, získat datum a čas z buňky, vypočítat vzorce v sešitu
  a získat výstupní hodnotu data a času.
draft: false
keywords:
- set custom number format
- get datetime from cell
- create excel workbook java
- calculate workbook formulas
- output datetime value
language: cs
og_description: Nastavte vlastní formát čísla v Excelu pomocí Javy. Tento průvodce
  ukazuje, jak vytvořit sešit Excel v Javě, získat datum a čas z buňky, vypočítat
  vzorce v sešitu a výstupní hodnotu data a času.
og_title: Nastavte vlastní formát čísel v Excelu pomocí Javy – kompletní tutoriál
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  headline: Set Custom Number Format in Excel with Java – Complete Guide
  type: TechArticle
- description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  name: Set Custom Number Format in Excel with Java – Complete Guide
  steps:
  - name: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
    text: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
  - name: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
    text: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
  - name: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
    text: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- DateTime
title: Nastavte vlastní číselný formát v Excelu pomocí Javy – kompletní průvodce
url: /cs/java/formatting/set-custom-number-format-in-excel-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nastavení vlastního formátu čísel v Excelu pomocí Javy – Kompletní průvodce

Už jste někdy potřebovali **nastavit vlastní formát čísel** v listu Excelu při práci v Javě? Nejste v tom sami. Ať už vytváříte reportingový engine nebo jen chcete správně zobrazit data japonských érá, zvládnutí tohoto triku vám ušetří nespočet hodin post‑processingu. V tomto tutoriálu projdeme reálný příklad, který **vytvoří Excel workbook Java**, použije formát specifický pro locale, přepočítá vzorce a nakonec **získá DateTime z buňky** a **vypíše datetime hodnotu**.

Použijeme populární knihovnu Aspose.Cells pro Java, protože zajišťuje formáty čísel a kulturně specifické datumy přímo z krabice. Na konci průvodce budete mít samostatný, spustitelný program, který můžete vložit do libovolného Maven nebo Gradle projektu. Žádné vágní „viz dokumentaci“ zkratky – jen solidní kód a jasná vysvětlení.

---

## Co se naučíte

- Jak **vytvořit Excel workbook Java** programově.
- Přesné kroky k **nastavení vlastního formátu čísel** pro data japonských érá.
- Proč je volání **calculate workbook formulas** nezbytné před extrakcí hodnoty.
- Správný způsob, jak **získat datetime z buňky** a **vypíše datetime hodnotu**.
- Běžné úskalí (chybějící locale, zastaralé vzorce) a rychlé opravy.

---

## Předpoklady

- Java 8 nebo novější nainstalovaná na vašem počítači.  
- Aspose.Cells pro Java 23.11 (nebo jakákoli novější verze).  
- Základní IDE nebo textový editor – IntelliJ IDEA, Eclipse, VS Code, cokoliv, co preferujete.  

Pokud jste ještě nepřidali Aspose.Cells do svého projektu, vložte následující Maven úryvek do souboru `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.11</version>
</dependency>
```

Uživatelé Gradle mohou přidat:

```gradle
implementation 'com.aspose:aspose-cells:23.11'
```

Nyní, když je prostředí připravené, pojďme se ponořit do kódu.

---

## Krok 1: Nastavení vlastního formátu čísel – Přehled

Než napíšeme jakýkoli Java kód, pomůže si představit, co chceme dosáhnout. Představte si buňku v Excelu, která by měla zobrazovat **„令和2年4月1日“** místo ISO‑8601 řetězce „2020‑04‑01“. Hodnota zůstane pravým datem (takže vzorce fungují), ale *zobrazení* následuje japonský formát éry. To je přesně to, co operace **set custom number format** provádí.

Níže je celý zdrojový soubor. Klidně jej zkopírujte do `src/main/java/SetCustomNumberFormatDemo.java`.

```java
// File: SetCustomNumberFormatDemo.java
import com.aspose.cells.*;

public class SetCustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Create Excel workbook Java – a fresh workbook
        // -------------------------------------------------
        Workbook workbook = new Workbook();               // in‑memory workbook, no file yet

        // -------------------------------------------------
        // 2️⃣ Access the first worksheet
        // -------------------------------------------------
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // -------------------------------------------------
        // 3️⃣ Retrieve cell A1 where we’ll store the date string
        // -------------------------------------------------
        Cell cellA1 = worksheet.getCells().get("A1");

        // -------------------------------------------------
        // 4️⃣ Insert a Japanese era date string (Reiwa 2‑04‑01)
        // -------------------------------------------------
        // Note: Aspose.Cells will treat this as a text value until we recalc.
        cellA1.putValue("R02-04-01");

        // -------------------------------------------------
        // 5️⃣ Apply the custom number format (our primary goal)
        // -------------------------------------------------
        // [$-ja-JP] tells Excel to use the Japanese locale.
        // ggge年m月d日 renders as "令和2年4月1日".
        cellA1.setNumberFormat("[$-ja-JP]ggge年m月d日");

        // -------------------------------------------------
        // 6️⃣ Calculate workbook formulas – crucial step!
        // -------------------------------------------------
        // Without this, the cell remains a plain string and the
        // DateTime conversion below will fail.
        workbook.calculateFormula();

        // -------------------------------------------------
        // 7️⃣ Get DateTime from cell – now the value is a true date
        // -------------------------------------------------
        // The getDateTime() method returns a java.util.Calendar instance.
        java.util.Calendar dt = cellA1.getDateTime();

        // -------------------------------------------------
        // 8️⃣ Output datetime value – see the result in console
        // -------------------------------------------------
        System.out.println("Converted DateTime: " + dt.getTime()); // → Tue Apr 01 00:00:00 UTC 2020
    }
}
```

### Proč to funguje

- **`setNumberFormat`** říká Excelu, jak má *zobrazit* podkladovou numerickou hodnotu. Formátovací řetězec `[$-ja-JP]ggge年m月d日` je klíč; `ggg` vybírá název éry, `e` rok v rámci éry, následované měsíci a dnem jako literály.
- **`calculateFormula`** nutí Aspose.Cells interpretovat text „R02-04-01“ jako datum podle japonského kalendáře. Vynechání tohoto kroku ponechá buňku jako prostý text a `getDateTime()` vyhodí výjimku.
- **`getDateTime`** nakonec extrahuje *skutečný* objekt `java.util.Calendar`, se kterým můžete dále pracovat, formátovat ho nebo uložit jinam.

---

## Krok 2: Vytvoření Excel workbook Java – Podrobnější pohled

Když **create Excel workbook Java**, nealokujete jen paměť; zároveň se vytvoří výchozí styly, výchozí list a výchozí kultura (obvykle locale systému). Pokud potřebujete jiné výchozí locale, můžete předat objekt `LoadOptions`:

```java
LoadOptions opts = new LoadOptions(LoadFormat.XLSX);
opts.setLocale(new java.util.Locale("ja", "JP"));
Workbook workbook = new Workbook(opts);
```

Pro většinu scénářů stačí jednoduchý konstruktor, ale je dobré znát alternativu – zejména když v jedné aplikaci pracujete s více locale.

*Tip:* Držte workbook v paměti, dokud nedokončíte formátování. Zapisování na disk po každé změně přináší zbytečné I/O zatížení.

---

## Krok 3: Získání DateTime z buňky – Zpracování výsledku

Řádek `java.util.Calendar dt = cellA1.getDateTime();` vykonává těžkou práci. Aspose.Cells na pozadí převádí interní sériové číslo (počet dní od 31.12.1899) na `Calendar`. Tento převod respektuje locale workbooku, takže získáte správné gregoriánské datum, i když zobrazení používá japonskou éru.

Pokud potřebujete `java.time.LocalDate` (novější API), převeďte takto:

```java
java.time.LocalDate localDate = dt.toInstant()
        .atZone(java.time.ZoneId.systemDefault())
        .toLocalDate();
System.out.println("LocalDate: " + localDate); // 2020-04-01
```

Tím je splněna požadavek **output datetime value** a zároveň zůstáváte moderní.

---

## Krok 4: Přepočítání vzorců workbooku – Kdy je to důležité

Možná se ptáte: *„Opravdu musím volat `calculateFormula()`?“* Odpověď zní rozhodně ano, pokud buňku neplníte nativním Java objektem `Date` od začátku. Když **set custom number format** na textový řetězec, Excel (a Aspose.Cells) jej považuje za výraz podobný vzorci, který je potřeba vyhodnotit. Bez přepočítání `getDateTime()` vrátí výchozí `1900‑01‑00` nebo vyhodí `CellValueException`.

Pokud váš workbook již obsahuje složité vzorce odkazující na nově formátovanou buňku, zavolejte `calculateFormula()` *jednou* po všech změnách. Opakované volání je nákladné.

---

## Krok 5: Výpis DateTime hodnoty – Ověření výsledku

Spuštění demoa vypíše něco jako:

```
Converted DateTime: Tue Apr 01 00:00:00 UTC 2020
```

Tento řádek potvrzuje tři věci:

1. **set custom number format** byl aplikován (můžete otevřít vygenerovaný `.xlsx` v Excelu a uvidíte „令和2年4月1日“).
2. Krok **calculate workbook formulas** uspěl a proměnil řetězec éry na skutečné datum.
3. Volání **get datetime from cell** vrátilo platný `Calendar`, který jsme následně **output datetime value** na konzoli.

Pokud otevřete workbook v tabulkovém programu, uvidíte formátovaný text, ale podkladová hodnota buňky zůstane sériové číslo `43831` (Excelová reprezentace 2020‑04‑01). Tato dualita je tím, co dělá Excel výkonným.

---

## Běžná úskalí a okrajové případy

| Problém | Proč se vyskytuje | Oprava |
|-------|----------------|-----|
| `cellA1.getDateTime()` vyhazuje `CellValueException` | Buňka je stále řetězec, protože byl vynechán `calculateFormula()`. | Vždy po nastavení textového data, které potřebuje konverzi, zavolejte `workbook.calculateFormula()`. |
| Japonská éra se nezobrazuje správně | Chybí nebo je nesprávný kód locale. | Použijte `[$-ja-JP]` ve formátovacím řetězci nebo nastavte locale workbooku pomocí `LoadOptions`. |
| Formát ukazuje “#VALUE!” v Excelu | Formátovací řetězec je špatně vytvořen. | Zkontrolujte závorky a znaky; vzor `ggge年m月d日` je vyžadován pro rok v éře. |
| Zobrazí se časová složka (např. “00:00:00”) | Zdrojový řetězec obsahuje čas nebo styl buňky ho přidává. | Ořízněte zdrojový řetězec nebo upravte formát na `ggge年m月d日;@`. |

---

## Kompletní funkční příklad – Jedním kliknutím

Pokud dáváte přednost jedinému souboru bez dalších komentářů, zde je minimální verze:



## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl ovládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Create an Excel Workbook using Aspose.Cells in Java&#58; A Step-by-Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Mastering Data Presentation in Excel&#58; Number and Custom Date Formatting with Aspose.Cells for Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}