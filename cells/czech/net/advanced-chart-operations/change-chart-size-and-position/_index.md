---
title: Změňte velikost a pozici grafu
linktitle: Změňte velikost a pozici grafu
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se měnit velikost a polohu grafů v Excelu pomocí Aspose.Cells for .NET pomocí tohoto snadno srozumitelného průvodce.
weight: 11
url: /cs/net/advanced-chart-operations/change-chart-size-and-position/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Změňte velikost a pozici grafu

## Zavedení

Pokud jde o programovou manipulaci s tabulkami, je těžké ignorovat všestrannost a sílu Aspose.Cells pro .NET. Už jste se někdy potýkali se změnou velikosti nebo přemístěním grafů v souborech aplikace Excel? Pokud ano, máte se na co těšit! Tato příručka vás provede neuvěřitelně jednoduchými kroky ke změně velikosti a polohy grafů ve vašich tabulkách pomocí Aspose.Cells. Připoutejte se, protože se do tohoto tématu ponoříme hluboko!

## Předpoklady

Než se pustíme do hrubky kódování a manipulace s grafy, vyjasněme si několik předpokladů. Díky pevnému základu bude vaše cesta plynulejší a příjemnější.

### Základní znalost C#
- Nezbytná je znalost programovacího jazyka C#. Pokud umíte procházet syntaxí C#, jste již o krok napřed!

