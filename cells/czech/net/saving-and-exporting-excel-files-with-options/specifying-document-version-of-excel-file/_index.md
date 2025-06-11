---
"description": "Naučte se, jak programově zadat vlastnosti dokumentu, jako je verze, autor a název, v souboru aplikace Excel pomocí Aspose.Cells pro .NET s podrobnými pokyny."
"linktitle": "Programové určení verze dokumentu souboru Excel v .NET"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Programové určení verze dokumentu souboru Excel v .NET"
"url": "/cs/net/saving-and-exporting-excel-files-with-options/specifying-document-version-of-excel-file/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Programové určení verze dokumentu souboru Excel v .NET

## Zavedení
Aspose.Cells pro .NET je výkonná knihovna, která vývojářům umožňuje snadno programově manipulovat s excelovými soubory. Ať už chcete vytvářet excelové soubory od nuly, nebo upravovat stávající, Aspose.Cells nabízí komplexní API pro dosažení vašich cílů. Jednou z takových funkcí je určení vlastností dokumentu, jako je verze, autor nebo název. Tento tutoriál vás provede programově určením verze dokumentu excelového souboru pomocí Aspose.Cells pro .NET.
## Předpoklady
Než se ponoříme do detailů, ujistěte se, že máte vše, co potřebujete k dodržování tohoto tutoriálu:
1. Aspose.Cells pro .NET: Můžete si stáhnout nejnovější verzi [zde](https://releases.aspose.com/cells/net/)Pokud jste si ještě nezakoupili licenci, můžete si ji zakoupit. [dočasná licence](https://purchase.aspose.com/temporary-license/) prozkoumat funkce.
2. Vývojové prostředí .NET: Můžete použít Visual Studio nebo jakékoli vývojové prostředí kompatibilní s .NET.
3. Základní znalost C#: Znalost programování v C# vám usnadní sledování textu.
## Importovat balíčky
Než začnete s kódováním, je třeba importovat potřebné jmenné prostory z knihovny Aspose.Cells. To vám umožní přístup ke třídám a metodám potřebným pro manipulaci s Excelovými soubory.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Tyto dva jmenné prostory budou nezbytné pro interakci se sešitem a jeho vestavěnými vlastnostmi dokumentu.
Nyní si rozebereme proces zadávání vlastností dokumentu v souboru aplikace Excel, včetně verze, názvu a autora.
## Krok 1: Inicializace objektu sešitu
Prvním krokem je vytvoření nové instance `Workbook` objekt. Tento objekt představuje celý soubor aplikace Excel, se kterým budete pracovat.
```csharp
Workbook wb = new Workbook();
```
Ten/Ta/To `Workbook` Třída poskytuje reprezentaci souboru aplikace Excel. Vytvořením instance vytvoříme prázdný sešit aplikace Excel, se kterým můžeme manipulovat.
## Krok 2: Přístup k vestavěným vlastnostem dokumentu
Aspose.Cells nabízí vestavěné vlastnosti dokumentu, které zahrnují pole jako název, autor a verze dokumentu. K těmto vlastnostem máte přístup prostřednictvím `BuiltInDocumentProperties` sbírka.
```csharp
Aspose.Cells.Properties.BuiltInDocumentPropertyCollection bdpc = wb.BuiltInDocumentProperties;
```
Ten/Ta/To `BuiltInDocumentPropertyCollection` Třída poskytuje přístup ke kolekci vestavěných vlastností dokumentu, jako je název, autor a další metadata obvykle spojená s dokumentem.
## Krok 3: Nastavení názvu dokumentu aplikace Excel
Dále nastavíme název dokumentu aplikace Excel. Tato metadata pomohou s pozdější identifikací a správou souboru.
```csharp
bdpc.Title = "Aspose File Format APIs";
```
Nastavení názvu je důležité pro organizaci dokumentu. Tato metadata lze zobrazit ve vlastnostech souboru a externí systémy je mohou použít k efektivnější katalogizaci nebo identifikaci dokumentu.
## Krok 4: Zadejte autora
Autor dokumentu může být také uveden tak, aby odrážel, kdo soubor vytvořil nebo upravil.
```csharp
bdpc.Author = "Aspose APIs Developers";
```
Tento krok pomáhá přiřadit dokument jeho tvůrci a poskytuje další metadata pro správu dokumentů nebo scénáře spolupráce.
## Krok 5: Zadejte verzi dokumentu
Jednou z nejdůležitějších vlastností, kterými se v tomto tutoriálu zabýváme, je verze dokumentu. Tento krok umožňuje zadat verzi dokumentu, což je užitečné při práci v prostředích, která vyžadují správu verzí.
```csharp
bdpc.DocumentVersion = "Aspose.Cells Version - 18.3";
```
Nastavení verze dokumentu poskytuje jasnou informaci o tom, která verze dokumentu nebo knihovny byla použita k vytvoření souboru. To je obzvláště důležité v prostředích, která potřebují sledovat revize souborů nebo kompatibilitu s různými verzemi knihoven.
## Krok 6: Uložte soubor Excel
Nakonec můžete soubor Excel uložit se všemi právě nastavenými vlastnostmi. Aspose.Cells umožňuje uložit soubor v různých formátech, ale v tomto příkladu se budeme držet formátu `.xlsx` formát.
```csharp
wb.Save("outputSpecifyDocumentVersionOfExcelFile.xlsx", SaveFormat.Xlsx);
```
Ten/Ta/To `Save` Metoda se používá k uložení souboru do vámi zadaného adresáře. Zde jej ukládáme jako soubor aplikace Excel v `.xlsx` formát. V případě potřeby Aspose.Cells podporuje i formáty jako `.xls`, `.csv`a `.pdf`, což poskytuje flexibilitu na základě potřeb vašeho projektu.
## Závěr
V tomto tutoriálu jsme si prošli, jak zadat vlastnosti dokumentu, zejména verzi dokumentu, v souboru aplikace Excel pomocí nástroje Aspose.Cells pro .NET. Aspose.Cells je extrémně flexibilní a výkonný nástroj, který umožňuje programově manipulovat s soubory aplikace Excel, což z něj činí skvělý přínos pro každého vývojáře .NET pracujícího s tabulkami.
## Často kladené otázky
### Mohu upravit další vestavěné vlastnosti pomocí Aspose.Cells?  
Ano, můžete upravit i další vestavěné vlastnosti, jako je mimo jiné předmět, klíčová slova a komentáře.
### Jaké formáty souborů podporuje Aspose.Cells?  
Aspose.Cells podporuje širokou škálu formátů včetně `.xls`, `.xlsx`, `.csv`, `.pdf`, a další.
### Potřebuji licenci k používání Aspose.Cells pro .NET?  
Můžete prozkoumat Aspose.Cells pomocí [bezplatná zkušební verze](https://releases.aspose.com/) nebo si zažádat o [dočasná licence](https://purchase.aspose.com/temporary-license/) pro prodloužené testování.
### Mohu použít Aspose.Cells ve webové aplikaci?  
Ano, Aspose.Cells lze použít jak v desktopových, tak i webových aplikacích. Je vysoce všestranný a dobře se integruje s webovými frameworky .NET.
### Kde mohu získat podporu pro Aspose.Cells?  
Komunitu a podporu můžete získat prostřednictvím [Fórum podpory Aspose.Cells](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}