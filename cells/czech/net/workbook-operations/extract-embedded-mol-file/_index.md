---
title: Extrahujte vložený soubor Mol ze sešitu
linktitle: Extrahujte vložený soubor Mol ze sešitu
second_title: Aspose.Cells .NET Excel Processing API
description: Zjistěte, jak extrahovat vložené soubory MOL ze sešitů aplikace Excel pomocí Aspose.Cells for .NET v tomto podrobném návodu krok za krokem.
weight: 18
url: /cs/net/workbook-operations/extract-embedded-mol-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahujte vložený soubor Mol ze sešitu

## Zavedení
Pokud jde o správu dat v sešitech aplikace Excel, někdy se setkáte s různými vloženými objekty, které nejsou ve standardním formátu. Jedním z takových formátů je MOL (Molecular Structure File), který se běžně používá v chemii k reprezentaci molekulární informace. Pokud chcete extrahovat tyto soubory MOL z excelového sešitu pomocí Aspose.Cells for .NET, narazili jste na správného průvodce. V tomto článku vás provedeme procesem krok za krokem, přičemž každou část cestou demystifikujeme.
## Předpoklady
Než se ponoříte do kódu, je nezbytné se ujistit, že máte potřebné dovednosti a nástroje. Zde je to, co budete potřebovat:
1. Základní porozumění programování .NET: Měli byste znát C# a framework .NET.
2.  Aspose.Cells for .NET: Ujistěte se, že máte knihovnu Aspose.Cells. Můžete[stáhněte si jej zde](https://releases.aspose.com/cells/net/).
3. IDE: Můžete použít Visual Studio nebo jakékoli jiné IDE kompatibilní s .NET.
4. Sešit aplikace Excel s vloženými soubory MOL: Pro tento výukový program potřebujete soubor aplikace Excel obsahující objekty MOL. Můžete si vytvořit svůj vlastní nebo použít jakýkoli vzorový soubor.
## Importujte balíčky
Chcete-li začít, budete muset do projektu importovat potřebné jmenné prostory. To je klíčové pro přístup k funkcím Aspose.Cells. Můžete to udělat takto:

```csharp
using Aspose.Cells.Drawing;
using Aspose.Cells.WebExtensions;
using System;
using System.IO;
```

Tyto jmenné prostory vám umožní manipulovat se sešity, přistupovat k listům a obecně pracovat se soubory.
Nyní, když máme naše předpoklady vyřešeny, pojďme se ponořit do kódu a porozumět každému kroku, který je součástí extrahování vložených souborů MOL z excelového sešitu. 
## Krok 1: Nastavení adresářů
Prvním krokem je definovat, kde se nachází váš zdrojový dokument a kam chcete uložit extrahované soubory MOL. Pojďme nastavit ty adresáře.
```csharp
string SourceDir = "Your Document Directory"; // Nahraďte svou cestu k adresáři
string outputDir = "Your Document Directory"; // Nahraďte svou výstupní cestou
```
 Tady vyměňte`"Your Document Directory"` cestou k vašim skutečným adresářům. Je důležité, aby zdrojový i výstupní adresář byly přístupné vaší aplikaci.
## Krok 2: Načtení sešitu
Jakmile máte adresáře nastavené, dalším úkolem je načíst sešit Excel. Udělejme to teď.

```csharp
Workbook workbook = new Workbook(SourceDir + "EmbeddedMolSample.xlsx");
```

 Vytváříme instanci`Workbook` třídy a předání cesty k našemu souboru Excel s názvem`EmbeddedMolSample.xlsx`. Tento krok inicializuje sešit, což vám umožní přístup k jeho obsahu.
## Krok 3: Iterace přes pracovní listy
Nyní, když je váš sešit načten, musíte procházet každý list v sešitu. To vám umožní prozkoumat každý list, zda neobsahuje vložené objekty.

```csharp
var index = 1; // Používá se pro pojmenování extrahovaných souborů MOL
foreach (Worksheet sheet in workbook.Worksheets)
{
    OleObjectCollection oles = sheet.OleObjects;
    // Zde je další logika extrakce
}
```

 Zde používáte a`foreach` smyčka pro procházení listů. Pro každý pracovní list máte přístup k`OleObjects` kolekce, která obsahuje všechny vložené objekty.
## Krok 4: Extrahování souborů MOL
Nyní přichází kritická část – extrahování souborů MOL z objektů OLE. To vyžaduje další smyčku uvnitř smyčky listu.

```csharp
foreach (OleObject ole in oles)
{
    string fileName = outputDir + "OleObject" + index + ".mol ";
    FileStream fs = File.Create(fileName);
    fs.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    fs.Close();
    index++;
}
```

 Pro každý objekt OLE, který jste našli, vytváříte nový soubor ve výstupním adresáři. The`ObjectData` vlastnictvím`OleObject` obsahuje data vloženého objektu, která zapíšete do nově vytvořeného souboru pomocí a`FileStream`. Soubor je pojmenován postupně (`OleObject1.mol`, `OleObject2.mol` atd.) na základě`index` variabilní.
## Krok 5: Potvrzení o dokončení procesu
Nakonec, jakmile byly všechny soubory MOL extrahovány, je dobrou praxí informovat uživatele, že proces byl úspěšně dokončen.

```csharp
Console.WriteLine("ExtractEmbeddedMolFile executed successfully.");
```

Tento řádek jednoduše vytiskne zprávu do konzole, která vás informuje, že extrakce byla úspěšná. Je to příjemný dotek pro zpětnou vazbu od uživatelů.
## Závěr
tady to máte! Úspěšně jste extrahovali vložené soubory MOL ze sešitu aplikace Excel pomocí Aspose.Cells for .NET. Tento proces integruje několik základních kroků a zajišťuje strukturovaný přístup k manipulaci s vloženými objekty. Ať už se zabýváte vědeckým výzkumem, chemickou analýzou nebo se jednoduše zabýváte složitými datovými sadami, schopnost extrahovat a manipulovat s těmito typy souborů může významně změnit způsob správy vašich informací. 
## FAQ
### Mohu z Excelu extrahovat jiné typy souborů kromě MOL?
Ano, podobnými technikami můžete extrahovat různé další typy vložených souborů.
### Je Aspose.Cells zdarma k použití?
 Aspose.Cells je komerční knihovna, ale můžete[vyzkoušet to zdarma na omezenou dobu](https://releases.aspose.com/).
### Funguje tato metoda se všemi verzemi Excelu?
Ano, pokud je formát souboru podporován Aspose.Cells.
### Mohu tento proces extrakce automatizovat?
Absolutně! Tento proces můžete automatizovat umístěním kódu do naplánované úlohy nebo skriptu.
### Kde najdu další dokumentaci k Aspose.Cells?
 Můžete se podívat na[Dokumentace Aspose.Cells](https://reference.aspose.com/cells/net/) pro další podrobnosti a příklady.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
