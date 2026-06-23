---
date: '2026-03-15'
description: Naučte se, jak rozdělit jména do samostatných sloupců a uložit sešit
  xlsx pomocí Aspose Cells Java v krok‑za‑krokem tutoriálu.
keywords:
- Aspose.Cells Java
- split names columns
- Excel manipulation
- text to columns Java
- Java Excel processing
title: aspose cells java – Rozdělit jména do sloupců
url: /cs/java/cell-operations/aspose-cells-java-split-names-columns/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ovládání **aspose cells java**: Rozdělení jmen do sloupců

Vítejte v našem komplexním tutoriálu **aspose cells java**. V tomto průvodci se naučíte **jak rozdělit jména**, která jsou uložena v jednom sloupci Excelu, do dvou samostatných sloupců – jméno a příjmení – pomocí výkonné funkce text‑to‑columns. Ať už čistíte seznam kontaktů, připravujete data pro import do CRM, nebo jen potřebujete rychlý způsob, jak přestrukturovat tabulky, tento tutoriál vám přesně ukáže, jak **uložit sešit xlsx** po transformaci.

## Rychlé odpovědi
- **Co tento tutoriál pokrývá?** Rozdělení řetězců s plným jménem do sloupců jméno a příjmení pomocí Aspose.Cells pro Java.  
- **Která verze knihovny je použita?** Nejnovější stabilní vydání (k roku 2026).  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro vývoj; pro produkci je vyžadována komerční licence.  
- **Mohu rozdělovat podle jiných oddělovačů?** Ano – stačí změnit oddělovač v `TxtLoadOptions`.  
- **Je výstup .xlsx soubor?** Ano, sešit je uložen ve formátu XLSX.

## Co je **aspose cells java**?
**Aspose.Cells java** je vysoce výkonný Java API, který umožňuje vývojářům vytvářet, upravovat, konvertovat a renderovat soubory Excel bez potřeby Microsoft Office. Podporuje všechny hlavní formáty Excelu a poskytuje pokročilé funkce jako vzorce, grafy a manipulaci s daty.

## Proč použít **aspose cells java** pro rozdělení jmen?
- **Zero‑install**: Funguje v jakémkoli serverovém Java prostředí.  
- **Rychlost**: Zpracovává velké tabulky rychleji než nativní Excel interop.  
- **Přesnost**: Plná kontrola nad oddělovači, rozsahy sloupců a výstupními formáty.  
- **Spolehlivost**: Žádné závislosti na COM nebo Office, což je ideální pro nasazení v cloudu nebo kontejnerech.

## Předpoklady
- Java Development Kit (JDK) 8 nebo novější.  
- IDE jako IntelliJ IDEA nebo Eclipse (volitelné, ale doporučené).  
- Maven nebo Gradle pro správu závislostí.  

### Nastavení Maven
Přidejte závislost Aspose.Cells do vašeho `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Nastavení Gradle
Přidejte knihovnu do vašeho `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

> **Tip:** Použijte dočasnou licenci z portálu Aspose k odemknutí plné funkčnosti během vývoje.

## Implementace krok za krokem

### Krok 1: Vytvořte sešit a přistupte k prvnímu listu
Nejprve importujte základní třídy a vytvořte novou instanci sešitu. Tím získáte čistý Excel soubor připravený pro vložení dat.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
```

```java
String dataDir = "YOUR_DATA_DIRECTORY"; // Define your directory path here

Workbook wb = new Workbook();
Worksheet ws = wb.getWorksheets().get(0);
```

### Krok 2: Naplňte list ukázkovými jmény
Dále přidejte několik řetězců s plným jménem do sloupce **A**. V reálném projektu byste je načítali z databáze nebo CSV souboru.

```java
import com.aspose.cells.Cell;

String outDir = "YOUR_OUTPUT_DIRECTORY"; // Define your output directory path here

ws.getCells().get("A1").putValue("John Teal");
ws.getCells().get("A2").putValue("Peter Graham");
ws.getCells().get("A3").putValue("Brady Cortez");
ws.getCells().get("A4").putValue("Mack Nick");
ws.getCells().get("A5").putValue("Hsu Lee");
```

### Krok 3: Nakonfigurujte Text Load Options pro rozdělení sloupců
Třída `TxtLoadOptions` říká Aspose.Cells, jak interpretovat text. Zde používáme mezeru (`' '`) jako oddělovač.

```java
import com.aspose.cells.TxtLoadOptions;

