---
title: Export vlastností sešitu dokumentu a listu v HTML
linktitle: Export vlastností sešitu dokumentu a listu v HTML
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se exportovat vlastnosti dokumentu, sešitu a listu aplikace Excel do HTML pomocí Aspose.Cells for .NET. Včetně jednoduchého průvodce krok za krokem.
weight: 11
url: /cs/net/exporting-excel-to-html-with-advanced-options/exporting-document-workbook-and-worksheet-properties/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export vlastností sešitu dokumentu a listu v HTML

## Zavedení

Pokud jde o práci s tabulkami, často se přistihneme, že potřebujeme převést soubory aplikace Excel do různých formátů pro sdílení, uchování nebo prezentaci. Jedním z běžných úkolů je export vlastností sešitu a listu do formátu HTML. V tomto článku vás provedeme tím, jak toho dosáhnout pomocí Aspose.Cells for .NET. Nebojte se, pokud jste v kódování nebo v knihovně Aspose nováčkem; rozebereme to krok za krokem, aby bylo snadné sledovat!

## Předpoklady

Než se ponoříme do kódu, ujistěte se, že máte vše, co potřebujete, abyste mohli začít:

1. .NET Framework: Ujistěte se, že vaše vývojové prostředí je nastaveno na .NET Framework. Aspose.Cells je kompatibilní s .NET Framework verzemi až do 4.8.
   
2.  Aspose.Cells pro .NET: Musíte mít nainstalovaný Aspose.Cells. Knihovnu si můžete stáhnout z[stránka ke stažení](https://releases.aspose.com/cells/net/). 

3. IDE: Vhodné integrované vývojové prostředí (IDE), jako je Visual Studio, vám zjednoduší práci s kódováním.

4.  Ukázkový soubor aplikace Excel: Pro účely testování se ujistěte, že máte soubor aplikace Excel s názvem`sampleExportDocumentWorkbookAndWorksheetPropertiesInHTML.xlsx` ve vašem pracovním adresáři.

## Importujte balíčky

Nyní, když jsme pokryli předpoklady, začněme importem potřebných balíčků do našeho projektu C#. Můžete to udělat takto:

### Vytvořit nový projekt

- Otevřete své IDE a vytvořte nový projekt C#. Můžete si vybrat konzolovou aplikaci, která je pro spouštění tohoto typu úloh ideální.

### Přidejte balíček NuGet Aspose.Cells

Chcete-li přidat balíček Aspose.Cells, postupujte takto:

- Klikněte pravým tlačítkem na svůj projekt v Průzkumníku řešení a vyberte „Spravovat balíčky NuGet“.
- Ve Správci balíčků NuGet vyhledejte „Aspose.Cells“ a nainstalujte jej.
- Tento balíček poskytne potřebné třídy a metody pro práci se soubory aplikace Excel.

### Import jmenných prostorů

V horní části hlavního souboru programu se ujistěte, že obsahuje následující jmenné prostory:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

 To nám umožní přístup k`Workbook` a`HtmlSaveOptions` třídy, které použijeme v našem příkladu.

Nyní, když jste vše nastavili, pojďme si celý proces rozdělit do jednoduchých kroků.

## Krok 1: Nastavte adresáře souborů

Nejprve musíme určit, kde budou umístěny naše vstupní a výstupní soubory. Ve svém kódu inicializujte adresáře takto:

```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory/";  // Aktualizujte svou skutečnou cestou

// Výstupní adresář
string outputDir = "Your Document Directory/";  // Aktualizujte svou skutečnou cestou
```

- Zdrojový adresář: Zde je váš vstupní soubor Excel (`sampleExportDocumentWorkbookAndWorksheetPropertiesInHTML.xlsx`) je uložen.
- Výstupní adresář: Toto je cesta, kam chcete uložit výstupní soubor HTML.

## Krok 2: Načtěte soubor Excel

 Nyní musíme načíst soubor Excel pomocí`Workbook` třída:

```csharp
// Načtěte ukázkový soubor Excel
Workbook workbook = new Workbook(sourceDir + "sampleExportDocumentWorkbookAndWorksheetPropertiesInHTML.xlsx");
```

-  Instance sešitu: The`Workbook` konstruktor vezme cestu k souboru Excel a vytvoří novou instanci, se kterou můžete manipulovat.

## Krok 3: Nastavte možnosti uložení HTML

Dále určíme, jak chceme uložit data aplikace Excel do HTML:

```csharp
// Zadejte možnosti uložení HTML
HtmlSaveOptions options = new HtmlSaveOptions();

// Zabránit exportu vlastností dokumentu, sešitu a listu
options.ExportDocumentProperties = false;
options.ExportWorkbookProperties = false;
options.ExportWorksheetProperties = false;
```

- HtmlSaveOptions: Tato třída pomáhá spravovat, jak bude soubor Excel převeden do HTML.
-  Nastavili jsme několik možností`false`protože nechceme zahrnout vlastnosti sešitu a listu do našeho výstupu HTML.

## Krok 4: Exportujte vše do HTML

Nyní jsme připraveni uložit náš sešit do formátu HTML:

```csharp
// Exportujte soubor Excel do Html pomocí Html Uložit možnosti
workbook.Save(outputDir + "outputExportDocumentWorkbookAndWorksheetPropertiesInHTML.html", options);
```

-  The`Save` metoda má dva parametry: cestu k souboru pro výstupní soubor HTML a možnosti, které jsme nastavili. Spuštěním tohoto vytvoříte soubor HTML v určeném výstupním adresáři.

## Krok 5: Zpětná vazba konzole

Nakonec nám poskytněte zpětnou vazbu v konzole, abyste věděli, že proces byl úspěšně dokončen:

```csharp
Console.WriteLine("ExportDocumentWorkbookAndWorksheetPropertiesInHTML executed successfully.");
```

## Závěr

právě tak jste úspěšně exportovali vlastnosti sešitu a listu do HTML pomocí Aspose.Cells for .NET! Prošli jste jednoduchým procesem, od nastavení prostředí až po export dat aplikace Excel. Krása používání knihoven, jako je Aspose.Cells, spočívá v tom, že zjednodušuje složité úkoly a usnadňuje vývojářům život. Nyní můžete své tabulky sdílet šířeji pomocí HTML, stejně jako nechat svět nahlédnout do vašich sešitů, aniž byste jim dali celou knihu.

## FAQ

### Jak nainstaluji Aspose.Cells pro .NET?  
Knihovnu Aspose.Cells můžete nainstalovat prostřednictvím NuGet ve vašem projektu Visual Studio prostřednictvím Správce balíčků NuGet.

### Mohu přizpůsobit výstup HTML?  
 Ano, Aspose.Cells nabízí různé možnosti v`HtmlSaveOptions` upravit způsob převodu souboru Excel do HTML.

### Existuje způsob, jak zahrnout vlastnosti dokumentu do exportu HTML?  
 Můžete nastavit`ExportDocumentProperties`, `ExportWorkbookProperties` a`ExportWorksheetProperties` na`true` v`HtmlSaveOptions` pokud je chcete zahrnout.

### Do jakých formátů mohu exportovat svůj soubor Excel kromě HTML?  
Aspose.Cells podporuje různé formáty včetně PDF, CSV, XML a dalších.

### Je k dispozici zkušební verze?  
 Ano, můžete získat bezplatnou zkušební verzi Aspose.Cells z[webové stránky](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
