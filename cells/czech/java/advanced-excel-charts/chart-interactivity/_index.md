---
date: 2025-11-28
description: Naučte se, jak přidat tooltipy, popisky dat a funkce drill‑down pro vytvoření
  interaktivního grafu v Javě pomocí Aspose.Cells.
language: cs
linktitle: How to Add Tooltips in Interactive Charts
second_title: Aspose.Cells Java Excel Processing API
title: Jak přidat tooltipy do interaktivních grafů (Aspose.Cells Java)
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Jak přidat tooltipy v interaktivních grafech (Aspose.Cells Java)

## Úvod

Interaktivní grafy umožňují uživatelům prozkoumávat data pomocí přejetí myší, kliknutí nebo drill‑downu do podrobností. V tomto tutoriálu se naučíte **jak přidat tooltipy** do grafu, stejně tak **přidat popisky dat** a implementovat **drill‑down** navigaci — vše pomocí Aspose.Cells pro Java. Na konci budete schopni vytvořit plně vybavený, interaktivní graf, který učiní vaše prezentace dat poutavějšími a informativnějšími.

## Rychlé odpovědi
- **Jaká knihovna je potřeba?** Aspose.Cells pro Java (nejnovější verze).  
- **Která hlavní funkce je v tomto průvodci pokryta?** Přidání tooltipů do grafů.  
- **Mohu také přidat popisky dat?** Ano — viz sekce „Přidání popisků dat“.  
- **Je podporován drill‑down?** Ano, pomocí hypertextových odkazů na datové body.  
- **Jaký formát souboru je vytvořen?** Excel sešit (`.xlsx`) s interaktivním grafem.

## Co je přidání tooltipů?

Tooltip je malý vyskakovací okno, které se zobrazí, když uživatel přejeďte myší nad prvek grafu, a ukazuje doplňující informace, jako je přesná hodnota nebo vlastní zpráva. Tooltipy zlepšují čitelnost dat, aniž by zahlcovaly vizuální rozvržení.

## Proč vytvářet interaktivní grafy v Javě?

- **Lepší rozhodování:** Uživatelé mohou okamžitě vidět přesné hodnoty.  
- **Profesionální zprávy:** Interaktivní prvky dodávají dashboardům moderní vzhled.  
- **Znovupoužitelné komponenty:** Jakmile ovládnete API, můžete jej použít v jakémkoli řešení založeném na Excelu.

## Předpoklady

Než začneme, ujistěte se, že máte:

- Vývojové prostředí Java (JDK 8 nebo novější).  
- Knihovnu Aspose.Cells pro Java (stáhněte z [zde](https://releases.aspose.com/cells/java/)).  
- Ukázkový soubor Excel pojmenovaný **data.xlsx** obsahující data, která chcete vizualizovat.

## Krok 1: Nastavení Java projektu

1. Vytvořte nový Java projekt ve svém oblíbeném IDE (IntelliJ IDEA, Eclipse atd.).  
2. Přidejte JAR soubor Aspose.Cells do classpath projektu.

## Krok 2: Načtení dat

Pro vytvoření interaktivního grafu nejprve potřebujete list s daty. Níže uvedený kód načte první list ze souboru **data.xlsx**.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Krok 3: Vytvoření grafu

Nyní přidáme sloupcový graf do listu. Graf bude umístěn v buňkách F6  až K16.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Krok 4: Přidání interaktivity

### 4.1. Jak přidat tooltipy

Následující úryvek povolí tooltipy pro první sérii v grafu. Každý datový bod zobrazí svou hodnotu při přejetí myší.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Přidat popisky dat do grafu

Pokud chcete také viditelné popisky vedle každého sloupce, použijte přístup **add data labels chart** zobrazený níže. Tím splníte sekundární klíčové slovo *add data labels chart*.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. Jak provést drill‑down (implementace drill‑downu)

Drill‑down umožňuje uživatelům kliknout na datový bod a přejít na podrobný pohled (např. webovou stránku). Zde připojujeme hypertextový odkaz k prvnímu bodu série.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

> **Pro tip:** Můžete generovat URL dynamicky na základě hodnoty bodu a vytvořit tak skutečně datově řízený drill‑down.

## Krok 5: Uložení sešitu

Po nastavení grafu uložte sešit. Výsledný soubor obsahuje interaktivní graf připravený k otevření v Excelu.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Časté problémy a řešení

| Problém | Příčina | Řešení |
|---------|----------|--------|
| Tooltipy se nezobrazují | Popisky dat nejsou povoleny | Ujistěte se, že je voláno `setHasDataLabels(true)` před nastavením `ShowValue`. |
| Hyperlink není klikací | Špatný index bodu | Ověřte, že odkazujete na správný bod (`get(0)` je první bod). |
| Graf vypadá špatně umístěný | Nesprávný rozsah buněk | Upravte řádek/sloupec v `add(ChartType.COLUMN, row1, col1, row2, col2)`. |

## Často kladené otázky

**Q: Jak mohu změnit typ grafu?**  
A: Nahraďte `ChartType.COLUMN` jinou hodnotou enumu, například `ChartType.LINE` nebo `ChartType.PIE`, při volání `worksheet.getCharts().add(...)`.

**Q: Mohu přizpůsobit vzhled tooltipů?**  
A: Ano. Použijte vlastnosti formátování objektu `DataLabel` (velikost písma, barva pozadí atd.) k úpravě textu tooltipu.

**Q: Jak zvládnout uživatelské interakce ve webové aplikaci?**  
A: Exportujte sešit do web‑kompatibilního formátu (např. HTML) a použijte JavaScript k zachycení kliknutí na elementy grafu.

**Q: Kde najdu více příkladů a dokumentaci?**  
A: Prozkoumejte oficiální referenci API na [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/).

**Q: Je možné přidat více drill‑down odkazů do stejného grafu?**  
A: Rozhodně. Projděte body série a přiřaďte unikátní URL každému bodu v kolekci `Hyperlinks`.

## Závěr

V tomto průvodci jste se naučili **jak přidat tooltipy**, **přidat popisky dat** a **implementovat drill‑down** funkčnost pro vytvoření **create interactive chart java** řešení pomocí Aspose.Cells. Tyto funkce promění statické Excel grafy na dynamické, uživatelsky přívětivé vizualizace, které pomáhají zainteresovaným stranám snadno prozkoumávat data.

---

**Poslední aktualizace:** 2025-11-28  
**Testováno s:** Aspose.Cells pro Java 24.12  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}