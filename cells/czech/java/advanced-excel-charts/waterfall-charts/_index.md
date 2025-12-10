---
date: 2025-12-10
description: Naučte se, jak vytvořit vodopádový graf v Javě pomocí Aspose.Cells. Krok
  za krokem průvodce přidáním grafu do listu, jeho přizpůsobením a uložením sešitu
  jako XLSX.
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: Jak vytvořit vodopádový graf pomocí Aspose.Cells pro Javu
url: /cs/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Vodopádové grafy

## Úvod do vodopádových grafů pomocí Aspose.Cells pro Java

V tomto tutoriálu se naučíte, jak **vytvořit vodopádový graf** pomocí Aspose.Cells pro Java. Vodopádové grafy jsou nezbytným nástrojem ve vizualizaci dat, protože umožňují vidět kumulativní efekt řady kladných a záporných hodnot. Ať už připravujete finanční výkaz, zprávu o prodeji, nebo jakoukoli jinou analýzu založenou na datech, vodopádový graf může převést surová čísla na jasné, akční poznatky.

## Rychlé odpovědi
- **Co je vodopádový graf?** Vizualizace, která ukazuje, jak je počáteční hodnota zvýšena a snížena řadou mezihodnot, a končí konečným součtem.  
- **Která knihovna se používá?** Aspose.Cells pro Java.  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro vývoj; pro produkci je vyžadována komerční licence.  
- **Mohu soubor uložit jako XLSX?** Ano – použijte `workbook.save("FileName.xlsx")`.  
- **Je vhodný pro vizualizaci dat v Javě?** Rozhodně; Aspose.Cells poskytuje bohaté funkce pro grafy bez nutnosti instalace Office.

## Co je vodopádový graf?
Vodopádový graf zobrazuje sekvenční kladné a záporné příspěvky k počáteční hodnotě, což vám pomáhá pochopit, jak každý komponent ovlivňuje celkový výsledek.

## Proč použít Aspose.Cells pro Java k přidání vodopádového grafu?
- **Není vyžadován Microsoft Excel** – generujte grafy na jakémkoli serveru nebo v CI pipeline.  
- **Plná kontrola nad formátováním** – barvy, popisky dat a osy lze přizpůsobit programově.  
- **Podporuje více výstupních formátů** – XLSX, PDF, HTML a další.  
- **Vysoký výkon** – ideální pro velké sešity a automatizované reportování.

## Předpoklady

Než se ponoříme do kódu, ujistěte se, že máte následující předpoklady:

- Aspose.Cells pro Java: Budete potřebovat nainstalovaný Aspose.Cells pro Java. Můžete jej stáhnout [zde](https://releases.aspose.com/cells/java/).
- Vývojové prostředí Java: Ujistěte se, že máte na svém systému nainstalovanou Javu.

Nyní začněme krok za krokem vytvářet vodopádový graf.

## Jak vytvořit vodopádový graf v Javě

### Krok 1: Import Aspose.Cells

```java
import com.aspose.cells.*;
```

Nejprve musíte do svého Java projektu importovat knihovnu Aspose.Cells. Tato knihovna poskytuje rozsáhlé funkce pro práci se soubory Excel, včetně vytváření grafů.

### Krok 2: Inicializace sešitu a listu

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

Vytvořte nový sešit a přidejte k němu list. Tento list použijeme k zadání našich dat a **přidání grafu do listu**.

### Krok 3: Zadání dat

Nyní naplňme list daty, která chceme zobrazit ve vodopádovém grafu.

```java
Cells cells = worksheet.getCells();

// Insert data
cells.get("A1").putValue("Categories");
cells.get("A2").putValue("Start");
cells.get("A3").putValue("Positive Value 1");
cells.get("A4").putValue("Negative Value 1");
cells.get("A5").putValue("Positive Value 2");
cells.get("A6").putValue("End");

cells.get("B1").putValue("Values");
cells.get("B2").putValue(0);
cells.get("B3").putValue(20);
cells.get("B4").putValue(-10);
cells.get("B5").putValue(15);
cells.get("B6").putValue(25);
```

V tomto příkladu máme kategorie ve sloupci A a odpovídající hodnoty ve sloupci B. Můžete tato data nahradit svým vlastním datasetem.

### Krok 4: Vytvoření vodopádového grafu

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

Do našeho listu jsme přidali vodopádový graf, určili datové řady a data kategorií. Toto je klíčový krok, který **přidává vodopádový graf** do vašeho listu. Můžete dále přizpůsobit vzhled grafu (barvy, popisky dat atd.) pomocí vlastností objektu `Chart`.

### Krok 5: Uložení sešitu

```java
workbook.save("WaterfallChart.xlsx");
```

Uložte sešit do souboru. Příklad používá formát XLSX, ale Aspose.Cells vám také umožní exportovat do PDF, CSV a mnoha dalších formátů. To splňuje požadavek **save workbook xlsx**.

## Časté problémy a řešení

- **Graf se zobrazuje prázdně** – Ověřte, že odkazy na datové rozsahy (`B2:B6` a `A2:A6`) odpovídají skutečným buňkám obsahujícím vaše hodnoty a kategorie.  
- **Záporné hodnoty se nezobrazují správně** – Ujistěte se, že typ řady je nastaven na `ChartType.WATERFALL`; jiné typy grafů zacházejí se zápornými hodnotami odlišně.  
- **Soubor se neotevírá v Excelu** – Ujistěte se, že používáte aktuální verzi Aspose.Cells (nejnovější vydání) a že přípona souboru odpovídá formátu (`.xlsx` pro Excel).

## Často kladené otázky

### Jak mohu přizpůsobit vzhled mého vodopádového grafu?

Vzhled svého vodopádového grafu můžete přizpůsobit úpravou vlastností, jako jsou barvy, popisky dat a popisky os. Podrobné pokyny najdete v dokumentaci Aspose.Cells.

### Mohu vytvořit více vodopádových grafů ve stejném listu?

Ano, můžete vytvořit více vodopádových grafů ve stejném listu tím, že postupujete podle stejných kroků s různými datovými rozsahy.

### Je Aspose.Cells kompatibilní s různými vývojovými prostředími Java?

Ano, Aspose.Cells pro Java je kompatibilní s různými vývojovými prostředími Java, včetně Eclipse, IntelliJ IDEA a NetBeans.

### Mohu přidat další datové řady do mého vodopádového grafu?

Samozřejmě, můžete do svého vodopádového grafu přidat další datové řady, abyste efektivně zobrazili složité datové scénáře.

### Kde najdu další zdroje a příklady pro Aspose.Cells pro Java?

Dokumentaci pro Aspose.Cells pro Java můžete prozkoumat na [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) pro podrobné informace a ukázky kódu.

---

**Last Updated:** 2025-12-10  
**Tested With:** Aspose.Cells for Java 24.12 (latest)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}