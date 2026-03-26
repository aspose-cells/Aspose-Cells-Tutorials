---
date: '2026-02-22'
description: Naučte se, jak automatizovat tvorbu reportů v Excelu pomocí Aspose.Cells
  v Javě s využitím CopyOptions a PasteOptions, aby byly vzorce přesné a vložily se
  pouze viditelné hodnoty.
keywords:
- Aspose.Cells Java
- CopyOptions ReferToDestinationSheet
- PasteOptions Excel
title: Automatizace reportování v Excelu – Ovládnutí CopyOptions a PasteOptions v
  Javě s Aspose.Cells
url: /cs/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

: preserve all code blocks (``` fenced). There are none except placeholders. So fine.

Now translate.

Let's produce final content.

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Automatizace reportování v Excelu pomocí Aspose.Cells: CopyOptions a PasteOptions v Javě

Hledáte způsob, jak **automatizovat reportování v Excelu** pomocí Javy? S Aspose.Cells můžete programově kopírovat, vkládat a upravovat vzorce tak, aby vaše zprávy zůstaly přesné a přenášela se jen potřebná data. V tomto tutoriálu projdeme dvě zásadní funkce — **CopyOptions.ReferToDestinationSheet** a **PasteOptions** — které umožňují zachovat odkazy ve vzorcích a vkládat hodnoty pouze z viditelných buněk.

## Rychlé odpovědi
- **Co dělá `CopyOptions.ReferToDestinationSheet`?** Přepíše vzorce tak, aby odkazovaly na cílový list při kopírování dat.  
- **Jak mohu vložit jen viditelné buňky?** Nastavte `PasteOptions.setOnlyVisibleCells(true)` spolu s `PasteType.VALUES`.  
- **Jaká verze knihovny je vyžadována?** Aspose.Cells 25.3 nebo novější.  
- **Potřebuji licenci pro produkci?** Ano, trvalá nebo dočasná licence odstraňuje omezení evaluační verze.  
- **Mohu použít Maven nebo Gradle?** Oba jsou podporovány; viz ukázky závislostí níže.

## Co znamená „automatizovat reportování v Excelu“?
Automatizace reportování v Excelu znamená programově generovat, konsolidovat a formátovat sešity Excelu, čímž se eliminuje ruční kopírování‑vkládání a snižuje chybovost. Aspose.Cells poskytuje bohaté API, které umožňuje vývojářům Javy manipulovat s tabulkami ve velkém měřítku.

## Proč použít CopyOptions a PasteOptions pro reportování?
- **Zachování integrity vzorců** při přesunu dat mezi listy.  
- **Vyloučení skrytých řádků/sloupců** pro čisté a přehledné zprávy.  
- **Zvýšení výkonu** kopírováním jen nezbytných dat místo celých oblastí.

## Předpoklady
- Java 8 nebo vyšší.  
- Maven nebo Gradle pro správu závislostí.  
- Aspose.Cells 25.3+ (zkušební, dočasná nebo trvalá licence).  

## Nastavení Aspose.Cells pro Javu

Přidejte knihovnu do projektu jedním z následujících způsobů:

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
- **Bezplatná zkušební verze** – Plná funkčnost pro hodnocení.  
- **Dočasná licence** – Odstraní omezení zkušební verze během testování.  
- **Trvalá licence** – Doporučeno pro produkční nasazení.

Inicializujte Aspose.Cells ve svém Java kódu:

```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Průvodce krok za krokem

### 1. CopyOptions s ReferToDestinationSheet

#### Přehled
Nastavením `CopyOptions.ReferToDestinationSheet` na `true` přepíše odkazy ve vzorcích tak, aby po operaci kopírování ukazovaly na nový list.

#### Krok 1: Inicializace Workbook a Worksheets
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Krok 2: Konfigurace CopyOptions
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Krok 3: Provedení operace kopírování
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Proč je to důležité*: Vzorce, které původně odkazovaly na `Sheet1`, nyní správně odkazují na `DestSheet`, což zajišťuje spolehlivost vašich automatizovaných zpráv.

**Tip pro řešení problémů**: Pokud vzorce stále odkazují na starý list, ujistěte se, že `setReferToDestinationSheet(true)` je voláno **před** kopírováním.

### 2. PasteOptions pro vložení pouze hodnot z viditelných buněk

#### Přehled
`PasteOptions` umožňuje definovat, co se vloží. Použitím `PasteType.VALUES` spolu s `onlyVisibleCells=true` zkopírujete jen zobrazené hodnoty, ignorujete skryté řádky/sloupce a formátování.

#### Krok 1: Inicializace Workbook a Worksheets
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Krok 2: Konfigurace PasteOptions
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Krok 3: Provedení operace vložení
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Proč je to důležité*: Ideální pro extrakci filtrovaných dat nebo tvorbu čistých zpráv bez skrytých řádků a rušivého formátování.

**Tip pro řešení problémů**: Ověřte, že řádky/sloupce jsou v Excelu skutečně skryté před kopírováním; jinak budou zahrnuty.

## Praktické aplikace
1. **Finanční konsolidace** – Sloučení měsíčních listů do hlavního sešitu při zachování všech vzorců.  
2. **Export filtrovaných dat** – Přenesení jen viditelných řádků z filtrované tabulky do souhrnného listu.  
3. **Plánované generování zpráv** – Automatizace noční tvorby Excel zpráv s přesnými hodnotami buněk a správnými odkazy.

## Úvahy o výkonu
- **Uvolňujte Workbook** po dokončení (`wb.dispose();`) pro uvolnění nativních zdrojů.  
- **Dávkové operace** – Skupinové volání více kopií/vložení snižuje režii.  
- **Sledujte paměť** – Velké sešity mohou vyžadovat zvýšený hald (`-Xmx2g`).

## Často kladené otázky

**Q1: K čemu slouží `CopyOptions.ReferToDestinationSheet`?**  
A: Přepíše odkazy ve vzorcích tak, aby po kopírování ukazovaly na cílový list, čímž zajistí správnost vzorců v reportech.

**Q2: Jak vložit jen viditelné buňky?**  
A: Nastavte `PasteOptions.setOnlyVisibleCells(true)` a zvolte `PasteType.VALUES`.

**Q3: Můžu používat Aspose.Cells bez zakoupení licence?**  
A: Ano, je k dispozici bezplatná zkušební nebo dočasná licence pro hodnocení, ale pro produkci je vyžadována trvalá licence.

**Q4: Proč jsou některé odkazy po kopírování stále špatné?**  
A: Ověřte, že `ReferToDestinationSheet` je povoleno **před** operací kopírování a že zdrojové vzorce neobsahují odkazy na externí sešity.

**Q5: Jaké jsou osvědčené postupy pro správu paměti?**  
A: Uvolňujte objekty `Workbook` po dokončení, zpracovávejte velké soubory po částech a monitorujte využití haldy JVM.

**Q6: Lze kombinovat CopyOptions a PasteOptions v jedné operaci?**  
A: Ano, můžete je řetězit tak, že nejprve zkopírujete s `CopyOptions` a následně použijete `PasteOptions` na cílový rozsah.

## Zdroje
- **Dokumentace**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Stáhnout**: [Aspose.Cells Releases for Java](https://releases.aspose.com/cells/java/)  
- **Koupit**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Bezplatná zkušební verze**: [Aspose.Cells Free Trial](https://releases.aspose.com/cells/java/)  
- **Dočasná licence**: [Apply for a Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Fórum podpory**: [Aspose Support](https://forum.aspose.com/c/cells)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Poslední aktualizace:** 2026-02-22  
**Testováno s:** Aspose.Cells 25.3 pro Javu  
**Autor:** Aspose