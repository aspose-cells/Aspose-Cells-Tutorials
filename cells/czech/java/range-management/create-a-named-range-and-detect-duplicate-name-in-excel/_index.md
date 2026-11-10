---
category: general
date: 2026-09-27
description: Vytvořte pojmenovaný rozsah v Excelu pomocí Aspose.Cells, nastavte název
  tabulky, přidejte pojmenovaný rozsah, vytvořte tabulku v Excelu a detekujte chyby
  duplicitních názvů.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create named range
- set table name
- create excel table
- add named range
- detect duplicate name
language: cs
lastmod: 2026-09-27
og_description: Vytvořte pojmenovaný rozsah v Excelu pomocí Aspose.Cells, poté nastavte
  název tabulky, přidejte pojmenovaný rozsah, vytvořte Excel tabulku a detekujte chyby
  duplicitních názvů.
og_image_alt: Screenshot showing how to create a named range in Excel with Aspose.Cells
og_title: Vytvořte pojmenovaný rozsah a zjistěte duplicitní název v Excelu
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Create a named range in Excel using Aspose.Cells, set table name, add
    named range, create Excel table, and detect duplicate name errors.
  headline: Create a named range and detect duplicate name in Excel
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Vytvořte pojmenovaný rozsah a detekujte duplicitní název v Excelu
url: /cs/java/range-management/create-a-named-range-and-detect-duplicate-name-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořte pojmenovaný rozsah a detekujte duplicitní název v Excelu

Pokud potřebujete **vytvořit pojmenovaný rozsah** v sešitu Excel a chcete se vyhnout kolizím názvů, tento návod vám ukáže přesně, jak to provést pomocí Aspose.Cells pro Java. Naučíte se **přidat pojmenovaný rozsah**, **vytvořit Excel tabulku**, **nastavit název tabulky** a **detekovat chyby duplicitního názvu** v jediném, samostatném příkladu.

Práce s pojmenovanými rozsahy je běžnou požadavkem při tvorbě nástrojů pro reportování, listů pro validaci dat nebo dynamických dashboardů. Na konci tohoto tutoriálu budete mít spustitelný program, který bezpečně vytvoří pojmenovaný rozsah, vytvoří tabulku a elegantně ošetří případnou výjimku způsobenou konfliktem názvů.

## Požadavky

- Java 17 nebo novější nainstalovaná
- Maven nebo Gradle pro správu závislostí
- Aspose.Cells pro Java (nejnovější verze; Maven koordináta `com.aspose:aspose-cells:23.9` v době psaní)
- Základní znalost konceptů Excelu, jako jsou listy, rozsahy a tabulky

## Krok 1: Vytvořte pojmenovaný rozsah v sešitu

Prvním krokem je vytvořit objekt `Workbook` a přidat pojmenovaný rozsah, který ukazuje na konkrétní blok buněk.

```java
import com.aspose.cells.*;

public class NamedRangeDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the default first worksheet (named "Sheet1")
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Define a named range called "MyRange" that covers A1:C5
        // This demonstrates the "add named range" operation.
        workbook.getNames().add("MyRange", "'Sheet1'!$A$1:$C$5");
```

**Proč je to důležité:**  
Pojmenovaný rozsah funguje jako opakovaně použitelné odkazy, na které mohou odkazovat vzorce a tabulky. Přidání již v rané fázi zajišťuje, že následující kroky mohou znovu použít stejný identifikátor bez nutnosti pevně kódovat adresy buněk.

## Krok 2: Vytvořte Excel tabulku, která používá pojmenovaný rozsah

Dále vytvoříme strukturovanou tabulku (ListObject), která zabírá stejnou oblast jako pojmenovaný rozsah. Tím demonstrujeme koncept **create excel table**.

```java
        // Create an Excel table (ListObject) that spans the same area as the named range.
        // The parameters (0,0,4,2) represent the top‑left cell (A1) and bottom‑right cell (C5).
        ListObject table = sheet.getListObjects().add(0, 0, 4, 2, true);
```

**Proč je to důležité:**  
Tabulky poskytují vestavěné řazení, filtrování a stylování. Zarovnáním tabulky s pojmenovaným rozsahem udržujete datový model konzistentní.

## Krok 3: Nastavte název tabulky a ošetřete možný konflikt

Nyní se pokusíme přiřadit tabulce název, který se shoduje s dříve vytvořeným pojmenovaným rozsahem. Tento krok ukazuje **set table name** a úmyslně vyvolává konflikt názvů.

```java
        try {
            // Attempt to set the table name to "MyRange".
            // Because a named range with the same identifier already exists,
            // Aspose.Cells will throw an exception.
            table.setName("MyRange"); // <-- conflict expected
        } catch (Exception e) {
            // Step 4: Detect duplicate name and respond appropriately
            System.out.println("Name conflict detected: " + e.getMessage());
        }
```

