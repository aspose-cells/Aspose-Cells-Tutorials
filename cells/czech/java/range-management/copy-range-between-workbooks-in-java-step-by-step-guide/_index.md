---
category: general
date: 2026-08-14
description: Kopírování rozsahu mezi sešity v Javě pomocí Aspose.Cells. Naučte se
  kopírovat sešit s kontingenční tabulkou, exportovat obrázek do PowerPointu a odstranit
  automatický filtr z tabulky v Excelu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range between workbooks
- copy pivot table workbook
- export picture to powerpoint
- copy excel range to new workbook
- remove autofilter from excel table
language: cs
lastmod: 2026-08-14
og_description: Kopírování rozsahu mezi sešity v Javě. Tento návod ukazuje, jak zkopírovat
  sešit s kontingenční tabulkou, exportovat obrázek do PowerPointu a odstranit automatický
  filtr z tabulky v Excelu.
og_image_alt: Screenshot of Java code copying range between workbooks with Aspose.Cells
og_title: Kopírování rozsahu mezi sešity v Javě – kompletní tutoriál Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Copy range between workbooks with Java using Aspose.Cells. Learn to
    copy pivot table workbook, export picture to PowerPoint and remove AutoFilter
    from Excel table.
  headline: Copy range between workbooks in Java – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Kopírování rozsahu mezi sešity v Javě – průvodce krok po kroku
url: /cs/java/range-management/copy-range-between-workbooks-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopírování rozsahu mezi sešity v Javě – krok za krokem

Pokud potřebujete **copy range between workbooks** v Javě, Aspose.Cells poskytuje čisté API, které zpracovává složité objekty, jako jsou kontingenční tabulky a obrázky. Tento tutoriál ukazuje, jak **copy pivot table workbook**, **export picture to PowerPoint** a **remove AutoFilter from Excel table**, přičemž kód zůstává snadno čitelný a udržovatelný.

Dozvíte se, jak:

* Načíst zdrojový sešit a definovat zdrojový rozsah.  
* Vytvořit cílový sešit a zkopírovat rozsah tak, aby kontingenční tabulka zůstala nedotčena.  
* Exportovat první obrázek na listu jako editovatelný objekt PowerPointu.  
* Odebrat AutoFilter z první Excel tabulky.  
* Načíst sešit s `SmartMarkerOptions`, aby se JSON pole zacházelo jako s jednou buňkou.

Příklad používá Aspose.Cells 23.10 pro Java, ale koncepty platí i pro starší verze.

---

## Požadavky

| Požadavek | Proč je to důležité |
|-------------|----------------|
| Java 17 nebo novější | Vyžadováno nejnovějším runtime Aspose.Cells. |
| Aspose.Cells for Java (Maven artifact `com.aspose:aspose-cells`) | Poskytuje třídy `Workbook`, `Worksheet`, `Range` a související třídy použité v kódu. |
| Zdrojový Excel soubor (`src.xlsx`), který obsahuje kontingenční tabulku, obrázek a tabulku s AutoFiltrem. | Tutoriál manipuluje s těmito objekty pro demonstraci jednotlivých funkcí. |

Přidejte Maven závislost do svého `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Kopírování rozsahu mezi sešity – načtení zdroje a cíle

Prvním krokem je otevřít zdrojový sešit, vybrat rozsah, který obsahuje data, jež chcete zkopírovat, a vytvořit prázdný cílový sešit.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table, picture, and table.
        Workbook sourceWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceWs = sourceWb.getWorksheets().get(0);

        // Define the range that includes the pivot table (A1:G20 in this example).
        Range sourceRange = sourceWs.getCells().createRange("A1:G20");

        // Create a new workbook that will receive the copied range.
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
        Range destRange = destWs.getCells().createRange("A1");
```

> **Proč je to důležité:** Použitím `Range.copy` Aspose.Cells kopíruje nejen surové hodnoty buněk, ale také podkladovou pivot cache, čímž zachovává funkčnost kontingenční tabulky v cílovém sešitu.

---

## Kopírování sešitu s kontingenční tabulkou při kopírování rozsahu

Nyní zkopírujte definovaný rozsah ze zdrojového sešitu do cílového sešitu. Kontingenční tabulka je automaticky zachována, protože rozsah zahrnuje pivot cache.

```java
        // Copy the source range to the destination range.
        destRange.copy(sourceRange);

        // Save the intermediate workbook to verify that the pivot table was copied.
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
```

> **Výsledek:** Otevřením `destination.xlsx` se zobrazí stejný rozvrh kontingenční tabulky jako v `src.xlsx`. Není potřeba žádný další kód pro obnovení pivot cache.

---

## Export obrázku do PowerPointu

Aspose.Cells může označit obrázek k exportu jako editovatelný objekt PowerPointu. Následující kód vybere první obrázek na cílovém listu a nastaví příznak exportu.

