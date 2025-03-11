---
title: Nastavte pořadí stránek aplikace Excel
linktitle: Nastavte pořadí stránek aplikace Excel
second_title: Aspose.Cells for .NET API Reference
description: Pomocí Aspose.Cells for .NET můžete bez námahy ovládat pořadí tisku stránek Excelu. V tomto podrobném průvodci se dozvíte, jak přizpůsobit pracovní postup.
weight: 120
url: /cs/net/excel-page-setup/set-excel-page-order/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nastavte pořadí stránek aplikace Excel

## Zavedení

Přistihli jste se někdy, že procházíte neuspořádanou změtí stránek v souboru aplikace Excel? Víte, co tím myslím – tištěný výstup nevypadá tak, jak jste si představovali. Co kdybych vám řekl, že můžete ovládat pořadí, ve kterém se vaše stránky tisknou? To je pravda! S Aspose.Cells for .NET můžete snadno nastavit pořadí stránek sešitů aplikace Excel, aby nejen vypadaly profesionálně, ale aby byly také snadno čitelné. Tento výukový program vás provede kroky potřebnými k nastavení pořadí stránek aplikace Excel a zajistí, že vaše tištěné dokumenty budou zobrazovat informace jasným a organizovaným způsobem.

## Předpoklady

Než se ponoříte do kódu, měli byste mít připraveno několik věcí:

- Prostředí .NET: Ujistěte se, že máte na svém počítači nastaveno prostředí .NET. Ať už je to .NET Framework nebo .NET Core, mělo by to fungovat hladce.
-  Knihovna Aspose.Cells: Budete potřebovat knihovnu Aspose.Cells for .NET. Nebojte se – začít je snadné! Můžete[stáhněte si jej zde](https://releases.aspose.com/cells/net/) nebo získejte bezplatnou zkušební verzi[zde](https://releases.aspose.com/).
- Základní znalosti programování: Základní znalost programování v C# vám pomůže lépe porozumět pojmům.

## Importujte balíčky

Nejprve musíte importovat potřebné balíčky do vaší aplikace C#. Postupujte takto:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Tento řádek kódu vám umožňuje využít výkonné funkce nabízené Aspose.Cells ve vašem projektu a poskytuje vám nástroje potřebné k bezproblémové manipulaci se soubory aplikace Excel.

Nyní, když jsme položili základy, pojďme rozdělit nastavení pořadí stránek aplikace Excel do zvládnutelných kroků!

## Krok 1: Zadejte svůj adresář dokumentů

Než se pustíte do vytváření sešitu, musíte určit, kam se má výstupní soubor uložit. To vám dává místo, kde můžete mít přehled o své práci. 

Proměnnou, která ukazuje na váš adresář dokumentů, nastavíte takto:

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

 V tomto řádku vyměňte`"YOUR DOCUMENT DIRECTORY"` s cestou, kam chcete soubor uložit. Pokud například chcete uložit soubor do složky s názvem „ExcelFiles“ na ploše, může vypadat nějak takto:

```csharp
string dataDir = @"C:\Users\YourUsername\Desktop\ExcelFiles\";
```

## Krok 2: Vytvořte nový sešit


Dále musíme vytvořit nový objekt sešitu. Tento objekt bude sloužit jako vaše plátno, se kterým budete pracovat.

Zde je návod, jak vytvořit sešit:

```csharp
Workbook workbook = new Workbook();
```

 Tento řádek inicializuje novou instanci souboru`Workbook` třídy, což je základní prvek pro práci se soubory Excel v Aspose.Cells.

## Krok 3: Otevřete Nastavení stránky


 Nyní musíme získat přístup k`PageSetup` vlastnost pracovního listu. To vám umožní upravit způsob tisku stránek.

 Pro přístup`PageSetup`, použijte následující kód:

```csharp
PageSetup pageSetup = workbook.Worksheets[0].PageSetup;
```

 Zde,`workbook.Worksheets[0]` odkazuje na první list ve vašem sešitu. The`PageSetup` vlastnost vám poskytne kontrolu nad nastavením stránkování vašeho listu.

## Krok 4: Nastavte pořadí tisku


 s`PageSetup`objekt, je čas sdělit Excelu, jak chcete stránky vytisknout. Máte možnost nastavit pořadí buď jako „Přes, pak dolů“ nebo „Dolů a potom přes“.

Zde je kód pro nastavení pořadí tisku:

```csharp
pageSetup.Order = PrintOrderType.OverThenDown;
```

 V tomto příkladu výběr`PrintOrderType.OverThenDown` znamená, že Excel vytiskne stránky počínaje shora dolů pro každý sloupec a poté přejde na další sloupec. Mohli jste si také vybrat`PrintOrderType.DownThenOver` pokud dáváte přednost jinému uspořádání.

## Krok 5: Uložte sešit


Konečně je čas uložit si práci! Tento krok zajistí, že všechna vaše přizpůsobení budou uložena pro budoucí použití.

Sešit můžete uložit pomocí tohoto kódu:

```csharp
workbook.Save(dataDir + "SetPageOrder_out.xls");
```

 Ujistěte se, že jste uvedli název souboru, v tomto případě „SetPageOrder_out.xls“, a ověřte, že`dataDir` proměnná správně ukazuje na zamýšlený adresář.

## Závěr

Gratuluji! Právě jste se naučili, jak nastavit pořadí stránek v Excelu pomocí Aspose.Cells for .NET. Pomocí několika řádků kódu máte možnost přizpůsobit si způsob tisku dokumentů aplikace Excel, aby se daly snadno sledovat a byly vizuálně přitažlivé. Tato funkce se hodí zejména při práci s velkými datovými sadami, kde může pořadí stránek výrazně ovlivnit čitelnost. 

## FAQ

### Co je Aspose.Cells?
Aspose.Cells je knihovna .NET, která poskytuje funkce pro manipulaci s tabulkami aplikace Microsoft Excel a umožňuje vývojářům vytvářet, upravovat a převádět soubory aplikace Excel programově.

### Jak získám dočasnou licenci pro Aspose.Cells?
 O dočasnou licenci můžete požádat na adrese[Stránka dočasné licence](https://purchase.aspose.com/temporary-license/) na webu Aspose.

### Mohu změnit pořadí stránek pro více listů?
 Ano! Ke každému listu máte přístup`PageSetup` a individuálně nakonfigurujte pořadí stránek.

### Jaké jsou možnosti pro pořadí tisku stránek?
Pro objednávku tisku stránky si můžete vybrat mezi "Over Then Down" a "Down Then Over".

### Kde najdu další příklady použití Aspose.Cells?
Další příklady a funkce můžete prozkoumat v[Dokumentace Aspose.Cells](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
