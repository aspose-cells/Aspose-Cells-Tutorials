---
"description": "Umožněte uživatelům upravovat určité rozsahy v tabulce aplikace Excel pomocí Aspose.Cells pro .NET. Podrobný návod se zdrojovým kódem v C#."
"linktitle": "Povolit uživateli upravovat rozsahy v listu aplikace Excel"
"second_title": "Referenční příručka k Aspose.Cells pro .NET API"
"title": "Povolit uživateli upravovat rozsahy v listu aplikace Excel"
"url": "/cs/net/protect-excel-file/allow-user-to-edit-ranges-in-excel-worksheet/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Povolit uživateli upravovat rozsahy v listu aplikace Excel

## Zavedení

Pokud jde o práci s excelovými listy, flexibilita je často klíčová – zejména když více uživatelů potřebuje přístup k úpravám určitých oblastí, aniž by byla ohrožena integrita dat celého listu. A právě zde vyniká Aspose.Cells pro .NET! V tomto tutoriálu se ponoříme do toho, jak umožnit uživatelům upravovat určité oblasti v excelovém listu a zároveň chránit zbytek dokumentu. Na konci tohoto článku nejen pochopíte koncepty, ale budete mít také hmatatelný příklad, se kterým můžete pracovat. 

## Předpoklady

Než se pustíme do detailů, ujistěte se, že máte vše, co potřebujete k zahájení:

1. Vývojové prostředí .NET: Měli byste mít nastavené funkční vývojové prostředí .NET (může to být Visual Studio nebo jakékoli jiné IDE dle vašeho výběru).
2. Knihovna Aspose.Cells pro .NET: Stáhněte a nainstalujte knihovnu Aspose.Cells. Najdete ji [zde](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: Znalost programování v C# vám pomůže snadno se orientovat v příkladech kódu.
4. Pochopení základů Excelu: Znalost fungování Excelu poskytne základ pro funkce, o kterých budeme diskutovat.

Jakmile jsou tyto předpoklady splněny, můžete začít!

## Importovat balíčky

Než začneme s kódováním, musíme se ujistit, že náš projekt rozpoznává jmenný prostor Aspose.Cells. Zde je návod, jak importovat potřebné balíčky:

```csharp
using System.IO;
using Aspose.Cells;
```

Nyní, když jsme importovali, co potřebujeme, pojďme se krok za krokem ponořit do našeho tutoriálu.

## Krok 1: Nastavení adresáře dokumentů

Pro jakékoli operace se soubory je zásadní mít definované umístění, kam budou naše dokumenty uloženy. Nastavme si pracovní adresář pro ukládání souborů aplikace Excel.

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Vytvořte adresář, pokud ještě neexistuje.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

Nejprve vyměňte `"YOUR DOCUMENT DIRECTORY"` cestou, kam chcete soubory uložit. Tento kód zkontroluje, zda adresář existuje; pokud ne, vytvoří jej.

## Krok 2: Vytvoření instance nového sešitu

S připraveným pracovním adresářem je čas vytvořit náš excelový sešit. 

```csharp
// Vytvořit instanci nového sešitu
Workbook book = new Workbook();
```

Zde vytváříme novou instanci třídy `Workbook` třída poskytovaná Aspose.Cells, která nám umožňuje manipulovat s excelovým souborem.

## Krok 3: Přístup k výchozímu pracovnímu listu

Každý nově vytvořený sešit obsahuje alespoň jeden pracovní list. Pojďme si ho prohlédnout.

```csharp
// Získejte první (výchozí) pracovní list
Worksheet sheet = book.Worksheets[0];
```

V tomto úryvku kódu přistupujeme k prvnímu listu našeho sešitu, se kterým budeme manipulovat v následujících krocích.

## Krok 4: Získejte povolení k úpravám rozsahů

Abychom mohli upravovat určité oblasti listu, potřebujeme přístup k `AllowEditRanges` vlastnictví.

```csharp
// Získejte povolení upravovat rozsahy
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```

Tato kolekce nám umožní spravovat, které oblasti lze v našem listu upravovat.

## Krok 5: Definování chráněného rozsahu

Dále definujme, kterou část listu chceme chránit a zároveň povolit úpravy v zadaném rozsahu.

```csharp
// Definovat chráněný rozsah (ProtectedRange)
ProtectedRange proteced_range;

// Vytvořte rozsah
int idx = allowRanges.Add("r2", 1, 1, 3, 3);
proteced_range = allowRanges[idx];

// Zadejte heslo
proteced_range.Password = "123";
```

V tomto kroku přidáváme nový upravitelný rozsah s názvem „r2“, který umožňuje úpravy buněk od řádku 1 (sloupec 1) do řádku 3 (sloupec 3). Dále nastavujeme heslo pro ochranu tohoto rozsahu, které zajistí, že jej budou moci upravovat pouze oprávnění uživatelé.

## Krok 6: Ochrana pracovního listu

Nyní, když jsme nastavili upravitelný rozsah, musíme list chránit.

```csharp
// Chraňte list
sheet.Protect(ProtectionType.All);
```

Tento kód ochrání celý list před nežádoucími změnami, s výjimkou rozsahu, který jsme právě zadali.

## Krok 7: Uložte soubor Excel

Uložme si sešit, abychom viděli provedené změny v souboru aplikace Excel.

```csharp
// Uložte soubor Excelu
book.Save(dataDir + "protectedrange.out.xls");
```

Nezapomeňte podle potřeby upravit název souboru. Tím se v zadaném adresáři vytvoří soubor aplikace Excel s nastavením, které jsme nakonfigurovali.

## Závěr

A máte to! Úspěšně jste vytvořili excelový list, který omezuje úpravy na určený rozsah a zároveň chrání zbytek listu. Použití Aspose.Cells pro .NET usnadňuje a zefektivňuje správu těchto úkolů. Ať už vyvíjíte složitou aplikaci, nebo jen potřebujete bezpečně spravovat data, tyto funkce mohou výrazně vylepšit váš pracovní postup.

## Často kladené otázky

### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna .NET pro práci s excelovými soubory, která nabízí funkce, jako je programově vytvářet, upravovat a převádět tabulky.

### Mohu použít více upravitelných rozsahů?
Rozhodně! Můžete zavolat `Add` metoda na `allowRanges` kolekci několikrát pro určení více upravitelných rozsahů.

### Co se stane, když zapomenu heslo?
Pokud bohužel zapomenete heslo pro upravitelný rozsah, budete muset ochranu odstranit nebo k souboru přistupovat předdefinovaným způsobem, který může vyžadovat přihlašovací údaje.

### Existuje bezplatná verze Aspose.Cells?
Ano, Aspose nabízí bezplatnou zkušební verzi, kterou můžete využít k prozkoumání funkcí před nákupem.

### Kde najdu více informací o Aspose.Cells?
Můžete zkontrolovat [dokumentace](https://reference.aspose.com/cells/net/) pro podrobné návody a reference.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}