---
title: Použití podmíněného formátování za běhu v Excelu
linktitle: Použití podmíněného formátování za běhu v Excelu
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak používat podmíněné formátování za běhu v Excelu s Aspose.Cells for .NET v tomto komplexním podrobném průvodci.
weight: 11
url: /cs/net/excel-conditional-formatting/applying-conditional-formatting-at-runtime/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Použití podmíněného formátování za běhu v Excelu

## Zavedení

jsou to výkonné nástroje pro analýzu a vizualizaci dat. Jednou z výjimečných funkcí Excelu je podmíněné formátování, které uživatelům umožňuje aplikovat na buňky specifické styly formátování na základě jejich hodnot. To může usnadnit identifikaci trendů, zvýraznění důležitých datových bodů nebo jednoduše učinit data čitelnějšími. Pokud chcete programově implementovat podmíněné formátování v souborech aplikace Excel, jste na správném místě! V této příručce si projdeme, jak použít podmíněné formátování za běhu pomocí Aspose.Cells for .NET.

## Předpoklady
Než se ponoříte do kódu, ujistěte se, že máte vše, co potřebujete, abyste mohli začít:

1. Visual Studio: Ujistěte se, že máte na svém počítači nainstalované Visual Studio. Můžete použít jakoukoli verzi, která podporuje vývoj .NET.
2.  Aspose.Cells for .NET: Musíte mít nainstalovaný Aspose.Cells for .NET. Můžete si jej stáhnout z[Aspose webové stránky](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: Znalost programování v C# vám pomůže lépe porozumět úryvkům kódu.
4. .NET Framework: Ujistěte se, že váš projekt cílí na kompatibilní verzi rozhraní .NET Framework.

Nyní, když máme pokryty předpoklady, pojďme se vrhnout na zábavnou část!

## Importujte balíčky
Chcete-li začít s Aspose.Cells, budete muset do svého projektu C# importovat potřebné jmenné prostory. Můžete to udělat takto:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Tyto jmenné prostory vám umožní přístup ke třídám a metodám potřebným pro manipulaci se soubory aplikace Excel a použití podmíněného formátování.

Nyní si rozeberme proces aplikace podmíněného formátování do zvládnutelných kroků.

## Krok 1: Nastavte svůj projekt
Nejprve musíte vytvořit nový projekt C# ve Visual Studiu. Zde je postup:

1. Otevřete Visual Studio a vyberte Soubor > Nový > Projekt.
2. Vyberte Console App (.NET Framework) a pojmenujte svůj projekt.
3. Klikněte na Vytvořit.

## Krok 2: Přidejte odkaz Aspose.Cells
Jakmile je váš projekt nastaven, musíte přidat odkaz na knihovnu Aspose.Cells:

1. Klepněte pravým tlačítkem myši na svůj projekt v Průzkumníku řešení.
2. Vyberte Spravovat balíčky NuGet.
3. Vyhledejte Aspose.Cells a nainstalujte jej.

To vám umožní používat všechny funkce poskytované knihovnou Aspose.Cells.

## Krok 3: Vytvořte objekt sešitu
Dále vytvoříme nový sešit a pracovní list. Tady se odehrává všechna ta kouzla:

```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
string filePath = dataDir + "Book1.xlsx";

// Vytvoření instance objektu sešitu
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

V tomto kroku definujeme adresář, kam se uloží náš soubor Excel, vytváříme nový sešit a přistupujeme k prvnímu listu.

## Krok 4: Přidejte podmíněné formátování
Nyní přidáme nějaké podmíněné formátování. Začneme vytvořením prázdného objektu podmíněného formátování:

```csharp
// Přidá prázdné podmíněné formátování
int index = sheet.ConditionalFormattings.Add();
FormatConditionCollection fcs = sheet.ConditionalFormattings[index];
```

Zde do našeho listu přidáváme novou kolekci podmíněného formátování, která bude obsahovat naše pravidla formátování.

## Krok 5: Definujte rozsah formátů
Dále musíme určit rozsah buněk, na které se bude podmíněné formátování vztahovat. Řekněme, že chceme formátovat první řádek a druhý sloupec:

```csharp
// Nastavuje rozsah podmíněného formátu.
CellArea ca = new CellArea();
ca.StartRow =0;
ca.EndRow =0;
ca.StartColumn =0;
ca.EndColumn =0;
fcs.AddArea(ca);

ca = new CellArea();
ca.StartRow =1;
ca.EndRow =1;
ca.StartColumn =1;
ca.EndColumn =1;
fcs.AddArea(ca);
```

V tomto kódu definujeme dvě oblasti pro podmíněné formátování. První oblast je pro buňku na (0,0) a druhá pro (1,1). Neváhejte upravit tyto rozsahy na základě vašich konkrétních potřeb!

## Krok 6: Přidejte podmínky podmíněného formátování
Nyní je čas definovat podmínky pro naše formátování. Řekněme, že chceme zvýraznit buňky na základě jejich hodnot:

```csharp
// Přidá podmínku.
int conditionIndex = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "=A2", "100");

