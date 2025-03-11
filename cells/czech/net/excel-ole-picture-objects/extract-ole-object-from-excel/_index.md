---
title: Extrahujte objekt OLE z aplikace Excel
linktitle: Extrahujte objekt OLE z aplikace Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se extrahovat objekty OLE ze souborů aplikace Excel pomocí Aspose.Cells for .NET. Návod krok za krokem pro snadnou extrakci.
weight: 10
url: /cs/net/excel-ole-picture-objects/extract-ole-object-from-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahujte objekt OLE z aplikace Excel

## Zavedení
dnešním technicky vyspělém světě je práce s excelovými soubory běžným úkolem, zejména pro ty, kteří se zabývají analýzou dat, financemi a řízením projektů. Jedním z často přehlížených aspektů je manipulace s objekty OLE (propojování a vkládání objektů) v tabulkách aplikace Excel. Mohou to být vložené dokumenty, obrázky nebo dokonce složité datové typy, které hrají klíčovou roli při vylepšování funkčnosti a bohatosti vašich souborů Excel. Pokud jste uživatelem Aspose.Cells a chcete extrahovat tyto objekty OLE programově pomocí .NET, jste na správném místě! Tento průvodce vás provede procesem krok za krokem a zajistí, že pochopíte nejen to, jak to udělat, ale také to, proč je každá část procesu důležitá.
## Předpoklady
Než se ponoříme do hrubších detailů extrahování OLE objektů, musíte mít připraveno několik věcí:
1. Základní znalost C#: Pokud jste obeznámeni s C#, jste již na správné cestě. Pokud ne, nebojte se! Uděláme věci přímočaré.
2. Instalováno Aspose.Cells: Budete potřebovat knihovnu Aspose.Cells. Můžete si jej stáhnout z webu[zde](https://releases.aspose.com/cells/net/).
3. Kompatibilní vývojové prostředí: Ujistěte se, že máte nastavené vývojové prostředí .NET, jako je Visual Studio, připravené k použití.
4. Ukázkový soubor Excel: Pro testování budete potřebovat soubor Excel s vloženými objekty OLE. 
Jakmile splníte tyto předpoklady, můžeme začít svou cestu do světa extrakce objektů OLE.
## Importujte balíčky
Nejprve si naimportujeme potřebné balíčky, které použijeme v našem tutoriálu. Ve svém projektu C# budete muset zahrnout jmenný prostor Aspose.Cells. Můžete to udělat takto:
```csharp
using System.IO;
using Aspose.Cells;
```
## Krok 1: Nastavte adresář dokumentů
V tomto kroku definujeme cestu, kde se nachází náš soubor Excel. Možná se divíte, proč je to důležité. Je to jako připravit scénu pro představení – pomáhá to scénáři vědět, kde herce najít (v našem případě soubor Excel).
```csharp
string dataDir = "Your Document Directory";
```
 Nahradit`"Your Document Directory"` se skutečnou cestou, kde je váš soubor Excel (`book1.xls`) je uložen.
## Krok 2: Otevřete soubor aplikace Excel
Nyní, když máme nastavený adresář dokumentů, je dalším krokem otevření souboru Excel. Berte to jako otevření knihy, než začnete číst – je důležité vidět, co je uvnitř.
```csharp
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
## Krok 3: Přístup ke kolekci objektů OLE
Každý list v sešitu aplikace Excel může obsahovat různé objekty, včetně objektů OLE. Zde přistupujeme ke kolekci objektů OLE prvního listu. Je to podobné, jako když vyberete stránku, abyste si prohlédli vložené obrázky a dokumenty.
```csharp
Aspose.Cells.Drawing.OleObjectCollection oles = workbook.Worksheets[0].OleObjects;
```
## Krok 4: Procházet objekty OLE
Nyní přichází ta zábavná část – procházení všemi OLE objekty v naší sbírce. Tento krok je zásadní, protože nám umožňuje efektivně zpracovávat více objektů OLE. Představte si, že procházíte truhlou s pokladem, abyste našli cenné předměty!
```csharp
for (int i = 0; i < oles.Count; i++)
{
    Aspose.Cells.Drawing.OleObject ole = oles[i];
    // Další logika pro manipulaci s každým objektem
}
```
## Krok 5: Zadejte název výstupního souboru
Když se ponoříme hlouběji do každého objektu OLE, musíme přijít s názvem souboru pro extrahované objekty. Proč? Protože jakmile je vytěžíme, chceme mít vše uspořádané, abychom své poklady později snadno našli.
```csharp
string fileName = dataDir + "ole_" + i + ".";
```
## Krok 6: Určete typ formátu souboru
Každý objekt OLE může být různých typů (např. dokumenty, tabulky, obrázky). Je důležité určit typ formátu, abyste jej mohli správně extrahovat. Je to jako znát recept na jídlo – musíte znát ingredience!
```csharp
switch (ole.FileFormatType)
{
    case FileFormatType.Doc:
        fileName += "doc";
        break;
    case FileFormatType.Xlsx:
        fileName += "xlsx";
        break;
    case FileFormatType.Ppt:
        fileName += "ppt";
        break;
    case FileFormatType.Pdf:
        fileName += "pdf";
        break;
    case FileFormatType.Unknown:
        fileName += "jpg";
        break;
    default:
        // Zvládněte jiné formáty souborů
        break;
}
```
## Krok 7: Uložte objekt OLE
 Nyní přejdeme k uložení objektu OLE. Pokud je objekt soubor Excel, uložíme jej pomocí a`MemoryStream` což nám umožňuje manipulovat s daty v paměti před jejich vypsáním. Tento krok je podobný zabalení pokladu před jeho odesláním příteli.
```csharp
if (ole.FileFormatType == FileFormatType.Xlsx)
{
    MemoryStream ms = new MemoryStream();
    ms.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    Workbook oleBook = new Workbook(ms);
    oleBook.Settings.IsHidden = false;
    oleBook.Save(dataDir + "Excel_File" + i + ".out.xlsx");
}
```
 Pro jiné typy souborů použijeme a`FileStream` k vytvoření souboru na disku.
```csharp
else
{
    FileStream fs = File.Create(fileName);
    fs.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    fs.Close();
}
```

## Závěr
právě tak jste úspěšně prošli vodami extrakce objektů OLE s Aspose.Cells for .NET! Pomocí těchto kroků můžete snadno extrahovat a spravovat vložené objekty ze souborů aplikace Excel. Pamatujte, že jako každá cenná dovednost, cvičení dělá mistra. Udělejte si tedy čas experimentováním s různými soubory aplikace Excel a brzy se stanete profesionálem na extrakci OLE!
## FAQ
### Co jsou objekty OLE v Excelu?
Objekty OLE jsou technologií, která umožňuje vkládání a propojování dokumentů a dat v jiných aplikacích v rámci listu aplikace Excel.
### Proč bych potřeboval extrahovat objekty OLE?
Extrahování objektů OLE vám umožňuje přistupovat a manipulovat s vloženými dokumenty nebo obrázky nezávisle na původním souboru aplikace Excel.
### Dokáže Aspose.Cells zpracovat všechny typy vložených souborů?
Ano, Aspose.Cells může spravovat různé objekty OLE, včetně dokumentů aplikace Word, listů aplikace Excel, prezentací v PowerPointu a obrázků.
### Jak nainstaluji Aspose.Cells pro .NET?
 Aspose.Cells můžete nainstalovat stažením z jejich[stránka vydání](https://releases.aspose.com/cells/net/).
### Kde najdu podporu pro Aspose.Cells?
Na jejich stránkách můžete získat podporu pro Aspose.Cells[fórum podpory](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
