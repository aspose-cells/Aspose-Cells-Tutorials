---
title: Vložte objekt OLE do aplikace Excel
linktitle: Vložte objekt OLE do aplikace Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se vkládat objekty OLE do souborů aplikace Excel pomocí Aspose.Cells for .NET v této komplexní příručce s podrobnými pokyny.
weight: 11
url: /cs/net/excel-ole-picture-objects/insert-ole-object-into-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vložte objekt OLE do aplikace Excel

## Zavedení
Ať už vkládáte obrázky, grafy nebo jakékoli jiné soubory, použití Aspose.Cells for .NET poskytuje přímočarý způsob, jak toho dosáhnout. V této příručce prozkoumáme kroky potřebné k vložení objektu OLE do listu aplikace Excel. Na konci budete moci vylepšit své excelové sešity personalizovanými vloženími, které mohou zapůsobit na vaše publikum nebo sloužit různým profesionálním potřebám. 
## Předpoklady
Než se ponoříte do toho nejhrubšího kódu, musíte mít po ruce několik věcí:
1. Visual Studio: V ideálním případě byste měli pracovat v prostředí, které podporuje .NET, jako je Visual Studio. Toto IDE usnadňuje psaní, testování a ladění vašich aplikací.
2. Knihovna Aspose.Cells: Musíte mít nainstalovanou knihovnu Aspose.Cells. Můžete jej získat prostřednictvím správce balíčků NuGet nebo si jej stáhnout přímo z[Aspose webové stránky](https://releases.aspose.com/cells/net/).
3.  Ukázkové soubory: Pro demonstrační účely se ujistěte, že máte obrázek (např`logo.jpg`) a soubor Excel (`book1.xls`) pracovat. Ty budou v kódu uvedeny.
4. Základní porozumění C#: Znalost C# vám pomůže porozumět příslušným krokům a v případě potřeby provést úpravy.
Jakmile budete mít vše na svém místě, je čas vyhrnout si rukávy a začít vkládat objekty OLE do Excelu!
## Importujte balíčky
Chcete-li manipulovat se soubory Excel pomocí Aspose.Cells, musíte nejprve importovat požadované balíčky. Přidejte následující jmenné prostory na začátek souboru C#:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Toto základní nastavení vám umožní pracovat se sešitem, listy a dalšími základními součástmi potřebnými pro váš úkol.
Pojďme si to rozebrat do lehce stravitelných kroků.
## Krok 1: Nastavte adresář dokumentů
Prvním krokem je určit, kde budou vaše dokumenty uloženy. To je docela jednoduché.
```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
```
 Nezapomeňte vyměnit`"Your Document Directory"` se skutečnou cestou k adresáři ve vašem systému, kam plánujete ukládat soubory.
## Krok 2: Vytvořte adresář, pokud neexistuje
Dále se chceme ujistit, že tento adresář existuje. Pokud ne, musíme ji vytvořit.
```csharp
// Vytvořte adresář, pokud ještě není přítomen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Tato jednoduchá kontrola chrání váš program před zbytečnými chybami.
## Krok 3: Vytvořte nový sešit
Nyní vytvoříme nový sešit, kde budeme pracovat s našimi objekty OLE.
```csharp
// Vytvořte nový sešit.
Workbook workbook = new Workbook();
```
Tento nový sešit bude sloužit jako plátno pro objekt OLE, který plánujete vložit.
## Krok 4: Získejte první pracovní list
Poté, co máme svůj sešit, musíme vzít první list. Obvykle zde budete nejaktivněji pracovat.
```csharp
// Získejte první pracovní list.
Worksheet sheet = workbook.Worksheets[0];
```
Pěkné a jednoduché! Jsme připraveni začít přidávat obsah do tohoto listu.
## Krok 5: Definujte cestu k obrázku
Nyní nastavíme cestu pro obrázek, který chcete vložit do souboru Excel.
```csharp
//Definujte řetězcovou proměnnou pro uložení cesty obrázku.
string ImageUrl = dataDir + "logo.jpg";
```
 Ujistěte se, že tato cesta správně odráží vaše`logo.jpg` soubor je uložen.
## Krok 6: Načtěte obrázek do pole Byte
Budeme muset obrázek načíst do formátu, se kterým můžeme pracovat. K tomu otevřeme souborový proud a načteme jeho data do bajtového pole.
```csharp
// Dostaňte obrázek do streamů.
FileStream fs = File.OpenRead(ImageUrl);
// Definujte bajtové pole.
byte[] imageData = new Byte[fs.Length];
// Získejte obrázek do pole bajtů z proudů.
fs.Read(imageData, 0, imageData.Length);
// Zavřete stream.
fs.Close();
```
Načtením obrázku do bajtového pole jej připravíme pro vložení do excelového listu.
## Krok 7: Získejte cestu k souboru Excel
Nyní definujme, kde se nachází váš soubor Excel.
```csharp
// Získejte cestu k souboru aplikace Excel v proměnné.
string path = dataDir + "book1.xls";
```
Znovu se ujistěte, že tato cesta je správná a ukazuje na správný soubor.
## Krok 8: Načtěte soubor aplikace Excel do pole Byte
Stejně jako jsme to udělali s obrázkem, musíme načíst samotný soubor Excel do bajtového pole.
```csharp
// Získejte soubor do streamů.
fs = File.OpenRead(path);
//Definujte pole bajtů.
byte[] objectData = new Byte[fs.Length];
// Uložte soubor ze streamů.
fs.Read(objectData, 0, objectData.Length);
// Zavřete stream.
fs.Close();
```
Tím připravíte soubor Excel pro naše vkládání objektů OLE.
## Krok 9: Přidejte objekt OLE do listu
S připravenými daty nyní můžeme vložit objekt OLE do listu.
```csharp
// Přidejte objekt OLE do listu s obrázkem.
sheet.OleObjects.Add(14, 3, 200, 220, imageData);
// Nastavte vložená data objektu OLE.
sheet.OleObjects[0].ObjectData = objectData;
```
 Tento řádek vytvoří v dokumentu aplikace Excel vložený objekt. Parametry`(14, 3, 200, 220)` určete umístění a velikost vloženého objektu. Upravte tyto hodnoty podle potřeby pro váš konkrétní případ použití.
## Krok 10: Uložte soubor Excel
Nakonec je čas uložit změny do souboru aplikace Excel.
```csharp
// Uložte soubor aplikace Excel
workbook.Save(dataDir + "output.out.xls");
```
Tento řádek uloží sešit s vloženým objektem OLE. Ujistěte se, že používáte název, který dává smysl!
## Závěr
Vkládání objektů OLE do souborů aplikace Excel pomocí Aspose.Cells for .NET je nejen užitečné, ale také přímočaré, jakmile to rozložíte na zvládnutelné kroky. Tento výkonný nástroj vám umožňuje vylepšit vaše dokumenty aplikace Excel a učinit je interaktivními a vizuálně přitažlivými. Ať už jste vývojář, který chce automatizovat sestavy, nebo analytik se zájmem o efektivní prezentaci dat, zvládnutí vkládání OLE může být klíčovým aktivem vaší sady nástrojů.
## FAQ
### Co je objekt OLE?
Objekt OLE je soubor, který lze vložit do dokumentu a umožňuje tak vzájemnou integraci různých aplikací. Příklady zahrnují obrázky, dokumenty aplikace Word a prezentace.
### Mohu používat Aspose.Cells zdarma?
 Aspose.Cells můžete vyzkoušet zdarma stažením zkušební verze dostupné na jejich webu[webové stránky](https://releases.aspose.com/).
### Jaké formáty souborů mohu použít s objekty OLE?
V závislosti na aplikaci můžete používat různé formáty včetně obrázků (JPEG, PNG), dokumentů Word, PDF a dalších.
### Je Aspose.Cells podporován na všech platformách?
Aspose.Cells for .NET je primárně navržen pro platformu .NET. Funkce se však mohou lišit v různých prostředích Windows, Mac nebo cloud.
### Jak mohu získat pomoc, pokud narazím na problémy?
 K podpoře se můžete dostat přes[Aspose fórum](https://forum.aspose.com/c/cells/9) kde vývojáři sdílejí postřehy a řešení.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
