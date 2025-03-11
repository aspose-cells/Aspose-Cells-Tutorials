---
title: Zadání verze dokumentu souboru aplikace Excel programově v .NET
linktitle: Zadání verze dokumentu souboru aplikace Excel programově v .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak určit vlastnosti dokumentu, jako je verze, autor a název, v souboru aplikace Excel programově pomocí Aspose.Cells for .NET pomocí podrobných pokynů.
weight: 12
url: /cs/net/saving-and-exporting-excel-files-with-options/specifying-document-version-of-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zadání verze dokumentu souboru aplikace Excel programově v .NET

## Zavedení
Aspose.Cells for .NET je výkonná knihovna, která umožňuje vývojářům snadno programově manipulovat se soubory aplikace Excel. Ať už chcete vytvořit soubory aplikace Excel od začátku nebo upravit ty stávající, Aspose.Cells nabízí komplexní API pro dosažení vašich cílů. Jednou z takových funkcí je určení vlastností dokumentu, jako je verze, autor nebo název. Tento tutoriál vás provede programovým určením verze dokumentu souboru aplikace Excel pomocí Aspose.Cells for .NET.
## Předpoklady
Než se ponoříme do podrobností, ujistěte se, že spolu s tímto návodem máte vše, co potřebujete:
1. Aspose.Cells pro .NET: Můžete si stáhnout nejnovější verzi[zde](https://releases.aspose.com/cells/net/) . Pokud jste si ještě nezakoupili licenci, můžete se rozhodnout pro a[dočasná licence](https://purchase.aspose.com/temporary-license/) prozkoumat funkce.
2. Vývojové prostředí .NET: Můžete použít Visual Studio nebo jakékoli IDE kompatibilní s .NET.
3. Základní znalost C#: Pochopení programování v C# vám usnadní sledování.
## Importujte balíčky
Než budete moci začít kódovat, musíte importovat potřebné jmenné prostory z knihovny Aspose.Cells. To vám umožní přístup ke třídám a metodám potřebným pro manipulaci se soubory aplikace Excel.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Tyto dva jmenné prostory budou nezbytné pro interakci se sešitem a jeho vestavěnými vlastnostmi dokumentu.
Nyní si rozeberme proces zadávání vlastností dokumentu v souboru aplikace Excel, včetně verze, názvu a autora.
## Krok 1: Inicializujte objekt sešitu
 Prvním krokem je vytvoření nové instance souboru`Workbook` objekt. Tento objekt představuje celý soubor Excel, se kterým budete pracovat.
```csharp
Workbook wb = new Workbook();
```
 The`Workbook`class poskytuje reprezentaci souboru Excel. Jeho instancí vytvoříme prázdný excelový sešit, se kterým můžeme manipulovat.
## Krok 2: Otevřete vlastnosti vestavěného dokumentu
 Aspose.Cells nabízí vestavěné vlastnosti dokumentu, které zahrnují pole jako název, autor a verze dokumentu. K těmto vlastnostem můžete přistupovat prostřednictvím`BuiltInDocumentProperties`sbírka.
```csharp
Aspose.Cells.Properties.BuiltInDocumentPropertyCollection bdpc = wb.BuiltInDocumentProperties;
```
 The`BuiltInDocumentPropertyCollection` class poskytuje přístup ke kolekci vestavěných vlastností dokumentu, jako je název, autor a další metadata obvykle spojená s dokumentem.
## Krok 3: Nastavte název dokumentu aplikace Excel
Dále nastavíme název dokumentu Excel. Tato metadata pomáhají později identifikovat a spravovat soubor.
```csharp
bdpc.Title = "Aspose File Format APIs";
```
Nastavení názvu je důležité pro organizaci dokumentu. Tato metadata lze vidět ve vlastnostech souboru a mohou je používat externí systémy k efektivnější katalogizaci nebo identifikaci dokumentu.
## Krok 4: Zadejte autora
Může být také určen autor dokumentu, který odráží, kdo soubor vytvořil nebo upravil.
```csharp
bdpc.Author = "Aspose APIs Developers";
```
Tento krok pomáhá při přiřazení dokumentu jeho tvůrci a poskytuje další metadata pro scénáře správy dokumentů nebo spolupráce.
## Krok 5: Zadejte verzi dokumentu
Jednou z nejdůležitějších vlastností, kterou se v tomto tutoriálu zabýváme, je verze dokumentu. Tento krok vám umožňuje zadat verzi dokumentu, což je užitečné při práci v prostředích, která vyžadují správu verzí.
```csharp
bdpc.DocumentVersion = "Aspose.Cells Version - 18.3";
```
Nastavení verze dokumentu objasní, která verze dokumentu nebo knihovny byla použita k vytvoření souboru. To je důležité zejména v prostředích, která potřebují sledovat revize souborů nebo kompatibilitu s různými verzemi knihoven.
## Krok 6: Uložte soubor Excel
 Nakonec můžete uložit soubor Excel se všemi vlastnostmi, které jste právě nastavili. Aspose.Cells umožňuje uložit soubor v různých formátech, ale pro tento příklad zůstaneme u`.xlsx` formát.
```csharp
wb.Save("outputSpecifyDocumentVersionOfExcelFile.xlsx", SaveFormat.Xlsx);
```
 The`Save` metoda se používá k uložení souboru do určeného adresáře. Zde jej ukládáme jako soubor aplikace Excel v`.xlsx`formát. V případě potřeby Aspose.Cells také podporuje formáty jako`.xls`, `.csv` a`.pdf`poskytující flexibilitu na základě potřeb vašeho projektu.
## Závěr
V tomto tutoriálu jsme si prošli, jak specifikovat vlastnosti dokumentu, zejména verzi dokumentu, v souboru aplikace Excel pomocí Aspose.Cells for .NET. Aspose.Cells je extrémně flexibilní a výkonný nástroj, který vám umožňuje programově manipulovat se soubory Excelu, což z něj dělá velkou výhodu pro každého vývojáře .NET pracujícího s tabulkami.
## FAQ
### Mohu upravit další vestavěné vlastnosti pomocí Aspose.Cells?  
Ano, můžete upravit další vestavěné vlastnosti, jako je mimo jiné předmět, klíčová slova a komentáře.
### Jaké formáty souborů podporuje Aspose.Cells?  
 Aspose.Cells podporuje širokou škálu formátů včetně`.xls`, `.xlsx`, `.csv`, `.pdf`a další.
### Potřebuji licenci k používání Aspose.Cells pro .NET?  
 Aspose.Cells můžete prozkoumat pomocí a[zkušební verze zdarma](https://releases.aspose.com/) nebo požádat o a[dočasná licence](https://purchase.aspose.com/temporary-license/) pro rozšířené testování.
### Mohu použít Aspose.Cells ve webové aplikaci?  
Ano, Aspose.Cells lze použít v desktopových i webových aplikacích. Je vysoce univerzální a dobře se integruje s webovými frameworky .NET.
### Kde mohu získat podporu pro Aspose.Cells?  
 Ke komunitě a podpoře můžete přistupovat prostřednictvím[Fórum podpory Aspose.Cells](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
