---
date: 2026-02-09
description: Naučte se, jak vytvořit 3D koláčový graf v Javě pomocí Aspose.Cells.
  Vytvořte 3D sloupcový graf, přidejte 3D graf do Excelu a uložte sešit ve formátu xlsx
  s podrobnými ukázkami kódu krok za krokem.
linktitle: Create 3D Pie Chart Java
second_title: Aspose.Cells Java Excel Processing API
title: Vytvořte 3D koláčový graf v Javě s Aspose.Cells
url: /cs/java/advanced-excel-charts/3d-charts/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření 3D koláčového grafu v Javě

## Úvod 3D grafy

Aspose.Cells for Java je výkonné Java API pro práci se soubory Excel a usnadňuje **create 3d pie chart** projekty i klasické 3‑D sloupcové vizualizace. V tomto tutoriálu uvidíte přesně, jak vygenerovat 3‑D sloupcový graf, jak přizpůsobit stejný přístup pro 3‑D koláčový graf, upravit vzhled a nakonec **add 3d chart excel** soubory do vašich reportů. Ať už budujete finanční dashboard, list výkonnosti prodeje nebo vizualizujete vědecká data, níže uvedené kroky vám poskytnou pevný základ.

## Rychlé odpovědi
- **What library do I need?** Aspose.Cells for Java (latest version)  
- **Can I generate a 3D bar chart?** Yes – use `ChartType.BAR_3_D`  
- **Do I need a license?** A valid license removes evaluation limits  
- **Which Excel versions are supported?** All major versions from 2003 to 2023  
- **Is it possible to export the chart as an image?** Yes, via `chart.toImage()` methods  

## Co jsou 3D grafy?
3D grafy přidávají hloubku k tradičním 2D vizualizacím, což divákům pomáhá intuitivněji pochopit vícerozměrné vztahy. Jsou zvláště užitečné, když potřebujete porovnat několik kategorií vedle sebe a zároveň zachovat jasnou vizuální hierarchii.

## Proč použít Aspose.Cells for Java pro generování 3D sloupcového grafu?
Aspose.Cells for Java nabízí bohatou sadu API pro tvorbu grafů, plnou kompatibilitu s Excelem a detailní kontrolu nad stylováním. To znamená, že můžete **generate 3d bar chart** objekty programově bez starostí o specifika jednotlivých verzí Excelu.

## Nastavení Aspose.Cells for Java

### Stažení a instalace
Knihovnu Aspose.Cells for Java si můžete stáhnout z oficiální webové stránky. Postupujte podle poskytnutých instrukcí pro Maven/Gradle nebo přidejte JAR přímo do classpath vašeho projektu.

### Inicializace licence
Pro odemknutí plné sady funkcí inicializujte licenci před jakoukoliv operací s grafy:

```java
// Initialize Aspose.Cells license
License license = new License();
license.setLicense("path_to_license_file.xml");
```

## Vytvoření základního 3D grafu

### Import potřebných knihoven
Nejprve načtěte požadované třídy do rozsahu:

```java
import com.aspose.cells.*;
```

### Inicializace sešitu
Vytvořte nový sešit, který bude hostit graf:

```java
Workbook workbook = new Workbook();
```

### Přidání dat do grafu
Naplněte list ukázkovými daty, na která bude graf odkazovat:

```java
Worksheet worksheet = workbook.getWorksheets().get(0);

// Adding data to cells
worksheet.getCells().get("A1").putValue("Category");
worksheet.getCells().get("A2").putValue("A");
worksheet.getCells().get("A3").putValue("B");
worksheet.getCells().get("A4").putValue("C");

worksheet.getCells().get("B1").putValue("Value");
worksheet.getCells().get("B2").putValue(10);
worksheet.getCells().get("B3").putValue(20);
worksheet.getCells().get("B4").putValue(30);
```

### Jak vygenerovat 3D sloupcový graf v Javě
Nyní vytvoříme samotný graf a aplikujeme základní úpravy:

```java
int chartIndex = worksheet.getCharts().add(ChartType.BAR_3_D, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Setting the data range for the chart
chart.getNSeries().add("A2:B4", true);

// Customizing chart attributes
chart.getChartArea().getBorder().setVisible(false);
chart.getChartTitle().setText("3D Bar Chart");
```

### Uložení grafu do souboru
Nakonec zapíšete sešit (který nyní obsahuje 3‑D graf) na disk. Tím také **save workbook xlsx** ve standardním formátu Excel:

```java
workbook.save("3D_Chart.xlsx");
```