### Aspose.Cells pro knihovnu .NET
-  Musíte mít nainstalovanou knihovnu Aspose.Cells. Pokud ho ještě nemáte, nezoufejte! Můžete si jej snadno stáhnout z[zde](https://releases.aspose.com/cells/net/).

### Vývojové prostředí
- Nastavte své vývojové prostředí (jako je Visual Studio), kde můžete bez problémů psát a spouštět svůj kód C#.

### Excel soubor s grafem
- Bylo by užitečné mít soubor aplikace Excel s alespoň jedním grafem, se kterým můžeme pro tento tutoriál manipulovat.

Jakmile zaškrtnete tyto předpoklady ze seznamu, můžete se naučit, jak změnit velikost a pozici grafu jako profesionál!

## Importujte balíčky

Nyní, když máme vše nastaveno, pojďme importovat potřebné balíčky. Tento krok je zásadní, protože nám umožňuje přístup k třídám a metodám Aspose.Cells potřebným k manipulaci se soubory Excel.

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Charts;
```

Tyto příkazy dávají kompilátoru vědět, že budeme používat třídy z knihovny Aspose.Cells. Ujistěte se, že to máte v horní části kódu, abyste se později vyhnuli jízdě po hrbolaté silnici!

Nyní si tento proces rozdělíme na zvládnutelné kroky. Půjdeme krok za krokem a zajistíme, aby bylo vše křišťálově čisté.

## Krok 1: Definujte zdrojové a výstupní adresáře

```csharp
string sourceDir = "Your Document Directory";
string outputDir = "Your Output Directory";
```

Nejprve musíme definovat, kde se nachází náš zdrojový soubor a kam chceme uložit výstupní soubor. Nahraďte "Váš adresář dokumentů" a "Váš výstupní adresář" svými skutečnými cestami ke složce. Považujte tyto adresáře za svou domovskou základnu a spouštěcí panel, kde jsou uloženy vaše soubory.

## Krok 2: Načtěte sešit

```csharp
Workbook workbook = new Workbook(sourceDir + "sampleChangeChartSizeAndPosition.xlsx");
```

 Zde vytvoříme novou instanci`Workbook` třídy a nahrajte do ní náš soubor Excel. Představte si sešit jako digitální zápisník obsahující všechny vaše listy a grafy. Parametr, který předáváme, je úplná cesta k našemu souboru Excel, takže se ujistěte, že obsahuje název souboru!

## Krok 3: Otevřete sešit

```csharp
Worksheet worksheet = workbook.Worksheets[0];
```

 Nyní, když máme načtený sešit, potřebujeme získat přístup ke konkrétnímu listu, se kterým chceme pracovat, což je v tomto případě první list (index`[0]`). Stejně jako při listování na správnou stránku v knize nám tento krok pomáhá zaměřit se na požadovaný list pro naše úpravy.

## Krok 4: Načtěte graf

```csharp
Chart chart = worksheet.Charts[0];
```

Po načtení listu se vrhneme přímo do přístupu k grafu! Chytáme první graf (opět index`[0]`). Je to jako výběr uměleckého díla, které chcete ozdobit. Ujistěte se, že váš graf v tomto listu existuje, nebo se budete škrábat na hlavě!

## Krok 5: Změňte velikost grafu

```csharp
chart.ChartObject.Width = 400;
chart.ChartObject.Height = 300;
```

 Je čas změnit rozměry grafu! Zde nastavíme šířku na`400` pixelů a výšku do`300` pixelů. Úprava velikosti je podobná výběru dokonalého rámu pro vaše umělecké dílo – příliš velký nebo příliš malý a do místnosti se prostě nehodí.

## Krok 6: Přemístěte graf

```csharp
chart.ChartObject.X = 250;
chart.ChartObject.Y = 150;
```

 Nyní, když máme správnou velikost, přesuňte graf! Změnou`X` a`Y` vlastnosti, v podstatě přemístíme graf na listu. Představte si to jako přetažení zarámovaného obrázku na nové místo na zdi, abyste lépe předvedli jeho krásu!

## Krok 7: Uložte sešit

```csharp
workbook.Save(outputDir + "outputChangeChartSizeAndPosition.xlsx");
```

Nakonec uložíme naše změny do nového souboru Excel. Zadejte vhodný název pro exportovaný soubor, abyste měli věci pořádané. Je to jako udělat snímek vašeho krásně uspořádaného pokoje poté, co přesunete nábytek – zachováte nové uspořádání!

## Krok 8: Potvrďte úspěch

```csharp
Console.WriteLine("ChangeChartSizeAndPosition executed successfully.");
```

Abychom vše řádně uzavřeli, poskytujeme zpětnou vazbu o tom, zda byla operace úspěšně dokončena. Je to skvělá praxe, která vám dává jasné a sebevědomé uzavření vašeho úkolu – stejně jako obdivování vaší práce po přeuspořádání nábytku!

## Závěr

Gratuluji! Právě jste se naučili, jak změnit velikost a pozici grafů v Excelu pomocí Aspose.Cells pro .NET. Pomocí těchto kroků můžete grafy nejen lépe vypadat, ale také dokonale zapadnout do vašich tabulek, což povede k profesionálnější prezentaci vašich dat. Proč to nezkusit a nezačít manipulovat s grafy ještě dnes? 

## FAQ

### Co je Aspose.Cells pro .NET?  
Aspose.Cells for .NET je výkonná knihovna, která umožňuje vývojářům vytvářet, manipulovat a převádět soubory aplikace Excel v aplikacích .NET.

### Potřebuji licenci k používání Aspose.Cells?  
 Aspose.Cells můžete vyzkoušet zdarma, ale pro další používání v produkčních aplikacích je vyžadována licence. Můžete získat jeden[zde](https://purchase.aspose.com/buy).

### Mohu používat Aspose.Cells bez sady Visual Studio?  
Ano, Aspose.Cells můžete použít v jakémkoli IDE kompatibilním s .NET, ale Visual Studio poskytuje nástroje, které usnadňují vývoj.

### Jak mohu získat podporu pro Aspose.Cells?  
 Podporu můžete najít v jejich vyhrazených[Fórum podpory](https://forum.aspose.com/c/cells/9).

### Je k dispozici dočasná licence?  
 Ano, můžete získat dočasnou licenci k hodnocení Aspose.Cells na krátkou dobu, která je k dispozici[zde](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
