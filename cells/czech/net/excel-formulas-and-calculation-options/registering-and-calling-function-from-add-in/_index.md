---
"description": "Zjistěte, jak registrovat a volat funkce z doplňků v Excelu pomocí Aspose.Cells pro .NET v našem jednoduchém podrobném tutoriálu."
"linktitle": "Registrace a volání funkce z doplňku v Excelu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Registrace a volání funkce z doplňku v Excelu"
"url": "/cs/net/excel-formulas-and-calculation-options/registering-and-calling-function-from-add-in/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Registrace a volání funkce z doplňku v Excelu

## Zavedení
Chcete vylepšit své zkušenosti s Excelem voláním funkcí z doplňku? Pokud ano, jste na správném místě! Doplňky pro Excel jsou jako pohádkové kmotry tabulek; magicky rozšiřují funkčnost a poskytují vám spoustu nových nástrojů na dosah ruky. A s Aspose.Cells pro .NET je registrace a používání těchto funkcí doplňku snazší než kdy dříve. 
V této příručce vás provedu procesem registrace a volání funkce z doplňku Excelu pomocí Aspose.Cells pro .NET. Vše si rozebereme krok za krokem, abyste se během chvilky cítili jako profesionál!
## Předpoklady
Než se ponoříme do kódovací magie, pojďme si probrat, co potřebujete mít připraveno:
1. Visual Studio: Ujistěte se, že máte na svém počítači nainstalované Visual Studio. Zde budeme psát a spouštět náš kód.
2. Knihovna Aspose.Cells: Budete potřebovat nainstalovanou knihovnu Aspose.Cells. Můžete si ji stáhnout z jejich [stránka ke stažení](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: Trocha znalosti C# vám hodně pomůže; pomůže vám plynule se orientovat.
4. Doplňky pro Excel: Měli byste mít soubor doplňku (například `.xlam`), který obsahuje funkce, které chcete zaregistrovat a používat.
5. Ukázkový doplněk pro Excel: V tomto tutoriálu použijeme doplněk pro Excel s názvem `TESTUDF.xlam`Takže se ujistěte, že to máte k dispozici!
Teď, když máte vše připravené, pojďme si vyhrnout rukávy a pustit se do programování!
## Import balíčků
Pro začátek budete muset importovat několik základních jmenných prostorů na začátek souboru C#. Zde je to, co je potřeba zahrnout:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Tyto jmenné prostory vám umožní přístup ke třídám a metodám, které budeme v tomto tutoriálu používat.
Rozdělme si to na zvládnutelné kroky. Na konci této příručky budete mít důkladnou představu o tom, jak registrovat doplňkové funkce a používat je v sešitech aplikace Excel.
## Krok 1: Nastavení zdrojového a výstupního adresáře
Než budete moci zaregistrovat doplněk, je třeba definovat, kde budou vaše soubory doplňku a výstupu uloženy.
```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory";
// Výstupní adresář
string outputDir = "Your Document Directory";
```
Nahradit `"Your Document Directory"` se skutečnou cestou, kde se nachází vaše `.xlam` Soubor a výstupní soubory budou uloženy. Je to jako příprava scény před začátkem představení.
## Krok 2: Vytvořte prázdný sešit
Dále budete chtít vytvořit prázdný sešit, kde si můžeme pohrát s doplňkovými funkcemi.
```csharp
// Vytvořit prázdný sešit
Workbook workbook = new Workbook();
```
Tento řádek kódu vytvoří nový sešit, který bude sloužit jako naše hřiště. Představte si ho jako nové plátno připravené pro vaše kreativní tahy.
## Krok 3: Registrace doplňkové funkce
A teď k jádru věci! Je čas zaregistrovat váš doplňkový modul. Zde je návod, jak to udělat:
```csharp
// Registrace doplňku s povolenými makry spolu s názvem funkce
int id = workbook.Worksheets.RegisterAddInFunction(sourceDir + @"TESTUDF.xlam", "TEST_UDF", false);
```
Tento řádek registruje doplňkovou funkci s názvem `TEST_UDF` nalezeno v `TESTUDF.xlam` soubor doplňku. `false` Parametr znamená, že doplněk není načten v „izolovaném“ režimu. 
## Krok 4: Registrace dalších funkcí (pokud existují)
Pokud máte ve stejném souboru doplňku zaregistrováno více funkcí, můžete zaregistrovat i je!
```csharp
// Zaregistrujte do souboru další funkce (pokud existují)
workbook.Worksheets.RegisterAddInFunction(id, "TEST_UDF1");
```
Zde vidíte, jak snadné je přidat další funkce ze stejného doplňku. Prostě je skládejte jako stavební bloky!
## Krok 5: Přístup k pracovnímu listu
Pojďme dál a otevřeme pracovní list, kde budeme používat naši funkci. 
```csharp
// Přístup k prvnímu listu
Worksheet worksheet = workbook.Worksheets[0];
```
Přistupujeme k prvnímu listu v sešitu, abychom tam umístili vzorec. Je to jako otevírat dveře do místnosti, kde se odehrává zábava.
## Krok 6: Přístup k určité buňce
Dále si musíme vybrat, kterou buňku chceme použít pro náš vzorec. 
```csharp
// Přístup k první buňce
var cell = worksheet.Cells["A1"];
```
Zde ukazujeme na buňku A1. Sem vložíme náš magický vzorec. Můžete si to představit jako připnutí cíle na mapu pokladů!
## Krok 7: Nastavení vzorce
teď je čas na velké odhalení! Nastavme vzorec, který volá naši registrovanou funkci.
```csharp
// Nastavit název vzorce v doplňku
cell.Formula = "=TEST_UDF()";
```
Tímto řádkem říkáme Excelu, aby použil naši funkci z buňky A1. Je to, jako bychom Excelu dali příkaz a řekli: „Hele, udělej tohle!“
## Krok 8: Uložení sešitu
V neposlední řadě je čas zachránit naše mistrovské dílo.
```csharp
// Uložit sešit do výstupního formátu XLSX.
workbook.Save(outputDir + @"test_udf.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```
Zde ukládáme náš sešit jako soubor XLSX. Tento poslední krok je jako byste zarámovali obraz a připravili se na jeho vystavení!
## Krok 9: Potvrzení provedení
Nakonec to celé zakončíme výpisem zprávy o úspěchu do konzole.
```csharp
Console.WriteLine("RegisterAndCallFuncFromAddIn executed successfully.");
```
Tato čára slouží jako naše vítězná vlajka. Je to příjemný malý detail, který potvrzuje, že vše proběhlo hladce.
## Závěr 
tady to máte! Naučili jste se nejen registrovat a volat funkce z doplňků Excelu pomocí Aspose.Cells pro .NET, ale také jste získali hlubší pochopení každého kroku. Život je teď o něco jednodušší, že? Tak proč si to nevyzkoušet sami? Ponořte se do doplňků Excelu a dodejte svým tabulkám novou úroveň interaktivity a funkčnosti.
## Často kladené otázky
### Co je doplněk Excelu?  
Doplněk pro Excel je program, který do Excelu přidává vlastní funkce, funkce nebo příkazy a umožňuje uživatelům rozšířit jeho možnosti.
### Mohu používat Aspose.Cells bez jeho lokální instalace?  
Ne, pro použití v .NET aplikacích je nutné nainstalovat knihovnu Aspose.Cells.
### Jak získám dočasnou licenci pro Aspose.Cells?  
Můžete je navštívit [stránka s dočasnou licencí](https://purchase.aspose.com/temporary-license/) pro více informací.
### Je možné volat více funkcí z jednoho doplňku?  
Ano! Můžete zaregistrovat více funkcí ze stejného souboru doplňku pomocí `RegisterAddInFunction` metoda.
### Kde najdu další dokumentaci k Aspose.Cells?  
Jejich komplexní dokumentaci si můžete prohlédnout na webu [zde](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}