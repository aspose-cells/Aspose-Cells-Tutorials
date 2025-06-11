---
"description": "Naučte se upravovat rozsahy v listech aplikace Excel pomocí Aspose.Cells pro .NET s touto komplexní příručkou s podrobnými pokyny."
"linktitle": "Upravit rozsahy v listu aplikace Excel"
"second_title": "Referenční příručka k Aspose.Cells pro .NET API"
"title": "Upravit rozsahy v listu aplikace Excel"
"url": "/cs/net/protect-excel-file/edit-ranges-in-excel-worksheet/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Upravit rozsahy v listu aplikace Excel

## Zavedení

Pokud jde o úpravu tabulek v Excelu, jednou z nejvýkonnějších funkcí, která se hodí, je možnost chránit určité oblasti a zároveň povolit úpravy v jiných. To může být neuvěřitelně užitečné v prostředích pro spolupráci, kde potřebuje přístup více uživatelů, ale měli by upravovat pouze určené buňky. Dnes se ponoříme do toho, jak využít Aspose.Cells pro .NET ke správě upravitelných oblastí v listu Excelu. Takže, vezměte si svůj oblíbený programátorský nápoj a pojďme na to!

## Předpoklady

Než se pustíme do kódování, ujistěme se, že máte vše připravené. Zde je to, co budete potřebovat:

1. Visual Studio: Ujistěte se, že máte nainstalované Visual Studio. Komunitní edice funguje perfektně.
2. Knihovna Aspose.Cells: Potřebujete knihovnu Aspose.Cells pro .NET. Můžete [stáhněte si to zde](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: Základní znalost C# bude velmi užitečná.
4. Nastavení projektu: Vytvořte novou konzolovou aplikaci C# ve Visual Studiu.

Bezchybné – máte vše připravené! A teď se pojďme ponořit do detailů kódu.

## Importovat balíčky

Jakmile si nastavíte projekt, prvním krokem je import potřebného jmenného prostoru Aspose.Cells. Chcete-li to provést, jednoduše vložte následující řádek na začátek souboru s kódem:

```csharp
using Aspose.Cells;
```

To vám umožní přístup ke všem funkcím, které Aspose.Cells ve vašem projektu poskytuje.

## Krok 1: Nastavení adresáře

Než začnete pracovat se soubory aplikace Excel, je vhodné si vytvořit adresář, kde budou vaše soubory umístěny. Tento krok zajistí, že vaše aplikace bude vědět, kam má číst a zapisovat data.

Pojďme si rozložit kód pro vytvoření adresáře (pokud ještě neexistuje):

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY";
// Vytvořte adresář, pokud ještě neexistuje.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

Nahradit `"YOUR DOCUMENT DIRECTORY"` s cestou, kam chcete ukládat soubory. Mohlo by to být něco jako `@"C:\ExcelFiles\"`.

## Krok 2: Vytvoření instance nového sešitu

Nyní, když máte adresář nastavený, vytvořme nový sešit aplikace Excel. Je to podobné, jako byste před zahájením malování spustili prázdné plátno.

```csharp
// Vytvořit instanci nového sešitu
Workbook book = new Workbook();
```

Tímto máte svůj prázdný sešit připravený k použití!

## Krok 3: Získejte první pracovní list

Každý sešit standardně obsahuje alespoň jeden list. Pro provedení operací s ním je nutné tento list načíst.

```csharp
// Získejte první (výchozí) pracovní list
Worksheet sheet = book.Worksheets[0];
```

Zde se dostaneme k prvnímu pracovnímu listu, což je podobné otevření nového listu papíru v sešitu.

## Krok 4: Získejte povolení k úpravám rozsahů

Než budeme moci nastavit upravitelné rozsahy, musíme z našeho listu načíst kolekci chráněných rozsahů.

```csharp
// Získejte povolení upravovat rozsahy
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```

Tento řádek načte kolekci, kde budete spravovat chráněné rozsahy. Je dobré vědět, co je k dispozici „pod kapotou“!

## Krok 5: Definování a vytvoření chráněného rozsahu

tomto okamžiku jsme připraveni definovat, ve kterém rozsahu chcete povolit úpravy. Vytvořme tento rozsah.

```csharp
// Definovat chráněný rozsah (ProtectedRange)
ProtectedRange proteced_range;

// Vytvořte rozsah
int idx = allowRanges.Add("r2", 1, 1, 3, 3);
proteced_range = allowRanges[idx];
```

Ve výše uvedeném kódu vytváříme chráněný rozsah s názvem „r2“, který umožňuje úpravy v buňkách od řádku 1, sloupce 1 do řádku 3, sloupce 3 (což v excelovém žargonu znamená blok A1 až C3). Tyto indexy můžete podle potřeby upravit.

## Krok 6: Nastavení hesla 

Nastavení hesla pro chráněný rozsah zajistí, že definovanou oblast budou moci upravovat pouze osoby s heslem. Tento krok zvyšuje zabezpečení vaší tabulky.

```csharp
// Zadejte heslo
proteced_range.Password = "YOUR_PASSWORD";
```

Nahradit `"YOUR_PASSWORD"` s heslem dle vlastního výběru. Jen nezapomeňte, nedělejte si to příliš zjednodušené – berte to jako zamykání vaší truhly s pokladem!

## Krok 7: Chraňte list

Nyní, když máme definovaný a zabezpečený heslem náš upravitelný rozsah, je čas chránit celý list.

```csharp
// Chraňte list
sheet.Protect(ProtectionType.All);
```

Vyvoláním této metody v podstatě uzamknete celý list. Změnit lze pouze oblasti definované pro úpravy.

## Krok 8: Uložte soubor Excel

Konečně jsme se dostali k poslednímu kroku našeho tutoriálu – uložení sešitu do vámi definovaného adresáře!

```csharp
// Uložte soubor Excelu
book.Save(dataDir + "protectedrange.out.xls");
```

Tím se váš chráněný sešit uloží jako `protectedrange.out.xls` ve vámi zadaném adresáři.

## Závěr

A tady to máte! Úspěšně jste vytvořili excelový list pomocí Aspose.Cells pro .NET, definovali upravitelné rozsahy, nastavili heslo a ochránili list – to vše v několika jednoduchých krocích. Nyní můžete svůj sešit sdílet s kolegy, čímž vylepšíte spolupráci a zároveň zachováte bezpečnost důležitých dat.

## Často kladené otázky

### Co je Aspose.Cells?  
Aspose.Cells je výkonná knihovna .NET, která umožňuje vývojářům programově vytvářet, manipulovat a převádět soubory aplikace Excel.

### Mohu chránit konkrétní buňky v listu aplikace Excel?  
Ano, pomocí Aspose.Cells můžete definovat konkrétní upravitelné rozsahy a chránit zbytek listu.

### Je k dispozici zkušební verze pro Aspose.Cells?  
Rozhodně! Můžete si stáhnout bezplatnou zkušební verzi [zde](https://releases.aspose.com/).

### Mohu používat Aspose.Cells s jinými programovacími jazyky?  
Ačkoli se tento tutoriál zaměřuje na .NET, Aspose.Cells je k dispozici pro několik programovacích jazyků, včetně Javy a cloudových API.

### Kde najdu více informací o Aspose.Cells?  
Můžete si prohlédnout celou dokumentaci [zde](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}