---
category: general
date: 2026-08-11
description: Vytvořte nový sešit Aspose v Javě, přidejte vlastní vlastnost Excel a
  následně uložte sešit jako XLSB s úplným krok‑za‑krokem příkladem.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook aspose
- save workbook as xlsb
- add custom property excel
- Aspose.Cells Java
- custom properties Excel
- workbook serialization
language: cs
lastmod: 2026-08-11
og_description: Vytvořte nový sešit Aspose v Javě, přidejte vlastní vlastnost Excel
  a uložte sešit jako XLSB s kompletním, připraveným k okamžitému spuštění příkladem.
og_image_alt: Java code screenshot that creates a new workbook Aspose, adds a custom
  Excel property, and saves it as an XLSB file
og_title: Vytvořit nový sešit Aspose – přidat vlastní vlastnost v Excelu
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  headline: Create new workbook Aspose – add custom property Excel and save as XLSB
  type: TechArticle
- description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  name: Create new workbook Aspose – add custom property Excel and save as XLSB
  steps:
  - name: What if I need to store a string property?
    text: '```java worksheet.getCustomProperties().add("Owner", "Alice"); ```'
  - name: Can I add multiple custom properties at once?
    text: Yes. Call `add` repeatedly for each name/value pair. Aspose.Cells does not
      limit the number of custom properties, but keep the total size reasonable to
      avoid bloating the file.
  - name: How does the binary format affect performance?
    text: XLSB files load faster because they avoid XML parsing. This is especially
      noticeable for workbooks with many rows, formulas, or embedded images.
  - name: What if I need to work with an existing XLSX file?
    text: Replace the `new Workbook()` constructor with `new Workbook("ExistingFile.xlsx")`.
      The rest of the steps (adding properties, saving as XLSB) remain identical.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- XLSB
- Custom Properties
title: Vytvořit nový sešit Aspose – přidat vlastní vlastnost Excel a uložit jako XLSB
url: /cs/java/spreadsheet-automation/create-new-workbook-aspose-add-custom-property-excel-and-sav/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořte nový sešit Aspose – přidejte vlastní vlastnost Excel a uložte jako XLSB

Pokud potřebujete **create new workbook Aspose** v Java aplikaci, tento průvodce vám přesně ukáže, jak na to. Naučíte se **add custom property Excel**, získat hodnotu a **save workbook as XLSB** bez ztráty jakýchkoli metadat.

Tutoriál pokrývá vše od nastavení projektu až po ověření uloženého souboru. Není potřeba žádná externí dokumentace; stačí postupovat podle kroků a spustit kód.

## Požadavky

- Java Development Kit (JDK) 8 nebo vyšší nainstalovaný.
- Maven nebo Gradle pro správu závislostí (příklad používá Maven).
- Aktivní licence Aspose.Cells pro Java (nebo použijte režim bezplatného hodnocení pro testování).

## Krok 1: Přidejte Aspose.Cells do svého projektu

Přidejte Maven artefakt Aspose.Cells do svého `pom.xml`. Tato závislost poskytuje třídy potřebné k **create new workbook Aspose** objektům.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

> **Tip:** Pokud dáváte přednost Gradle, nahraďte Maven úryvek ekvivalentním řádkem `implementation "com.aspose:aspose-cells:23.12"`.

## Krok 2: Vytvořte nový sešit Aspose

Prvním funkčním krokem je vytvořit instanci objektu `Workbook`. Tento objekt představuje soubor Excel v paměti a je vstupním bodem pro všechny další operace.

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {

    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();               // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0); // Default first sheet
```

Vytvoření nového sešitu Aspose vám poskytne čistý sešit s výchozím listem, připravený k úpravám.

## Krok 3: Přidejte vlastní vlastnost Excel

Vlastní vlastnosti vám umožňují uložit libovolná metadata uvnitř souboru Excel. Zde **add custom property Excel** s názvem `ProjectId` a číselnou hodnotou.

```java
        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);