// Přidá podmínku.
int conditionIndex2 = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "50", "100");
```

 V tomto kroku přidáváme dvě podmínky: jednu pro hodnoty mezi`A2` a`100` a další pro hodnoty mezi`50` a`100`. To vám umožní dynamicky zvýrazňovat buňky na základě jejich hodnot.

## Krok 7: Nastavte styly formátování
S našimi podmínkami nyní můžeme nastavit styly formátování. Změňme barvu pozadí pro naše podmínky:

```csharp
// Nastaví barvu pozadí.
FormatCondition fc = fcs[conditionIndex];
fc.Style.BackgroundColor = Color.Red;
```

Zde nastavujeme barvu pozadí první podmínky na červenou. Toto můžete dále přizpůsobit změnou barvy písma, ohraničení a dalších stylů podle potřeby!

## Krok 8: Uložte soubor Excel
Konečně je čas zachránit naši práci! Sešit uložíme do zadaného adresáře:

```csharp
// Uložení souboru Excel
workbook.Save(dataDir + "output.xls");
```

Tento řádek kódu uloží soubor aplikace Excel s použitým podmíněným formátováním. Nezapomeňte zkontrolovat zadaný adresář pro váš výstupní soubor!

## Závěr
tady to máte! Úspěšně jste použili podmíněné formátování za běhu v Excelu pomocí Aspose.Cells for .NET. Tato výkonná knihovna usnadňuje programovou manipulaci se soubory aplikace Excel, což vám umožňuje automatizovat únavné úkoly a vylepšovat prezentace dat. Ať už pracujete na malém projektu nebo na rozsáhlé aplikaci, Aspose.Cells vám může pomoci zefektivnit váš pracovní postup a zlepšit vaši produktivitu.

## FAQ

### Co je Aspose.Cells?
Aspose.Cells je knihovna .NET, která umožňuje vývojářům vytvářet, manipulovat a převádět soubory Excelu programově.

### Mohu používat Aspose.Cells s jinými programovacími jazyky?
Ano, Aspose.Cells je k dispozici pro více programovacích jazyků, včetně Javy, Pythonu a dalších.

### Je k dispozici bezplatná zkušební verze pro Aspose.Cells?
 Ano, můžete si stáhnout bezplatnou zkušební verzi z[Aspose webové stránky](https://releases.aspose.com/).

### Jak mohu získat podporu pro Aspose.Cells?
 Podporu můžete získat návštěvou stránky[Aspose fórum podpory](https://forum.aspose.com/c/cells/9).

### Potřebuji licenci k používání Aspose.Cells?
 Ano, pro komerční použití je vyžadována licence, ale můžete požádat o dočasnou licenci[zde](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
