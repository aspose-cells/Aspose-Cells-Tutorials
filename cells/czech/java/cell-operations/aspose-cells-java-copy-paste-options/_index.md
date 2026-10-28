---
date: '2026-10-28'
description: Naučte se, jak vložit hodnoty pomocí možností kopírování a vkládání v
  Aspose.Cells v jazyce Java, s podrobným kódem krok za krokem, nastavením závislosti
  Maven a tipy k licencování.
keywords:
- how to paste values
- aspose cells maven dependency
- java generate excel report
- aspose cells license java
- copyoptions refertodestinationsheet
lastmod: '2026-10-28'
og_description: Naučte se, jak vložit hodnoty pomocí možností kopírování a vkládání
  v Aspose.Cells v jazyce Java, s podrobným kódem krok za krokem, nastavením závislosti
  Maven a tipy k licencování.
og_image_alt: Developer guide showing Java code for copying and pasting Excel data
  with Aspose.Cells
og_title: Jak vložit hodnoty pomocí možností kopírování a vkládání v Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to paste values using Aspose.Cells copy and paste options
    in Java, with step‑by‑step code, Maven dependency setup, and licensing tips.
  headline: How to paste values with Aspose.Cells copy and paste options
  type: TechArticle
- questions:
  - answer: It rewrites formula references so they point to the destination sheet
      after a copy, ensuring reporting formulas stay correct.
    question: What is `CopyOptions.ReferToDestinationSheet` used for?
  - answer: Set `PasteOptions.setOnlyVisibleCells(true)` and choose `PasteType.VALUES`.
    question: How do I paste only visible cells?
  - answer: Yes, a free trial or temporary license is available for evaluation, but
      a permanent license is required for production.
    question: Can I use Aspose.Cells without purchasing a license?
  - answer: Double‑check that `ReferToDestinationSheet` is enabled **before** the
      copy operation and that the source formulas don’t contain external workbook
      links.
    question: Why are some references still wrong after copying?
  - answer: Dispose of `Workbook` objects when finished, process large files in chunks,
      and monitor JVM heap usage.
    question: What memory‑management best practices should I follow?
  type: FAQPage
tags:
- paste values
- Aspose.Cells
- Java Excel automation
- copy options
- paste options
title: Jak vložit hodnoty pomocí možností kopírování a vkládání v Aspose.Cells
url: /cs/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vložit hodnoty pomocí možností kopírování a vkládání v Aspose.Cells

Automatizace reportování v Excelu v Javě vám umožní generovat, konsolidovat a formátovat sešity, aniž byste museli ručně otevírat Excel. S **Aspose.Cells** získáte plnou kontrolu nad vzorci, skrytými řádky a hodnotami buněk, takže vaše reporty zůstávají přesné a lehké. V tomto tutoriálu se naučíte, jak použít **CopyOptions.ReferToDestinationSheet**, aby vzorce zůstaly správné, a **PasteOptions**, aby se vložily jen viditelné hodnoty, které potřebujete.

## Rychlé odpovědi
- **Co dělá `CopyOptions.ReferToDestinationSheet`?** Přepisuje vzorce tak, aby odkazovaly na cílový list po operaci kopírování.  
- **Jak mohu vložit jen viditelné buňky?** Zavolejte `PasteOptions.setOnlyVisibleCells(true)` spolu s `PasteType.VALUES`.  
- **Jaká verze knihovny je vyžadována?** Aspose.Cells 25.3 nebo novější.  
- **Potřebuji licenci pro produkci?** Ano – trvalá nebo dočasná licence odstraňuje omezení zkušební verze.  
- **Mohu použít Maven nebo Gradle?** Obě jsou podporovány; viz ukázky závislostí níže.

## Co je „automatizace reportování v Excelu“?
Automatizace reportování v Excelu znamená programové generování a aktualizaci Excelových sešitů, což vám umožní vytvářet, slučovat a formátovat reporty bez ručního kopírování‑vkládání, čímž se snižuje počet chyb a šetří hodiny opakované práce. Tento přístup je ideální pro plánované dávkové úlohy, datově řízené dashboardy a finanční konsolidační pipeline.

## Proč použít CopyOptions a PasteOptions pro reportování?
Tyto dvě třídy vám umožní zachovat referenční odkazy ve vzorcích při kopírování dat **a** extrahovat jen buňky, které jsou viditelné po filtrování nebo skrytí řádků. Použití obou společně snižuje objem přenášených dat až o 80 % v typických scénářích filtrovaných tabulek a zajišťuje, že vzorce nadále správně počítají v cílovém listu.

## Požadavky
- Java 8 nebo vyšší.  
- Maven nebo Gradle pro správu závislostí.  
- Aspose.Cells 25.3+ (zkušební, dočasná nebo trvalá licence).  

## Nastavení Aspose.Cells pro Java

Přidejte knihovnu do svého projektu jednou z následujících možností:

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**  
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Získání licence
- **Free trial** – plná sada funkcí pro hodnocení.  
- **Temporary license** – odstraňuje omezení zkušební verze během testování.  
- **Permanent license** – doporučeno pro produkční zatížení.

