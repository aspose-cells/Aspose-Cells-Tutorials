---
category: general
date: 2026-06-21
description: Naučte se, jak v Javě použít expand k rozšíření pole na řádky, psát kód
  Excelových vzorců a uložit soubor Excel v Java stylu – vše v jednom tutoriálu.
draft: false
keywords:
- how to use expand
- expand array to rows
- write excel formula code
- save excel file java
language: cs
og_description: Jak použít expand v Javě k manipulaci s daty v Excelu, rozšířit pole
  na řádky, psát kód Excelových vzorců a uložit soubor Excel pomocí Javy.
og_title: Jak používat Expand v Javě – Kompletní průvodce Excel
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Learn how to use expand in Java to expand array to rows, write Excel
    formula code, and save Excel file Java style—all in a single tutorial.
  headline: How to Use Expand in Java – Complete Excel Guide
  type: TechArticle
- description: Learn how to use expand in Java to expand array to rows, write Excel
    formula code, and save Excel file Java style—all in a single tutorial.
  name: How to Use Expand in Java – Complete Excel Guide
  steps:
  - name: Why This Works
    text: '- **`Workbook`**: Represents the entire Excel file. Creating a new one
      gives you a clean canvas; loading an existing file lets you augment a pre‑existing
      template. - **`Worksheet`**: Think of it as a single tab. We grab the first
      one because that’s where we’ll demonstrate the formula. - **`setFormul'
  - name: Real‑World Use Cases
    text: '| Scenario | How EXPAND Helps | |----------|------------------| | Generating
      a month‑long schedule from a short list of tasks | `=EXPAND(taskList,30)` |
      | Padding a matrix for a statistical model | `=EXPAND(matrix,10,10,0)` | | Creating
      placeholder rows for user input | `=EXPAND({""},20)` |'
  - name: Expected Output
    text: 'When you open `output.xlsx`:'
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- Formulas
title: Jak používat Expand v Javě – Kompletní průvodce Excel
url: /cs/java/spreadsheet-automation/how-to-use-expand-in-java-complete-excel-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat funkci EXPAND v Javě – kompletní průvodce pro Excel

Už jste se někdy zamýšleli **jak používat expand**, když automatizujete Excel pomocí Javy? Nejste jediní – vývojáři se neustále ptají, jak rozšířit pole do řádků bez psaní nekonečných smyček. Dobrou zprávou je, že to můžete udělat jedním vzorcem a Java kód, který tento vzorec vloží do sešitu, je překvapivě krátký.

V tomto tutoriálu projdeme praktickým příkladem, který vám ukáže přesně, jak použít expand, jak napsat Excel vzorec v Javě a jak uložit Excel soubor „java‑style“, abyste výsledek mohli okamžitě zkontrolovat. Na konci budete mít spustitelný program, který načte existující sešit, vloží funkci `EXPAND` do buňky a zapíše soubor zpět na disk.

## Předpoklady

Než se pustíme do detailů, ujistěte se, že máte:

- Java 17 (nebo jakýkoli novější JDK) nainstalovanou.
- Maven nebo Gradle pro správu závislostí.
- Knihovnu **Aspose.Cells for Java** (nejjednodušší způsob, jak manipulovat s Excelem z Javy). Můžete ji získat z Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- check for the latest -->
</dependency>
```

Žádná další instalace Excelu není vyžadována; knihovna interně pracuje s formátem souboru. Pokud dáváte přednost Gradlu, stačí odpovídajícím způsobem nahradit blok závislosti.

Nyní, když máme základy pokryté, pojďme se pustit do praxe.

## Jak používat funkci EXPAND v Javě

Funkce `EXPAND` je součástí rodiny dynamických polí v Excelu. Přijímá zdrojové pole a rozšíří jej na zadanou velikost, prázdné buňky standardně vyplní `#N/A`. V našem případě předáme jednoduché jednorozměrné pole `{1,2,3}` a požádáme Excel, aby jej rozšířil na **5 řádků**.

