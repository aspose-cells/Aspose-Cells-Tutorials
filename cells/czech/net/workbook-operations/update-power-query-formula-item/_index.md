---
title: Aktualizujte položku vzorce Power Query v sešitu
linktitle: Aktualizujte položku vzorce Power Query v sešitu
second_title: Aspose.Cells .NET Excel Processing API
description: V tomto komplexním podrobném průvodci se dozvíte, jak aktualizovat vzorce Power Query v Excelu pomocí Aspose.Cells pro .NET.
weight: 27
url: /cs/net/workbook-operations/update-power-query-formula-item/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aktualizujte položku vzorce Power Query v sešitu

## Zavedení
Pochopení toho, jak efektivně spravovat data pomocí Power Query v Excelu, je prvořadé pro každého datového analytika nebo nadšence do Excelu. Pokud jste někdy potřebovali aktualizovat položky vzorců v sešitu Power Query, jste na správném místě. Tato příručka je přizpůsobena tak, aby vám pomohla naučit se používat Aspose.Cells for .NET k bezproblémové aktualizaci vzorců Power Query v sešitu aplikace Excel. Pomocí několika jednoduchých kroků budete moci manipulovat a zefektivňovat svá data a zajistit, aby vaše sešity zůstaly dynamické a centralizované.
## Předpoklady
Než se pustíte do ukázkového kódu a kroků, pojďme si projít, co budete potřebovat:
1. Základní porozumění C# a .NET: Znalost programovacích konceptů v C# bude prospěšná, protože budeme psát nějaký kód.
2.  Instalace Aspose.Cells for .NET: Knihovnu Aspose.Cells musíte mít integrovanou do svého projektu .NET. Můžete si jej stáhnout[zde](https://releases.aspose.com/cells/net/).
3. Soubor Excel připravený k úpravě: Ujistěte se, že máte soubor Excelu, který obsahuje Power Query, který chcete aktualizovat. Musíte mít vzorový sešit jako`SamplePowerQueryFormula.xlsx` k dispozici.
## Importujte balíčky
Chcete-li začít, ujistěte se, že máte v souboru C# zahrnuty následující jmenné prostory:
```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```
To vám umožní přístup k funkcím, které poskytuje knihovna Aspose.Cells, zejména pro práci se sešity a daty Power Query.
## Krok 1: Nastavte své pracovní adresáře
Nejprve musíte definovat, kde jsou umístěny vaše zdrojové a výstupní soubory. 
```csharp
string SourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
```
 V tomto kroku zadáte cesty k adresáři. Nahradit`"Your Document Directory"` se skutečnou cestou, kde jsou uloženy vaše soubory Excel. To programu sdělí, kde má hledat zdrojový soubor a kam uložit aktualizovaný.
## Krok 2: Načtěte sešit
Nyní, když máte nastavené pracovní adresáře, je dalším krokem načtení souboru Excel do programu.
```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
 Zde vytvoříte a`Workbook` objekt, který načte zadaný soubor Excel. The`Workbook`třída je součástí knihovny Aspose.Cells a je nezbytná pro všechny operace, které budete s tímto souborem Excelu provádět.
## Krok 3: Přístup k datům Power Query
Po načtení sešitu je čas získat přístup k vzorcům Power Query uloženým v něm.
```csharp
DataMashup mashupData = workbook.DataMashup;
```
 V tomto řádku,`DataMashup` vlastnost pomáhá přistupovat k datovým strukturám Power Query v sešitu. Tato vlastnost vám umožňuje pracovat s různými aspekty dat Power Query obsažených v souboru Excel.
## Krok 4: Procházení vzorců Power Query
S dostupnými daty Power Query je dalším krokem iterace každého z přítomných vzorců.
```csharp
foreach (PowerQueryFormula formula in mashupData.PowerQueryFormulas)
{
    foreach (PowerQueryFormulaItem item in formula.PowerQueryFormulaItems)
    {
        if (item.Name == "Source")
        {
            item.Value = "Excel.Workbook(File.Contents(\"" + SourceDir + "SamplePowerQueryFormulaSource.xlsx\"), null, true)";
        }
    }
}
```
 Tady se děje kouzlo. Procházíme každým`PowerQueryFormula` a pak přes každou`PowerQueryFormulaItem` . The`if` příkaz vyhledá položku vzorce s názvem „Zdroj“ a aktualizuje její hodnotu tak, aby byla cestou ke zdrojovému souboru, na který má Power Query odkazovat. To vám umožňuje dynamicky měnit, ze kterého souboru Power Query získává data.
## Krok 5: Uložte aktualizovaný sešit
Po aktualizaci nezbytných položek vzorce je vaším posledním krokem uložení sešitu.
```csharp
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
```
Tento řádek uloží upravený sešit do nového souboru, čímž zachová původní a zároveň vám umožní pracovat s aktualizovanou verzí.
## Krok 6: Potvrzující zpráva
Nakonec je dobrým zvykem zkontrolovat, zda byl váš kód správně proveden.
```csharp
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
Tato jednoduchá zpráva vám v konzole potvrdí, že vaše operace byla úspěšná, a poskytne uklidňující konec procesu.
## Závěr
A tady to máte! Aktualizaci položek vzorce Power Query v Excelu pomocí Aspose.Cells for .NET lze provést v několika jednoduchých krocích. Podle této příručky můžete efektivně spravovat svá datová připojení aplikace Excel a zajistit hladký chod sešitů. Ať už jste ostřílený profík nebo s manipulací s daty teprve začínáte, Aspose.Cells poskytuje výkonný způsob automatizace a vylepšení pracovních postupů aplikace Excel. 
## FAQ
### Mohu použít Aspose.Cells s jakoukoli verzí .NET?
Aspose.Cells je kompatibilní s více verzemi .NET, včetně .NET Framework a .NET Core.
### Je Aspose.Cells zdarma k použití?
 Aspose.Cells nabízí bezplatnou zkušební verzi, ale pro nepřetržité používání je vyžadována licence. Můžete získat dočasnou licenci[zde](https://purchase.aspose.com/temporary-license/).
### Co když můj stávající soubor Excel nemá Power Query?
Popsaný proces se zaměřuje na aktualizaci položek Power Query, takže pokud je váš soubor postrádá, musíte nejprve začlenit Power Query.
### Kde najdu více informací o Aspose.Cells?
 Podívejte se do dokumentace, kde najdete komplexní pokyny a příklady. Navštivte[dokumentace](https://reference.aspose.com/cells/net/).
### Jak nahlásím chyby nebo problémy s Aspose.Cells?
Na jejich podporovaném fóru se můžete obrátit o pomoc s jakýmikoli problémy, na které narazíte.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