Inicializujte Aspose.Cells ve svém Java kódu:  
```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Postup krok za krokem

### 1. copyOptions s referToDestinationSheet

#### Přehled
`CopyOptions` je konfigurační objekt Aspose.Cells, který řídí, jak jsou vzorce a odkazy na buňky zpracovány během operace kopírování. Nastavení `CopyOptions.ReferToDestinationSheet` na `true` přepíše odkazy ve vzorcích tak, aby ukazovaly na nový list po kopírování.

#### Krok 1: inicializace sešitu a listů  
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Krok 2: konfigurace copyOptions  
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Krok 3: provedení operace kopírování  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Proč je to důležité*: Vzorce, které původně odkazovaly na `Sheet1`, nyní budou správně odkazovat na `DestSheet`, což udržuje vaše automatizované reporty spolehlivé.

**Tip pro řešení problémů**: Pokud vzorce stále odkazují na starý list, ujistěte se, že `setReferToDestinationSheet(true)` je voláno **před** kopírováním.

### 2. pasteOptions pro pouze hodnoty z viditelných buněk

#### Přehled
`PasteOptions` je nastavení Aspose.Cells, které určuje, co se vloží. Použití `PasteType.VALUES` spolu s `onlyVisibleCells=true` kopíruje jen zobrazené hodnoty, ignoruje skryté řádky/sloupce a formátování.

#### Krok 1: inicializace sešitu a listů  
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Krok 2: konfigurace pasteOptions  
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Krok 3: provedení operace vkládání  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Proč je to důležité*: Ideální pro extrakci filtrovaných dat nebo generování čistých reportů bez skrytých řádků či rušivého formátování.

**Tip pro řešení problémů**: Ověřte, že řádky/sloupce jsou v Excelu skutečně skryté před kopírováním; jinak budou zahrnuty.

## Praktické aplikace
1. **Financial consolidation** – sloučit měsíční listy do hlavního sešitu při zachování všech vzorců přesných.  
2. **Filtered data export** – vybrat jen viditelné řádky z filtrované tabulky do souhrnného listu.  
3. **Scheduled report generation** – automatizovat noční tvorbu Excelových reportů s přesnými hodnotami buněk a správnými odkazy.

## Úvahy o výkonu
- **Dispose of workbooks** když je práce dokončena (`wb.dispose();`) pro uvolnění nativních zdrojů.  
- **Batch operations** – seskupte více volání copy/paste pro snížení režie.  
- **Monitor memory** – velké sešity mohou vyžadovat zvýšený heap (`-Xmx2g`).  
- Aspose.Cells podporuje **více než 50 vstupních a výstupních formátů** a dokáže zpracovat sešity s **až 2 miliony řádků** bez načítání celého souboru do paměti, což poskytuje vysokou propustnost pro podnikovou zátěž.

## Často kladené otázky

**Q: K čemu se používá `CopyOptions.ReferToDestinationSheet`?**  
A: Přepisuje odkazy ve vzorcích tak, aby po kopírování ukazovaly na cílový list, čímž zajišťuje, že vzorce v reportech zůstávají správné.

**Q: Jak vložit jen viditelné buňky?**  
A: Nastavte `PasteOptions.setOnlyVisibleCells(true)` a zvolte `PasteType.VALUES`.

**Q: Mohu používat Aspose.Cells bez zakoupení licence?**  
A: Ano, je k dispozici bezplatná zkušební verze nebo dočasná licence pro hodnocení, ale pro produkci je vyžadována trvalá licence.

**Q: Proč jsou po kopírování některé odkazy stále špatné?**  
A: Zkontrolujte, že je `ReferToDestinationSheet` povoleno **před** operací kopírování a že zdrojové vzorce neobsahují odkazy na externí sešity.

**Q: Jaké jsou osvědčené postupy pro správu paměti?**  
A: Uvolňujte objekty `Workbook` po dokončení, zpracovávejte velké soubory po částech a sledujte využití heapu JVM.

**Q: Lze kombinovat CopyOptions a PasteOptions v jedné operaci?**  
A: Ano, můžete je řetězit tak, že nejprve kopírujete s `CopyOptions` a poté na cílový rozsah použijete `PasteOptions`.

## Zdroje
- **Documentation**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Download**: [Aspose.Cells releases for Java](https://releases.aspose.com/cells/java/)  
- **Purchase**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Free trial**: [Aspose.Cells free trial](https://releases.aspose.com/cells/java/)  
- **Temporary license**: [Apply for a temporary license](https://purchase.aspose.com/temporary-license/)  
- **Support forum**: [Aspose support](https://forum.aspose.com/c/cells)

---

**Poslední aktualizace:** 2026-10-28  
**Testováno s:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose

## Související tutoriály

- [Read Excel File Java – Master Workbook Cell Manipulation with Aspose.Cells](/cells/java/cell-operations/aspose-cells-java-workbook-cell-manipulation/)
- [Add Data to Cell in Excel Using Aspose.Cells for Java](/cells/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Convert Excel Cell Row Column Indices with Aspose.Cells Java](/cells/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}