```java
// Import statements
import com.aspose.cells.*;

public class ExpandDemo {
    public static void main(String[] args) {
        try {
            // 1️⃣ Load or create a workbook
            Workbook wb = new Workbook(); // creates a blank workbook
            // Optionally, load an existing file:
            // Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // 2️⃣ Get the first worksheet (index 0)
            Worksheet ws = wb.getWorksheets().get(0);

            // 3️⃣ Apply the EXPAND function in cell A1
            // This is where we **write excel formula code** from Java.
            ws.getCells().get("A1").setFormula("=EXPAND({1,2,3},5)");

            // 4️⃣ Save the workbook — **save excel file java** style.
            wb.save("YOUR_DIRECTORY/output.xlsx");
            System.out.println("Workbook saved successfully!");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### Proč to funguje

- **`Workbook`**: Reprezentuje celý Excel soubor. Vytvořením nového získáte čisté plátno; načtením existujícího souboru můžete doplnit předpřipravenou šablonu.
- **`Worksheet`**: Přemýšlejte o něm jako o jedné záložce. Vezmeme první, protože tam budeme demonstrovat vzorec.
- **`setFormula`**: Tato metoda vloží libovolný platný Excel vzorec jako řetězec. Zde předáváme funkci `EXPAND`, která říká Excelu, aby **rozšířil pole do řádků** (a sloupců, pokud je požadujete).
- **`save`**: Uloží změny na disk. Toto je krok **save excel file java**, který zajistí, že soubor můžete následně otevřít v Excelu nebo jakémkoli prohlížeči.

Spusťte program, otevřete `output.xlsx` a uvidíte ve sloupci A hodnoty `1, 2, 3, #N/A, #N/A`. Změňte druhý argument funkce `EXPAND` na `3` a získáte jen tři řádky – ideální pro dynamické reporty.

## Rozšíření pole do řádků pomocí funkce EXPAND

Pokud jste zvyklí ručně procházet řádky pomocí smyček, funkce `EXPAND` může nahradit tento boilerplate. Zde je rychlý rozpis syntaxe:

```
EXPAND(source, rows, columns, fill)
```

- **source** – Pole, které chcete rozšířit. V našem příkladu `{1,2,3}`.
- **rows** – Požadovaný počet řádků. Použili jsme `5`.
- **columns** – Volitelné; výchozí hodnota je počet sloupců ve zdrojovém poli.
- **fill** – Co vložit do prázdných buněk (`#N/A` ve výchozím nastavení).

### Reálné příklady použití

| Scénář | Jak pomáhá EXPAND |
|----------|------------------|
| Generování měsíčního rozvrhu z krátkého seznamu úkolů | `=EXPAND(taskList,30)` |
| Vyplnění matice pro statistický model | `=EXPAND(matrix,10,10,0)` |
| Vytváření zástupných řádků pro vstup uživatele | `=EXPAND({""},20)` |

Nechte Excel udělat těžkou práci a váš Java kód zůstane přehledný a bez zbytečných smyček.

## Psát Excel vzorec v Javě

Možná se ptáte: „Mohu vytvořit řetězec vzorce dynamicky?“ Rozhodně ano. Zde je úryvek, který sestaví volání `EXPAND` na základě proměnných:

```java
int[] numbers = {4, 5, 6};
int targetRows = 7;

// Convert int array to Excel‑style literal: {4,5,6}
StringBuilder sb = new StringBuilder("{");
for (int i = 0; i < numbers.length; i++) {
    sb.append(numbers[i]);
    if (i < numbers.length - 1) sb.append(",");
}
sb.append("}");

String formula = String.format("=EXPAND(%s,%d)", sb.toString(), targetRows);
ws.getCells().get("B2").setFormula(formula);
```

Všimněte si, jak **write excel formula code** programově, a poté jej vložíme do buňky `B2`. Tento přístup se dobře škáluje, když potřebujete generovat vzorce za běhu – například načíst data z databáze a převést je na dynamický Excel report.

## Uložit Excel soubor v Javě – trvalé uložení změn

Uložení sešitu je poslední část skládačky. Aspose.Cells nabízí několik možností:

- **`wb.save("path.xlsx")`** – Uloží ve výchozím formátu XLSX.
- **`wb.save("path.xls", SaveFormat.EXCEL_97_TO_2003)`** – Pro starší kompatibilitu.
- **`wb.save(outputStream, SaveFormat.XLSX)`** – Když potřebujete streamovat soubor (např. ve webové aplikaci).

