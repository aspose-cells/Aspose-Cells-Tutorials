---
title: Přizpůsobení formátů zobrazení pomocí uživatelem definovaných čísel
linktitle: Přizpůsobení formátů zobrazení pomocí uživatelem definovaných čísel
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak přizpůsobit formáty zobrazení pomocí Aspose.Cells pro .NET. Formátujte data, procenta a měnu pomocí tohoto podrobného průvodce.
weight: 11
url: /cs/net/number-and-display-formats-in-excel/customizing-display-formats-with-user-defined-numbers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přizpůsobení formátů zobrazení pomocí uživatelem definovaných čísel

## Zavedení
Práce se soubory aplikace Excel často vyžaduje vlastní formátování buněk, aby byla data prezentována smysluplnějším a uživatelsky přívětivějším způsobem. Představte si, že vytváříte soubor Excel pro sestavu. Nechcete jen hrubá čísla. Chcete, aby data, procenta a měny vypadaly elegantně a profesionálně, že? Zde přicházejí na řadu vlastní formáty zobrazení. V tomto tutoriálu se ponoříme hluboko do Aspose.Cells for .NET, abychom vám ukázali, jak přizpůsobit formát zobrazení čísel pomocí uživatelsky definovaných nastavení.
## Předpoklady
Než začnete, ujistěte se, že máte vše připraveno k pokračování spolu s tímto návodem. Zde je to, co budete potřebovat:
-  Aspose.Cells for .NET nainstalován.[Stáhněte si jej zde](https://releases.aspose.com/cells/net/).
- Základní znalost C# a .NET frameworku.
-  Platná licence pro Aspose.Cells. Pokud žádný nemáte, vezměte si[zkušební verze zdarma](https://releases.aspose.com/) nebo požádat a[dočasná licence](https://purchase.aspose.com/temporary-license/).
- IDE jako Visual Studio.
- .NET Framework 4.0 nebo vyšší.
 Pokud vám něco chybí, nebojte se. Tyto odkazy můžete kdykoli znovu navštívit a stáhnout si potřebné soubory nebo vyhledat pomoc na webu[Aspose fórum podpory](https://forum.aspose.com/c/cells/9).
## Importovat jmenné prostory
Než skočíte do kódu, musíte importovat požadované jmenné prostory, abyste získali přístup ke všem potřebným funkcím Aspose.Cells.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Tyto dva jmenné prostory budou vašimi základními nástroji v tomto tutoriálu. Nyní přejdeme k zábavnější části:
## Krok 1: Nastavení adresáře projektu
Nejprve potřebujete místo pro uložení souborů, že? Vytvořme adresář pro uložení výstupního souboru Excel. V tomto kroku se také před uložením čehokoli ujistíme, že adresář existuje.
```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
// Vytvořte adresář, pokud ještě není přítomen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
-  Definujeme a`dataDir` proměnná pro uložení cesty, kam půjde výstupní soubor Excel.
-  Poté zkontrolujeme, zda adresář existuje pomocí`System.IO.Directory.Exists()`.
-  Pokud adresář neexistuje, bude vytvořen pomocí`System.IO.Directory.CreateDirectory()`.
## Krok 2: Vytvořte nový sešit a přidejte list
Nyní, když máme svůj adresář, vytvoříme nový excelový sešit a přidáme do něj list.
```csharp
// Vytvoření instance objektu sešitu
Workbook workbook = new Workbook();
// Přidání nového listu do objektu aplikace Excel
int i = workbook.Worksheets.Add();
// Získání odkazu na nově přidaný list předáním jeho indexu listu
Worksheet worksheet = workbook.Worksheets[i];
```
-  Nejprve vytvoříme nový`Workbook` objekt. Představte si to jako soubor aplikace Excel.
-  Do tohoto sešitu přidáme nový pracovní list pomocí`Add()` uložte index do proměnné`i`.
-  Na tento pracovní list odkazujeme pomocí`workbook.Worksheets[i]`.
## Krok 3: Přidání data do buňky a přizpůsobení jejího formátu
 Nyní vložíme aktuální datum do buňky a naformátujeme jej tak, aby se zobrazoval vlastním způsobem. Místo výchozího formátu data nastavíme vlastní formát jako`d-mmm-yy`.
```csharp
// Přidání aktuálního systémového data do buňky "A1".
worksheet.Cells["A1"].PutValue(DateTime.Now);
// Získání stylu buňky A1
Style style = worksheet.Cells["A1"].GetStyle();
// Nastavení vlastního formátu zobrazení pro zobrazení data jako "d-mmm-rr"
style.Custom = "d-mmm-yy";
// Použití stylu na buňku A1
worksheet.Cells["A1"].SetStyle(style);
```
-  Do buňky přidáme aktuální systémové datum`A1` pomocí`PutValue(DateTime.Now)`.
-  Načteme aktuální styl buňky`A1` pomocí`GetStyle()`.
-  Nastavením upravíme styl buňky`style.Custom = "d-mmm-yy"`, který formátuje datum tak, aby zobrazoval den, zkrácený měsíc a rok.
-  Nakonec aplikujeme nový styl na buňku s`SetStyle()`.
## Krok 4: Formátování buňky jako procento
 Dále pracujme s čísly. Do jiné buňky přidáme číselnou hodnotu, řekněme`A2`a naformátujte jej jako procento.
```csharp
//Přidání číselné hodnoty do buňky "A2".
worksheet.Cells["A2"].PutValue(20);
// Získání stylu buňky A2
style = worksheet.Cells["A2"].GetStyle();
// Nastavení vlastního formátu zobrazení pro zobrazení hodnoty v procentech
style.Custom = "0.0%";
// Použití stylu na buňku A2
worksheet.Cells["A2"].SetStyle(style);
```
-  Přidáme hodnotu`20` do buňky`A2`.
-  Načteme styl buňky`A2` a nastavte vlastní formát na`0.0%` pro zobrazení hodnoty v procentech (tj. 20 %).
-  Nakonec aplikujeme styl na buňku pomocí`SetStyle()`.
## Krok 5: Formátování buňky jako měny
 Přidejme další hodnotu, řekněme do buňky`A3`a naformátujte jej tak, aby se zobrazoval jako měna. Aby to bylo zajímavější, použijeme formát, který zobrazuje kladné hodnoty jako měnu v librách a záporné hodnoty v dolarech.
```csharp
// Přidání číselné hodnoty do buňky "A3".
worksheet.Cells["A3"].PutValue(2546);
// Získání stylu buňky A3
style = worksheet.Cells["A3"].GetStyle();
// Nastavení vlastního formátu zobrazení pro zobrazení hodnoty jako měny
style.Custom = "£#,##0;[Red]$-#,##0";
// Použití stylu na buňku A3
worksheet.Cells["A3"].SetStyle(style);
```
-  Přidáme hodnotu`2546` do buňky`A3`.
-  Nastavíme vlastní formát`£#,##0;[Red]$-#,##0`, která zobrazuje kladné hodnoty se znakem libry a záporné hodnoty červeně se znakem dolaru.
- Styl aplikujeme na buňku pomocí`SetStyle()`.
## Krok 6: Uložení sešitu
Posledním krokem je uložení sešitu jako souboru aplikace Excel. Pro tento tutoriál použijeme formát Excel 97-2003.
```csharp
// Uložení souboru Excel
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
-  The`Save()` metoda uloží sešit do zadaného adresáře.
-  vybíráme`SaveFormat.Excel97To2003` aby byla zajištěna kompatibilita se staršími verzemi Excelu.
## Závěr
Tady to máš! Právě jsme vytvořili soubor Excel, přidali vlastní datum, procento a formáty měny do konkrétních buněk pomocí Aspose.Cells pro .NET a soubor uložili. Díky vlastnímu formátování jsou vaše soubory Excel mnohem čitelnější a profesionálnější. Nezapomeňte prozkoumat další možnosti formátování v Aspose.Cells, jako je podmíněné formátování, abyste získali ještě větší kontrolu nad tím, jak vaše data vypadají.
## FAQ
### Jak mohu použít složitější možnosti formátování v Aspose.Cells?
S vlastními formáty čísel můžete kombinovat různé styly formátování, jako je barva písma, ohraničení a pozadí.
### Mohu použít vlastní číselný formát na rozsah buněk?
Ano, Aspose.Cells vám umožňuje použít styl na řadu buněk pomocí`Range.SetStyle()` metoda.
### V jakých dalších formátech souborů mohu sešit uložit?
 Aspose.Cells podporuje mnoho formátů, včetně XLSX, CSV a PDF. Jednoduše změňte`SaveFormat` v`Save()` metoda.
### Mohu záporná čísla formátovat jinak?
Absolutně! K zobrazení záporných čísel s různými barvami nebo symboly můžete použít vlastní formáty čísel.
### Je Aspose.Cells for .NET zdarma?
 Aspose.Cells nabízí bezplatnou zkušební verzi, ale pro plnou funkčnost budete potřebovat platnou licenci. Můžete získat a[dočasná licence zde](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
