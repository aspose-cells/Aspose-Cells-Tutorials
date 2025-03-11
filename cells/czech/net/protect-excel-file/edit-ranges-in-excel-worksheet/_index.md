---
title: Upravit rozsahy v listu aplikace Excel
linktitle: Upravit rozsahy v listu aplikace Excel
second_title: Aspose.Cells for .NET API Reference
description: Naučte se upravovat rozsahy v listech aplikace Excel pomocí Aspose.Cells for .NET s tímto komplexním průvodcem obsahujícím podrobné pokyny.
weight: 20
url: /cs/net/protect-excel-file/edit-ranges-in-excel-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Upravit rozsahy v listu aplikace Excel

## Zavedení

Pokud jde o úpravy tabulek Excelu, jednou z nejvýkonnějších funkcí, která se hodí, je možnost chránit určité oblasti a zároveň povolit úpravy v jiných. To může být neuvěřitelně užitečné v prostředích pro spolupráci, kde potřebuje přístup více uživatelů, ale měli by upravovat pouze určené buňky. Dnes se ponoříme do toho, jak využít Aspose.Cells pro .NET ke správě upravitelných rozsahů v rámci listu aplikace Excel. Takže si vezměte svůj oblíbený kódovací nápoj a můžeme začít!

## Předpoklady

Než se pustíme do kódování, ujistíme se, že jste vše nastavili. Zde je to, co potřebujete:

1. Visual Studio: Ujistěte se, že máte nainstalované Visual Studio. Komunitní edice funguje naprosto v pořádku.
2.  Knihovna Aspose.Cells: Potřebujete knihovnu Aspose.Cells for .NET. Můžete[stáhněte si jej zde](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: Základní znalost C# bude dlouhá cesta.
4. Nastavení projektu: Vytvořte novou konzolovou aplikaci C# ve Visual Studiu.

Bezvadné – vše je připraveno! Nyní se pojďme ponořit do toho nejhrubšího kódu.

## Importujte balíčky

Jakmile nastavíte svůj projekt, počáteční krok zahrnuje import potřebného jmenného prostoru Aspose.Cells. Chcete-li to provést, jednoduše vložte následující řádek do horní části souboru kódu:

```csharp
using Aspose.Cells;
```

To vám umožní přístup ke všem funkcím poskytovaným Aspose.Cells ve vašem projektu.

## Krok 1: Nastavte adresář

Než začnete pracovat se soubory aplikace Excel, je dobré vytvořit adresář, kde budou soubory umístěny. Tento krok zajistí, že vaše aplikace ví, kde má číst a zapisovat data.

Pojďme si rozložit kód pro vytvoření adresáře (pokud ještě neexistuje):

```csharp
// Cesta k adresáři dokumentů.
string dataDir = "YOUR DOCUMENT DIRECTORY";
// Vytvořte adresář, pokud ještě není přítomen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

 Nahradit`"YOUR DOCUMENT DIRECTORY"` s cestou, kam chcete soubory uložit. Tohle by mohlo být něco jako`@"C:\ExcelFiles\"`.

## Krok 2: Vytvořte nový sešit

Nyní, když je váš adresář nastaven, pojďme vytvořit nový sešit aplikace Excel. Je to podobné jako zapálení prázdného plátna, než začnete malovat.

```csharp
// Vytvořte nový sešit
Workbook book = new Workbook();
```

Díky tomu máte svůj prázdný sešit připravený k použití!

## Krok 3: Získejte první pracovní list

Každý sešit obsahuje ve výchozím nastavení alespoň jeden list. Chcete-li s ním provádět operace, musíte tento list načíst.

```csharp
// Získejte první (výchozí) list
Worksheet sheet = book.Worksheets[0];
```

Zde se dostaneme k prvnímu pracovnímu listu, který je podobný otevření nového listu papíru v poznámkovém bloku.

## Krok 4: Získejte Povolit úpravy rozsahů

Než budeme moci nastavit upravitelné rozsahy, musíme načíst kolekci chráněných rozsahů z našeho listu.

```csharp
// Získejte možnosti Povolit úpravy rozsahů
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```

Tento řádek načte kolekci, kde budete spravovat chráněné rozsahy. Je dobré vědět, co je k dispozici pod kapotou!

## Krok 5: Definujte a vytvořte chráněný rozsah

V tuto chvíli jsme připraveni definovat, ve kterém rozsahu chcete povolit úpravy. Pojďme vytvořit tento rozsah.

```csharp
// Definujte ProtectedRange
ProtectedRange proteced_range;

// Vytvořte rozsah
int idx = allowRanges.Add("r2", 1, 1, 3, 3);
proteced_range = allowRanges[idx];
```

Ve výše uvedeném kódu vytváříme chráněný rozsah s názvem „r2“, který umožňuje úpravy v buňkách od řádku 1, sloupce 1 do řádku 3, sloupce 3 (což v jazyce Excelu znamená blok A1 až C3). Tyto indexy můžete upravit podle potřeby.

## Krok 6: Nastavte heslo 

Nastavení hesla pro chráněný rozsah zajistí, že pouze ti, kdo mají heslo, mohou upravit definovanou oblast. Tento krok zvyšuje zabezpečení vaší tabulky.

```csharp
// Zadejte heslo
proteced_range.Password = "YOUR_PASSWORD";
```

 Nahradit`"YOUR_PASSWORD"` s heslem dle vašeho výběru. Jen si pamatujte, nedělejte to příliš jednoduchým – berte to jako zamykání vaší truhly s pokladem!

## Krok 7: Chraňte list

Nyní, když máme náš upravitelný rozsah definovaný a zabezpečený heslem, je čas chránit celý list.

```csharp
// Chraňte list
sheet.Protect(ProtectionType.All);
```

Vyvoláním této metody v podstatě uzamknete celý list. Změnit lze pouze rozsahy definované pro úpravy.

## Krok 8: Uložte soubor Excel

Konečně jsme dosáhli posledního kroku v našem tutoriálu – uložení sešitu do vámi definovaného adresáře!

```csharp
// Uložte soubor aplikace Excel
book.Save(dataDir + "protectedrange.out.xls");
```

Tím se váš chráněný sešit uloží jako`protectedrange.out.xls` ve vámi zadaném adresáři.

## Závěr

A tady to máte! Úspěšně jste vytvořili excelový list pomocí Aspose.Cells pro .NET, definovali upravitelné rozsahy, nastavili heslo a ochránili list – to vše v několika jednoduchých krocích. Nyní můžete svůj sešit sdílet s kolegy, čímž se zlepší spolupráce a zároveň budou důležitá data v bezpečí.

## FAQ

### Co je Aspose.Cells?  
Aspose.Cells je výkonná knihovna .NET, která umožňuje vývojářům vytvářet, manipulovat a převádět soubory Excelu programově.

### Mohu chránit konkrétní buňky v listu aplikace Excel?  
Ano, pomocí Aspose.Cells můžete definovat konkrétní upravitelné rozsahy a chránit zbytek listu.

### Je k dispozici zkušební verze pro Aspose.Cells?  
 Absolutně! Můžete si stáhnout bezplatnou zkušební verzi[zde](https://releases.aspose.com/).

### Mohu používat Aspose.Cells s jinými programovacími jazyky?  
Zatímco tento tutoriál se zaměřuje na .NET, Aspose.Cells je k dispozici pro několik programovacích jazyků, včetně Java a Cloud API.

### Kde najdu více informací o Aspose.Cells?  
 Můžete prozkoumat celou dokumentaci[zde](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
