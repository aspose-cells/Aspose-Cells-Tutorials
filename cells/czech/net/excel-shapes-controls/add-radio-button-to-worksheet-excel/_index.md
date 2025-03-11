---
title: Přidat přepínač do listu v aplikaci Excel
linktitle: Přidat přepínač do listu v aplikaci Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak přidat přepínače do listu aplikace Excel pomocí Aspose.Cells for .NET, pomocí tohoto snadného průvodce krok za krokem. Ideální pro vytváření interaktivních formulářů Excel.
weight: 19
url: /cs/net/excel-shapes-controls/add-radio-button-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidat přepínač do listu v aplikaci Excel

## Zavedení
Přemýšleli jste někdy, jak okořenit své excelové listy interaktivními prvky, jako jsou přepínače? Ať už vytváříte průzkum, formulář nebo analytický nástroj, přidání přepínačů může skutečně zlepšit interakci uživatele. V tomto tutoriálu vás provedeme procesem přidávání přepínačů do listů aplikace Excel pomocí Aspose.Cells for .NET. Vše rozdělíme do snadno pochopitelných kroků a zajistíme, že na konci tohoto článku budete profesionálem. Jste připraveni se ponořit? Začněme!
## Předpoklady
Než se vrhneme na zábavnou část přidávání přepínačů, ujistěte se, že máte vše nastaveno, abyste mohli začít.
1.  Aspose.Cells pro .NET: Nejprve se ujistěte, že jste si stáhli a nainstalovali soubor[Aspose.Cells for .NET](https://releases.aspose.com/cells/net/) knihovna. Můžete si jej stáhnout prostřednictvím NuGet ve Visual Studiu nebo ze stránky stahování.
2. IDE (Integrované vývojové prostředí): K psaní a spouštění kódu C# budete potřebovat IDE, jako je Visual Studio.
3. .NET Framework: Ujistěte se, že máte na svém počítači nainstalované rozhraní .NET Framework 4.0 nebo vyšší. Aspose.Cells to vyžaduje, aby to fungovalo.
4. Základní porozumění C#: Znalost syntaxe C# a programování .NET vám usnadní práci.
Jakmile budete mít vše na svém místě, jsme připraveni začít!
## Importujte balíčky
Před kódováním je nezbytné importovat potřebné jmenné prostory, aby se předešlo případným chybám později. Přidejte do svého kódu následující:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Drawing;
```
Tyto importy jsou nezbytné pro přístup k funkcím sešitu, přidávání přepínačů a manipulaci se soubory.
## Krok 1: Nastavení sešitu
Nejprve vytvořte nový excelový sešit.
 Chcete-li začít, budete muset vytvořit instanci nového`Workbook` objekt. To bude reprezentovat váš soubor Excel v kódu.
```csharp
// Vytvořte nový sešit.
Workbook excelbook = new Workbook();
```
V tomto kroku vytváříte prázdný sešit. Představte si to jako své prázdné plátno, kam v následujících krocích přidáte přepínače.
## Krok 2: Přidání a formátování hodnoty buňky
Dále do listu přidáme název. Do buňky přidáme nějaký text`C2` a naformátujte jej tak, aby byl tučný. Tento krok přidá kontext k vašim přepínačům.
### Vložit text do buňky
```csharp
// Vložte hodnotu do buňky C2.
excelbook.Worksheets[0].Cells["C2"].PutValue("Age Groups");
```
### Změňte text na tučný
```csharp
// Nastavte text písma v buňce C2 na tučné.
excelbook.Worksheets[0].Cells["C2"].GetStyle().Font.IsBold = true;
```
 Zde jsme do buňky přidali jednoduchý název „Věkové skupiny“.`C2`, a udělal to tučně, aby vyniklo. Snadné, že?
## Krok 3: Přidání prvního přepínače
Nyní přichází ta vzrušující část: přidání prvního přepínače do listu!
### Přidejte přepínač
```csharp
// Přidejte přepínač na první list.
Aspose.Cells.Drawing.RadioButton radio1 = excelbook.Worksheets[0].Shapes.AddRadioButton(3, 0, 2, 0, 30, 110);
```
Tento řádek přidá přepínač na konkrétní pozici na listu. Čísla představují jeho umístění a velikost. Představte si to jako nastavení souřadnic X a Y tlačítka.
### Nastavit text přepínacího tlačítka
```csharp
// Nastavte jeho textový řetězec.
radio1.Text = "20-29";
```
Zde jsme přepínači přiřadili štítek „20–29“, který představuje věkovou skupinu.
### Propojte přepínač s buňkou
```csharp
// Nastavte buňku A1 jako propojenou buňku pro přepínač.
radio1.LinkedCell = "A1";
```
 Toto propojí přepínač s buňkou`A1`což znamená, že výsledek výběru tlačítka bude uložen do této buňky.
### Přidat 3D efekt
```csharp
// Udělejte přepínač 3D.
radio1.Shadow = true;
```
Protože chceme, aby se tento přepínač objevil, přidali jsme 3D efekt.
### Přizpůsobte linii přepínacího tlačítka
```csharp
// Nastavte váhu čáry přepínače.
radio1.Line.Weight = 4;
// Nastavte styl čárky řádku přepínače.
radio1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Tyto řádky kódu upravují tloušťku a styl čárky okraje přepínače, aby byl vizuálně přitažlivější.
## Krok 4: Přidání dalších přepínacích tlačítek
Přidejme další dva přepínače pro zbývající věkové skupiny: „30-39“ a „40-49“. Kroky jsou stejné, jen s drobnými odchylkami v souřadnicích a štítcích.
### Přidejte druhý přepínač
```csharp
// Přidejte další přepínač na první list.
Aspose.Cells.Drawing.RadioButton radio2 = excelbook.Worksheets[0].Shapes.AddRadioButton(6, 0, 2, 0, 30, 110);
// Nastavte jeho textový řetězec.
radio2.Text = "30-39";
// Nastavte buňku A1 jako propojenou buňku pro přepínač.
radio2.LinkedCell = "A1";
// Udělejte přepínač 3D.
radio2.Shadow = true;
// Nastavte váhu přepínače.
radio2.Line.Weight = 4;
// Nastavte styl pomlčky přepínače.
radio2.Line.DashStyle = MsoLineDashStyle.Solid;
```
### Přidejte třetí přepínač
```csharp
// Přidejte další přepínač na první list.
Aspose.Cells.Drawing.RadioButton radio3 = excelbook.Worksheets[0].Shapes.AddRadioButton(9, 0, 2, 0, 30, 110);
// Nastavte jeho textový řetězec.
radio3.Text = "40-49";
// Nastavte buňku A1 jako propojenou buňku pro přepínač.
radio3.LinkedCell = "A1";
// Udělejte přepínač 3D.
radio3.Shadow = true;
// Nastavte váhu přepínače.
radio3.Line.Weight = 4;
// Nastavte styl pomlčky přepínače.
radio3.Line.DashStyle = MsoLineDashStyle.Solid;
```
## Krok 5: Uložení souboru Excel
Jakmile jsou všechna vaše přepínače přidána a naformátována, je čas soubor uložit.
```csharp
// Uložte soubor aplikace Excel.
string dataDir = "Your Document Directory";
excelbook.Save(dataDir + "book1.out.xls");
```
tomto kroku se sešit uloží do zadaného adresáře. Je to tak jednoduché – váš interaktivní pracovní list je nyní připraven!
## Závěr
Tady to máš! Právě jste přidali přepínače do listu aplikace Excel pomocí Aspose.Cells pro .NET. Tento kurz pokryl vše od nastavení sešitu, vložení a formátování hodnoty, přidání více přepínačů a jejich propojení s buňkou. Nyní jste připraveni vytvořit interaktivní excelové listy, které nejen skvěle vypadají, ale také poskytují vylepšené uživatelské prostředí. Bavte se objevováním dalších možností s Aspose.Cells!
## FAQ
### Mohu přidat další přepínače do různých listů?  
Absolutně! Proces můžete opakovat na libovolném listu v sešitu zadáním správného indexu listu.
### Mohu si vzhled přepínacích tlačítek dále přizpůsobit?  
Ano, Aspose.Cells poskytuje řadu možností přizpůsobení, včetně změny barev, velikostí a dalších atributů formátování.
### Jak zjistím, který přepínač je vybrán?  
Propojená buňka (např. A1) zobrazí index vybraného přepínače. Můžete zkontrolovat hodnotu propojené buňky a zjistit, která z nich je vybrána.
### Existuje omezení počtu přepínačů, které mohu přidat?  
Ne, neexistuje žádný pevný limit na počet přepínačů, které můžete přidat. Je však dobré zachovat uživatelské rozhraní.
### Mohu používat Aspose.Cells s jinými programovacími jazyky?  
Ano, Aspose.Cells podporuje více programovacích jazyků, včetně Javy. Ale tento tutoriál se konkrétně zaměřuje na .NET.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