```java
        // Retrieve the first picture on the destination sheet.
        Shape picture = destWs.getPictures().get(0);

        // Instruct Aspose.Cells to export this picture as a PowerPoint object.
        picture.getPictureFormat().setExportToPptx(true);

        // Optionally, save the workbook as PPTX to see the result.
        destWb.save("YOUR_DIRECTORY/destination.pptx");
```

> **Co vidíte:** Otevřením `destination.pptx` v PowerPointu se obrázek zobrazí jako nativní tvar, který můžete upravovat, měnit jeho velikost nebo animovat.

---

## Odebrání AutoFiltru z Excel tabulky

Pokud zdrojový list obsahuje tabulku s AutoFiltrem, můžete jej po kopírování vymazat. Níže uvedený kód přistupuje k první tabulce a odstraní její filtr.

```java
        // Access the first table on the destination sheet.
        Table table = destWs.getTables().get(0);

        // Remove the AutoFilter by assigning null.
        table.setAutoFilter(null);

        // Save the final workbook.
        destWb.save("YOUR_DIRECTORY/final_output.xlsx");
```

> **Efekt:** Tabulka zůstane v sešitu, ale šipky rozbalovacího filtru zmizí, což vám poskytne čistý pohled na data.

---

## Načtení sešitu s možnostmi SmartMarker – zacházet s JSON poli jako s jednou buňkou

Když generujete zprávu z JSON, Aspose.Cells může zacházet s celým polem jako s jednou hodnotou buňky. To je užitečné pro vložení JSON řetězců do šablony, aniž by se rozbalily do více buněk.

```java
        // Configure LoadOptions to enable SmartMarker array handling.
        LoadOptions loadOptions = new LoadOptions();
        SmartMarkerOptions smOptions = new SmartMarkerOptions();
        smOptions.setArrayAsSingle(true);
        loadOptions.setSmartMarkerOptions(smOptions);

        // Load a template workbook using the configured options.
        Workbook smartMarkerWb = new Workbook("YOUR_DIRECTORY/template.xlsx", loadOptions);

        // Continue processing (e.g., populate markers) as needed.
        // ...

        // Save the processed workbook.
        smartMarkerWb.save("YOUR_DIRECTORY/template_filled.xlsx");
    }
}
```

> **Proč byste to mohli použít:** Pokud váš JSON payload obsahuje pole, které by mělo být v jedné buňce jako JSON řetězec, `setArrayAsSingle(true)` zabrání Aspose.Cells v rozbalení pole do samostatných řádků nebo sloupců.

---

![Kopírování rozsahu mezi sešity v Javě – příklad kódu Aspose.Cells](copy-range-workbooks.png)

*Text alternativy obrázku:* **Kopírování rozsahu mezi sešity v Javě – příklad kódu Aspose.Cells** (odpovídá hlavnímu klíčovému slovu).

---

## Očekávaný výstup

| Název souboru                | Obsahuje |
|--------------------------|----------|
| `destination.xlsx`       | Zkopírovaný rozsah s funkční kontingenční tabulkou. |
| `destination.pptx`       | Exportovaný obrázek jako editovatelný tvar v PowerPointu. |
| `final_output.xlsx`      | Tabulka bez šipek AutoFiltru. |
| `template_filled.xlsx`   | JSON pole uložené jako hodnota jedné buňky. |

Otevřete každý soubor v příslušné aplikaci (Excel nebo PowerPoint), abyste ověřili, že operace proběhly úspěšně.

---

## Závěr

Nyní víte, jak **copy range between workbooks** v Javě pomocí Aspose.Cells, přičemž zachováte kontingenční tabulku, exportujete obrázek do PowerPointu a odstraníte AutoFilter z Excel tabulky. Stejný vzor lze rozšířit pro kopírování libovolného Excel rozsahu do nového sešitu, práci s JSON poli pomocí SmartMarker nebo řetězení dalších transformací.

Další kroky, které můžete prozkoumat:

* **Copy Excel range to new workbook** s více listy.  
* Použijte **export picture to PowerPoint** pro dávkové získávání obrázků.  
* Použijte **remove autofilter from excel table** ve větších reportovacích pipelinech.  
* Kombinujte tyto techniky s Aspose.Slides pro kompletní automatizaci Excel‑to‑PowerPoint.

Neváhejte experimentovat s různými adresami rozsahů, více kontingenčními tabulkami nebo vlastními formáty obrázků. API Aspose.Cells je navrženo pro programovou flexibilitu, takže můžete přizpůsobit zde ukázané vzory tak, aby vyhovovaly jakémukoli podnikovému scénáři automatizace Excelu.

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s krok‑za‑krokem vysvětleními, která vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vlastních projektech.

- [Kopírování obrázků mezi listy v Excelu pomocí Aspose.Cells pro Java: Kompletní průvodce](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Kopírování nastavení rozvržení stránky mezi listy v Excelu pomocí Aspose.Cells Java](/cells/english/java/headers-footers/copy-page-setup-excel-aspose-cells-java/)
- [Kopírování listů Excelu mezi sešity](/cells/english/net/excel-copy-worksheet/excel-copy-worksheets-between-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}