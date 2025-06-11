---
"description": "tomto komplexním tutoriálu se naučíte, jak spravovat externí připojení v souborech XLSB pomocí Aspose.Cells pro .NET."
"linktitle": "Čtení a zápis externího připojení souboru XLSB"
"second_title": "Referenční příručka k Aspose.Cells pro .NET API"
"title": "Čtení a zápis externího připojení souboru XLSB"
"url": "/cs/net/excel-workbook/read-and-write-external-connection-of-xlsb-file/"
"weight": 130
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Čtení a zápis externího připojení souboru XLSB

## Zavedení

Ahoj, nadšenci do Excelu! Jste připraveni ponořit se do fascinujícího světa souborů XLSB a externích připojení? Pokud jste někdy s Excelem pracovali, víte, jak mocný a všestranný může být, ale někdy má své zvláštnosti – zejména při práci s připojením k externím databázím. A v tom případě přichází na pomoc Aspose.Cells pro .NET! Tato šikovná knihovna vám umožňuje snadno manipulovat s excelovými soubory. V tomto článku vás provedeme podrobným návodem, jak číst a zapisovat externí připojení v souboru XLSB.

## Předpoklady

Než začneme, zde je několik věcí, které budete potřebovat:

1. Základní znalost jazyka C#: Znalost programovacího jazyka C# vám nesmírně pomůže. Pokud umíte psát kód v jazyce C#, můžete začít!
2. Aspose.Cells pro .NET: Tuto knihovnu budete muset mít nainstalovanou ve svém vývojovém prostředí. Pokud jste tak ještě neučinili, můžete si ji snadno stáhnout. [zde](https://releases.aspose.com/cells/net/). 
3. IDE: Budete potřebovat editor kódu nebo integrované vývojové prostředí (IDE), jako je Visual Studio. 
4. Ukázkový soubor XLSB: Budeme pracovat s ukázkovým souborem XLSB, který obsahuje externí připojení. Můžete si vytvořit vlastní nebo si ukázky stáhnout online. 

Jakmile budete mít všechny tyto předpoklady splněny, můžeme se pustit do kódování!

## Importovat balíčky

Nejprve si do našeho projektu importujeme potřebné balíčky. Ujistěte se, že jste do projektu přidali odkaz na Aspose.Cells. Zde je návod, jak to udělat v C#:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Tyto importy vám poskytují přístup k funkcím, které budete potřebovat k manipulaci se soubory aplikace Excel a jejich propojením.

## Krok 1: Nastavení adresářů

Než budete pracovat se souborem XLSB, je třeba nastavit zdrojový a výstupní adresář. Tento krok je nezbytný pro udržení pořádku v souborech.

```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory";
// Výstupní adresář
string outputDir = "Your Output Directory";
```

V tomto úryvku kódu `"Your Document Directory"` a `"Your Document Directory"` Předpokládá se, že načtou příslušné cesty ke místům, kde budou umístěny vaše vstupní a výstupní soubory. Pokud chcete, můžete tyto metody nahradit pevně zakódovanými cestami.

## Krok 2: Načtěte soubor XLSB

Nyní je čas načíst soubor aplikace Excel do objektu Workbook. To vám dává možnost manipulovat s daty uvnitř.

```csharp
// Načtěte zdrojový soubor Excel XLSB
Workbook wb = new Workbook(sourceDir + "sampleExternalConnection_XLSB.xlsb");
```

Jen se ujistěte, že váš soubor XLSB se nachází v zadaném adresáři. `sourceDir`Pokud je cesta správná, bude váš sešit připraven k manipulaci!

## Krok 3: Přístup k externím připojením

Po načtení sešitu můžete přistupovat k jeho externím připojením. V našem případě načteme první připojení k databázi.

```csharp
// Přečtěte si první externí připojení, které je ve skutečnosti DB připojením.
Aspose.Cells.ExternalConnections.DBConnection dbCon = wb.DataConnections[0] as Aspose.Cells.ExternalConnections.DBConnection;
```

Zde, `DataConnections[0]` odkazuje na první připojení v sešitu. Přetypujeme ho jako `DBConnection` typ pro další manipulaci.

## Krok 4: Extrahování informací o připojení

Nyní, když máte přístup k databázovému připojení, pojďme extrahovat a vypsat jeho podrobnosti do konzole. To nám pomůže přesně vidět, s čím pracujeme.

```csharp
// Vytiskněte název, příkaz a informace o připojení DB-Connection
Console.WriteLine("Connection Name: " + dbCon.Name);
Console.WriteLine("Command: " + dbCon.Command);
Console.WriteLine("Connection Info: " + dbCon.ConnectionInfo);
```

Tento krok vám umožní ověřit aktuální stav vašeho externího připojení. V konzoli se zobrazí název připojení, použitý příkaz a informace o připojení.

## Krok 5: Úprava připojení

Někdy stačí změnit název, aby bylo vše srozumitelnější nebo aby odpovídalo novým konvencím pojmenování. Změňme stávající název připojení na něco relevantnějšího.

```csharp
// Změnit název připojení
dbCon.Name = "NewCust";
```

Tento řádek kódu efektivně přejmenuje vaše připojení z původního názvu na „NewCust“. Je to jednoduchá, ale účinná změna!

## Krok 6: Uložte změny

Po provedení úprav je budete chtít uložit změny zpět do souboru XLSB. Postupujte takto:

```csharp
// Uložení souboru Excel XLSB
wb.Save(outputDir + "outputExternalConnection_XLSB.xlsb");
```

Tento řádek kódu uloží aktualizovaný sešit a zachová všechny provedené změny, včetně nového názvu připojení.

## Krok 7: Potvrzení provedení

Nakonec si ověřme, že vše proběhlo hladce. Jednoduchá zpráva na konci to objasní.

```csharp
Console.WriteLine("ReadAndWriteExternalConnectionOfXLSBFile executed successfully.\r\n");
```

Tato zpráva vás ujistí, že váš kód proběhl úspěšně a všechny změny byly uloženy podle očekávání.

## Závěr

tady to máte! Úspěšně jste se naučili, jak číst a zapisovat externí připojení v souborech XLSB pomocí Aspose.Cells pro .NET. Dodržováním těchto kroků můžete efektivně spravovat datová připojení v Excelu, což vám práci s Excelem výrazně zjednoduší a zmírní její frustraci. Nezapomeňte, že ať už pracujete s rozsáhlými datovými sadami nebo jen organizujete informace, Aspose.Cells má nástroje, které potřebujete.

## Často kladené otázky

### Co je soubor XLSB?  
Soubor XLSB je binární formát souboru aplikace Excel, který ukládá data tabulky v binárním formátu, díky čemuž je kompaktnější a rychlejší otevírání.

### Jak nainstaluji Aspose.Cells pro .NET?  
Můžete si jej snadno stáhnout z webových stránek Aspose. [zde](https://releases.aspose.com/cells/net/).

### Mohu používat Aspose.Cells zdarma?  
Ano! Můžete začít s bezplatnou zkušební verzí, která je k dispozici [zde](https://releases.aspose.com/).

### Podporuje Aspose.Cells i jiné formáty souborů?  
Rozhodně! Aspose.Cells podporuje různé formáty souborů, včetně XLSX, CSV a dalších.

### Kam mohu hledat pomoc, pokud narazím na problémy?  
Podporu můžete získat na fórech Aspose [zde](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}