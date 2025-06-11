---
"description": "Využijte sílu Aspose.Cells pro .NET a snadno upravujte koláčové grafy v Excelu. Postupujte podle tohoto návodu, který vás krok za krokem povede."
"linktitle": "Upravit koláčový graf"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Upravit koláčový graf"
"url": "/cs/net/manipulating-chart-types/modify-pie-chart/"
"weight": 16
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Upravit koláčový graf

## Zavedení

Přemýšleli jste někdy, jak vylepšit koláčové grafy ve vašich excelových tabulkách? Koláčové grafy mohou být fantastickým způsobem, jak vizualizovat data a udržet vaše publikum zaujaté a informované. Někdy však tyto grafy hned po vybalení z krabice nevyprávějí příběh, který byste chtěli. A právě zde přichází na řadu Aspose.Cells pro .NET. Tato výkonná knihovna umožňuje programově manipulovat s excelovými soubory a poskytuje vám nástroje, které potřebujete k přizpůsobení koláčových grafů do nejmenších detailů. V tomto tutoriálu se podrobně ponoříme do úprav koláčového grafu pomocí Aspose.Cells. Ať už jde o změnu popisků dat nebo úpravu vzhledu grafu.

## Předpoklady

Než se ponoříme do detailů úprav koláčových grafů, měli byste splnit několik předpokladů:

- Základní znalost C#: Základní znalost programování v C# vám pomůže snadno se orientovat.
- Aspose.Cells pro .NET: Budete muset mít nainstalovanou knihovnu Aspose.Cells. Ať už se rozhodnete používat plnou verzi, nebo si zvolíte bezplatnou zkušební verzi, ujistěte se, že je připravena k použití.
- Visual Studio nebo jakékoli C# IDE: Budete potřebovat prostředí pro psaní a spouštění kódu C#.
- Ukázkový soubor Excelu: Pro tento tutoriál je použit ukázkový soubor Excelu s názvem `sampleModifyPieChart.xlsx` bude použito.

