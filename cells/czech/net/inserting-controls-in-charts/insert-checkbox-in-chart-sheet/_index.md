---
title: Vložit zaškrtávací políčko do listu s grafem
linktitle: Vložit zaškrtávací políčko do listu s grafem
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak snadno vložit zaškrtávací políčko do listu s grafem aplikace Excel pomocí Aspose.Cells for .NET pomocí tohoto podrobného návodu.
weight: 13
url: /cs/net/inserting-controls-in-charts/insert-checkbox-in-chart-sheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vložit zaškrtávací políčko do listu s grafem

## Zavedení

Pokud jste někdy vytvořili graf v Excelu, víte, že mohou být neuvěřitelně výkonné pro vizualizaci dat. Ale co kdybyste mohli tuto interaktivitu ještě více vylepšit přidáním zaškrtávacího políčka přímo do grafu? I když to může znít trochu nuance, ve skutečnosti je to s knihovnou Aspose.Cells pro .NET docela jednoduché. V tomto tutoriálu vás provedu procesem krok za krokem, aby byl jednoduchý a snadno sledovatelný.

## Předpoklady

Než se pustíte do výukového programu, ujistěte se, že máte vše nastaveno. Zde je to, co potřebujete:

### Visual Studio nainstalováno
- první řadě budete potřebovat Visual Studio. Pokud jej ještě nemáte nainstalovaný, můžete si jej stáhnout ze stránek společnosti Microsoft.