Zde je příklad, který zapisuje do `ByteArrayOutputStream`, takže můžete vrátit bajty z REST endpointu:

```java
ByteArrayOutputStream baos = new ByteArrayOutputStream();
wb.save(baos, SaveFormat.XLSX);
byte[] excelBytes = baos.toByteArray();
// Now you can send `excelBytes` as a response payload.
```

To je vzor **save excel file java**, na který se spoléhá mnoho podnikových služeb.

## Časté úskalí a tipy pro profesionály

- **Časování vyhodnocení vzorce** – Aspose.Cells **nevyhodnocuje** vzorce automaticky při `save`. Pokud potřebujete vypočtené hodnoty, zavolejte `wb.calculateFormula()` před uložením.
- **Podpora dynamických polí** – Funkce `EXPAND` je dostupná jen v Excelu 365 / 2021+. Otevření souboru ve starších verzích zobrazí `#NAME?`. Pokud musíte podporovat starší klienty, zvažte ruční rozšíření.
- **Problémy s locale** – Používejte anglický název funkce (`EXPAND`) bez ohledu na jazyk sešitu; Aspose.Cells používá anglickou syntaxi.
- **Velká pole** – Rozšíření na tisíce řádků může zvětšit velikost souboru. Sledujte využití paměti a zvažte streamování velkých datových sad.

## Kompletní funkční příklad

Níže je kompletní, samostatný program, který můžete zkopírovat a vložit do IDE. Obsahuje všechny importy, ošetření chyb a komentáře, které vás provedou.

```java
import com.aspose.cells.*;

public class ExpandDemoFull {
    public static void main(String[] args) {
        // Adjust these paths as needed
        String inputPath = "YOUR_DIRECTORY/input.xlsx";
        String outputPath = "YOUR_DIRECTORY/output.xlsx";

        try {
            // Step 1: Load an existing workbook or create a new one
            Workbook wb;
            if (new java.io.File(inputPath).exists()) {
                wb = new Workbook(inputPath);
                System.out.println("Loaded existing workbook.");
            } else {
                wb = new Workbook(); // brand‑new workbook
                System.out.println("Created a new workbook.");
            }

            // Step 2: Access the first worksheet
            Worksheet ws = wb.getWorksheets().get(0);

            // Step 3: Build a dynamic EXPAND formula (expand array to rows)
            int[] sourceArray = {1, 2, 3};
            int rowsDesired = 5;

            // Convert Java array to Excel literal syntax
            StringBuilder literal = new StringBuilder("{");
            for (int i = 0; i < sourceArray.length; i++) {
                literal.append(sourceArray[i]);
                if (i < sourceArray.length - 1) literal.append(",");
            }
            literal.append("}");

            String formula = String.format("=EXPAND(%s,%d)", literal, rowsDesired);
            ws.getCells().get("A1").setFormula(formula);
            System.out.println("Inserted formula: " + formula);

            // Optional: force calculation so the file contains values, not just formulas
            wb.calculateFormula();

            // Step 4: Save the workbook – **save excel file java** style
            wb.save(outputPath);
            System.out.println("Workbook saved to " + outputPath);
        } catch (Exception ex) {
            System.err.println("Error occurred: " + ex.getMessage());
            ex.printStackTrace();
        }
    }
}
```

### Očekávaný výstup

Po otevření `output.xlsx`:

| A   |
|-----|
| 1   |
| 2   |
| 3   |
| #N/A |
| #N/A |

Pokud změníte `rowsDesired` na `3`, sloupec skončí po třetím řádku. Zástupné hodnoty `#N/A` jsou Excelovým způsobem, jak říct „žádná data zde“ – můžete je nahradit předáním čtvrtého argumentu do `EXPAND`, např. `=EXPAND({1,

## Co se naučíte dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobným vysvětlením, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [How to Insert Rows into Excel Workbooks Using Aspose.Cells for Java](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)
- [How to Delete Rows in Excel Using Aspose.Cells for Java | Guide & Tutorial](/cells/english/java/worksheet-management/delete-row-excel-aspose-cells-java/)
- [How to Save Excel Files in Various Formats Using Aspose.Cells Java](/cells/english/java/workbook-operations/save-excel-files-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}