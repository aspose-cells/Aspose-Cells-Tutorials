---
title: Přidejte textové pole do listu v aplikaci Excel
linktitle: Přidejte textové pole do listu v aplikaci Excel
second_title: Aspose.Cells .NET Excel Processing API
description: V tomto podrobném návodu se dozvíte, jak přidat přizpůsobitelná textová pole do Excelu pomocí Aspose.Cells for .NET.
weight: 14
url: /cs/net/excel-shapes-controls/add-textbox-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidejte textové pole do listu v aplikaci Excel

## Zavedení
Máte zájem vylepšit své excelové tabulky jedinečnými vizuálními prvky, které mohou zaujmout vaše publikum? Přidání textových polí je skvělý způsob, jak toho dosáhnout! S Aspose.Cells for .NET můžete snadno integrovat textová pole do svých excelových listů, díky čemuž budou vaše dokumenty informativnější a vizuálně přitažlivější. Tento podrobný průvodce vás provede jednoduchým procesem přidávání textových polí pomocí Aspose.Cells a ukáže vám, jak je personalizovat pomocí textu, barev, hypertextových odkazů a dalších!
## Předpoklady
Než se ponoříme do zázraku kódování, zde jsou základní předpoklady pro zajištění hladkého zážitku z plavby:
1. Vývojové prostředí .NET: Budete potřebovat funkční rámec .NET spolu s IDE, jako je Visual Studio. Ujistěte se, že je aktualizován na nejnovější verzi!
2.  Aspose.Cells for .NET: Ujistěte se, že máte staženou knihovnu Aspose.Cells. Nejnovější verzi si můžete stáhnout z[zde](https://releases.aspose.com/cells/net/).
3. Základní znalosti programování: Znalost jazyka C# a některé obecné koncepty práce se soubory Excelu usnadní tento tutoriál!
## Importujte balíčky
Nezapomeňte importovat potřebné balíčky na začátku souboru C#. Můžete to udělat takto:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## Nainstalujte Aspose.Cells
Pokud jste tak ještě neučinili, můžete přidat Aspose.Cells prostřednictvím NuGet Package Manager v sadě Visual Studio:
1. Otevřete Visual Studio.
2.  Přejít na`Tools` ->`NuGet Package Manager` ->`Manage NuGet Packages for Solution`.
3. Vyhledejte „Aspose.Cells“ a nainstalujte jej pro svůj projekt.
Nyní, když jsme položili základy, pojďme se vrhnout na zábavnou část!
## Krok 1: Nastavení adresáře dokumentů
Nejprve nastavíme adresář, kde budou uloženy všechny vaše excelové dokumenty. Než začneme vytvářet náš sešit, je nezbytné se ujistit, že tento adresář existuje.
```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory"; 
// Vytvořte adresář, pokud ještě není přítomen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists) 
    System.IO.Directory.CreateDirectory(dataDir);
```
Tento fragment kódu vytvoří adresář s názvem`Your Document Directory` (nahraďte to prosím svou skutečnou cestou), pokud ještě neexistuje. Snadno, ne?
## Krok 2: Vytvoření nového sešitu
Dále musíme vytvořit nový sešit, kam budeme přidávat naše textová pole. To lze snadno provést pomocí několika řádků kódu:
```csharp
// Vytvořte nový sešit.
Workbook workbook = new Workbook();
```
Tento řádek kódu vytvoří nový sešit aplikace Excel. Jednoduché a přímočaré!
## Krok 3: Přístup k prvnímu listu
Nyní, když máme náš sešit připravený, dáme si první list, kam přidáme naše textové pole:
```csharp
// Získejte první pracovní list v knize.
Worksheet worksheet = workbook.Worksheets[0];
```
 Právě tak máte nyní přístup k prvnímu pojmenovanému listu`worksheet`. Je čas to rozzářit!
## Krok 4: Přidání textového pole
Dobře, je čas přidat do našeho prvního textového pole! Jak na to:
```csharp
// Přidejte do kolekce nové textové pole.
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
V tomto řádku určujeme řádek a sloupec, kam bude textové pole umístěno, a také jeho šířku a výšku (160 a 200). Neváhejte a upravte tato čísla podle svého rozvržení!
## Krok 5: Získání objektu TextBox
Po přidání textového pole na něj musíme získat odkaz, abychom mohli přizpůsobit jeho obsah:
```csharp
// Získejte objekt textového pole.
Aspose.Cells.Drawing.TextBox textbox0 = worksheet.TextBoxes[textboxIndex];
```
 Teď,`textbox0` je vaše zlatá vstupenka k úpravě tohoto textového pole!
## Krok 6: Vyplnění textového pole obsahem
Dále poskytneme text do textového pole:
```csharp
// Vyplňte text.
textbox0.Text = "ASPOSE______The .NET & JAVA Component Publisher!";
```
Vkládání textu do textového pole je tak jednoduché! 
## Krok 7: Přizpůsobte vzhled textového pole
Co kdybychom to trochu zpestřili? Můžete upravit barvy písma, styly a další!
```csharp
// Nastavte barvu písma.
textbox0.Font.Color = Color.Blue;
// Nastavte písmo na tučné.
textbox0.Font.IsBold = true;
// Nastavte velikost písma.
textbox0.Font.Size = 14;
// Nastavte atribut písma na kurzívu.
textbox0.Font.IsItalic = true;
```
Neváhejte a pohrajte si s různými barvami a styly, abyste viděli, co vypadá vizuálně nejlépe!
## Krok 8: Přidání hypertextového odkazu
Chcete proměnit textové pole na odkaz, na který lze kliknout? Udělejme jen to:
```csharp
// Přidejte do textového pole hypertextový odkaz.
textbox0.AddHyperlink("http://www.aspose.com/");
```
Nyní každý, kdo klikne na vaše textové pole, bude přenesen na web Aspose. Je to jako kouzlo!
## Krok 9: Nastavení typu umístění textového pole
Máte různé možnosti, jak se má textové pole chovat ve vztahu k vašemu listu. Zde je příklad, jak jej nastavit tak, aby byl volně plovoucí:
```csharp
// Nastavte umístění.
textbox0.Placement = PlacementType.FreeFloating;
```
Případně, pokud chcete změnit velikost a přesunout s buňkami, můžete to nastavit takto:
```csharp
// Nastavte typ umístění tak, jak se bude textové pole pohybovat a měnit velikost s buňkami.
textbox1.Placement = PlacementType.MoveAndSize;
```
## Krok 10: Přizpůsobení formátů čar a výplní
Zde je návod, jak můžete změnit vzhled ohraničení a výplně textového pole:
```csharp
// Získejte formát výplně textového pole.
Aspose.Cells.Drawing.FillFormat fillformat = textbox0.Fill;            
// Získejte typ formátu řádku textového pole.
Aspose.Cells.Drawing.LineFormat lineformat = textbox0.Line;           
// Nastavte tloušťku čáry.
lineformat.Weight = 6;
// Nastavte styl čárky na čtverec.
lineformat.DashStyle = MsoLineDashStyle.SquareDot;
```
Díky tomu můžete textové pole dále přizpůsobit a přidat vizuály, které vyhovují vašemu stylu.
## Krok 11: Přidání dalšího textového pole
Nikdo neřekl, že můžeme přidat pouze jedno textové pole! Vložíme další s jiným textem:
```csharp
// Přidejte další textové pole.
textboxIndex = worksheet.TextBoxes.Add(15, 4, 85, 120);
// Získejte druhé textové pole.
Aspose.Cells.Drawing.TextBox textbox1 = worksheet.TextBoxes[textboxIndex];
// Vložte do něj nějaký text.
textbox1.Text = "This is another simple text box";
```
Nyní opravdu oživíte svůj excelový list několika textovými poli!
## Krok 12: Uložení sešitu
Konečně je čas zachránit naše mistrovské dílo! Zde je poslední řádek kódu pro daný den:
```csharp
// Uložte soubor aplikace Excel.
workbook.Save(dataDir + "book1.out.xls");
```
Pouze s tímto jedním řádkem kódu jste vytvořili a upravili soubor Excel s přizpůsobitelnými textovými poli!
## Závěr
Gratuluji! Úspěšně jste prošli světem textových polí v Excelu pomocí Aspose.Cells for .NET. Naučili jste se nejen přidat textové pole, ale také jak je upravit, aby byly vaše tabulky poutavější. Od změny barev a stylů až po přidání hypertextových odkazů – možnosti jsou prakticky nekonečné! 
Jste připraveni začít transformovat své excelové dokumenty? Nechte svou kreativitu zazářit a experimentujte s různými rozvrženími!
## FAQ
### Co je Aspose.Cells pro .NET?
Aspose.Cells for .NET je výkonná knihovna, která umožňuje vývojářům snadno vytvářet, manipulovat a převádět soubory aplikace Excel.
### Mohu Aspose.Cells před nákupem vyzkoušet?
 Ano! Můžete si stáhnout a používat bezplatnou zkušební verzi[zde](https://releases.aspose.com/).
### Kde najdu dokumentaci k Aspose.Cells?
 Komplexní dokumentaci získáte na adrese[Dokumentace Aspose.Cells](https://reference.aspose.com/cells/net/).
### Je k dispozici podpora, pokud narazím na problémy?
 Absolutně! Pokud potřebujete pomoc, zamiřte na[Fórum Aspose](https://forum.aspose.com/c/cells/9) o pomoc.
### Mohu používat Aspose.Cells bez licence?
 I když můžete používat bezplatnou zkušební verzi, pro přístup k plné funkčnosti si budete muset zakoupit licenci. Podívejte se na ceník[zde](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
