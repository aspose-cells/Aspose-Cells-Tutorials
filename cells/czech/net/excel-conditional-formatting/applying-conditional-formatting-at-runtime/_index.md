---
"description": "Naučte se, jak v Excelu s Aspose.Cells pro .NET za běhu použít podmíněné formátování v tomto komplexním návodu krok za krokem."
"linktitle": "Použití podmíněného formátování za běhu v Excelu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Použití podmíněného formátování za běhu v Excelu"
"url": "/cs/net/excel-conditional-formatting/applying-conditional-formatting-at-runtime/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Použití podmíněného formátování za běhu v Excelu

## Zavedení

Jsou to výkonné nástroje pro analýzu a vizualizaci dat. Jednou z výjimečných funkcí Excelu je podmíněné formátování, které uživatelům umožňuje aplikovat na buňky specifické styly formátování na základě jejich hodnot. To může usnadnit identifikaci trendů, zvýraznění důležitých datových bodů nebo jednoduše zvýšit čitelnost dat. Pokud chcete programově implementovat podmíněné formátování do souborů Excelu, jste na správném místě! V této příručce si ukážeme, jak aplikovat podmíněné formátování za běhu pomocí Aspose.Cells pro .NET.

## Předpoklady
Než se ponoříme do kódu, ujistěte se, že máte vše, co potřebujete k zahájení:

1. Visual Studio: Ujistěte se, že máte na svém počítači nainstalované Visual Studio. Můžete použít libovolnou verzi, která podporuje vývoj v .NET.
2. Aspose.Cells pro .NET: Budete muset mít nainstalovaný Aspose.Cells pro .NET. Můžete si ho stáhnout z [Webové stránky Aspose](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: Znalost programování v C# vám pomůže lépe porozumět úryvkům kódu.
4. .NET Framework: Ujistěte se, že váš projekt cílí na kompatibilní verzi rozhraní .NET Framework.

Teď, když máme splněny všechny předpoklady, pojďme se pustit do té zábavné části!

## Importovat balíčky
Abyste mohli začít s Aspose.Cells, budete muset importovat potřebné jmenné prostory do svého projektu v C#. Zde je návod, jak to udělat:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Tyto jmenné prostory vám poskytnou přístup ke třídám a metodám potřebným pro manipulaci s excelovými soubory a použití podmíněného formátování.

Nyní si rozdělme proces použití podmíněného formátování na zvládnutelné kroky.

## Krok 1: Nastavení projektu
Nejdříve je potřeba vytvořit nový projekt v jazyce C# ve Visual Studiu. Postupujte takto:

1. Otevřete Visual Studio a vyberte Soubor > Nový > Projekt.
2. Vyberte Konzolová aplikace (.NET Framework) a zadejte název projektu.
3. Klikněte na Vytvořit.

## Krok 2: Přidání odkazu na Aspose.Cells
Jakmile je váš projekt nastaven, je třeba přidat odkaz na knihovnu Aspose.Cells:

1. Klikněte pravým tlačítkem myši na svůj projekt v Průzkumníku řešení.
2. Vyberte Spravovat balíčky NuGet.
3. Vyhledejte Aspose.Cells a nainstalujte jej.

To vám umožní využívat všechny funkce poskytované knihovnou Aspose.Cells.

## Krok 3: Vytvoření objektu sešitu
Dále si vytvořme nový sešit a pracovní list. Tady se začne dít všechna ta magie:

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "Your Document Directory";
string filePath = dataDir + "Book1.xlsx";

// Vytvoření instance objektu Workbook
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

V tomto kroku definujeme adresář, kam bude uložen náš soubor Excel, vytvoříme nový sešit a přistupujeme k prvnímu listu.

## Krok 4: Přidání podmíněného formátování
Nyní přidáme podmíněné formátování. Začneme vytvořením prázdného objektu podmíněného formátování:

```csharp
// Přidá prázdné podmíněné formátování
int index = sheet.ConditionalFormattings.Add();
FormatConditionCollection fcs = sheet.ConditionalFormattings[index];
```

Zde přidáváme do našeho listu novou kolekci podmíněného formátování, která bude obsahovat naše pravidla formátování.

## Krok 5: Definování rozsahu formátu
Dále musíme určit rozsah buněk, na které se bude podmíněné formátování vztahovat. Řekněme, že chceme formátovat první řádek a druhý sloupec:

```csharp
// Nastaví rozsah podmíněného formátování.
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

V tomto kódu definujeme dvě oblasti pro podmíněné formátování. První oblast je pro buňku na pozici (0,0) a druhá pro pozici (1,1). Tyto rozsahy si můžete upravit podle svých specifických potřeb!

## Krok 6: Přidání podmínek podmíněného formátování
Nyní je čas definovat podmínky pro formátování. Řekněme, že chceme zvýraznit buňky na základě jejich hodnot:

```csharp
// Přidává podmínku.
int conditionIndex = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "=A2", "100");

// Přidává podmínku.
int conditionIndex2 = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "50", "100");
```

V tomto kroku přidáváme dvě podmínky: jednu pro hodnoty mezi `A2` a `100`a další pro hodnoty mezi `50` a `100`To umožňuje dynamicky zvýrazňovat buňky na základě jejich hodnot.

## Krok 7: Nastavení stylů formátování
Po nastavení podmínek můžeme nyní nastavit styly formátování. Změňme barvu pozadí našich podmínek:

```csharp
// Nastaví barvu pozadí.
FormatCondition fc = fcs[conditionIndex];
fc.Style.BackgroundColor = Color.Red;
```

Zde nastavujeme barvu pozadí první podmínky na červenou. Tuto barvu si můžete dále přizpůsobit změnou barvy písma, ohraničení a dalších stylů dle potřeby!

## Krok 8: Uložte soubor Excel
Konečně je čas uložit naši práci! Uložíme sešit do zadaného adresáře:

```csharp
// Uložení souboru aplikace Excel
workbook.Save(dataDir + "output.xls");
```

Tento řádek kódu uloží soubor aplikace Excel s použitým podmíněným formátováním. Nezapomeňte zkontrolovat zadaný adresář pro výstupní soubor!

## Závěr
tady to máte! Úspěšně jste aplikovali podmíněné formátování za běhu v Excelu pomocí knihovny Aspose.Cells pro .NET. Tato výkonná knihovna usnadňuje programovou manipulaci s excelovými soubory, umožňuje automatizovat únavné úkoly a vylepšovat prezentace dat. Ať už pracujete na malém projektu nebo na rozsáhlé aplikaci, Aspose.Cells vám může pomoci zefektivnit váš pracovní postup a zvýšit vaši produktivitu.

## Často kladené otázky

### Co je Aspose.Cells?
Aspose.Cells je knihovna .NET, která umožňuje vývojářům programově vytvářet, manipulovat a převádět soubory aplikace Excel.

### Mohu používat Aspose.Cells s jinými programovacími jazyky?
Ano, Aspose.Cells je k dispozici pro více programovacích jazyků, včetně Javy, Pythonu a dalších.

### Je k dispozici bezplatná zkušební verze pro Aspose.Cells?
Ano, můžete si stáhnout bezplatnou zkušební verzi z [Webové stránky Aspose](https://releases.aspose.com/).

### Jak mohu získat podporu pro Aspose.Cells?
Podporu můžete získat návštěvou [Fórum podpory Aspose](https://forum.aspose.com/c/cells/9).

### Potřebuji licenci k používání Aspose.Cells?
Ano, pro komerční použití je vyžadována licence, ale můžete požádat o dočasnou licenci. [zde](https://purchase.aspose.com/temporary-license/).


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}