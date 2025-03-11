---
title: Povolit uživateli upravovat rozsahy v listu aplikace Excel
linktitle: Povolit uživateli upravovat rozsahy v listu aplikace Excel
second_title: Aspose.Cells for .NET API Reference
description: Umožněte uživatelům upravovat konkrétní rozsahy v tabulce Excel pomocí Aspose.Cells for .NET. Průvodce krok za krokem se zdrojovým kódem v C#.
weight: 10
url: /cs/net/protect-excel-file/allow-user-to-edit-ranges-in-excel-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Povolit uživateli upravovat rozsahy v listu aplikace Excel

## Zavedení

Pokud jde o práci s excelovými listy, flexibilita je často klíčová – zvláště když více uživatelů potřebuje přístup k úpravám konkrétních oblastí, aniž by byla ohrožena integrita dat celého listu. To je místo, kde Aspose.Cells pro .NET září! V tomto tutoriálu se ponoříme do toho, jak umožnit uživatelům upravovat určité rozsahy v listu aplikace Excel a zároveň chránit zbytek dokumentu. Na konci tohoto článku nejen pochopíte pojmy, ale budete mít také hmatatelný příklad, se kterým můžete pracovat. 

## Předpoklady

Než se vrhneme na to, abychom mohli začít, ujistěte se, že máte vše, co potřebujete:

1. Vývojové prostředí .NET: Měli byste mít nastavené funkční vývojové prostředí .NET (může to být Visual Studio nebo jakékoli jiné IDE dle vašeho výběru).
2.  Aspose.Cells for .NET Library: Stáhněte a nainstalujte knihovnu Aspose.Cells. Můžete to najít[zde](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: Znalost programování v C# vám pomůže snadno procházet příklady kódu.
4. Pochopení základů Excelu: Znalost toho, jak Excel funguje, poskytne základ pro funkce, o kterých budeme diskutovat.

Jakmile jsou tyto předpoklady seřazeny, můžete vyrazit!

## Importujte balíčky

Než začneme kódovat, musíme se ujistit, že náš projekt rozpozná jmenný prostor Aspose.Cells. Zde je návod, jak importovat potřebné balíčky:

```csharp
using System.IO;
using Aspose.Cells;
```

Nyní, když jsme importovali, co potřebujeme, pojďme se ponořit do našeho tutoriálu krok za krokem.

## Krok 1: Nastavte adresář dokumentů

Pro jakékoli operace se soubory je klíčové mít definované místo, kam se budou naše dokumenty ukládat. Pojďme nastavit náš pracovní adresář pro ukládání souborů aplikace Excel.

```csharp
// Cesta k adresáři dokumentů.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Vytvořte adresář, pokud ještě není přítomen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

 Nejprve vyměňte`"YOUR DOCUMENT DIRECTORY"` s cestou, kam chcete soubory uložit. Tento kód zkontroluje, zda adresář existuje; pokud ne, vytvoří jeden.

## Krok 2: Vytvořte nový sešit

S připraveným pracovním adresářem je čas vytvořit náš excelový sešit. 

```csharp
// Vytvořte nový sešit
Workbook book = new Workbook();
```

 Zde vytváříme novou instanci`Workbook` třídy poskytované Aspose.Cells, která nám umožňuje manipulovat se souborem Excel.

## Krok 3: Přístup k výchozímu listu

Každý nově vytvořený sešit je dodáván s alespoň jedním pracovním listem. Pojďme k tomu přistupovat.

```csharp
// Získejte první (výchozí) list
Worksheet sheet = book.Worksheets[0];
```

V tomto fragmentu kódu přistupujeme k prvnímu listu našeho sešitu, se kterým budeme v následujících krocích manipulovat.

## Krok 4: Získejte Povolit úpravy rozsahů

 Chcete-li povolit konkrétní rozsahy listu pro úpravy, musíme získat přístup k`AllowEditRanges` vlastnictví.

```csharp
// Získejte možnosti Povolit úpravy rozsahů
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```

Tato kolekce nám umožní spravovat, které rozsahy lze v našem listu upravovat.

## Krok 5: Definujte chráněný rozsah

Dále definujme, kterou část listu chceme chránit a zároveň povolit úpravy zadaného rozsahu.

```csharp
// Definujte ProtectedRange
ProtectedRange proteced_range;

// Vytvořte rozsah
int idx = allowRanges.Add("r2", 1, 1, 3, 3);
proteced_range = allowRanges[idx];

// Zadejte heslo
proteced_range.Password = "123";
```

V tomto kroku přidáváme nový upravitelný rozsah nazvaný „r2“, který umožňuje úpravy v buňkách od řádku 1, sloupce 1 po řádek 3, sloupec 3. Navíc nastavujeme heslo pro ochranu tohoto rozsahu, což zajišťuje, že pouze oprávnění uživatelé mohou upravit to.

## Krok 6: Chraňte pracovní list

Nyní, když jsme nastavili náš upravitelný rozsah, musíme chránit list.

```csharp
// Chraňte list
sheet.Protect(ProtectionType.All);
```

Tento kód ochrání celý list před nežádoucími změnami, s výjimkou rozsahu, který jsme právě zadali.

## Krok 7: Uložte soubor Excel

Uložme sešit, abychom viděli, jak se naše změny projeví v souboru aplikace Excel.

```csharp
// Uložte soubor aplikace Excel
book.Save(dataDir + "protectedrange.out.xls");
```

Nezapomeňte upravit název souboru podle potřeby. Tím se ve vašem zadaném adresáři vytvoří soubor Excel s nastavením, které jsme nakonfigurovali.

## Závěr

Tady to máš! Úspěšně jste vytvořili list aplikace Excel, který omezuje úpravy na určený rozsah a zároveň chrání zbytek listu. Pomocí Aspose.Cells pro .NET je správa těchto druhů úkolů mnohem jednodušší a efektivnější. Ať už vyvíjíte složitou aplikaci nebo jen potřebujete bezpečně spravovat data, tyto funkce mohou výrazně zlepšit váš pracovní postup.

## FAQ

### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna .NET pro práci se soubory aplikace Excel, která nabízí funkce, jako je vytváření, úprava a převod tabulek programově.

### Mohu použít více upravitelných rozsahů?
 Absolutně! Můžete zavolat na`Add` metoda na`allowRanges` sbírat vícekrát, abyste určili více upravitelných rozsahů.

### Co se stane, když zapomenu heslo?
Bohužel, pokud zapomenete heslo pro upravitelný rozsah, budete muset odstranit ochranu nebo přistupovat k souboru předem definovaným způsobem, který může zahrnovat přihlašovací údaje.

### Existuje bezplatná verze Aspose.Cells?
Ano, Aspose poskytuje bezplatnou zkušební verzi, kterou můžete využít k prozkoumání funkcí před nákupem.

### Kde najdu více informací o Aspose.Cells?
 Můžete zkontrolovat[dokumentace](https://reference.aspose.com/cells/net/)pro podrobné návody a reference.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
