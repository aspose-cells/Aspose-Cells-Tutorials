---
title: Registrace a volání funkce z doplňku v aplikaci Excel
linktitle: Registrace a volání funkce z doplňku v aplikaci Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Objevte, jak se zaregistrovat a volat funkce z doplňků v Excelu pomocí Aspose.Cells for .NET s naším jednoduchým návodem krok za krokem.
weight: 20
url: /cs/net/excel-formulas-and-calculation-options/registering-and-calling-function-from-add-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Registrace a volání funkce z doplňku v aplikaci Excel

## Zavedení
Chcete vylepšit své prostředí Excel voláním funkcí z doplňku? Pokud ano, jste na správném místě! Doplňky Excelu jsou jako pohádkové kmotry tabulek; magicky rozšiřují funkčnost a poskytují vám spoustu nových nástrojů na dosah ruky. A s Aspose.Cells pro .NET je registrace a používání těchto doplňkových funkcí snazší než kdy dříve. 
V této příručce vás provedu procesem registrace a volání funkce z doplňku aplikace Excel pomocí Aspose.Cells pro .NET. Vše rozebereme krok za krokem, takže se během chvilky budete cítit jako profík!
## Předpoklady
Než se ponoříme do kouzelného kódování, proberme si, co potřebujete mít na svém místě:
1. Visual Studio: Ujistěte se, že máte na počítači nastavené Visual Studio. Zde napíšeme a spustíme náš kód.
2.  Knihovna Aspose.Cells: Budete potřebovat nainstalovanou knihovnu Aspose.Cells. Můžete to vzít od nich[stránka ke stažení](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: Trocha porozumění C# bude dlouhá cesta; pomůže vám to plynule následovat.
4.  Doplňky aplikace Excel: Měli byste mít soubor doplňku (např`.xlam`), který obsahuje funkce, které chcete zaregistrovat a používat.
5.  Ukázkový doplněk aplikace Excel: V tomto kurzu použijeme doplněk aplikace Excel s názvem`TESTUDF.xlam`. Tak se ujistěte, že to máte k dispozici!
Nyní, když jste připraveni, vyhrňme si rukávy a pusťte se do kódování!
## Import balíčků
Chcete-li začít, budete muset importovat některé základní jmenné prostory v horní části souboru C#. Zde je to, co musíte zahrnout:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Tyto jmenné prostory vám umožní přístup ke třídám a metodám, které budeme používat v tomto kurzu.
Pojďme si to rozdělit na zvládnutelné kroky. Na konci této příručky budete dobře rozumět tomu, jak registrovat doplňkové funkce a používat je ve svých excelových sešitech.
## Krok 1: Nastavte zdrojové a výstupní adresáře
Než budete moci zaregistrovat svůj doplněk, musíte definovat, kde budou umístěny soubory doplňku a výstupní soubory.
```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory";
// Výstupní adresář
string outputDir = "Your Document Directory";
```
 Nahradit`"Your Document Directory"` se skutečnou cestou, kde jste`.xlam` soubor a výstupní soubory budou uloženy. Je to jako připravit scénu před začátkem představení.
## Krok 2: Vytvořte prázdný sešit
Dále budete chtít vytvořit prázdný sešit, kde si budeme moci pohrát s doplňkovými funkcemi.
```csharp
// Vytvořte prázdný sešit
Workbook workbook = new Workbook();
```
Tento řádek kódu vytváří nový sešit, který bude sloužit jako naše hřiště. Představte si to jako čerstvé plátno připravené pro vaše kreativní tahy.
## Krok 3: Zaregistrujte funkci doplňku
Nyní pojďme k jádru věci! Je čas zaregistrovat vaši doplňkovou funkci. Jak na to:
```csharp
// Zaregistrujte doplněk s povoleným makrem spolu s názvem funkce
int id = workbook.Worksheets.RegisterAddInFunction(sourceDir + @"TESTUDF.xlam", "TEST_UDF", false);
```
 Tento řádek registruje funkci doplňku s názvem`TEST_UDF` nalezený v`TESTUDF.xlam` doplňkový soubor. The`false`parametr znamená, že doplněk není načten v „izolovaném“ režimu. 
## Krok 4: Zaregistrujte další funkce (pokud existují)
Pokud máte ve stejném souboru doplňku zaregistrováno více funkcí, můžete je zaregistrovat také!
```csharp
// Zaregistrujte více funkcí v souboru (pokud existují)
workbook.Worksheets.RegisterAddInFunction(id, "TEST_UDF1");
```
Zde můžete vidět, jak snadné je přidat další funkce ze stejného doplňku. Jen je skládejte jako stavební kostky!
## Krok 5: Otevřete sešit
Pojďme dál a vstoupíme do pracovního listu, kde budeme naši funkci používat. 
```csharp
// Přístup k prvnímu listu
Worksheet worksheet = workbook.Worksheets[0];
```
Přistupujeme k prvnímu listu v sešitu, abychom umístili náš vzorec. Je to jako otevřít dveře do místnosti, kde se odehrává zábava.
## Krok 6: Přístup ke konkrétní buňce
Dále si musíme vybrat, kterou buňku chceme použít pro náš vzorec. 
```csharp
// Přístup k první buňce
var cell = worksheet.Cells["A1"];
```
Zde ukazujeme na buňku A1. Tady vypustíme naši kouzelnou formuli. Můžete si to představit jako připnutí cíle na mapu pokladu!
## Krok 7: Nastavte vzorec
Nyní je čas na velkolepé odhalení! Nastavíme vzorec, který volá naši registrovanou funkci.
```csharp
// Nastavit název vzorce přítomný v doplňku
cell.Formula = "=TEST_UDF()";
```
Tímto řádkem říkáme Excelu, aby použil naši funkci v buňce A1. Je to jako dát Excel příkaz a říct: "Hej, udělej to!"
## Krok 8: Uložte sešit
V neposlední řadě je čas zachránit naše mistrovské dílo.
```csharp
// Uložte sešit do výstupního formátu XLSX.
workbook.Save(outputDir + @"test_udf.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```
Zde ukládáme náš sešit jako soubor XLSX. Tento poslední krok je jako dát svůj obraz do rámu a připravit se na jeho předvedení!
## Krok 9: Potvrďte provedení
Nakonec to všechno zabalíme vytištěním zprávy o úspěchu na konzoli.
```csharp
Console.WriteLine("RegisterAndCallFuncFromAddIn executed successfully.");
```
Tato linie funguje jako naše vítězná vlajka. Je to příjemný malý dotyk, který potvrzuje, že vše proběhlo hladce.
## Závěr 
tady to máte! Naučili jste se nejen registrovat a volat funkce z doplňků aplikace Excel pomocí Aspose.Cells pro .NET, ale také jste hlouběji porozuměli jednotlivým krokům. Život je teď o něco jednodušší, že? Tak proč to nezkusit na vlastní kůži? Ponořte se do těchto doplňků aplikace Excel a dejte svým tabulkám novou úroveň interaktivity a funkčnosti.
## FAQ
### Co je doplněk aplikace Excel?  
Doplněk aplikace Excel je program, který do aplikace Excel přidává vlastní funkce, funkce nebo příkazy a umožňuje uživatelům rozšířit její možnosti.
### Mohu používat Aspose.Cells bez místní instalace?  
Ne, musíte si nainstalovat knihovnu Aspose.Cells, abyste ji mohli používat ve svých aplikacích .NET.
### Jak získám dočasnou licenci pro Aspose.Cells?  
 Můžete navštívit jejich[dočasná licenční stránka](https://purchase.aspose.com/temporary-license/) pro více informací.
### Je možné volat více funkcí z jednoho doplňku?  
 Ano! Můžete zaregistrovat více funkcí ze stejného souboru doplňku pomocí`RegisterAddInFunction` metoda.
### Kde najdu další dokumentaci na Aspose.Cells?  
 Jejich komplexní dokumentaci si můžete prohlédnout na webu[zde](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
