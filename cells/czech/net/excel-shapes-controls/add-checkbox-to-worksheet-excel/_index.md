---
title: Přidat zaškrtávací políčko do listu v aplikaci Excel
linktitle: Přidat zaškrtávací políčko do listu v aplikaci Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Zjistěte, jak snadno přidat zaškrtávací políčka do listů aplikace Excel pomocí Aspose.Cells for .NET pomocí našeho podrobného kurzu, doplněného ukázkami kódu a vysvětleními.
weight: 18
url: /cs/net/excel-shapes-controls/add-checkbox-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidat zaškrtávací políčko do listu v aplikaci Excel

## Zavedení
Pokud jde o správu dat v Excelu, existuje nespočet funkcí a metod, které mohou zefektivnit vaše úkoly a vylepšit vaše tabulky. Jednou z takových funkcí je zaškrtávací políčko – šikovný malý nástroj, který uživatelům umožňuje provádět binární volby přímo v jejich excelových listech. V této příručce vás provedeme procesem přidání zaškrtávacího políčka do listu aplikace Excel pomocí knihovny Aspose.Cells pro .NET. Takže se připoutejte a připravte se na vzrušující cestu do světa automatizace Excelu!
## Předpoklady
Než se ponoříme do groteskního kódování, ujistěte se, že máte vše, co potřebujete, abyste mohli začít. Zde jsou předpoklady:
- Visual Studio: Předpokládáme, že máte pracovní prostředí nastavené pomocí sady Visual Studio. Pokud ne, můžete si jej snadno stáhnout z[Visual Studio](https://visualstudio.microsoft.com/vs/).
- .NET Framework: Ujistěte se, že máte v systému nainstalované rozhraní .NET Framework. Zkontrolujte kompatibilitu Aspose.Cells s vaší verzí .NET.
-  Aspose.Cells for .NET: Budete muset mít knihovnu Aspose.Cells staženou a odkazovanou ve vašem projektu. Můžete si jej stáhnout z[zde](https://releases.aspose.com/cells/net/).
- Základní porozumění C#: Základní pochopení programování C# vám pomůže snadněji následovat příklady.
S těmito předpoklady zaškrtnutými ve vašem seznamu můžeme začít!
## Importujte balíčky
Než začneme kódovat, musíme do našeho projektu C# naimportovat potřebné balíčky. Knihovna Aspose.Cells je pro náš úkol nezbytná a její import je hračka. Postupujte podle těchto kroků:
### Vytvořte nový projekt C#
- Otevřete Visual Studio a vytvořte novou C# Console Application.
### Přidejte odkaz do Aspose.Cells
- Klepněte pravým tlačítkem myši na svůj projekt v Průzkumníku řešení.
- Vyberte „Spravovat balíčky NuGet“.
- Ve Správci balíčků NuGet vyhledejte „Aspose.Cells“ a nainstalujte jej.
### Importujte jmenný prostor
V horní části souboru Program.cs uveďte následující odkaz na jmenný prostor Aspose.Cells:
```csharp
using System.IO;
using Aspose.Cells;
```
Nyní jste připraveni začít kódovat!

Teď se pustíme do práce. Níže jsou uvedeny podrobné pokyny, jak přidat zaškrtávací políčko do listu aplikace Excel pomocí Aspose.Cells.
## Krok 1: Nastavte adresář
Nejprve se musíme ujistit, že adresář pro uložení našeho souboru Excel existuje. Toto je zásadní krok, protože zabraňuje chybám při běhu při pokusu o uložení souboru.
```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
// Vytvořte adresář, pokud ještě není přítomen.
bool isExists = System.IO.Directory.Exists(dataDir);
if (!isExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
## Krok 2: Vytvořte nový sešit
Dále musíme vytvořit novou instanci sešitu. To bude sloužit jako základ pro celý náš soubor Excel.
```csharp
// Vytvořte nový sešit.
Workbook excelBook = new Workbook();
```
## Krok 3: Přidejte do listu zaškrtávací políčko
 Nyní přidáme zaškrtávací políčko do prvního listu našeho sešitu. Polohu a velikost zaškrtávacího políčka můžete určit pomocí`Add` metoda:
```csharp
// Přidejte zaškrtávací políčko do prvního listu v sešitu.
int index = excelBook.Worksheets[0].CheckBoxes.Add(5, 5, 100, 120);
```
## Krok 4: Získejte objekt zaškrtávacího políčka
Jakmile přidáme zaškrtávací políčko, musíme objekt zaškrtávacího políčka načíst, abychom mohli provést další přizpůsobení.
```csharp
// Získejte objekt zaškrtávacího políčka.
Aspose.Cells.Drawing.CheckBox checkbox = excelBook.Worksheets[0].CheckBoxes[index];
```
## Krok 5: Nastavte text zaškrtávacího pole
Co je to zaškrtávací políčko bez štítku? Dejte našemu zaškrtávacímu políčku nějaký text, aby uživatelé věděli, o co jde!
```csharp
// Nastavte jeho textový řetězec.
checkbox.Text = "Click it!";
```
## Krok 6: Propojte zaškrtávací políčko s buňkou
Propojení našeho zaškrtávacího políčka s konkrétní buňkou nám umožňuje snadno sledovat její stav. V tomto případě jej propojíme s buňkou B1.
```csharp
// Vložte hodnotu do buňky B1.
excelBook.Worksheets[0].Cells["B1"].PutValue("LnkCell");
// Nastavte buňku B1 jako propojenou buňku pro zaškrtávací políčko.
checkbox.LinkedCell = "B1";
```
## Krok 7: Nastavte výchozí hodnotu zaškrtávacího políčka
Pokud chcete, aby bylo zaškrtávací políčko ve výchozím nastavení zaškrtnuto při otevření souboru, můžete to také snadno udělat!
```csharp
// Ve výchozím nastavení zaškrtněte políčko.
checkbox.Value = true;
```
## Krok 8: Uložte soubor Excel
Nakonec, po všech těchto krocích, je čas uložit naše mistrovské dílo do určeného adresáře. 
```csharp
// Uložte soubor aplikace Excel.
excelBook.Save(dataDir + "book1.out.xls");
```
A právě tak jste vytvořili soubor Excel s funkčním zaškrtávacím políčkem!
## Závěr
Gratuluji! Právě jste přidali zaškrtávací políčko do listu aplikace Excel pomocí Aspose.Cells pro .NET. Tato výkonná knihovna umožňuje velké množství manipulací s tabulkami a přidávání zaškrtávacích políček je jen poškrábání povrchu. Nyní můžete své dokumenty aplikace Excel přizpůsobit pomocí interaktivních prvků, které vylepšují uživatelskou zkušenost. Tak na co čekáš? Ponořte se do světa automatizace Excelu a prozkoumejte všechny možnosti, které Aspose.Cells nabízí!
## FAQ
### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna .NET, která umožňuje vývojářům vytvářet, manipulovat a spravovat soubory Excelu programově.
### Mohu používat Aspose.Cells zdarma?
 Ano, Aspose nabízí bezplatnou zkušební verzi Aspose.Cells. Můžete si jej stáhnout z[zde](https://releases.aspose.com/).
### Potřebuji licenci k používání Aspose.Cells?
 Zatímco zkušební verzi můžete používat zdarma, pro nepřetržité používání a pro přístup ke všem funkcím je vyžadována placená licence. Můžete si jej zakoupit[zde](https://purchase.aspose.com/buy).
### Kde najdu dokumentaci pro Aspose.Cells?
 K dispozici je kompletní dokumentace[zde](https://reference.aspose.com/cells/net/).
### Jak mohu získat podporu pro Aspose.Cells?
 Pokud máte nějaké dotazy nebo potřebujete pomoc, můžete navštívit fórum podpory Aspose[zde](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
