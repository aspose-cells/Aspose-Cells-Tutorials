---
"description": "Naučte se, jak změnit hlavní mřížku v grafech aplikace Excel pomocí Aspose.Cells pro .NET s naším podrobným návodem krok za krokem."
"linktitle": "Změna hlavních mřížkových čar v grafu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Změna hlavních mřížkových čar v grafu"
"url": "/cs/net/setting-chart-appearance/change-major-gridlines-in-chart/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Změna hlavních mřížkových čar v grafu

## Zavedení

Vytváření vizuálně poutavých grafů v Excelu je nezbytné pro efektivní prezentaci dat. Ať už jste datový analytik, projektový manažer nebo se jen zajímáte o vizualizaci dat, pochopení toho, jak grafy přizpůsobit, může výrazně vylepšit vaše sestavy. V tomto článku se naučíme, jak změnit hlavní mřížku v grafu v Excelu pomocí knihovny Aspose.Cells pro .NET.

## Předpoklady

Než začneme, je třeba mít na paměti několik věcí, které vám zajistí bezproblémový chod práce s Aspose.Cells:

- Visual Studio: Ujistěte se, že máte v počítači nainstalované Visual Studio. Zde budete psát a spouštět svůj kód.
- Aspose.Cells pro .NET: Nejnovější verzi Aspose.Cells si můžete stáhnout z [webové stránky](https://releases.aspose.com/cells/net/)Pokud si chcete před koupí něco vyzkoušet, můžete zvážit registraci do [bezplatná zkušební verze](https://releases.aspose.com/).
- Základní znalost C#: Znalost programování v C# vám usnadní sledování příkladů v tomto tutoriálu.

Jakmile máme vše nastavené, můžeme začít psát náš kód!

## Importovat balíčky

Pro práci s Aspose.Cells je prvním krokem import potřebných balíčků do vašeho projektu v jazyce C#. Otevřete projekt ve Visual Studiu a na začátek souboru v jazyce C# přidejte následující pomocí direktiv:

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

Tyto balíčky vám umožňují přístup ke třídám a metodám, které budete potřebovat pro vytváření a úpravy sešitů a grafů aplikace Excel.

Nyní si celý proces rozdělme na podrobné a snadno sledovatelné kroky. Vytvoříme jednoduchý graf s nějakými daty a poté změníme barvu jeho hlavních mřížkových čar.

## Krok 1: Nastavení výstupního adresáře

První věc, kterou budete chtít udělat, je definovat, kam chcete uložit výstupní soubor Excel. To se provede zadáním cesty k adresáři v kódu:

```csharp
// Výstupní adresář
string outputDir = "Your Output Directory"; // Aktualizujte požadovanou cestou
```

Nahradit `"Your Output Directory"` se skutečnou cestou, kam chcete soubor uložit.

## Krok 2: Vytvoření instance objektu Workbook

Dále je třeba vytvořit novou instanci `Workbook` třída. Tento objekt bude reprezentovat váš soubor aplikace Excel a umožní vám manipulovat s jeho obsahem.

```csharp
// Vytvoření instance objektu Workbook
Workbook workbook = new Workbook();
```

Tento řádek kódu inicializuje nový sešit, který poskytne prázdné plátno pro náš list a graf.

## Krok 3: Přístup k pracovnímu listu

Po vytvoření sešitu máte přístup k jeho výchozímu listu. Listy v Aspose.Cells jsou indexované, takže pokud chcete první list, odkazujete na něj pomocí indexu. `0`.

```csharp
// Získání odkazu na nově přidaný list předáním jeho indexu listu
Worksheet worksheet = workbook.Worksheets[0];
```

## Krok 4: Naplnění pracovního listu vzorovými daty

Přidejme do buněk listu několik vzorových hodnot, které budou sloužit jako data pro náš graf. To je důležité, protože graf bude na tato data odkazovat.

```csharp
// Přidávání vzorových hodnot do buněk
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(60);
worksheet.Cells["B2"].PutValue(32);
worksheet.Cells["B3"].PutValue(50);
```

Zde zadáme několik číselných hodnot do konkrétních buněk. Sloupce „A“ a „B“ obsahují datové body, které budeme vizualizovat.

## Krok 5: Přidání grafu do pracovního listu

S daty na místě je čas vytvořit graf. Přidáme sloupcový graf, který vizualizuje naši datovou sadu.

```csharp
// Přidání grafu do listu
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Column, 5, 0, 25, 10);
```

V tomto kódu určujeme typ grafu (v tomto případě sloupcový graf) a pozici, kam ho chceme umístit.

## Krok 6: Přístup k instanci grafu

Jakmile vytvoříme graf, musíme přistupovat k jeho instanci, abychom mohli upravit jeho vlastnosti. To se provádí načtením pomocí `Charts` sbírka.

```csharp
// Přístup k instanci nově přidaného grafu
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

## Krok 7: Přidání datové řady do grafu

Nyní musíme propojit naše data s grafem. To zahrnuje určení buněk jako zdroje dat pro graf.

```csharp
// Přidání SeriesCollection (zdroj dat grafu) do grafu v rozsahu od buňky „A1“ do buňky „B3“
chart.NSeries.Add("A1:B3", true);
```

V tomto kroku informujeme graf o rozsahu dat, která má vizualizovat.

## Krok 8: Přizpůsobení vzhledu grafu

Trochu vylepšeme náš graf změnou barev oblasti vykreslování, oblasti grafu a kolekcí sérií. To pomůže našemu grafu vyniknout a zlepší jeho vizuální atraktivitu.

```csharp
// Nastavení barvy popředí oblasti grafu
chart.PlotArea.Area.ForegroundColor = Color.Blue;

// Nastavení barvy popředí oblasti grafu
chart.ChartArea.Area.ForegroundColor = Color.Yellow;

// Nastavení barvy popředí pro oblast 1. kolekce SeriesCollection
chart.NSeries[0].Area.ForegroundColor = Color.Red;

// Nastavení barvy popředí oblasti 1. sběrného bodu série
chart.NSeries[0].Points[0].Area.ForegroundColor = Color.Cyan;

// Vyplnění oblasti kolekce 2. série přechodem
chart.NSeries[1].Area.FillFormat.SetOneColorGradient(Color.Lime, 1, Aspose.Cells.Drawing.GradientStyleType.Horizontal, 1);
```

V tomto kódu nastavujeme různé barvy pro různé části grafu. Úpravy vzhledu mohou vaše data učinit mnohem poutavějšími!

## Krok 9: Změna hlavních barev mřížky

A teď k hlavní události! Pro lepší čitelnost změníme barvu hlavních čar mřížky podél obou os našeho grafu.

```csharp
// Nastavení barvy hlavních mřížkových čar osy kategorií na stříbrnou
chart.CategoryAxis.MajorGridLines.Color = Color.Silver;

// Nastavení barvy hlavních mřížkových čar osy hodnot na červenou
chart.ValueAxis.MajorGridLines.Color = Color.Red;
```

Tyto příkazy nastaví hlavní čáry mřížky pro osy kategorií a hodnot na stříbrnou, respektive červenou. Toto rozlišení zajišťuje, že diváci mohou snadno sledovat čáry mřížky v grafu.

## Krok 10: Uložení sešitu

Po provedení všech úprav je čas sešit uložit. Toto je poslední krok, který dovede vaši snahu k naplnění.

```csharp
// Uložení souboru aplikace Excel
workbook.Save(outputDir + "outputChangingMajorGridlinesInChart.xlsx");
```

Tento řádek uloží nově vytvořený soubor aplikace Excel do zadaného výstupního adresáře s názvem, který odpovídá jeho účelu.

## Krok 11: Potvrzovací zpráva

Nakonec přidejme zprávu potvrzující, že náš úkol byl úspěšný:

```csharp
Console.WriteLine("Changing Major Gridlines in Chart executed successfully.");
```

Tento jednoduchý výstup z konzole vás informuje, že váš program proběhl správně a bez jakýchkoli zádrhelů.

## Závěr

A tady to máte! Úspěšně jste se naučili, jak změnit hlavní mřížku v grafu pomocí Aspose.Cells pro .NET. Dodržováním tohoto podrobného návodu jste nejen programově upravili soubory aplikace Excel, ale také vylepšili jejich vizuální atraktivitu pomocí barevných úprav. Nebojte se s Aspose.Cells dále experimentovat, abyste prohloubili své dovednosti v prezentaci dat a učinili své grafy ještě dynamičtějšími!

## Často kladené otázky

### Co je Aspose.Cells?  
Aspose.Cells je knihovna .NET určená pro programově vytvářet, manipulovat a spravovat soubory aplikace Excel.

### Mohu si Aspose.Cells vyzkoušet zdarma?  
Ano, můžete se zaregistrovat na bezplatnou zkušební verzi [zde](https://releases.aspose.com/).

### Jak mohu změnit další prvky v grafu pomocí Aspose.Cells?  
Různé vlastnosti grafu můžete přizpůsobit podobným způsobem, a to přístupem k prvkům grafu prostřednictvím `Chart` třídy, jako jsou názvy, legendy a popisky dat.

### Jaké formáty souborů podporuje Aspose.Cells?  
Aspose.Cells podporuje více formátů souborů, včetně XLSX, XLS, CSV a dalších.

### Kde najdu dokumentaci k Aspose.Cells?  
Podrobnou dokumentaci si můžete prohlédnout na adrese [Dokumentace k Aspose.Cells](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}