---
title: Změňte zdrojová data kontingenční tabulky programově v .NET
linktitle: Změňte zdrojová data kontingenční tabulky programově v .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak změnit zdrojová data kontingenční tabulky programově pomocí Aspose.Cells for .NET s naším komplexním výukovým programem krok za krokem.
weight: 10
url: /cs/net/creating-and-configuring-pivot-tables/changing-source-data/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Změňte zdrojová data kontingenční tabulky programově v .NET

## Zavedení
Ve světě analýzy dat jen málo nástrojů září tak jasně jako Microsoft Excel. Každý den je nespočet uživatelů závislý na Excelu při správě a analýze dat, ale v zákulisí je to mnohem složitější než pouhé klikání a přetahování. Pokud jste někdy chtěli programově manipulovat se soubory Excelu – konkrétně měnit zdrojová data kontingenční tabulky – jste na správném místě! V této příručce prozkoumáme, jak toho můžete dosáhnout pomocí Aspose.Cells pro .NET. Ať už jste ostřílený vývojář nebo jen ponoříte prsty do moře programování, najdete tento tutoriál plný cenných informací, které lze snadno sledovat.
## Předpoklady
Než se pustíme do naší cesty ke změně zdrojových dat kontingenční tabulky, ujistěte se, že máte vše nastaveno a připraveno:
1. Visual Studio: Ujistěte se, že máte nainstalovanou kopii Microsoft Visual Studio, protože zde budeme psát náš kód.
2. Knihovna Aspose.Cells: Budete muset mít staženou knihovnu Aspose.Cells a odkazovat na ni ve svém projektu. Můžete si jej stáhnout[zde](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: I když je tento tutoriál zjednodušený, znalost C# vám pomůže lépe porozumět kódu.
4. Soubor aplikace Excel: Měli byste mít vzorový soubor aplikace Excel (například „Book1.xlsx“) obsahující kontingenční tabulku, se kterou můžeme manipulovat.
Dobře, s těmito předpoklady můžeme pokračovat v importu potřebných balíčků a získat kódování!
## Importujte balíčky
První věci – importujme balíčky, které budeme potřebovat. Otevřete svůj projekt C# v aplikaci Visual Studio a přidejte následující pomocí direktiv v horní části souboru kódu:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Tyto jmenné prostory vám umožní přístup k základním třídám potřebným pro práci se soubory Excel a manipulaci s jejich obsahem pomocí Aspose.Cells.

Nyní si tento proces rozdělíme na zvládnutelné kroky. Projdeme si otevřením souboru aplikace Excel, úpravou listu, změnou zdroje dat kontingenční tabulky a uložením výsledků.
## Krok 1: Definujte svůj adresář dokumentů
 Nejprve musíte určit, kde se váš soubor Excel nachází. Upravte`dataDir` proměnná, aby ukazovala na složku obsahující váš "Book1.xlsx".
```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
```
Tento řádek nastavuje adresář, kde je uložen váš soubor Excel, což usnadňuje pozdější přístup.
## Krok 2: Zadejte cestu vstupu
Dále vytvořte řetězec, který určí úplnou cestu k vašemu vstupnímu souboru Excel:
```csharp
string InputPath = dataDir + "Book1.xlsx";
```
To pomáhá zjednodušit přístup k souborům; nebudete muset psát stejnou cestu několikrát v celém kódu.
## Krok 3: Vytvořte stream souborů
 Nyní je čas otevřít soubor Excel. Vytvoříme a`FileStream` který vám umožní číst obsah souboru Excel:
```csharp
// Vytvoření datového proudu souboru obsahujícího soubor Excel, který se má otevřít
FileStream fstream = new FileStream(InputPath, FileMode.Open);
```
Tento řádek otevře soubor v režimu čtení, což nám umožní přístup k jeho datům.
## Krok 4: Načtěte sešit
Když je datový proud souborů na místě, dalším krokem je načtení sešitu:
```csharp
// Otevření souboru aplikace Excel prostřednictvím datového proudu souborů
Workbook workbook = new Workbook(fstream);
```
 Tento příkaz vezme váš soubor Excel a načte jej do a`Workbook` objekt. Po načtení můžete se souborem manipulovat podle potřeby.
## Krok 5: Otevřete sešit
Čas ponořit se do specifik. Získáme přístup k prvnímu listu v sešitu:
```csharp
// Přístup k prvnímu listu v souboru aplikace Excel
Worksheet worksheet = workbook.Worksheets[0];
```
To vám dává přímý přístup k datům v prvním listu, což usnadňuje úpravy.
## Krok 6: Vyplňte nová data
Dále chceme do buněk vložit nová data. V tomto příkladu přidáme některá ukázková data:
```csharp
// Vyplnění nových dat do buněk listu
worksheet.Cells["A9"].PutValue("Golf");
worksheet.Cells["B9"].PutValue("Qtr4");
worksheet.Cells["C9"].PutValue(7000);
```
 Zde vkládáme hodnoty „Golf“, „Qtr4“ a`7000` do konkrétních buněk. Tyto hodnoty můžete změnit na cokoliv, co vyhovuje vašim potřebám.
## Krok 7: Změňte pojmenovaný rozsah
Nyní změníme pojmenovaný rozsah, na který kontingenční tabulka odkazuje. To zahrnuje vytvoření nebo aktualizaci rozsahu:
```csharp
// Změna pojmenovaného rozsahu "DataSource"
Range range = worksheet.Cells.CreateRange(0,0,9,3);
range.Name = "DataSource";
```
Definováním nového rozsahu zajistíme, že kontingenční tabulka použije tato nová data při aktualizaci.
## Krok 8: Uložte upravený soubor Excel
Po všech změnách je zásadní uložit si práci! Uložíme upravený sešit:
```csharp
// Uložení upraveného souboru Excel
workbook.Save(dataDir + "output.xls");
```
Tento příkaz uloží sešit do nového souboru, takže svůj původní soubor nepřepíšete, pokud nechcete!
## Krok 9: Zavřete Stream souborů
Nakonec je nezbytné zavřít datový proud souborů, aby se uvolnily všechny zdroje, které používáte:
```csharp
// Zavřením datového proudu souborů uvolníte všechny zdroje
fstream.Close();
```
Tento krok zajistí, že vaše aplikace nepropustí paměť a zůstane efektivní.
## Závěr
Gratuluji! Právě jste úspěšně změnili zdrojová data kontingenční tabulky programově v .NET pomocí Aspose.Cells. Tato funkce otevírá mnoho možností pro automatizaci úloh aplikace Excel a zlepšení vašeho pracovního postupu. Ať už aktualizujete finanční výkazy, sledujete údaje o prodeji nebo si dokonce jen hrajete s datovými sadami, možnost dělat to programově vám může ušetřit spoustu času a snížit riziko chyb.

## FAQ
### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna .NET pro práci se soubory aplikace Excel, která uživatelům umožňuje programově vytvářet, upravovat a manipulovat s dokumenty aplikace Excel.
### Mohu pomocí této metody změnit zdrojová data existujících kontingenčních tabulek?
Absolutně! Tato metoda umožňuje aktualizovat zdroj dat pro existující kontingenční tabulky v sešitu aplikace Excel.
### Musím mít nainstalovaný Office, abych mohl používat Aspose.Cells?
Ne! Aspose.Cells je samostatná knihovna, což znamená, že pro práci se soubory aplikace Excel nepotřebujete nainstalovaný Microsoft Office.
### Je Aspose.Cells zdarma k použití?
Aspose.Cells nabízí bezplatnou zkušební verzi, ale pro plnou funkčnost si budete muset zakoupit licenci. Podrobnosti najdete[zde](https://purchase.aspose.com/buy).
### Kde najdu další příklady a podporu?
 Další příklady a podporu naleznete na[Dokumentace Aspose.Cells](https://reference.aspose.com/cells/net/) a jejich komunitním fóru[zde](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
