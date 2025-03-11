---
title: Čtení a zápis externího připojení souboru XLSB
linktitle: Čtení a zápis externího připojení souboru XLSB
second_title: Aspose.Cells for .NET API Reference
description: V tomto komplexním kurzu se dozvíte, jak spravovat externí připojení v souborech XLSB pomocí Aspose.Cells for .NET.
weight: 130
url: /cs/net/excel-workbook/read-and-write-external-connection-of-xlsb-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Čtení a zápis externího připojení souboru XLSB

## Zavedení

Ahoj, nadšenci Excelu! Jste připraveni ponořit se do fascinujícího světa souborů XLSB a externích připojení? Pokud jste někdy pracovali s Excelem, víte, jak výkonný a všestranný může být, ale někdy přichází se svými zvláštnostmi – zejména při práci s připojeními k externím databázím. To je místo, kde Aspose.Cells for .NET přichází na pomoc! Tato šikovná knihovna vám umožňuje manipulovat se soubory Excelu přímočarým způsobem. V tomto článku vás provedeme podrobným průvodcem, jak číst a zapisovat externí připojení do souboru XLSB.

## Předpoklady

Než začneme, zde je několik věcí, které budete potřebovat:

1. Základní znalost C#: Znalost programovacího jazyka C# vám nesmírně pomůže. Pokud vám vyhovuje psaní kódu C#, můžete začít!
2.  Aspose.Cells for .NET: Tuto knihovnu musíte mít nainstalovanou ve svém vývojovém prostředí. Pokud jste to ještě neudělali, můžete si jej snadno stáhnout[zde](https://releases.aspose.com/cells/net/). 
3. IDE: Budete potřebovat editor kódu nebo integrované vývojové prostředí (IDE), jako je Visual Studio. 
4. Ukázkový soubor XLSB: Budeme pracovat s ukázkovým souborem XLSB, který obsahuje externí připojení. Můžete si vytvořit vlastní nebo stáhnout ukázky online. 

Jakmile splníte všechny tyto předpoklady, jsme připraveni skočit do kódu!

## Importujte balíčky

Pro začátek importujme potřebné balíčky do našeho projektu. Ujistěte se, že jste do projektu přidali odkaz na Aspose.Cells. Zde je návod, jak to udělat v C#:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Tyto importy vám umožní přístup k funkcím, které budete potřebovat k manipulaci se soubory Excel a jejich připojeními.

## Krok 1: Nastavení adresářů

Než začnete pracovat se souborem XLSB, musíte nastavit zdrojový a výstupní adresář. Tento krok je nezbytný pro udržení pořádku v souborech.

```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory";
// Výstupní adresář
string outputDir = "Your Output Directory";
```

 V tomto fragmentu kódu`"Your Document Directory"` a`"Your Document Directory"` předpokládá se, že načítají příslušné cesty, kde budou umístěny vaše vstupní a výstupní soubory. Pokud chcete, můžete tyto metody nahradit pevně zakódovanými cestami.

## Krok 2: Načtěte soubor XLSB

Nyní je čas načíst soubor aplikace Excel do objektu Sešit. To vám dává možnost manipulovat s daty uvnitř.

```csharp
// Načtěte zdrojový soubor Excel Xlsb
Workbook wb = new Workbook(sourceDir + "sampleExternalConnection_XLSB.xlsb");
```

 Jen se ujistěte, že váš soubor XLSB je umístěn v zadaném místě`sourceDir`. Pokud je cesta správná, váš sešit bude připraven k manipulaci!

## Krok 3: Přístup k externím připojením

S načteným sešitem máte přístup k jeho externím připojením. V našem případě načteme první připojení k databázi.

```csharp
// Přečtěte si první externí připojení, které je ve skutečnosti DB-Connection
Aspose.Cells.ExternalConnections.DBConnection dbCon = wb.DataConnections[0] as Aspose.Cells.ExternalConnections.DBConnection;
```

 Zde,`DataConnections[0]` odkazuje na první připojení v sešitu. Odléváme to jako a`DBConnection` typ pro další manipulaci.

## Krok 4: Extrahujte informace o připojení

Nyní, když máte přístup k připojení k databázi, pojďme extrahovat a vytisknout jeho podrobnosti do konzoly. To nám pomůže přesně vidět, s čím pracujeme.

```csharp
// Vytiskněte název, příkaz a informace o připojení DB-Connection
Console.WriteLine("Connection Name: " + dbCon.Name);
Console.WriteLine("Command: " + dbCon.Command);
Console.WriteLine("Connection Info: " + dbCon.ConnectionInfo);
```

Tento krok vám umožní ověřit aktuální stav vašeho externího připojení. Uvidíte název připojení, použitý příkaz a informace o připojení vytištěné na konzoli.

## Krok 5: Upravte připojení

Někdy je změna názvu vše, co je potřeba k tomu, aby byly věci jasnější nebo aby odpovídaly novým konvencím pojmenování. Změňme stávající název připojení na něco relevantnějšího.

```csharp
// Upravte název připojení
dbCon.Name = "NewCust";
```

Tento řádek kódu efektivně přejmenuje vaše připojení z původního názvu na "NewCust". Je to jednoduchá, ale působivá změna!

## Krok 6: Uložte změny

Po provedení úprav budete chtít uložit změny zpět do souboru XLSB. Jak na to:

```csharp
// Uložte soubor Excel Xlsb
wb.Save(outputDir + "outputExternalConnection_XLSB.xlsb");
```

Tento řádek kódu uloží váš aktualizovaný sešit a zachová všechny vaše změny, včetně nového názvu připojení.

## Krok 7: Potvrďte provedení

Nakonec si pojďme potvrdit, že vše fungovalo hladce. Jednoduchá zpráva na konci to objasní.

```csharp
Console.WriteLine("ReadAndWriteExternalConnectionOfXLSBFile executed successfully.\r\n");
```

Tato zpráva vás ujistí, že váš kód byl úspěšně spuštěn a všechny změny byly uloženy podle očekávání.

## Závěr

A tady to máte! Úspěšně jste se naučili číst a zapisovat externí připojení v souborech XLSB pomocí Aspose.Cells for .NET. Pomocí těchto kroků můžete efektivně spravovat svá datová připojení aplikace Excel, díky čemuž bude vaše práce s Excelem mnohem efektivnější a méně frustrující. Pamatujte, že ať už pracujete s rozsáhlými datovými sadami nebo jednoduše organizujete své informace, Aspose.Cells má nástroje, které potřebujete.

## FAQ

### Co je soubor XLSB?  
Soubor XLSB je binární formát souboru aplikace Excel, který ukládá data tabulky v binárním formátu, takže je kompaktnější a rychleji se otevírá.

### Jak nainstaluji Aspose.Cells pro .NET?  
 Můžete si jej snadno stáhnout z webu Aspose[zde](https://releases.aspose.com/cells/net/).

### Mohu používat Aspose.Cells zdarma?  
 Ano! Můžete začít s bezplatnou zkušební verzí, která je k dispozici[zde](https://releases.aspose.com/).

### Podporuje Aspose.Cells jiné formáty souborů?  
Absolutně! Aspose.Cells podporuje různé formáty souborů, včetně XLSX, CSV a dalších.

### Kde mohu vyhledat pomoc, pokud narazím na problémy?  
Podporu můžete získat na fórech Aspose[zde](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