TxtLoadOptions opts = new TxtLoadOptions();
opts.setSeparator(' ');
```

### Krok 4: Rozdělte text do dvou sloupců
Nyní zavolejte `textToColumns()` na oblast buněk, která obsahuje jména. Parametry `(0, 0, 5, opts)` znamenají *začít na řádku 0, sloupci 0, zpracovat 5 řádků, s použitím právě definovaných možností*.

```java
ws.getCells().textToColumns(0, 0, 5, opts);
```

Po tomto volání sloupec A obsahuje křestní jména a sloupec B obsahuje příjmení.

### Krok 5: Uložte sešit jako soubor XLSX
Nakonec zapište upravený sešit na disk. Výčtový typ `SaveFormat` zajišťuje, že soubor je uložen v moderním formátu XLSX.

```java
import com.aspose.cells.SaveFormat;

wb.save(outDir + "outputTextToColumns.xlsx");
```

> **Proč je to důležité:** Použitím **save workbook xlsx** zaručujete kompatibilitu s nejnovějšími verzemi Excelu, Google Sheets a dalších tabulkových nástrojů.

## Praktické aplikace
- **Čištění dat:** Rychle oddělte spojená pole před načtením do analytických pipeline.  
- **Integrace s CRM:** Přetvořte plochý seznam kontaktů na strukturovanou tabulku pro import.  
- **HR systémy:** Rozdělte plná jména zaměstnanců pro zpracování mezd nebo benefitů.

## Úvahy o výkonu
Při práci s tisíci řádky:

1. **Dávkové aktualizace:** Použijte `ws.getCells().setRowHeight()` nebo podobné dávkové metody ke snížení režie.  
2. **Správa paměti:** Volajte `wb.calculateFormula()` jen když je to nutné a rychle uvolňujte velké objekty.  
3. **Garbage Collection:** Spusťte JVM s vhodnými nastaveními haldy (`-Xmx2g` pro velké soubory), aby nedošlo k chybám OutOfMemory.

## Časté problémy a řešení

| Problém | Řešení |
|-------|----------|
| **Jména obsahují prostřední iniciály** (např. “John A. Doe”) | Upravte oddělovač nebo po‑zpracujte druhý sloupec pro extrakci příjmení. |
| **Neočekávané prázdné buňky** | Ověřte, že zdrojový rozsah (parametry `textToColumns`) odpovídá skutečným řádkům s daty. |
| **Licence nebyla nalezena** | Umístěte dočasný licenční soubor (`Aspose.Cells.lic`) do kořenového adresáře projektu nebo nastavte licenci programově. |

## Často kladené otázky

**Q: Co je Aspose.Cells Java?**  
A: Výkonná knihovna, která umožňuje programově vytvářet, upravovat a konvertovat soubory Excel pomocí Javy.

**Q: Mohu rozdělovat sloupce podle oddělovačů jiných než mezery?**  
A: Ano, můžete přizpůsobit oddělovač v `TxtLoadOptions` podle potřeby vašich dat.

**Q: Jak zacházet s velkými datovými sadami pomocí Aspose.Cells?**  
A: Optimalizujte výkon spravováním paměti a minimalizací operací sešitu, jak je popsáno výše.

**Q: Je k dispozici podpora, pokud narazím na problémy?**  
A: Navštivte [Aspose Forum](https://forum.aspose.com/c/cells/9) pro komunitní pomoc nebo kontaktujte přímo tým podpory Aspose.

**Q: V jakých formátech může Aspose.Cells ukládat sešity?**  
A: Podporuje širokou škálu formátů souborů Excel, včetně XLSX, XLS, CSV a dalších.

## Zdroje

- **Dokumentace**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **Stáhnout**: [Aspose.Cells Java Releases](https://releases.aspose.com/cells/java/)
- **Koupit**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Bezplatná zkušební verze**: [Try Aspose.Cells for Free](https://releases.aspose.com/cells/java/)
- **Dočasná licence**: [Request a Temporary License](https://purchase.aspose.com/temporary-license/)

Šťastné programování a užívejte si plný potenciál **aspose cells java** ve svých projektech!

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Poslední aktualizace:** 2026-03-15  
**Testováno s:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose