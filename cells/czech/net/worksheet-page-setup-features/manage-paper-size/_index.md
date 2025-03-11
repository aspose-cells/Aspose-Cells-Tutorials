---
title: Správa velikosti papíru listu
linktitle: Správa velikosti papíru listu
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak nastavit vlastní velikosti papíru v Excelu pomocí Aspose.Cells for .NET, pomocí tohoto jednoduchého průvodce krok za krokem.
weight: 16
url: /cs/net/worksheet-page-setup-features/manage-paper-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Správa velikosti papíru listu

## Zavedení
Správa velikosti papíru v excelových listech může být zásadní, zvláště když potřebujete tisknout dokumenty na konkrétní velikosti nebo sdílet soubory v univerzálně formátovaném rozložení. V této příručce vás provedeme pomocí Aspose.Cells for .NET k snadnému nastavení velikosti papíru listu v Excelu. Pokryjeme vše, co potřebujete, od předpokladů a importu balíčků až po kompletní rozpis kódu ve snadno srozumitelných krocích.
## Předpoklady
Než se ponoříte, musíte si připravit několik věcí:
-  Aspose.Cells pro .NET Library: Ujistěte se, že jste si stáhli a nainstalovali[Aspose.Cells for .NET](https://releases.aspose.com/cells/net/). Toto je základní knihovna, kterou budeme používat k programové manipulaci se soubory aplikace Excel.
- Prostředí .NET: Na vašem počítači byste měli mít nainstalovaný .NET. Jakákoli nejnovější verze by měla fungovat.
- Editor nebo IDE: Editor kódu jako Visual Studio, Visual Studio Code nebo JetBrains Rider pro psaní a spouštění vašeho kódu.
- Základní znalost C#: Ačkoli vás provedeme krok za krokem, určitá znalost C# bude užitečná.
## Importujte balíčky
Začněme importem potřebných balíčků pro Aspose.Cells.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Tento řádek importuje základní balíček Aspose.Cells, který poskytuje všechny třídy a metody potřebné pro manipulaci se soubory aplikace Excel.
Nyní se pojďme ponořit do základních kroků! Projdeme si každý řádek kódu a vysvětlíme, co dělá a proč je to nezbytné.
## Krok 1: Nastavte adresář dokumentů
Nejprve potřebujeme místo pro uložení našeho souboru Excel. Nastavení cesty k adresáři zajistí, že se náš soubor uloží na definované místo.
```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
```
 Nahradit`"Your Document Directory"` s cestou, kam chcete soubor uložit. Může to být konkrétní složka ve vašem počítači, např`"C:\\Documents\\ExcelFiles\\"`.
## Krok 2: Inicializujte nový sešit
Musíme vytvořit nový sešit (soubor Excel), kde použijeme změny velikosti papíru.
```csharp
// Vytvoření instance objektu sešitu
Workbook workbook = new Workbook();
```
 The`Workbook` třída představuje soubor Excel. Vytvořením instance této třídy v podstatě vytváříme prázdný sešit aplikace Excel, se kterým můžeme manipulovat, jak chceme.
## Krok 3: Otevřete první pracovní list
Každý sešit obsahuje několik pracovních listů. Zde se dostaneme k prvnímu listu, kde použijeme naše nastavení.
```csharp
// Přístup k prvnímu listu v souboru aplikace Excel
Worksheet worksheet = workbook.Worksheets[0];
```
 The`Worksheets`kolekce obsahuje všechny listy v sešitu. Použitím`workbook.Worksheets[0]`, vybíráme první list. Tento rejstřík můžete upravit a vybrat i jiné listy.
## Krok 4: Nastavte Paper Size na A4
Nyní přichází jádro našeho úkolu – nastavení velikosti papíru na A4.
```csharp
// Nastavení velikosti papíru na A4
worksheet.PageSetup.PaperSize = PaperSizeType.PaperA4;
```
 The`PageSetup` vlastnictvím`Worksheet` třída nám umožňuje přístup k nastavení rozvržení stránky.`PaperSizeType.PaperA4` nastaví velikost stránky na A4, což je jedna ze standardních velikostí papíru běžně používaných po celém světě.
 Chcete použít jiný formát papíru? Aspose.Cells poskytuje různé možnosti jako`PaperSizeType.PaperLetter`, `PaperSizeType.PaperLegal` a další. Stačí vyměnit`PaperA4` s vámi preferovanou velikostí!
## Krok 5: Uložte sešit
Nakonec sešit uložíme s našimi úpravami velikosti papíru.
```csharp
// Uložte sešit.
workbook.Save(dataDir + "ManagePaperSize_out.xls");
```
 The`Save` metoda uloží sešit do zadané cesty. Název souboru`"ManagePaperSize_out.xls"` lze přizpůsobit na základě vašich preferencí. Zde je uložen jako soubor aplikace Excel`.xls` formátu, ale můžete jej uložit`.xlsx` nebo jiné podporované formáty změnou přípony souboru.
## Závěr
tady to máte! Pomocí těchto jednoduchých kroků jste pomocí Aspose.Cells for .NET nastavili velikost papíru excelového listu na A4. Tento přístup je neocenitelný, když potřebujete zajistit, aby si vaše dokumenty zachovaly konzistentní velikost papíru, zejména pro tisk nebo sdílení. 
S Aspose.Cells nejste omezeni pouze na formát A4 – můžete si vybrat ze široké škály velikostí papíru a dále přizpůsobit nastavení stránky, což z něj činí výkonný nástroj pro automatizaci a přizpůsobení dokumentů aplikace Excel.
## FAQ
### Mohu pro každý list nastavit jinou velikost papíru?
 Ano, naprosto! Jednoduše přistupujte ke každému listu jednotlivě a nastavte jedinečnou velikost papíru pomocí`worksheet.PageSetup.PaperSize`.
### Je Aspose.Cells kompatibilní s .NET Core?
Ano, Aspose.Cells je kompatibilní s .NET Framework i .NET Core, takže je všestranný pro různé projekty .NET.
### Jak uložím sešit ve formátu PDF?
 Stačí vyměnit`.Save(dataDir + "ManagePaperSize_out.xls")` s`.Save(dataDir + "ManagePaperSize_out.pdf", SaveFormat.Pdf)`a Aspose.Cells jej uloží jako PDF.
### Mohu upravit další nastavení nastavení stránky pomocí Aspose.Cells?
Ano, Aspose.Cells vám umožňuje upravit mnoho nastavení, jako je orientace, měřítko, okraje a záhlaví/zápatí prostřednictvím`worksheet.PageSetup`.
### Jak získám bezplatnou zkušební verzi Aspose.Cells?
 Můžete si stáhnout bezplatnou zkušební verzi z[Stránka ke stažení Aspose.Cells](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
