---
date: 2025-12-04
description: Naučte se, jak vytvořit interaktivní graf v Javě pomocí Aspose.Cells,
  přidat tooltipy do grafu a přidat drill‑down graf pro bohatší vizualizaci dat.
language: cs
linktitle: Create Interactive Chart Java
second_title: Aspose.Cells Java Excel Processing API
title: Vytvořte interaktivní graf v Javě s Aspose.Cells
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření interaktivního grafu Java

## Úvod

Interaktivní grafy poskytují vašim uživatelům možnost prozkoumávat datové body, zobrazovat podrobnosti při najetí myší a dokonce se ponořit do podrobnějších datových sad – vše bez opuštění tabulky. V tomto tutoriálu se naučíte **jak vytvořit interaktivní graf Java** aplikace pomocí Aspose.Cells. Provedeme vás přidáváním tooltipů, datových popisků a implementací funkce drill‑down, aby vaše grafy byly poutavější a informativnější.

## Rychlé odpovědi
- **Jaká knihovna se používá?** Aspose.Cells for Java  
- **Mohu do grafu přidat tooltipy?** Ano, pomocí API NSeries data‑label  
- **Je podporován drill‑down?** Ano, připojením hypertextových odkazů k datovým bodům  
- **Jaký formát souboru se vytváří?** Standardní sešit XLSX s vloženými grafy  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro hodnocení; pro produkční nasazení je vyžadována komerční licence  

## Předpoklady

Než se pustíme dál, ujistěte se, že máte:

- Vývojové prostředí Java (doporučeno JDK 8+)  
- Knihovnu Aspose.Cells for Java (stáhněte z oficiální [Aspose release page](https://releases.aspose.com/cells/java/))  
- Ukázkový soubor Excel pojmenovaný **data.xlsx** obsahující data, která chcete vizualizovat  

## Krok 1: Nastavení Java projektu

1. Vytvořte nový Java projekt ve svém oblíbeném IDE (IntelliJ IDEA, Eclipse, VS Code atd.).  
2. Přidejte JAR Aspose.Cells do classpath vašeho projektu – buď umístěním JARu do složky `libs`, nebo přidáním Maven/Gradle závislosti.  

## Krok 2: Načtení dat

Pro vytvoření interaktivního grafu nejprve potřebujete list s daty. Níže uvedený úryvek otevře existující sešit a získá první list.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **Tip:** Ujistěte se, že datový rozsah, který chcete zobrazit v grafu, je souvislý; Aspose.Cells automaticky detekuje rozsah při svázání sérií.  

## Krok 3: Vytvoření grafu

Nyní vytvoříme sloupcový graf a umístíme jej na list. Můžete změnit `ChartType.COLUMN` na jakýkoli jiný typ (např. `ChartType.LINE`), pokud preferujete jiný vizuální styl.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Proč je to důležité:** Přidání grafu programově vám dává plnou kontrolu nad jeho velikostí, umístěním a zdrojem dat, což je nezbytné pro tvorbu interaktivních zážitků.  

## Krok 4: Přidání interaktivity

### Jak přidat tooltipy do grafu

Tooltipy (nebo datové popisky zobrazující hodnoty) pomáhají uživatelům okamžitě vidět přesnou hodnotu za každým sloupcem. Následující kód povolí datové popisky a nastaví je tak, aby zobrazovaly hodnotu.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### Jak přidat datové popisky (callouty)

Pokud chcete, aby se popisky zobrazovaly jako callouty místo prostého textu, přepněte vlastnost `ShowLabelAsDataCallout`.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### Jak přidat drill‑down graf

Drill‑down umožňuje uživateli kliknout na datový bod a přejít na související detailní pohled – běžně implementováno pomocí hypertextového odkazu. Níže připojujeme URL k prvnímu bodu v sérii.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

> **Častá chyba:** Nezapomeňte nastavit cíl hypertextového odkazu na stránku, která dokáže zobrazit podrobná data (např. webovou zprávu nebo jiný list Excel). Jinak kliknutí povede na neexistující odkaz.  

## Krok 5: Uložení sešitu

Po nastavení grafu uložte sešit. Výsledný soubor obsahuje interaktivní graf připravený k otevření v Excelu nebo jakémkoli kompatibilním prohlížeči.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Závěr

V tomto průvodci jste se naučili **jak vytvořit interaktivní graf Java** řešení s Aspose.Cells, pokrývající:

- Načtení dat z existujícího sešitu  
- Programové vytvoření sloupcového grafu  
- Přidání tooltipů a callout datových popisků  
- Implementaci funkce drill‑down pomocí hypertextových odkazů  
- Uložení finálního sešitu  

Tyto techniky promění statické tabulky na dynamické, uživatelsky přívětivé dashboardy, které zvyšují pochopení dat a rozhodovací proces.

## Často kladené otázky

**Q: Jak mohu změnit typ grafu?**  
A: Změňte výčtový typ `ChartType` v metodě `add` (např. `ChartType.LINE` pro čárový graf).

**Q: Mohu přizpůsobit vzhled tooltipů?**  
A: Ano, můžete upravit velikost písma, barvu, pozadí a další stylové vlastnosti pomocí objektu `DataLabels`.

**Q: Jak řešit interaktivitu grafu ve webové aplikaci?**  
A: Exportujte sešit do XLSX, poté použijte JavaScriptovou knihovnu pro grafy (např. Highcharts) k vykreslení dat na straně klienta, nebo vložte soubor Excel do Office Web Vieweru, který respektuje hypertextové odkazy.

**Q: Kde najdu více příkladů?**  
A: Navštivte oficiální [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) pro úplný seznam tříd a metod souvisejících s grafy.

**Q: Potřebuji licenci pro produkční použití?**  
A: Ano, pro nasazení je vyžadována komerční licence; pro testování je k dispozici bezplatná zkušební licence.

---

**Poslední aktualizace:** 2025-12-04  
**Testováno s:** Aspose.Cells for Java 24.12 (nejnovější v době psaní)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}