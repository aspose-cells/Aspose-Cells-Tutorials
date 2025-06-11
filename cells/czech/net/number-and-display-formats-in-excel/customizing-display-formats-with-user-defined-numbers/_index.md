---
"description": "Naučte se, jak přizpůsobit formáty zobrazení pomocí Aspose.Cells pro .NET. Formátujte data, procenta a měnu pomocí tohoto podrobného návodu."
"linktitle": "Přizpůsobení formátů zobrazení pomocí uživatelem definovaných čísel"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Přizpůsobení formátů zobrazení pomocí uživatelem definovaných čísel"
"url": "/cs/net/number-and-display-formats-in-excel/customizing-display-formats-with-user-defined-numbers/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přizpůsobení formátů zobrazení pomocí uživatelem definovaných čísel

## Zavedení
Práce se soubory aplikace Excel často vyžaduje vlastní formátování buněk, aby se data zobrazovala smysluplnějším a uživatelsky přívětivějším způsobem. Představte si, že vytváříte soubor aplikace Excel pro sestavu. Nechcete jen nezpracovaná čísla. Chcete, aby data, procenta a měny vypadaly elegantně a profesionálně, že? A právě zde přicházejí na řadu vlastní formáty zobrazení. V tomto tutoriálu se podrobně ponoříme do Aspose.Cells pro .NET, abychom vám ukázali, jak si přizpůsobit formát zobrazení čísel pomocí uživatelem definovaných nastavení.
## Předpoklady
Než začnete, ujistěte se, že máte vše připravené, abyste mohli pokračovat v tomto tutoriálu. Zde je to, co budete potřebovat:
- Nainstalován Aspose.Cells pro .NET. [Stáhněte si to zde](https://releases.aspose.com/cells/net/).
- Základní znalost C# a .NET frameworku.
- Platná licence pro Aspose.Cells. Pokud ji nemáte, pořiďte si ji. [bezplatná zkušební verze](https://releases.aspose.com/) nebo požádejte o [dočasná licence](https://purchase.aspose.com/temporary-license/).
- IDE podobné Visual Studiu.
- .NET Framework 4.0 nebo vyšší.
Pokud vám něco chybí, nebojte se. Vždy se můžete vrátit k těmto odkazům a stáhnout si potřebné soubory nebo požádat o pomoc od [Fórum podpory Aspose](https://forum.aspose.com/c/cells/9).
## Importovat jmenné prostory
Než se pustíte do kódu, je třeba importovat požadované jmenné prostory, abyste měli přístup ke všem potřebným funkcím Aspose.Cells.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Tyto dva jmenné prostory budou vašimi hlavními nástroji v tomto tutoriálu. Nyní se přesuňme k té zábavné části:
## Krok 1: Nastavení adresáře projektu
Nejdříve potřebujete místo pro ukládání souborů, že? Vytvořme adresář pro uložení výstupního souboru Excelu. V tomto kroku se také ujistíme, že adresář existuje, než cokoli uložíme.
```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "Your Document Directory";
// Vytvořte adresář, pokud ještě neexistuje.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- Definujeme `dataDir` proměnná pro uložení cesty, kam se bude ukládat výstupní soubor aplikace Excel.
- Pak zkontrolujeme, zda adresář existuje pomocí `System.IO.Directory.Exists()`.
- Pokud adresář neexistuje, bude vytvořen pomocí `System.IO.Directory.CreateDirectory()`.
## Krok 2: Vytvořte nový sešit a přidejte pracovní list
Nyní, když máme adresář, vytvořme nový sešit aplikace Excel a přidejme do něj list.
```csharp
// Vytvoření instance objektu Workbook
Workbook workbook = new Workbook();
// Přidání nového listu do objektu aplikace Excel
int i = workbook.Worksheets.Add();
// Získání odkazu na nově přidaný list předáním jeho indexu listu
Worksheet worksheet = workbook.Worksheets[i];
```
- Nejprve vytvoříme nový `Workbook` objekt. Představte si to jako váš soubor aplikace Excel.
- Do tohoto sešitu přidáme nový list pomocí `Add()` metodu a uložit index do proměnné `i`.
- Na tento pracovní list odkazujeme pomocí `workbook.Worksheets[i]`.
## Krok 3: Přidání data do buňky a úprava jeho formátu
Nyní vložíme aktuální datum do buňky a naformátujeme ho tak, aby se zobrazovalo vlastním způsobem. Místo výchozího formátu data nastavíme vlastní formát, například `d-mmm-yy`.
```csharp
// Přidání aktuálního systémového data do buňky „A1“
worksheet.Cells["A1"].PutValue(DateTime.Now);
// Získání stylu buňky A1
Style style = worksheet.Cells["A1"].GetStyle();
// Nastavení vlastního formátu zobrazení data ve formátu „d-mmm-rr“
style.Custom = "d-mmm-yy";
// Použití stylu na buňku A1
worksheet.Cells["A1"].SetStyle(style);
```
- Do buňky přidáme aktuální systémové datum `A1` pomocí `PutValue(DateTime.Now)`.
- Získáme aktuální styl buňky `A1` pomocí `GetStyle()`.
- Styl buňky upravíme nastavením `style.Custom = "d-mmm-yy"`, který formátuje datum tak, aby zobrazovalo den, zkrácený měsíc a rok.
- Nakonec aplikujeme nový styl na buňku pomocí `SetStyle()`.
## Krok 4: Formátování buňky jako procenta
Dále se budeme zabývat čísly. Přidáme číselnou hodnotu do jiné buňky, například `A2`a naformátujte jej jako procento.
```csharp
// Přidání číselné hodnoty do buňky „A2“
worksheet.Cells["A2"].PutValue(20);
// Získání stylu buňky A2
style = worksheet.Cells["A2"].GetStyle();
// Nastavení vlastního formátu zobrazení pro zobrazení hodnoty v procentech
style.Custom = "0.0%";
// Použití stylu na buňku A2
worksheet.Cells["A2"].SetStyle(style);
```
- Přidáváme hodnotu `20` do buňky `A2`.
- Zjistíme styl buňky `A2` a nastavte vlastní formát na `0.0%` zobrazit hodnotu v procentech (tj. 20 %).
- Nakonec aplikujeme styl na buňku pomocí `SetStyle()`.
## Krok 5: Formátování buňky jako měny
Přidejme další hodnotu, řekněme do buňky `A3`naformátujeme jej tak, aby se zobrazoval jako měna. Abychom to udělali zajímavější, použijeme formát, který zobrazuje kladné hodnoty jako měnu v librách a záporné hodnoty v dolarech.
```csharp
// Přidání číselné hodnoty do buňky „A3“
worksheet.Cells["A3"].PutValue(2546);
// Získání stylu buňky A3
style = worksheet.Cells["A3"].GetStyle();
// Nastavení vlastního formátu zobrazení pro zobrazení hodnoty jako měny
style.Custom = "£#,##0;[Red]$-#,##0";
// Použití stylu na buňku A3
worksheet.Cells["A3"].SetStyle(style);
```
- Přidáváme hodnotu `2546` do buňky `A3`.
- Nastavili jsme vlastní formát `£#,##0;[Red]$-#,##0`, který zobrazuje kladné hodnoty se znakem libry a záporné hodnoty červeně se znakem dolaru.
- Styl aplikujeme na buňku pomocí `SetStyle()`.
## Krok 6: Uložení sešitu
Posledním krokem je uložení sešitu jako souboru aplikace Excel. V tomto tutoriálu použijeme formát Excel 97-2003.
```csharp
// Uložení souboru aplikace Excel
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
- Ten/Ta/To `Save()` Metoda uloží sešit do zadaného adresáře.
- Vybíráme `SaveFormat.Excel97To2003` aby byla zajištěna kompatibilita se staršími verzemi Excelu.
## Závěr
máte to! Právě jsme vytvořili soubor aplikace Excel, přidali vlastní formáty data, procent a měny do konkrétních buněk pomocí Aspose.Cells pro .NET a soubor uložili. Vlastní formátování dělá vaše soubory aplikace Excel mnohem čitelnějšími a profesionálnějšími. Nezapomeňte prozkoumat další možnosti formátování v Aspose.Cells, jako je podmíněné formátování, pro ještě větší kontrolu nad tím, jak vaše data vypadají.
## Často kladené otázky
### Jak mohu v Aspose.Cells použít složitější možnosti formátování?
Můžete kombinovat různé styly formátování, jako je barva písma, ohraničení a barvy pozadí, s vlastními formáty čísel.
### Mohu použít vlastní formát čísla na oblast buněk?
Ano, Aspose.Cells umožňuje aplikovat styl na oblast buněk pomocí `Range.SetStyle()` metoda.
### V jakých dalších formátech souborů mohu sešit uložit?
Aspose.Cells podporuje mnoho formátů, včetně XLSX, CSV a PDF. Jednoduše změňte `SaveFormat` v `Save()` metoda.
### Mohu záporná čísla formátovat jinak?
Rozhodně! Můžete použít vlastní formáty čísel k zobrazení záporných čísel s různými barvami nebo symboly.
### Je Aspose.Cells pro .NET zdarma?
Aspose.Cells nabízí bezplatnou zkušební verzi, ale pro plnou funkčnost budete potřebovat platnou licenci. Můžete získat [dočasná licence zde](https://purchase.aspose.com/temporary-license/).


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}