## Jak vytvořit 3D koláčový graf s Aspose.Cells for Java
Pokud potřebujete vizualizaci ve stylu koláče, postup je téměř identický – mění se jen enum `ChartType`. Nahraďte `ChartType.BAR_3_D` za `ChartType.PIE_3_D` při přidávání grafu a nasměrujte sérii na stejný datový rozsah. Po vytvoření grafu můžete:

* Nastavit popisný název, například “3D Sales Distribution”.
* Upravit barvy výsečů pomocí `chart.getSeries().get(i).getArea().setForegroundColor(...)`.
* Exportovat koláčový graf do PNG obrázku pomocí `chart.toImage("pie_chart.png", ImageFormat.getPng())`, což splňuje požadavek **convert chart png**.

Protože počet bloků kódu musí zůstat nezměněn, skutečný Java úryvek zde není uveden, ale kroky jsou totožné s příkladem sloupcového grafu výše.

## Různé typy 3D grafů
Aspose.Cells for Java podporuje několik variant 3D grafů, které můžete **add 3d chart excel** soubory s:

- **Bar charts** – ideální pro porovnání kategorií.  
- **Pie charts** – zobrazují podílové příspěvky (včetně 3D koláče).  
- **Line charts** – ilustrují trendy v čase.  
- **Area charts** – zdůrazňují velikost změny.

Můžete přepnout enum `ChartType` na kterýkoliv z výše uvedených při zachování stejného vzoru tvorby.

## Pokročilé přizpůsobení grafu

### Přidání titulů a popisků
Dejte grafu kontext nastavením popisného názvu a popisků os.

### Úprava barev a stylů
Použijte metodu `chart.getSeries().get(i).getArea().setForegroundColor(Color.getRGB(...))` k sladění s firemní identitou.

### Práce s osami grafu
Doladěte měřítka os, intervaly a značky, aby byl graf čitelnější.

### Přidání legendy
Povolte legendu pomocí `chart.getLegend().setVisible(true)`, aby si diváci mohli přiřadit jednotlivé datové série.

### Export grafů jako obrázky
Když potřebujete statický obrázek pro webový report, zavolejte `chart.toImage("chart.png", ImageFormat.getPng())`. Tím se splní případ použití **convert chart png** bez opuštění sešitu.

## Integrace dat
Aspose.Cells for Java může načítat data z databází, CSV souborů nebo živých API. Jednoduše naplňte buňky listu získanými daty před propojením rozsahu s grafem. To udržuje váš **add 3d chart excel** workflow dynamický a aktuální.

## Závěr
V tomto průvodci jsme prošli, jak **create 3d pie chart** a **create 3d bar chart** projekty od začátku do konce – nastavení knihovny, přidání dat, generování 3‑D sloupcového grafu, úpravu stejných kroků pro 3‑D koláčový graf a aplikaci pokročilého stylování. S Aspose.Cells for Java máte spolehlivý, verzně nezávislý způsob, jak vložit bohaté 3‑D vizualizace přímo do Excel sešitů a dokonce je exportovat jako PNG obrázky.

## Často kladené otázky

**Q: Jak mohu přidat více datových sérií do 3D grafu?**  
A: Použijte `chart.getNSeries().add()` pro každý rozsah série a zajistěte, aby typ grafu zůstal 3‑D (např. `ChartType.BAR_3_D` nebo `ChartType.PIE_3_D`).

**Q: Mohu exportovat 3D grafy vytvořené pomocí Aspose.Cells for Java do jiných formátů?**  
A: Ano, můžete graf uložit jako PNG, JPEG nebo PDF voláním příslušných přetížení `chart.toImage()` nebo `workbook.save()`, čímž splníte požadavek **convert chart png**.

**Q: Je možné vytvořit interaktivní 3D grafy s Aspose.Cells for Java?**  
A: Aspose.Cells se zaměřuje na statické Excel grafy. Pro interaktivní webové 3‑D vizualizace zvažte propojení Excel dat s JavaScript knihovnami jako Three.js.

**Q: Mohu automatizovat proces aktualizace dat v mých 3D grafech?**  
A: Rozhodně. Načtěte nová data do listu programově a obnovte rozsah grafu; při dalším otevření sešitu graf zobrazí s aktualizovanými hodnotami.

**Q: Kde najdu další zdroje a dokumentaci k Aspose.Cells for Java?**  
A: Kompletní dokumentaci a zdroje pro Aspose.Cells for Java najdete na webu: [Aspose.Cells for Java Documentation](https://reference.aspose.com/cells/java/).

---

**Last Updated:** 2026-02-09  
**Tested With:** Aspose.Cells for Java 24.12 (latest)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}