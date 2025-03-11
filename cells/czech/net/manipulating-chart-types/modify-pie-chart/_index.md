---
title: Upravit výsečový graf
linktitle: Upravit výsečový graf
second_title: Aspose.Cells .NET Excel Processing API
description: Odemkněte sílu Aspose.Cells pro .NET a bez námahy upravujte své výsečové grafy Excel. Postupujte podle tohoto návodu, kde najdete podrobné pokyny.
weight: 16
url: /cs/net/manipulating-chart-types/modify-pie-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Upravit výsečový graf

## Zavedení

Přemýšleli jste někdy, jak byste mohli vylepšit tyto koláčové grafy v listech Excelu? Koláčové grafy mohou být fantastickým způsobem, jak vizualizovat data, udržet vaše publikum zapojené a informované. Někdy však tyto grafy nevyprávějí příběh, který chcete, aby vyprávěly hned po vybalení. To je místo, kde Aspose.Cells for .NET přichází do hry. Tato výkonná knihovna vám umožňuje programově manipulovat se soubory aplikace Excel a poskytuje vám nástroje, které potřebujete k přizpůsobení výsečových grafů do nejmenších detailů. V tomto tutoriálu se hluboce ponoříme do úpravy koláčového grafu pomocí Aspose.Cells. Ať už jde o změnu štítků dat nebo úpravu estetiky grafu.

## Předpoklady

Než se vrhneme na to, co je při úpravách koláčových grafů složité, měli byste mít splněno několik předpokladů:

- Základní znalost C#: Základní znalost programování v C# vám pomůže snadno sledovat.
- Aspose.Cells for .NET: Budete muset mít nainstalovanou knihovnu Aspose.Cells. Ať už se rozhodnete používat plnou verzi nebo se rozhodnete pro bezplatnou zkušební verzi, ujistěte se, že je připravena k použití.
- Visual Studio nebo libovolné C# IDE: Pro psaní a spouštění kódu C# budete potřebovat prostředí.
-  Ukázkový soubor aplikace Excel: Pro tento výukový program je ukázkový soubor aplikace Excel s názvem`sampleModifyPieChart.xlsx` budou použity.

 Můžete si stáhnout knihovnu Aspose.Cells[zde](https://releases.aspose.com/cells/net/).

## Importujte balíčky

Prvním krokem na naší cestě je import potřebných balíčků do našeho projektu C#. Můžete to udělat takto:

## Nastavte svůj projekt

Chcete-li začít, otevřete své IDE C# (důrazně doporučujeme Visual Studio) a vytvořte nový projekt:

1. Otevřete Visual Studio.
2. Vyberte „Vytvořit nový projekt“.
3. Vyberte konzolovou aplikaci C#.
4.  Pojmenujte svůj projekt (např.`ModifyPieChartDemo`).
5. Klikněte na Vytvořit.

## Nainstalujte Aspose.Cells

Jakmile je váš projekt připraven, je čas přidat knihovnu Aspose.Cells. Můžete jej nainstalovat pomocí NuGet:

1. V "Solution Explorer" klikněte pravým tlačítkem na svůj projekt.
2. Vyberte Spravovat balíčky NuGet.
3. Přejděte na kartu Procházet.
4. Vyhledejte Aspose.Cells.
5. Klikněte na Instalovat a přijměte všechny licenční smlouvy.

Nyní, když máte nainstalovanou knihovnu, pojďme importovat potřebné jmenné prostory do vašeho kódu.

## Import jmenných prostorů

 V horní části vašeho`Program.cs` importujte následující jmenné prostory:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

Po dokončení jsme nyní připraveni přejít ke skutečnému kódu!

## Krok 1: Definujte vstupní a výstupní adresáře

Začněme definováním adresářů pro vaše vstupní a výstupní soubory. Zde určíte, kde se váš soubor Excel nachází a kam chcete upravený soubor uložit.

 Ve vašem`Main` metoda, zadejte následující kód:

```csharp
// Výstupní adresář
string outputDir = "Your Output Directory Path";

// Zdrojový adresář
string sourceDir = "Your Document Directory Path";
```

 Nezapomeňte vyměnit`Your Output Directory Path` a`Your Document Directory Path` se skutečnými cestami ve vašem systému.

## Krok 2: Otevřete existující sešit

 Dále musíme otevřít soubor aplikace Excel, který obsahuje koláčový graf, který chcete upravit. K tomu použijte`Workbook` třída:

```csharp
// Otevřete existující soubor.
Workbook workbook = new Workbook(sourceDir + "sampleModifyPieChart.xlsx");
```

 V tomto úryvku vytváříme nový`Workbook` objekt a načteme do něj náš soubor Excel.

## Krok 3: Otevřete sešit

Nyní se pojďme ponořit do konkrétního listu, který obsahuje výsečový graf. Budeme předpokládat, že výsečový graf je na druhém listu (index 1):

```csharp
// Získejte graf návrháře na druhém listu.
Worksheet sheet = workbook.Worksheets[1];
```

 Přístupem k`Worksheets` kolekce, můžeme se dostat ke konkrétnímu listu, který potřebujeme.

## Krok 4: Získejte graf

Nyní jsme připraveni získat přístup k samotnému grafu. Za předpokladu, že na tomto listu je pouze jeden graf, můžeme jej načíst přímo:

```csharp
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

Zde bereme první graf ze zadaného listu.

## Krok 5: Přístup k štítkům dat

Nyní přichází ta vzrušující část – úprava štítků dat na výsečovém grafu. Pojďme k datovým štítkům datových řad:

```csharp
// Získejte štítky dat v datové řadě třetího datového bodu.
Aspose.Cells.Charts.DataLabels datalabels = chart.NSeries[0].Points[2].DataLabels;
```

Tímto řádkem cílíme na štítky dat konkrétně pro třetí bod naší datové řady. 

## Krok 6: Upravte text štítku

Dále je čas změnit to, co tento štítek říká. V našem příkladu jej aktualizujeme na „United Kingdom, 400K“:

```csharp
// Změňte text štítku.
datalabels.Text = "United Kingdom, 400K";
```

Právě tak jsme aktualizovali štítek! 

## Krok 7: Uložte sešit

Nyní, když jsme provedli změny, uložme upravený sešit. 

```csharp
// Uložte soubor aplikace Excel.
workbook.Save(outputDir + "outputModifyPieChart.xlsx");
```

Tento řádek uloží sešit do zadaného výstupního adresáře. 

## Krok 8: Potvrďte provedení

Nakonec vydejme potvrzovací zprávu, abychom zajistili, že vše proběhne hladce:

```csharp
Console.WriteLine("ModifyPieChart executed successfully.");
```

To vám dává trochu jistoty, že vaše změny byly provedeny podle očekávání.

# Závěr

Tady to máš! Pomocí několika jednoduchých kroků jste úspěšně upravili výsečový graf pomocí Aspose.Cells for .NET. Tato výkonná knihovna nejen usnadňuje manipulaci se soubory aplikace Excel, ale také umožňuje personalizovat vizualizace dat pro maximální dopad. Pokud ve své práci řešíte prezentaci dat, investovat čas do učení se Aspose.Cells se určitě vyplatí. Takže pokračujte, pohrajte si s těmito grafy a uvidíte, jak můžete svá data oživit!

# FAQ

### Co je Aspose.Cells pro .NET?  
Aspose.Cells for .NET je výkonná knihovna navržená pro vytváření, manipulaci a převod souborů aplikace Excel programově bez potřeby aplikace Microsoft Excel.

### Mohu upravit grafy jiné než výsečové?  
Absolutně! Aspose.Cells podporuje různé typy grafů, včetně pruhových, spojnicových a plošných grafů, což umožňuje flexibilní vizualizaci dat.

### Existuje bezplatná verze Aspose.Cells?  
Ano! Aspose nabízí bezplatnou zkušební verzi, která vám umožní otestovat knihovnu před jejím zakoupením.

### Kde najdu podporu pro Aspose.Cells?  
Podporu můžete najít na fórech Aspose, kde vám mohou pomoci členové komunity a zaměstnanci Aspose.

### Musím mít nainstalovaný Microsoft Excel, abych mohl používat Aspose.Cells?  
Ne, Aspose.Cells funguje nezávisle na aplikaci Microsoft Excel. Nemusíte jej mít nainstalovaný v systému.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