### Knihovna Aspose.Cells
-  Dalším nezbytným nástrojem je knihovna Aspose.Cells pro .NET. Můžete to snadno získat z[Aspose webové stránky](https://releases.aspose.com/cells/net/) ke stažení. Pokud dáváte přednost testování před nákupem, je zde také a[bezplatná zkušební verze k dispozici](https://releases.aspose.com/).

### Základní porozumění C#
- Vzhledem k tomu, že budeme psát nějaký kód, bude užitečné základní porozumění C#. Nebojte se; Vysvětlím věci za pochodu!

### Výstupní adresář
- Budete potřebovat adresář, kam budou uloženy vaše výstupní soubory Excel. Ujistěte se, že to máte po ruce.

S těmito předpoklady zaškrtnutými ve vašem seznamu jsme připraveni skočit do akce!

## Importujte balíčky

Chcete-li začít, nastavte náš projekt ve Visual Studiu a importujte potřebné balíčky. Zde je jednoduchý průvodce krok za krokem:

### SVytvořte nový projekt

Otevřete Visual Studio a vytvořte nový projekt aplikace konzoly. Postupujte podle těchto jednoduchých kroků:
- Klikněte na „Vytvořit nový projekt“.
- možností vyberte „Console App (.NET Framework)“.
- Svůj projekt pojmenujte jako „CheckboxInChart“.

### Nainstalujte Aspose.Cells přes NuGet

Jakmile je váš projekt nastaven, je čas přidat knihovnu Aspose.Cells. Můžete to udělat prostřednictvím Správce balíčků NuGet:
- Klikněte pravým tlačítkem na svůj projekt v Průzkumníku řešení a vyberte „Spravovat balíčky NuGet“.
- Vyhledejte „Aspose.Cells“ a klikněte na „Instalovat“.
- Tím se zavedou všechny potřebné závislosti, což usnadní zahájení používání knihovny.

### Přidejte potřebné direktivy pomocí

 V horní části vašeho`Program.cs` přidejte následující pomocí direktiv, abyste zpřístupnili funkce Aspose.Cells:
```csharp
using Aspose.Cells.Charts;
using System;
using Aspose.Cells.Drawing;
```

Nyní jste dokončili nastavení! Je to jako položení pevných základů před stavbou domu – zásadní pro stabilní konstrukci.

Nyní, když jsme vše nastavili, pojďme se ponořit do části kódování! Zde je podrobný rozpis toho, jak vložit zaškrtávací políčko do listu grafu pomocí Aspose.Cells.

## Krok 1: Definujte svůj výstupní adresář

Než se dostaneme k tomu zajímavému, musíme definovat, kam chceme náš soubor uložit. Budete chtít poskytnout cestu k výstupnímu adresáři.
```csharp
string outputDir = "C:\\YourOutputDirectory\\"; // Přejděte do určeného adresáře
```
 Nezapomeňte vyměnit`"C:\\YourOutputDirectory\\"` cestou, kam chcete soubor uložit. Berte to jako nastavení vašeho pracovního prostoru; musíte vědět, kam ukládáte své nástroje (nebo v tomto případě soubor Excel).

## Krok 2: Vytvoření instance objektu sešitu

 Dále vytváříme instanci`Workbook` třída. Zde se bude odehrávat veškerá naše práce.
```csharp
Workbook workbook = new Workbook();
```
Tento řádek kódu je jako otevření prázdného plátna. Jste připraveni začít malovat (nebo v našem případě kódovat)!

## Krok 3: Přidání grafu do listu

Nyní je čas přidat graf do sešitu. Postup je následující:
```csharp
int index = workbook.Worksheets.Add(SheetType.Chart);
Worksheet sheet = workbook.Worksheets[index];
sheet.Charts.AddFloatingChart(ChartType.Column, 0, 0, 1024, 960);
```
V tomto kódu jste:
- Přidání nového listu grafu do sešitu.
- Výběr typu grafu. Zde máme jednoduchý sloupcový graf.
- Zadání rozměrů grafu.

Považujte tento krok za výběr typu rámečku obrazu, který chcete, než do něj umístíte kresbu.

## Krok 4: Přidání datových řad do grafu

V tomto okamžiku naplníme graf nějakými datovými řadami. Chcete-li přidat ukázková data:
```csharp
sheet.Charts[0].NSeries.Add("{1,2,3}", false);
```
Tato linie je zásadní! Je to jako dát si barvu na plátno. Čísla představují některé příklady datových bodů pro váš graf.

## Krok 5: Přidání zaškrtávacího políčka do grafu

Nyní se dostáváme k zábavnější části – přidání zaškrtávacího políčka do našeho grafu. Zde je postup:
```csharp
sheet.Charts[0].Shapes.AddShapeInChart(MsoDrawingType.CheckBox, PlacementType.Move, 400, 400, 1000, 600);
sheet.Charts[0].Shapes[0].Text = "CheckBox 1";
```
V tomto kódu:
- Určíme typ tvaru, který chceme přidat — v tomto případě zaškrtávací políčko.
- `PlacementType.Move` znamená, že pokud se graf pohne, pohne se i zaškrtávací políčko.
- Nastavíme také polohu a velikost zaškrtávacího políčka v oblasti grafu a nakonec nastavíme textový popisek zaškrtávacího políčka.

Přidání zaškrtávacího políčka je jako umístění třešničky na vrchol poháru; vylepšuje to celou prezentaci!

## Krok 6: Uložení souboru Excel

Nakonec si práci uložme. Zde je poslední díl skládačky:
```csharp
workbook.Save(outputDir + "InsertCheckboxInChartSheet_out.xlsx");
```
Tento řádek uloží váš nově vytvořený soubor Excel se zaškrtávacím políčkem do definovaného výstupního adresáře. Je to podobné jako zapečetění vašeho uměleckého díla v ochranném pouzdře!

## Závěr

tady to máte! Úspěšně jste přidali zaškrtávací políčko na list grafu v souboru aplikace Excel pomocí Aspose.Cells for .NET. Podle těchto kroků můžete vytvořit interaktivní a dynamické excelové listy, které nabízejí skvělé funkce a díky nimž budou vaše vizualizace dat ještě poutavější.

## FAQ

### Co je Aspose.Cells?  
Aspose.Cells je výkonná knihovna pro vytváření a manipulaci se soubory Excel v aplikacích .NET.

### Mohu používat Aspose.Cells zdarma?  
 Ano, Aspose nabízí bezplatnou zkušební verzi. Můžete začít s dostupnou zkušební verzí[zde](https://releases.aspose.com/).

### Je přidání zaškrtávacího políčka do listu s grafem složité?  
Vůbec ne! Jak je ukázáno v tomto tutoriálu, lze to provést pomocí několika jednoduchých řádků kódu.

### Kde mohu koupit Aspose.Cells?  
 Aspose.Cells si můžete zakoupit u nich[odkaz na nákup](https://purchase.aspose.com/buy).

### Jak mohu získat podporu, pokud narazím na problémy?  
 Aspose poskytuje fórum podpory, kde můžete klást otázky a hledat řešení. Podívejte se na jejich[stránka podpory](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