```

Metoda `add` přijímá název vlastnosti a hodnotu libovolného podporovaného typu (string, číslo, datum, atd.). Tato metadata cestují se souborem kamkoli jej zkopírujete.

## Krok 4: Načtěte a zobrazte vlastní vlastnost

Načtení vlastnosti zpět ověřuje, že byla uložena správně. Můžete také použít načtenou hodnotu ve své obchodní logice.

```java
        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);
```

Přetypování na `int` funguje, protože jsme uložili číselnou hodnotu. Pokud uložíte řetězec, použijte místo toho `(String)`.

## Krok 5: Uložte sešit jako XLSB

Nyní **save workbook as XLSB**. Formát XLSB ukládá sešit v binárním reprezentaci, což je rychlejší při otevírání a menší na disku. Všechny vlastní vlastnosti jsou automaticky zachovány.

```java
        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

Nahraďte `"WithCustomProps.xlsb"` absolutní cestou, pokud potřebujete soubor v konkrétním adresáři. Výčtový typ `SaveFormat.XLSB` říká Aspose.Cells, aby zapsal binární formát.

## Krok 6: Ověřte výstup

Spusťte program ze svého IDE nebo z příkazové řádky:

```bash
mvn compile exec:java -Dexec.mainClass=CustomPropertiesXlsb
```

Měli byste vidět:

```
ProjectId = 12345
```

Otevřete `WithCustomProps.xlsb` v Excelu. Přejděte na **File → Info → Properties → Advanced Properties → Custom**. Záznam `ProjectId` s hodnotou `12345` bude uveden, což potvrzuje, že krok **add custom property excel** byl úspěšný a operace **save workbook as xlsb** zachovala metadata.

## Časté otázky a okrajové případy

### Co když potřebuji uložit řetězcovou vlastnost?

```java
worksheet.getCustomProperties().add("Owner", "Alice");
```

Načtěte ji pomocí:

```java
String owner = (String) worksheet.getCustomProperties().get("Owner").getValue();
```

### Můžu přidat více vlastních vlastností najednou?

Ano. Volajte `add` opakovaně pro každý pár název/hodnota. Aspose.Cells neomezuje počet vlastních vlastností, ale udržujte celkovou velikost rozumnou, aby nedošlo k nafouknutí souboru.

### Jak binární formát ovlivňuje výkon?

Soubory XLSB se načítají rychleji, protože se vyhýbají parsování XML. To je zvláště patrné u sešitů s mnoha řádky, vzorci nebo vloženými obrázky.

### Co když potřebuji pracovat s existujícím souborem XLSX?

Nahraďte konstruktor `new Workbook()` za `new Workbook("ExistingFile.xlsx")`. Zbytek kroků (přidávání vlastností, ukládání jako XLSB) zůstává stejný.

## Kompletní zdrojový kód

Níže je kompletní, připravený k spuštění příklad. Zkopírujte jej do souboru pojmenovaného `CustomPropertiesXlsb.java` ve vašem adresáři `src/main/java`.

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {
    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();                       // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // Default first sheet

        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);

        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);

        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

Spuštěním této třídy vznikne soubor XLSB, který obsahuje vlastní vlastnost a lze jej otevřít v jakékoli moderní verzi Microsoft Excel.

## Závěr

Nyní víte, jak **create new workbook Aspose**, **add custom property Excel** a **save workbook as XLSB** pomocí Javy. Příklad demonstruje celý životní cyklus: inicializaci, injekci metadat, ověření a binární serializaci.

Dále prozkoumejte související témata jako **setting document properties**, **working with Excel formulas** nebo **converting between XLSX and XLSB**. Každé z nich staví na stejném API Aspose.Cells, které jste právě použili, takže můžete rozšířit řešení bez nutnosti učit se nové knihovny.

Neváhejte experimentovat s různými datovými typy, více listy nebo ochranou heslem — Aspose.Cells podporuje všechny tyto scénáře přímo. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Create Save Excel Workbook Aspose Cells Java](/cells/english/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Create Excel Workbook and Add Labels with Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/data-labeling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}