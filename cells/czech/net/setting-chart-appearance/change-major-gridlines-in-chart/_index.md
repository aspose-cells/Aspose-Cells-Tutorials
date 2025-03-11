---
title: Změňte hlavní mřížku v grafu
linktitle: Změňte hlavní mřížku v grafu
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak změnit hlavní mřížky v grafech aplikace Excel pomocí Aspose.Cells for .NET s naším podrobným průvodcem krok za krokem.
weight: 11
url: /cs/net/setting-chart-appearance/change-major-gridlines-in-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Změňte hlavní mřížku v grafu

## Zavedení

Vytváření vizuálně atraktivních grafů v Excelu je nezbytné pro efektivní prezentaci dat. Ať už jste datový analytik, projektový manažer nebo jen někdo, kdo se zajímá o vizualizaci dat, pochopení toho, jak přizpůsobit grafy, může výrazně zlepšit vaše sestavy. V tomto článku se naučíme, jak změnit hlavní čáry mřížky v grafu Excel pomocí knihovny Aspose.Cells pro .NET.

## Předpoklady

Než začneme, je zde několik věcí, které musíte mít na místě, abyste zajistili hladký průběh práce s Aspose.Cells:

- Visual Studio: Ujistěte se, že máte v počítači nainstalované Visual Studio. Zde budete psát a provádět svůj kód.
-  Aspose.Cells pro .NET: Nejnovější verzi Aspose.Cells si můžete stáhnout z[webové stránky](https://releases.aspose.com/cells/net/) . Pokud chcete před nákupem experimentovat, můžete zvážit registraci do a[zkušební verze zdarma](https://releases.aspose.com/).
- Základní znalost C#: Znalost programování v C# vám usnadní sledování spolu s příklady v tomto tutoriálu.

Jakmile budete mít vše nastaveno, můžeme začít psát náš kód!

## Importujte balíčky

Chcete-li pracovat s Aspose.Cells, prvním krokem je importovat potřebné balíčky do vašeho projektu C#. Otevřete projekt Visual Studio a zahrňte následující pomocí direktiv v horní části souboru C#:

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

Tyto balíčky umožňují přístup ke třídám a metodám, které budete potřebovat pro vytváření a úpravy sešitů a grafů aplikace Excel.

Nyní si tento proces rozdělíme do podrobných a snadno pochopitelných kroků. Vytvoříme jednoduchý graf s některými daty a poté změníme barvu jeho hlavních mřížek.

## Krok 1: Nastavte svůj výstupní adresář

První věc, kterou budete chtít udělat, je definovat, kam chcete uložit výstupní soubor Excel. To se provádí zadáním cesty k adresáři ve vašem kódu:

```csharp
// Výstupní adresář
string outputDir = "Your Output Directory"; // Aktualizujte požadovanou cestu
```

 Nahradit`"Your Output Directory"` se skutečnou cestou, kam chcete soubor uložit.

## Krok 2: Vytvořte instanci objektu sešitu

 Dále musíte vytvořit novou instanci souboru`Workbook` třída. Tento objekt bude reprezentovat váš soubor Excel a umožní vám manipulovat s jeho obsahem.

```csharp
// Vytvoření instance objektu sešitu
Workbook workbook = new Workbook();
```

Tento řádek kódu inicializuje nový sešit, který poskytne prázdné plátno pro náš list a graf.

## Krok 3: Otevřete sešit

 Po vytvoření sešitu získáte přístup k jeho výchozímu listu. Listy v Aspose.Cells jsou indexovány, takže pokud chcete první list, odkazujete na něj podle indexu`0`.

```csharp
// Získání odkazu na nově přidaný list předáním jeho indexu listu
Worksheet worksheet = workbook.Worksheets[0];
```

## Krok 4: Vyplňte pracovní list ukázkovými daty

Do buněk listu přidáme několik vzorových hodnot, které budou sloužit jako data pro náš graf. To je důležité, protože graf bude na tato data odkazovat.

```csharp
// Přidání vzorových hodnot do buněk
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(60);
worksheet.Cells["B2"].PutValue(32);
worksheet.Cells["B3"].PutValue(50);
```

Zde zadáváme několik číselných hodnot do konkrétních buněk. Sloupce "A" a "B" obsahují datové body, které budeme vizualizovat.

## Krok 5: Přidejte graf do listu

S našimi daty na místě je čas vytvořit graf. Přidáme sloupcový graf, který vizualizuje naši datovou sadu.

```csharp
// Přidání grafu do listu
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Column, 5, 0, 25, 10);
```

V tomto kódu určíme typ grafu (v tomto případě sloupcový graf) a pozici, kam jej chceme umístit.

## Krok 6: Přístup k instanci grafu

 Jakmile vytvoříme graf, potřebujeme získat přístup k jeho instanci, abychom mohli upravit jeho vlastnosti. To se provádí načtením přes`Charts`sbírka.

```csharp
// Přístup k instanci nově přidaného grafu
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

## Krok 7: Přidejte datové řady do grafu

Nyní musíme svá data svázat s grafem. To zahrnuje určení buněk jako zdroje dat pro graf.

```csharp
// Přidání SeriesCollection (zdroj dat grafu) do grafu v rozsahu od buňky "A1" po "B3"
chart.NSeries.Add("A1:B3", true);
```

V tomto kroku informujeme graf o rozsahu dat, který má vizualizovat.

## Krok 8: Přizpůsobte vzhled grafu

Pojďme náš graf trochu vylepšit změnou barev oblasti grafu, oblasti grafu a sbírek sérií. To pomůže našemu grafu vyniknout a zlepšit jeho vizuální přitažlivost.

```csharp
// Nastavení barvy popředí oblasti vykreslování
chart.PlotArea.Area.ForegroundColor = Color.Blue;

// Nastavení barvy popředí oblasti grafu
chart.ChartArea.Area.ForegroundColor = Color.Yellow;

// Nastavení barvy popředí oblasti kolekce 1. série
chart.NSeries[0].Area.ForegroundColor = Color.Red;

// Nastavení barvy popředí oblasti bodu kolekce 1. série
chart.NSeries[0].Points[0].Area.ForegroundColor = Color.Cyan;

// Vyplnění oblasti kolekce 2. série přechodem
chart.NSeries[1].Area.FillFormat.SetOneColorGradient(Color.Lime, 1, Aspose.Cells.Drawing.GradientStyleType.Horizontal, 1);
```

V tomto kódu nastavujeme různé barvy pro různé části grafu. Přizpůsobením vzhledu mohou být vaše data mnohem poutavější!

## Krok 9: Změňte barvy hlavní mřížky

Nyní k hlavní události! Pro zlepšení čitelnosti změníme barvu hlavních čar mřížky podél obou os našeho grafu.

```csharp
// Nastavení barvy hlavní mřížky osy kategorie na stříbrnou
chart.CategoryAxis.MajorGridLines.Color = Color.Silver;

// Nastavení barvy hlavních mřížek osy hodnot na červenou
chart.ValueAxis.MajorGridLines.Color = Color.Red;
```

Tyto příkazy nastavují hlavní mřížku pro osu kategorií a hodnot na stříbrnou a červenou. Toto rozlišení zajišťuje, že vaši diváci mohou snadno sledovat mřížku napříč grafem.

## Krok 10: Uložte sešit

Po provedení všech úprav je čas sešit uložit. Toto je poslední krok, který přivede vaše úsilí k uskutečnění.

```csharp
// Uložení souboru Excel
workbook.Save(outputDir + "outputChangingMajorGridlinesInChart.xlsx");
```

Tento řádek uloží váš nově vytvořený soubor Excel do určeného výstupního adresáře s názvem, který odráží jeho účel.

## Krok 11: Potvrzující zpráva

Nakonec přidáme zprávu pro potvrzení, že náš úkol byl úspěšný:

```csharp
Console.WriteLine("Changing Major Gridlines in Chart executed successfully.");
```

Tento jednoduchý výstup z konzoly vás informuje, že váš program běžel správně bez jakýchkoliv problémů.

## Závěr

tady to máte! Úspěšně jste se naučili, jak změnit hlavní čáry mřížky v grafu pomocí Aspose.Cells for .NET. Podle tohoto podrobného průvodce jste nejen programově manipulovali se soubory Excelu, ale také zlepšili jejich vizuální přitažlivost pomocí přizpůsobení barev. Nebojte se dále experimentovat s Aspose.Cells, abyste prohloubili své dovednosti prezentace dat a udělejte své grafy ještě dynamičtějšími!

## FAQ

### Co je Aspose.Cells?  
Aspose.Cells je .NET knihovna určená pro vytváření, manipulaci a správu souborů aplikace Excel programově.

### Mohu vyzkoušet Aspose.Cells zdarma?  
 Ano, můžete se přihlásit k bezplatné zkušební verzi[zde](https://releases.aspose.com/).

### Jak mohu změnit další prvky v grafu pomocí Aspose.Cells?  
 Různé vlastnosti grafu můžete upravit podobně přístupem k prvkům grafu prostřednictvím`Chart` třídy, jako jsou názvy, legendy a štítky dat.

### Jaké formáty souborů Aspose.Cells podporuje?  
Aspose.Cells podporuje více formátů souborů, včetně XLSX, XLS, CSV a dalších.

### Kde najdu dokumentaci pro Aspose.Cells?  
 Podrobnou dokumentaci naleznete na adrese[Dokumentace Aspose.Cells](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