Můžete si stáhnout knihovnu Aspose.Cells [zde](https://releases.aspose.com/cells/net/).

## Importovat balíčky

Prvním krokem na naší cestě je import potřebných balíčků do našeho projektu v C#. Zde je návod, jak to udělat:

## Nastavení projektu

Chcete-li začít, otevřete si C# IDE (důrazně doporučujeme Visual Studio) a vytvořte nový projekt:

1. Otevřete Visual Studio.
2. Vyberte možnost „Vytvořit nový projekt“.
3. Vyberte konzolovou aplikaci v C#.
4. Pojmenujte svůj projekt (např. `ModifyPieChartDemo`).
5. Klikněte na Vytvořit.

## Instalace Aspose.Cells

Jakmile je váš projekt připravený, je čas přidat knihovnu Aspose.Cells. Můžete ji nainstalovat pomocí NuGetu:

1. „Průzkumníku řešení“ klikněte pravým tlačítkem myši na váš projekt.
2. Vyberte Spravovat balíčky NuGet.
3. Přejděte na kartu Procházet.
4. Hledat Aspose.Cells.
5. Klikněte na tlačítko Instalovat a přijměte veškeré licenční podmínky.

Nyní, když máte knihovnu nainstalovanou, importujme potřebné jmenné prostory do vašeho kódu.

## Import jmenných prostorů

Na vrcholu tvého `Program.cs` soubor, importujte následující jmenné prostory:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

Jakmile to máme hotové, můžeme se pustit do samotného kódu!

## Krok 1: Definování vstupních a výstupních adresářů

Začněme definováním adresářů pro vstupní a výstupní soubory. Zde určíte, kde se nachází váš soubor Excel a kam chcete uložit upravený soubor.

Ve vašem `Main` metodu, zadejte následující kód:

```csharp
// Výstupní adresář
string outputDir = "Your Output Directory Path";

// Zdrojový adresář
string sourceDir = "Your Document Directory Path";
```

Nezapomeňte vyměnit `Your Output Directory Path` a `Your Document Directory Path` se skutečnými cestami ve vašem systému.

## Krok 2: Otevření existujícího sešitu

Dále musíme otevřít soubor aplikace Excel, který obsahuje koláčový graf, který chcete upravit. K tomu použijte `Workbook` třída:

```csharp
// Otevřete existující soubor.
Workbook workbook = new Workbook(sourceDir + "sampleModifyPieChart.xlsx");
```

V tomto úryvku vytváříme nový `Workbook` objekt a načtení našeho souboru Excel do něj.

## Krok 3: Přístup k pracovnímu listu

Nyní se ponořme do konkrétního listu, který obsahuje koláčový graf. Budeme předpokládat, že koláčový graf je na druhém listu (index 1):

```csharp
// Získejte návrhářský graf na druhém listu.
Worksheet sheet = workbook.Worksheets[1];
```

Přístupem k `Worksheets` kolekce, můžeme se dostat ke konkrétnímu listu, který potřebujeme.

## Krok 4: Získejte graf

Nyní jsme připraveni získat přístup k samotnému grafu. Za předpokladu, že na daném listu je pouze jeden graf, můžeme ho načíst přímo:

```csharp
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

Zde načítáme první graf ze zadaného listu.

## Krok 5: Přístup k popiskům dat

Nyní přichází ta vzrušující část – úprava popisků dat v koláčovém grafu. Pojďme se podívat na popisky datových řad:

```csharp
// Získejte popisky dat v datové řadě třetího datového bodu.
Aspose.Cells.Charts.DataLabels datalabels = chart.NSeries[0].Points[2].DataLabels;
```

Touto čárou cílíme na datové popisky konkrétně pro třetí bod naší datové řady. 

## Krok 6: Úprava textu štítku

Dále je čas změnit, co tento popisek říká. V našem příkladu jej aktualizujeme na „Spojené království, 400 tisíc“:

```csharp
// Změňte text štítku.
datalabels.Text = "United Kingdom, 400K";
```

Prostě jsme aktualizovali štítek! 

## Krok 7: Uložení sešitu

Nyní, když jsme provedli změny, uložme upravený sešit. 

```csharp
// Uložte soubor Excelu.
workbook.Save(outputDir + "outputModifyPieChart.xlsx");
```

Tento řádek uloží sešit do zadaného výstupního adresáře. 

## Krok 8: Potvrzení provedení

Nakonec vypíšeme potvrzovací zprávu, abychom se ujistili, že vše proběhlo hladce:

```csharp
Console.WriteLine("ModifyPieChart executed successfully.");
```

To vám dává trochu jistoty, že vaše změny byly provedeny podle očekávání.

# Závěr

je to! Pomocí několika jednoduchých kroků jste úspěšně upravili koláčový graf pomocí knihovny Aspose.Cells pro .NET. Tato výkonná knihovna nejen usnadňuje manipulaci s excelovými soubory, ale také umožňuje přizpůsobit vizualizace dat pro maximální efekt. Pokud ve své práci pracujete s prezentací dat, investice do učení se používání Aspose.Cells se vám určitě vyplatí. Tak si s těmito grafy pohrajte a zjistěte, jak můžete svým datům vdechnout život!

# Často kladené otázky

### Co je Aspose.Cells pro .NET?  
Aspose.Cells pro .NET je výkonná knihovna určená k programovému vytváření, manipulaci a převodu souborů aplikace Excel bez nutnosti použití aplikace Microsoft Excel.

### Mohu upravovat i jiné grafy než koláčové grafy?  
Rozhodně! Aspose.Cells podporuje různé typy grafů, včetně sloupcových, spojnicových a plošných grafů, což umožňuje flexibilní vizualizaci dat.

### Existuje bezplatná verze Aspose.Cells?  
Ano! Aspose nabízí bezplatnou zkušební verzi, která vám umožní si knihovnu před zakoupením vyzkoušet.

### Kde najdu podporu pro Aspose.Cells?  
Podporu najdete na fórech Aspose, kde vám mohou pomoci členové komunity a zaměstnanci Aspose.

### Musím mít nainstalovaný Microsoft Excel, abych mohl používat Aspose.Cells?  
Ne, Aspose.Cells funguje nezávisle na Microsoft Excelu. Nemusíte ho mít nainstalovaný ve svém systému.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}