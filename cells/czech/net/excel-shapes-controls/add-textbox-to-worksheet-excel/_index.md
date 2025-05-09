---
"description": "V tomto podrobném tutoriálu se naučte, jak přidat přizpůsobitelná textová pole do Excelu pomocí Aspose.Cells pro .NET."
"linktitle": "Přidání textového pole do listu v Excelu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Přidání textového pole do listu v Excelu"
"url": "/cs/net/excel-shapes-controls/add-textbox-to-worksheet-excel/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přidání textového pole do listu v Excelu

## Zavedení
Chcete vylepšit své excelovské tabulky jedinečnými vizuálními prvky, které zaujmou vaše publikum? Přidání textových polí je skvělý způsob, jak toho dosáhnout! S Aspose.Cells pro .NET můžete snadno integrovat textová pole do excelových listů, čímž se vaše dokumenty stanou informativnějšími a vizuálně atraktivnějšími. Tento podrobný návod vás provede jednoduchým procesem přidávání textových polí pomocí Aspose.Cells a ukáže vám, jak je přizpůsobit pomocí textu, barev, hypertextových odkazů a dalších prvků!
## Předpoklady
Než se ponoříme do zázraku kódování, zde jsou základní předpoklady pro zajištění hladkého průběhu:
1. Vývojové prostředí .NET: Budete potřebovat funkční framework .NET a vývojové prostředí (IDE), jako je Visual Studio. Ujistěte se, že je aktualizované na nejnovější verzi!
2. Aspose.Cells pro .NET: Ujistěte se, že máte staženou knihovnu Aspose.Cells. Nejnovější verzi si můžete stáhnout z [zde](https://releases.aspose.com/cells/net/).
3. Základní znalosti programování: Znalost jazyka C# a některých obecných konceptů práce se soubory Excelu vám tento tutoriál usnadní!
## Importovat balíčky
Nezapomeňte importovat potřebné balíčky na začátek souboru C#. Zde je návod, jak to udělat:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## Instalace Aspose.Cells
Pokud jste tak ještě neučinili, můžete Aspose.Cells přidat pomocí Správce balíčků NuGet ve Visual Studiu:
1. Otevřete Visual Studio.
2. Jdi na `Tools` -> `NuGet Package Manager` -> `Manage NuGet Packages for Solution`.
3. Vyhledejte „Aspose.Cells“ a nainstalujte si jej pro svůj projekt.
Teď, když jsme položili základy, pojďme se pustit do té zábavné části!
## Krok 1: Nastavení adresáře dokumentů
Nejprve si nastavme adresář, kam budou uloženy všechny vaše dokumenty aplikace Excel. Než začneme vytvářet sešit, je nezbytné se ujistit, že tento adresář existuje.
```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "Your Document Directory"; 
// Vytvořte adresář, pokud ještě neexistuje.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists) 
    System.IO.Directory.CreateDirectory(dataDir);
```
Tento úryvek kódu vytvoří adresář s názvem `Your Document Directory` (prosím, nahraďte to svou skutečnou cestou), pokud ještě neexistuje. Jednoduché, že?
## Krok 2: Vytvoření instance nového sešitu
Dále musíme vytvořit nový sešit, do kterého budeme přidávat textová pole. To lze snadno provést pomocí několika řádků kódu:
```csharp
// Vytvořte instanci nového sešitu.
Workbook workbook = new Workbook();
```
Tento řádek kódu vytvoří nový sešit aplikace Excel. Jednoduché a přímočaré!
## Krok 3: Přístup k prvnímu pracovnímu listu
Nyní, když máme připravený sešit, si připravme první list, kam přidáme textové pole:
```csharp
// Vezměte si první pracovní list v knize.
Worksheet worksheet = workbook.Worksheets[0];
```
A právě tak máte nyní přístup k prvnímu listu s názvem `worksheet`Je čas to zazářit!
## Krok 4: Přidání textového pole
Dobře, je čas přidat naše první textové pole! Zde je návod, jak to udělat:
```csharp
// Přidejte do kolekce nové textové pole.
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
tomto řádku určujeme řádek a sloupec, kam bude textové pole umístěno, a také nastavujeme jeho šířku a výšku (160 a 200). Tato čísla můžete upravit podle svého rozvržení!
## Krok 5: Získání objektu TextBox
Po přidání textového pole potřebujeme získat odkaz na něj, abychom mohli přizpůsobit jeho obsah:
```csharp
// Získejte objekt textového pole.
Aspose.Cells.Drawing.TextBox textbox0 = worksheet.TextBoxes[textboxIndex];
```
Teď, `textbox0` je vaše zlatá vstupenka k úpravě tohoto textového pole!
## Krok 6: Naplnění textového pole obsahem
Dále zadáme text pro textové pole:
```csharp
// Doplňte text.
textbox0.Text = "ASPOSE______The .NET & JAVA Component Publisher!";
```
Vkládání textu do textového pole je tak jednoduché! 
## Krok 7: Přizpůsobení vzhledu textového pole
Co kdybychom to trochu vylepšili? Můžete upravit barvy písma, styly a další!
```csharp
// Nastavte barvu písma.
textbox0.Font.Color = Color.Blue;
// Nastavte písmo na tučné.
textbox0.Font.IsBold = true;
// Nastavte velikost písma.
textbox0.Font.Size = 14;
// Nastavit atribut písma na kurzívu.
textbox0.Font.IsItalic = true;
```
Nebojte se hrát si s různými barvami a styly, abyste zjistili, co vizuálně nejlépe vynikne!
## Krok 8: Přidání hypertextového odkazu
Chcete proměnit textové pole v odkaz, na který lze kliknout? Udělejme to:
```csharp
// Přidejte hypertextový odkaz do textového pole.
textbox0.AddHyperlink("http://www.aspose.com/");
```
Nyní bude každý, kdo klikne na vaše textové pole, přesměrován na webové stránky Aspose. Je to jako kouzlo!
## Krok 9: Nastavení typu umístění textového pole
Máte různé možnosti, jak se má textové pole chovat ve vztahu k listu. Zde je příklad, jak ho nastavit jako volně plovoucí:
```csharp
// Nastavte umístění.
textbox0.Placement = PlacementType.FreeFloating;
```
Alternativně, pokud chcete, aby se velikost a pohyb buněk měnily, můžete to nastavit takto:
```csharp
// Nastavte typ umístění, protože textové pole se bude pohybovat a měnit jeho velikost s buňkami.
textbox1.Placement = PlacementType.MoveAndSize;
```
## Krok 10: Úprava formátů čar a výplní
Zde je návod, jak změnit vzhled okraje a výplně textového pole:
```csharp
// Získejte formát výplně textového pole.
Aspose.Cells.Drawing.FillFormat fillformat = textbox0.Fill;            
// Získá typ formátu řádku textového pole.
Aspose.Cells.Drawing.LineFormat lineformat = textbox0.Line;           
// Nastavte tloušťku čáry.
lineformat.Weight = 6;
// Nastavte styl čárkování na čtvercový bod.
lineformat.DashStyle = MsoLineDashStyle.SquareDot;
```
Díky tomu si můžete textové pole dále přizpůsobit a přidat vizuální prvky, které odpovídají vašemu stylu.
## Krok 11: Přidání dalšího textového pole
Nikdo neříkal, že můžeme přidat jen jedno textové pole! Vložme tam další s jiným textem:
```csharp
// Přidejte další textové pole.
textboxIndex = worksheet.TextBoxes.Add(15, 4, 85, 120);
// Získejte druhé textové pole.
Aspose.Cells.Drawing.TextBox textbox1 = worksheet.TextBoxes[textboxIndex];
// Vložte do něj nějaký text.
textbox1.Text = "This is another simple text box";
```
Teď si svůj excelový list pořádně vylepšujete několika textovými poli!
## Krok 12: Uložení sešitu
Konečně je čas uložit naše mistrovské dílo! Zde je poslední řádek kódu pro dnešek:
```csharp
// Uložte soubor Excelu.
workbook.Save(dataDir + "book1.out.xls");
```
S tímto jediným řádkem kódu jste vytvořili a upravili soubor aplikace Excel s přizpůsobitelnými textovými poli!
## Závěr
Gratulujeme! Úspěšně jste se zorientovali ve světě textových polí v Excelu pomocí Aspose.Cells pro .NET. Naučili jste se nejen, jak přidat textové pole, ale také jak si ho přizpůsobit, aby vaše tabulky byly poutavější. Od změny barev a stylů až po přidání hypertextových odkazů, možnosti jsou prakticky nekonečné! 
Jste připraveni začít transformovat své excelovské dokumenty? Nechte zazářit svou kreativitu a experimentujte s různými rozvrženími!
## Často kladené otázky
### Co je Aspose.Cells pro .NET?
Aspose.Cells pro .NET je výkonná knihovna, která vývojářům umožňuje snadno vytvářet, manipulovat a převádět soubory aplikace Excel.
### Mohu si Aspose.Cells vyzkoušet před koupí?
Ano! Můžete si stáhnout a používat bezplatnou zkušební verzi [zde](https://releases.aspose.com/).
### Kde najdu dokumentaci k Aspose.Cells?
Komplexní dokumentaci získáte na adrese [Dokumentace k Aspose.Cells](https://reference.aspose.com/cells/net/).
### Je k dispozici podpora, pokud narazím na problémy?
Rozhodně! Pokud potřebujete pomoc, zamiřte na [Fórum Aspose](https://forum.aspose.com/c/cells/9) o pomoc.
### Mohu používat Aspose.Cells bez licence?
I když můžete používat bezplatnou zkušební verzi, pro přístup k plné funkcionalitě si budete muset zakoupit licenci. Podívejte se na ceny. [zde](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}