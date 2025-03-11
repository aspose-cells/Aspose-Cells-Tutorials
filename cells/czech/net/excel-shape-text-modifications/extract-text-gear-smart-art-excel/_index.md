---
title: Extrahujte text z Gear Type Smart Art v Excelu
linktitle: Extrahujte text z Gear Type Smart Art v Excelu
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak extrahovat text ze SmartArt typu ozubeného kola v Excelu pomocí Aspose.Cells for .NET. Součástí je podrobný průvodce a příklad kódu.
weight: 10
url: /cs/net/excel-shape-text-modifications/extract-text-gear-smart-art-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahujte text z Gear Type Smart Art v Excelu

## Zavedení
Při práci s Excelem se můžete setkat s grafikou SmartArt, která pomáhá předávat vaše zprávy vizuálně přitažlivým způsobem. Mezi těmito grafikami je SmartArt typu ozubeného kola oblíbený pro své hierarchické a směrové toky, které se často používají při řízení projektů nebo modelování systémů. Ale co když potřebujete extrahovat text z těchto tvarů programově? Zde se Aspose.Cells for .NET hodí! V tomto příspěvku na blogu vás provedeme podrobným průvodcem, jak extrahovat text z tvarů SmartArt typu ozubeného kola v aplikaci Excel pomocí Aspose.Cells for .NET.
## Předpoklady
Než se do toho pustíme, je potřeba splnit několik základních předpokladů. Nebojte se; je to jednoduché a já vás tím provedu.
### .NET prostředí
Ujistěte se, že máte na svém počítači nastavené vývojové prostředí .NET. Může to být Visual Studio nebo libovolné IDE podle vašeho výběru, které podporuje vývoj .NET.
### Aspose.Cells pro .NET
 Dále budete muset nainstalovat knihovnu Aspose.Cells. Toto je síla, která vám umožní bezproblémově manipulovat se soubory aplikace Excel. Můžete si jej stáhnout z[Stránka Aspose Releases](https://releases.aspose.com/cells/net/) . Pokud to chcete nejprve prozkoumat, využijte možnosti[zkušební verze zdarma](https://releases.aspose.com/).
### Základní znalost C#
Základní znalost programování v C# je právě to, co musíte dodržovat spolu s tímto tutoriálem. Pokud s tím začínáte, žádný strach – navrhnu kroky tak, aby byly co nejpřívětivější pro začátečníky.
### Ukázkový soubor Excel
Pro tento výukový program budete také potřebovat ukázkový soubor Excel, který obsahuje tvary SmartArt typu ozubeného kola. Šablonu si můžete snadno vytvořit nebo najít šablonu online. Jen se ujistěte, že SmartArt obsahuje alespoň jeden tvar ozubeného kola.
## Importujte balíčky
Chcete-li začít kódovat, budete muset importovat potřebné balíčky. Jak na to:
### Vytvořit nový projekt
1. Otevřete své .NET IDE.
2. Vytvořte nový projekt. Vyberte například 'Console Application' pod možnostmi .NET.
3. Pojmenujte svůj projekt a nastavte požadovaný rámec. 
### Přidat reference
Chcete-li použít Aspose.Cells, budete muset do projektu přidat odkazy na knihovnu:
1. Klepněte pravým tlačítkem myši na název projektu v Průzkumníku řešení.
2. Vyberte „Spravovat balíčky NuGet“.
3. Vyhledejte "Aspose.Cells" a nainstalujte jej.
Po instalaci jste připraveni na kódování!
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Nyní si rozeberme kód, který použijete k extrahování textu. Budeme to dělat krok za krokem.
## Krok 1: Nastavte zdrojový adresář
Začněte definováním adresáře, kde se nachází váš soubor Excel:
```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory";
```
 Nezapomeňte vyměnit`"Your Document Directory"` se skutečnou cestou k souboru Excel.
## Krok 2: Načtěte sešit aplikace Excel
Dále načteme sešit Excel. K jeho obsahu se dostaneme takto:
```csharp
// Načtěte ukázkový soubor aplikace Excel obsahující tvar chytrého umění typu ozubeného kola.
Workbook wb = new Workbook(sourceDir + "sampleExtractTextFromGearTypeSmartArtShape.xlsx");
```
Tato část načte váš vzorový sešit aplikace Excel.
## Krok 3: Otevřete první pracovní list
Nyní, když jsme načetli sešit, pojďme se dostat k prvnímu listu, kde existuje náš SmartArt:
```csharp
// Přístup k prvnímu listu.
Worksheet ws = wb.Worksheets[0];
```
Tím se načte první list pro další manipulaci.
## Krok 4: Přístup k prvnímu tvaru
Dále musíme získat přístup k prvnímu tvaru v našem listu. Tímto způsobem můžeme procházet našimi grafickými prvky SmartArt:
```csharp
// Přístup k prvnímu tvaru.
Aspose.Cells.Drawing.Shape sh = ws.Shapes[0];
```
Zde se zaměřujeme na první tvar, o kterém předpokládáme, že je to SmartArt, který potřebujeme.
## Krok 5: Získejte tvar skupiny
Jakmile máme tvar, je čas získat výsledek naší reprezentace SmartArt:
```csharp
// Získejte výsledek tvaru inteligentního umění typu ozubeného kola ve formě tvaru skupiny.
Aspose.Cells.Drawing.GroupShape gs = sh.GetResultOfSmartArt();
```
Tím se načte náš SmartArt typu ozubeného kola jako seskupený tvar.
## Krok 6: Extrahujte jednotlivé tvary
Nyní si vyberme jednotlivé tvary, které tvoří náš SmartArt:
```csharp
// Získejte seznam jednotlivých tvarů sestávajících ze skupinových tvarů.
Aspose.Cells.Drawing.Shape[] shps = gs.GetGroupedShapes();
```
Toto pole bude obsahovat všechny jednotlivé tvary, které potřebujeme procházet.
## Krok 7: Extrahujte a vytiskněte text
Nakonec můžeme procházet polem tvarů a extrahovat text z libovolného tvaru ozubeného kola:
```csharp
// Extrahujte text tvarů typu ozubeného kola a vytiskněte je na konzole.
for (int i = 0; i < shps.Length; i++)
{
    Aspose.Cells.Drawing.Shape s = shps[i];
    if (s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear9 || s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear6)
    {
        Console.WriteLine("Gear Type Shape Text: " + s.Text);
    }
}
```
této smyčce zkontrolujeme typ tvaru a vytiskneme text, pokud se jedná o tvar ozubeného kola.
## Krok 8: Potvrzení provedení
Nakonec můžete chtít přidat potvrzovací zprávu, jakmile bude proces úspěšně dokončen:
```csharp
Console.WriteLine("ExtractTextFromGearTypeSmartArtShape executed successfully.");
```
Tímto je vaše extrakce dokončena a textový výstup byste měli vidět v konzole!
## Závěr
 Gratuluji! Právě jste se naučili, jak extrahovat text z tvarů SmartArt typu ozubeného kola v Excelu pomocí Aspose.Cells for .NET. Tato šikovná technika otevírá dveře k automatizaci zpráv nebo dokumentace, které se spoléhají na vizuální reprezentaci dat. Ať už jste zkušený vývojář nebo teprve začínáte, ovládání a extrahování informací z obrázků SmartArt může zefektivnit váš pracovní postup a zvýšit efektivitu. Nezapomeňte prozkoumat podrobnosti[Dokumentace Aspose.Cells](https://reference.aspose.com/cells/net/) pro další schopnosti.
## FAQ
### Co je Aspose.Cells?
Aspose.Cells je knihovna .NET, která umožňuje vývojářům snadno vytvářet a manipulovat se soubory aplikace Excel.
### Mohu používat Aspose.Cells s jinými jazyky?
Ano! Aspose.Cells je k dispozici ve více programovacích jazycích, včetně Javy a Pythonu.
### Musím si koupit Aspose.Cells pro .NET?
 Aspose.Cells nabízí bezplatnou zkušební verzi, ale pro delší používání je vyžadován nákup. Můžete najít možnosti nákupu[zde](https://purchase.aspose.com/buy).
### Je k dispozici podpora pro uživatele Aspose.Cells?
 Absolutně! Podporu komunity najdete na[Fórum Aspose.Cells](https://forum.aspose.com/c/cells/9).
### Mohu pomocí této metody extrahovat další typy obrázků SmartArt?
Ano, s malými úpravami můžete extrahovat text z různých tvarů SmartArt změnou podmínek v kódu.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
