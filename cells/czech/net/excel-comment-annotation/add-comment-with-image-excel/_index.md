---
title: Přidejte komentář s obrázkem v Excelu
linktitle: Přidejte komentář s obrázkem v Excelu
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se přidávat komentáře k obrázkům v Excelu pomocí Aspose.Cells for .NET. Vylepšete své tabulky pomocí personalizovaných poznámek.
weight: 10
url: /cs/net/excel-comment-annotation/add-comment-with-image-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidejte komentář s obrázkem v Excelu

## Zavedení
Excel je mocný nástroj pro správu a analýzu dat, ale někdy potřebujete přidat do svých tabulek osobní přístup, že? Možná budete chtít přidat poznámky k datům, poskytnout zpětnou vazbu nebo dokonce přidat trochu vkusu do obrázků. Tady se komentáře hodí! V tomto tutoriálu prozkoumáme, jak přidat komentář s obrázkem v Excelu pomocí knihovny Aspose.Cells pro .NET. Tento přístup může být zvláště užitečný pro vytváření interaktivnějších a vizuálně přitažlivějších tabulek.
## Předpoklady
Než se ponoříme do hrubšího přidávání komentářů s obrázky v Excelu, ujistěte se, že máte vše, co potřebujete, abyste mohli začít:
1. Visual Studio: Ujistěte se, že máte v počítači nainstalované Visual Studio. Zde napíšete a spustíte svůj kód.
2.  Aspose.Cells for .NET: Musíte mít knihovnu Aspose.Cells. Pokud jste jej ještě nenainstalovali, můžete si jej stáhnout z[zde](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: Znalost programování v C# vám pomůže lépe porozumět úryvkům kódu.
4. Soubor obrázku: Připravte si soubor obrázku (jako logo), který chcete vložit do komentáře aplikace Excel. Pro tento tutoriál budeme předpokládat, že máte soubor s názvem`logo.jpg`.
5. .NET Framework: Ujistěte se, že máte nainstalované rozhraní .NET Framework, protože Aspose.Cells vyžaduje, aby fungovalo správně.
Nyní, když máme pokryty naše předpoklady, přejděme ke skutečnému kódování!
## Importujte balíčky
Nejprve musíme naimportovat potřebné balíčky. Ve svém projektu C# nezapomeňte přidat odkaz na knihovnu Aspose.Cells. Můžete to udělat pomocí Správce balíčků NuGet v sadě Visual Studio. Zde je postup:
1. Otevřete Visual Studio.
2. Vytvořte nový projekt nebo otevřete existující.
3. Klepněte pravým tlačítkem myši na svůj projekt v Průzkumníku řešení.
4. Vyberte Spravovat balíčky NuGet.
5. Vyhledejte Aspose.Cells a nainstalujte jej.

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Jakmile máte knihovnu nainstalovanou, můžete začít psát svůj kód. Zde je návod, jak to udělat krok za krokem.
## Krok 1: Nastavte adresář dokumentů
Chcete-li začít, musíme nastavit adresář, kam můžeme ukládat naše soubory Excel. Je to zásadní krok, protože chceme, aby byla naše práce organizovaná.
```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
// Vytvořte adresář, pokud ještě není přítomen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- dataDir: Tato proměnná obsahuje cestu k adresáři dokumentů. Nahradit`"Your Document Directory"` se skutečnou cestou, kam chcete soubor Excel uložit.
- Directory.Exists: Zkontroluje, zda adresář již existuje.
- Directory.CreateDirectory: Pokud adresář neexistuje, vytvoří se tímto.
## Krok 2: Vytvořte sešit
 Dále musíme vytvořit instanci`Workbook` třída. Tato třída představuje sešit aplikace Excel v paměti.
```csharp
//Vytvořte sešit
Workbook workbook = new Workbook();
```
- Sešit: Toto je hlavní třída v Aspose.Cells, která vám umožňuje vytvářet a manipulovat se soubory aplikace Excel. Jeho vytvořením v podstatě vytvoříte nový excelový sešit.
## Krok 3: Získejte sbírku komentářů
Nyní, když máme náš sešit, pojďme se dostat ke kolekci komentářů prvního listu.
```csharp
// Získejte odkaz na kolekci komentářů s prvním listem
CommentCollection comments = workbook.Worksheets[0].Comments;
```
- Pracovní listy[ 0]: Otevře první list v sešitu. Pamatujte, že index je založen na nule`[0]` odkazuje na první list.
- Komentáře: Tato vlastnost nám umožňuje přístup ke kolekci komentářů na tomto listu.
## Krok 4: Přidejte komentář k buňce
Pojďme přidat komentář ke konkrétní buňce. V tomto případě do buňky A1 přidáme komentář.
```csharp
// Přidejte komentář do buňky A1
int commentIndex = comments.Add(0, 0);
Comment comment = comments[commentIndex];
comment.Note = "First note.";
comment.Font.Name = "Times New Roman";
```
- comments.Add(0, 0): Tato metoda přidá komentář do buňky A1 (řádek 0, sloupec 0).
- komentář.Poznámka: Zde nastavujeme text komentáře.
- comment.Font.Name: Toto nastavuje písmo textu komentáře.
## Krok 5: Načtěte obrázek do streamu
 Nyní je čas načíst obrázek, který chceme vložit do našeho komentáře. Použijeme a`MemoryStream` pro uložení obrazových dat.
```csharp
// Nahrajte obrázek do streamu
Bitmap bmp = new Bitmap(dataDir + "logo.jpg");
MemoryStream ms = new MemoryStream();
bmp.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
```
- Bitmap: Tato třída se používá k načtení souboru obrázku. Ujistěte se, že cesta je správná.
- MemoryStream: Toto je stream, který použijeme k uložení obrázku do paměti.
- bmp.Save: Uloží bitmapový obrázek do paměťového toku ve formátu PNG.
## Krok 6: Nastavte Data obrázku na tvar komentáře
Nyní musíme nastavit obrazová data na tvar spojený s komentářem, který jsme vytvořili dříve.
```csharp
// Nastavte obrazová data na tvar spojený s komentářem
comment.CommentShape.Fill.ImageData = ms.ToArray();
```
- comment.CommentShape.Fill.ImageData: Tato vlastnost umožňuje nastavit obrázek pro tvar komentáře. Převádíme`MemoryStream` do bajtového pole pomocí`ms.ToArray()`.
## Krok 7: Uložte sešit
Nakonec uložme náš sešit s komentářem a obrázkem.
```csharp
// Uložte sešit
workbook.Save(dataDir + "book1.out.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```
- workbook.Save: Tato metoda uloží sešit do zadané cesty. Ukládáme to jako soubor XLSX.
## Závěr
A tady to máte! Úspěšně jste přidali komentář s obrázkem do souboru aplikace Excel pomocí Aspose.Cells for .NET. Tato funkce může učinit vaše tabulky informativnější a vizuálně přitažlivější. Ať už přidáváte poznámky k datům, poskytujete zpětnou vazbu nebo jednoduše přidáváte osobní dotek, komentáře s obrázky mohou výrazně zlepšit uživatelský zážitek.
## FAQ
### Mohu přidat více komentářů do stejné buňky?
Ne, Excel neumožňuje více komentářů ve stejné buňce. Pro každou buňku můžete mít pouze jeden komentář.
### Jaké formáty obrázků jsou podporovány?
Aspose.Cells podporuje různé formáty obrázků, včetně PNG, JPEG a BMP.
### Potřebuji licenci k používání Aspose.Cells?
Aspose.Cells nabízí bezplatnou zkušební verzi, ale pro plnou funkčnost si budete muset zakoupit licenci.
### Mohu upravit vzhled komentáře?
Ano, můžete přizpůsobit písmo, velikost a barvu textu komentáře a také můžete změnit tvar a velikost komentáře samotného.
### Kde najdu další dokumentaci na Aspose.Cells?
 Kompletní dokumentaci najdete na Aspose.Cells[zde](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
