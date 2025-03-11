---
title: Získejte seznam písem použitých v tabulce
linktitle: Získejte seznam písem použitých v tabulce
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak načítat a vypisovat písma z tabulek Excelu pomocí Aspose.Cells for .NET pomocí tohoto snadno srozumitelného návodu.
weight: 10
url: /cs/net/working-with-fonts-in-spreadsheets/get-list-of-fonts-used-in-spreadsheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Získejte seznam písem použitých v tabulce

## Zavedení
Přistihli jste se někdy, že procházíte tabulkou Excel a přemýšlíte o písmech používaných v jejích různých buňkách? Možná jste se setkali se starým dokumentem a rádi byste věděli, jaké typografické volby jste zvolili? Tak to máš štěstí! S Aspose.Cells for .NET je to jako mít sadu nástrojů, která vám umožní procházet a odhalovat tajemství písma skrytá ve vašich tabulkách. V této příručce vás provedeme tím, jak snadno načíst seznam všech písem použitých v souboru aplikace Excel. Připoutejte se a pojďme se ponořit do světa tabulek!
## Předpoklady
Než se pustíme do kódu, je několik věcí, které budete potřebovat, abyste mohli začít. Nebojte se, je to opravdu jednoduché. Zde je kontrolní seznam toho, co potřebujete:
1. Visual Studio: Ujistěte se, že máte na počítači nainstalovanou verzi sady Visual Studio. Zde napíšeme náš kód.
2. Aspose.Cells for .NET: Musíte mít k dispozici knihovnu Aspose.Cells. Pokud jste si ji ještě nestáhli, můžete si ji stáhnout z[místo](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: Malá znalost programování v C# vám určitě pomůže snadno se v kódu orientovat.
4. Ukázkový soubor aplikace Excel: K práci budete potřebovat ukázkový soubor aplikace Excel, například „sampleGetFonts.xlsx“. Zde použijeme náš průzkum písem.
Jakmile budete mít vše urovnané, jste připraveni skočit do kódování!
## Importujte balíčky
Abychom to nastartovali, importujme potřebné jmenné prostory. V .NET je import balíčků podobný pozvání správných hostů na večírek – bez nich to prostě nebude fungovat hladce.
Zde je návod, jak importovat Aspose.Cells:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
Pomocí této jednoduché linie zveme základní funkce Aspose.Cells do našeho projektu. Nyní přejdeme k načítání sešitu.
## Krok 1: Nastavte adresář dokumentů
Nejdříve – než se ponoříme do kódu, musíte nastavit cestu k adresáři dokumentů. Zde se nachází váš soubor Excel. 
```csharp
string dataDir = "Your Document Directory";
```
Nahradíte „Your Document Directory“ skutečnou cestou, kde se nachází váš soubor Excel. Berte to tak, že říkáte programu: „Hele, tady jsem schoval svůj soubor Excel; běž se podívat!"
## Krok 2: Načtěte zdrojový sešit
 Je čas načíst soubor Excel. Vytvoříme novou instanci`Workbook` třídy a předejte cestu k souboru. 
```csharp
Workbook wb = new Workbook(dataDir + "sampleGetFonts.xlsx");
```
 co se tu děje? V podstatě otevíráme dveře naší tabulce. The`Workbook` třída nám umožňuje interakci s obsahem souboru Excel. 
## Krok 3: Získejte všechna písma
 Nyní přichází kouzelný okamžik – pojďme skutečně načíst písma! The`GetFonts()` metoda je náš zlatý lístek.
```csharp
Aspose.Cells.Font[] fnts = wb.GetFonts();
```
 Zde žádáme sešit, aby prozradil všechna písma použitá v něm. The`fnts` pole pojme naše poklady.
## Krok 4: Vytiskněte písma
Nakonec vezmeme ty fonty a vytiskneme je. To nám pomůže ověřit, co jsme našli.
```csharp
for (int i = 0; i < fnts.Length; i++)
{
	Console.WriteLine(fnts[i]);
}
```
 Tato smyčka prochází každým fontem v našem`fnts` pole a odesílá je do konzole jeden po druhém. Je to jako předvádět všechny skvělé možnosti typografie, které máte ve svém souboru Excel!
## Závěr
A tady to máte! Pomocí několika řádků kódu jste pomocí Aspose.Cells for .NET úspěšně načetli a vytiskli seznam písem použitých ve vaší excelové tabulce. Nejde jen o písma; jde o pochopení jemností vašich dokumentů, vylepšení vašich prezentací a zvládnutí umění typografie ve vašich tabulkách. Ať už jste vývojář nebo někdo, kdo si prostě rád hraje s Excelem, tento malý úryvek může změnit hru. 
## FAQ
### Musím instalovat Aspose.Cells samostatně?
Ano, musíte si stáhnout a odkazovat na knihovnu ve vašem projektu. 
### Mohu použít Aspose.Cells pro jiné formáty?
Absolutně! Aspose.Cells pracuje s více formáty aplikace Excel, jako jsou XLSX, XLS a CSV.
### Je k dispozici bezplatná zkušební verze?
 Ano, můžete získat bezplatnou zkušební verzi z[odkaz ke stažení](https://releases.aspose.com/).
### Jak mohu získat technickou podporu?
 Pokud potřebujete pomoc,[Aspose fórum podpory](https://forum.aspose.com/c/cells/9) je skvělým zdrojem.
### Je Aspose.Cells kompatibilní s .NET Core?
Ano, Aspose.Cells je kompatibilní i s projekty .NET Core.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
