---
title: Uložení kontingenční tabulky ve formátu ODS Programově v .NET
linktitle: Uložení kontingenční tabulky ve formátu ODS Programově v .NET
second_title: Aspose.Cells .NET Excel Processing API
description: tomto podrobném průvodci se dozvíte, jak uložit kontingenční tabulky ve formátu ODS pomocí Aspose.Cells for .NET.
weight: 25
url: /cs/net/creating-and-configuring-pivot-tables/saving-in-ods-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Uložení kontingenční tabulky ve formátu ODS Programově v .NET

## Zavedení
Pokud jde o správu dat v tabulkách, nic se nevyrovná výkonu kontingenčních tabulek. Jedná se o praktický nástroj pro shrnutí, analýzu a prezentaci komplexních datových sad. Dnes se ponoříme do použití Aspose.Cells pro .NET k uložení kontingenční tabulky ve formátu ODS. Ať už jste ostřílený vývojář nebo si jen smočíte nohy s .NET, tento průvodce je pro vás jednoduchý. 
Začněme!
## Předpoklady
Než se pustíme do kódu, budete potřebovat několik základních věcí:
### 1. Základní znalost .NET
Základní znalost .NET a jeho programovacích konceptů vám pomůže snadno sledovat.
### 2. Aspose.Cells pro .NET
 Budete muset mít nainstalovaný Aspose.Cells for .NET. Můžete si jej stáhnout z[Aspose stránku vydání](https://releases.aspose.com/cells/net/) . K dispozici je také zkušební verze[zde](https://releases.aspose.com/).
### 3. Vývojové prostředí
Ujistěte se, že máte IDE jako Visual Studio, kde můžete psát a testovat svůj kód .NET.
### 4. Trochu trpělivosti
Stejně jako u každého kódovacího úsilí je klíčem trpělivost. Nedělejte si starosti, pokud věci napoprvé nefungují dokonale; ladění je součástí procesu.
## Importujte balíčky
Chcete-li pracovat s Aspose.Cells, budete muset importovat potřebné jmenné prostory. Na začátek souboru kódu přidejte následující direktivu using:
```csharp
using System;
using Aspose.Cells.Pivot;
```
Tento řádek vám umožňuje přístup ke všem funkcím v rámci knihovny Aspose.Cells, díky čemuž je váš proces kódování hračkou.
Nyní si tento proces rozdělíme na zvládnutelné kroky.
## Krok 1: Nastavte svůj výstupní adresář
Nejprve musíte definovat, kam chcete uložit soubor ODS. Toto je jednoduché přiřazení cesty k adresáři.
```csharp
string outputDir = "Your Document Directory";
```
 V tomto řádku vyměňte`"Your Document Directory"` s cestou, kam chcete soubor uložit.
## Krok 2: Vytvořte nový sešit
Dále vytvoříte instanci nového objektu Workbook, který bude obsahovat všechna vaše data a struktury, včetně kontingenční tabulky.
```csharp
Workbook workbook = new Workbook();
```
Zde v podstatě začínáte znovu – představte si to jako prázdné plátno, na kterém vytvoříte své mistrovské dílo.
## Krok 3: Otevřete sešit
Nyní, když máme náš sešit, musíme se pustit do práce na našem listu. Aspose.Cells umožňuje snadný přístup k prvnímu dostupnému listu.
```csharp
Worksheet sheet = workbook.Worksheets[0];
```
Tento řádek nás přivede k úplně prvnímu listu, připravenému pro zadávání dat.
## Krok 4: Naplňte buňky daty
Je čas vyplnit náš pracovní list nějakými údaji. Použijeme jednoduchý příklad dat sportovních prodejů. 
Takto můžete nastavit hodnoty v různých buňkách:
```csharp
Cells cells = sheet.Cells;
cells["A1"].PutValue("Sport");
cells["B1"].PutValue("Quarter");
cells["C1"].PutValue("Sales");
cells["A2"].PutValue("Golf");
cells["A3"].PutValue("Golf");
cells["A4"].PutValue("Tennis");
cells["A5"].PutValue("Tennis");
cells["A6"].PutValue("Tennis");
cells["A7"].PutValue("Tennis");
cells["A8"].PutValue("Golf");
cells["B2"].PutValue("Qtr3");
cells["B3"].PutValue("Qtr4");
cells["B4"].PutValue("Qtr3");
cells["B5"].PutValue("Qtr4");
cells["B6"].PutValue("Qtr3");
cells["B7"].PutValue("Qtr4");
cells["B8"].PutValue("Qtr3");
cells["C2"].PutValue(1500);
cells["C3"].PutValue(2000);
cells["C4"].PutValue(600);
cells["C5"].PutValue(1500);
cells["C6"].PutValue(4070);
cells["C7"].PutValue(5000);
cells["C8"].PutValue(6430);
```
V těchto řádcích definujeme nadpisy a naplňujeme údaje o prodeji. Přemýšlejte o tomto kroku jako o zásobení spíže před vařením jídla; čím lepší jsou vaše ingredience (data), tím lepší je vaše jídlo (analýza).
## Krok 5: Vytvořte kontingenční tabulku
Nyní přichází ta zábavná část – vytvoření kontingenční tabulky! Zde je návod, jak jej přidat do pracovního listu:
```csharp
PivotTableCollection pivotTables = sheet.PivotTables;
// Přidání kontingenční tabulky do listu
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```
 V tomto úryvku určujeme rozsah dat pro kontingenční tabulku a kam ji umístit na listu. Rozsah dat`=A1:C8` pokrývá oblast, kde existují naše data.
## Krok 6: Přizpůsobte si kontingenční tabulku
Dále budete chtít upravit kontingenční tabulku tak, aby vyhovovala vašim potřebám. To zahrnuje kontrolu toho, co se zobrazuje, jak je to kategorizováno a jak vypočítává data.
```csharp
PivotTable pivotTable = pivotTables[index];
// Nezobrazování celkových součtů pro řádky.
pivotTable.RowGrand = false;
// Přetažením prvního pole do oblasti řádku.
pivotTable.AddFieldToArea(PivotFieldType.Row, 0);
// Přetažením druhého pole do oblasti sloupců.
pivotTable.AddFieldToArea(PivotFieldType.Column, 1);
// Přetažením třetího pole do datové oblasti.
pivotTable.AddFieldToArea(PivotFieldType.Data, 2);
pivotTable.CalculateData();
```
Zde se rozhodujete, která datová pole chcete shrnout a jak by měla být reprezentována. Je to jako prostírání stolu na večeři; vy rozhodnete, co se nejlépe hodí a jak to prezentovat.
## Krok 7: Uložte sešit
Nakonec jste připraveni uložit svou práci do požadovaného formátu ODS. Postup je následující:
```csharp
workbook.Save(outputDir + "PivotTableSaveInODS_out.ods");
```
Tímto krokem zabalíte svůj projekt a zajistíte jej ve zvoleném adresáři – uspokojivý výsledek!
## Krok 8: Ověřte svůj výstup
Nakonec je vždy dobré zkontrolovat, zda byl proces úspěšně dokončen. Můžete přidat jednoduchou konzolovou zprávu:
```csharp
Console.WriteLine("PivotTableSaveInODS executed successfully.");
```
Tato zpráva se objeví na vaší konzoli, aby potvrdila, že vše proběhlo bez problémů. Stejně jako kuchař, který před podáváním kontroluje, zda je vše uvařeno k dokonalosti!
## Závěr 
tady to máte! Nejenže jste vytvořili kontingenční tabulku pomocí Aspose.Cells, ale také jste ji uložili ve formátu ODS. Tento průvodce vás provede každým krokem a zajistí, že budete vyzbrojeni znalostmi a sebedůvěrou, abyste se v budoucnu mohli vypořádat s podobnými úkoly.
## FAQ
### Co je Aspose.Cells?
Aspose.Cells je propracovaná knihovna, která umožňuje vytvářet a manipulovat se soubory Excelu v aplikacích .NET.
### Mohu používat Aspose.Cells zdarma?
 Ano, můžete si stáhnout bezplatnou zkušební verzi z[Aspose webové stránky](https://releases.aspose.com/).
### Jaké formáty Aspose.Cells podporuje?
Podporuje řadu formátů, včetně XLSX, XLS, ODS, PDF a mnoha dalších.
### Jak získám podporu pro Aspose.Cells?
 Nápovědu najdete na[Aspose Support Forum](https://forum.aspose.com/c/cells/9).
### Je k dispozici dočasná licence?
 Ano, můžete požádat o dočasnou licenci prostřednictvím webu Aspose[zde](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