**Proč je to důležité:**  
Excel neumožňuje, aby tabulka a pojmenovaný rozsah sdílely stejný identifikátor. Včasná detekce konfliktu zabraňuje poškození sešitu a usnadňuje ladění.

## Krok 4: Detekujte duplicitní název a vyřešte jej

Když je výjimka zachycena, můžete buď přejmenovat tabulku, nebo odstranit konfliktní pojmenovaný rozsah. Níže je jednoduchá strategie řešení, která přidá příponu k názvu tabulky.

```java
            // Resolve the conflict by appending a numeric suffix
            String baseName = "MyRange";
            int suffix = 1;
            String newName;
            do {
                newName = baseName + "_" + suffix;
                suffix++;
            } while (workbook.getNames().get(newName) != null);

            table.setName(newName);
            System.out.println("Table renamed to: " + newName);
        }

        // Save the workbook to verify the result
        workbook.save("NamedRangeDemo.xlsx");
    }
}
```

**Klíčové body řešení:**

- **detect duplicate name** – blok `catch` potvrzuje konflikt.
- Smyčka kontroluje kolekci názvů sešitu, aby zajistila, že nový identifikátor je jedinečný.
- Nakonec je sešit uložen, takže jej můžete otevřít v Excelu a ověřit, že tabulka má odlišný název, zatímco původní pojmenovaný rozsah zůstává beze změny.

## Kompletní, spustitelný příklad

Spojením všech částí vypadá kompletní program takto:

```java
import com.aspose.cells.*;

public class NamedRangeDemo {
    public static void main(String[] args) throws Exception {
        // Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Add a named range called "MyRange" covering A1:C5
        workbook.getNames().add("MyRange", "'Sheet1'!$A$1:$C$5");

        // Create an Excel table that occupies the same cells
        ListObject table = sheet.getListObjects().add(0, 0, 4, 2, true);

        try {
            // Try to set the table name to the same identifier
            table.setName("MyRange");
        } catch (Exception e) {
            // Detect duplicate name and resolve it
            System.out.println("Name conflict detected: " + e.getMessage());

            String baseName = "MyRange";
            int suffix = 1;
            String newName;
            do {
                newName = baseName + "_" + suffix;
                suffix++;
            } while (workbook.getNames().get(newName) != null);

            table.setName(newName);
            System.out.println("Table renamed to: " + newName);
        }

        // Save the file for inspection
        workbook.save("NamedRangeDemo.xlsx");
    }
}
```

**Očekávaný výstup po spuštění programu:**

```
Name conflict detected: A name with the specified identifier already exists.
Table renamed to: MyRange_1
```

Po otevření souboru `NamedRangeDemo.xlsx` v Excelu uvidíte:

- Pojmenovaný rozsah **MyRange**, který odkazuje na buňky A1:C5.
- Tabulku s názvem **MyRange_1**, která pokrývá stejné buňky.
- Žádná chyba pojmenování při přidávání vzorců odkazujících na `MyRange`.

## Časté úskalí a osvědčené postupy

- **Neznovu používejte identifikátory**: Vždy ověřte, že název ještě neexistuje, než jej přiřadíte tabulce.  
- **Preferujte explicitní kontroly**: `workbook.getNames().get("Name")` vrací `null`, pokud je název volný, což je bezpečnější než zachytávat obecnou výjimku.  
- **Udržujte konzistentní pojmenovací konvence**: Použití předpony jako `tbl_` pro tabulky a `rng_` pro rozsahy snižuje pravděpodobnost kolizí.  
- **Kompatibilita verzí**: Kód funguje s Aspose.Cells 23.9 a novějšími; starší verze mohou mít odlišné zprávy o výjimkách.

## Závěr

Nyní víte, jak **vytvořit pojmenovaný rozsah**, **přidat pojmenovaný rozsah**, **vytvořit Excel tabulku**, **nastavit název tabulky** a **detekovat duplicitní název** pomocí Aspose.Cells pro Java. Proaktivním řešením kolizí názvů udržujete své sešity čisté a automatizační skripty robustní.

**Další kroky**

- Dále prozkoumejte API **set table name** a aplikujte možnosti stylování.  
- Používejte vzor **detect duplicate name** při programovém generování více tabulek.  
- Kombinujte pojmenované rozsahy s vzorci nebo validací dat pro dynamické reportování.

Šťastné programování!


## Co se naučíte dál?


Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobným krok‑za‑krokem vysvětlením, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy ve vlastních projektech.

- [Vytvořit stylovaný pojmenovaný rozsah Excel Aspose Cells Java](/cells/hindi/java/tables-structured-references/create-style-named-range-excel-aspose-cells-java/)
- [Vytvořit stylovaný pojmenovaný rozsah Excel Aspose Cells Java](/cells/german/java/tables-structured-references/create-style-named-range-excel-aspose-cells-java/)
- [Vytvořit stylovaný pojmenovaný rozsah Excel Aspose Cells Java](/cells/french/java/tables-structured-references/create-style-named-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}