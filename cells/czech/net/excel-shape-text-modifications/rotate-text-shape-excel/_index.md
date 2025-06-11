---
"description": "Naučte se, jak otáčet text s tvary v Excelu pomocí Aspose.Cells pro .NET. Postupujte podle tohoto podrobného návodu pro perfektní prezentaci v Excelu."
"linktitle": "Otočení textu s tvarem v Excelu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Otočení textu s tvarem v Excelu"
"url": "/cs/net/excel-shape-text-modifications/rotate-text-shape-excel/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Otočení textu s tvarem v Excelu

## Zavedení
Ve světě Excelu je vizuální reprezentace stejně důležitá jako samotná data. Ať už vytváříte sestavu nebo navrhujete dynamický dashboard, způsob, jakým jsou informace rozloženy, může dramaticky ovlivnit jejich čitelnost a celkový vzhled. Chtěli jste tedy někdy otočit text, abyste jej stylově zarovnali s tvary? Máte štěstí! V tomto tutoriálu se ponoříme do toho, jak otáčet text s tvary pomocí Aspose.Cells pro .NET, a zajistíme tak, aby vaše tabulky nejen informovaly, ale také zapůsobily.
## Předpoklady
Než začneme, ujistěme se, že máte vše, co potřebujete:
1. Visual Studio: Ujistěte se, že máte na svém počítači nainstalované Visual Studio, protože tam budeme psát náš kód.
2. Aspose.Cells pro .NET: Budete potřebovat knihovnu Aspose.Cells. Můžete [stáhněte si nejnovější verzi zde](https://releases.aspose.com/cells/net/) nebo si to vyzkoušejte zdarma s [bezplatná zkušební verze](https://releases.aspose.com/).
3. Základní znalost C#: Znalost prostředí C# a .NET bude užitečná, i když vás provedeme každým krokem.
4. Soubor Excel: Ukázkový soubor Excel, nazvěme ho `sampleRotateTextWithShapeInsideWorksheet.xlsx`, je potřeba k otestování našeho kódu. Tento soubor byste měli umístit do adresáře, ke kterému máte snadný přístup.
Máte všechno připravené? Skvělé! Pojďme se pustit do té zábavné části.
## Importovat balíčky
Abychom mohli projekt spustit, musíme do něj importovat potřebné balíčky. Postupujte takto:
### Vytvořit nový projekt
1. Otevřete Visual Studio.
2. Vyberte možnost „Vytvořit nový projekt“.
3. Vyberte „Konzolová aplikace“ a jako preferovaný programovací jazyk vyberte C#.
### Instalace Aspose.Cells
Nyní přidejme do vašeho projektu Aspose.Cells. Můžete to udělat pomocí Správce balíčků NuGet:
1. V horní nabídce otevřete „Nástroje“.
2. Vyberte „Správce balíčků NuGet“ a poté „Spravovat balíčky NuGet pro řešení“.
3. Hledat „Aspose.Cells“.
4. Klikněte na tlačítko „Instalovat“ pro přidání do projektu.
### Přidat pomocí direktivy
Na začátek hlavního souboru C# je třeba přidat následující direktivu:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
Teď už jsme připraveni začít s kódováním!
Rozdělme si proces na snadno stravitelné kroky. Zde je návod, jak otočit text s tvary v souboru aplikace Excel:
## Krok 1: Nastavení cest k adresářům
Nejprve je třeba nastavit zdrojové a výstupní adresáře, kam budou uloženy vaše soubory aplikace Excel. Postupujte takto:
```csharp
//Zdrojový adresář
string sourceDir = "Your Document Directory"; // Nastavení adresáře dokumentů
//Výstupní adresář
string outputDir = "Your Document Directory"; // Nastavte výstupní adresář
```
Nahradit `"Your Document Directory"` se skutečnou cestou, kde se nachází vaše `sampleRotateTextWithShapeInsideWorksheet.xlsx` soubor se nachází.
## Krok 2: Načtěte ukázkový soubor Excel
Nyní si načtěme ukázkový soubor aplikace Excel. To je klíčové, protože chceme manipulovat s existujícími daty.
```csharp
//Načíst ukázkový soubor Excel.
Workbook wb = new Workbook(sourceDir + "sampleRotateTextWithShapeInsideWorksheet.xlsx");
```
## Krok 3: Přístup k pracovnímu listu
Jakmile je soubor načten, potřebujeme přistupovat ke konkrétnímu listu, který chceme upravit. V našem případě je to první list.
```csharp
//Zpřístupněte první pracovní list.
Worksheet ws = wb.Worksheets[0];
```
## Krok 4: Úprava buňky
Dále upravíme konkrétní buňku tak, aby zobrazovala zprávu. V našem příkladu použijeme buňku B4.
```csharp
//Otevřete buňku B4 a přidejte do ní zprávu.
Cell b4 = ws.Cells["B4"];
b4.PutValue("Text is not rotating with shape because RotateTextWithShape is false.");
```
V tomto kroku se jedná o komunikaci – o zajištění toho, aby ten, kdo tento list otevře, chápal, co upravujeme.
## Krok 5: Získejte přístup k prvnímu tvaru
Pro otáčení textu potřebujeme tvar, se kterým budeme pracovat. Zde si vybereme první tvar v listu.
```csharp
//Zpřístupněte první tvar.
Shape sh = ws.Shapes[0];
```
## Krok 6: Úprava zarovnání textu tvaru
A tady se začne dít ta pravá magie. Upravíme vlastnosti zarovnání textu tvaru.
```csharp
//Zarovnání textu tvaru v Accessu.
Aspose.Cells.Drawing.Texts.ShapeTextAlignment shapeTextAlignment = sh.TextBody.TextAlignment;
//Neotáčejte text s tvarem nastavením RotateTextWithShape na hodnotu false.
shapeTextAlignment.RotateTextWithShape = false;
```
Nastavením `RotateTextWithShape` Na hodnotu false zajistíme, aby text zůstal svislý a neotáčel se s tvarem, čímž zachováme přehlednost a přehlednost.
## Krok 7: Uložení výstupního souboru Excel
Nakonec uložme změny do nového souboru aplikace Excel. Tím zajistíme, že o úpravy nepřijdeme a budeme mít přehledný výstup.
```csharp
//Uložte výstupní soubor Excel.
wb.Save(outputDir + "outputRotateTextWithShapeInsideWorksheet.xlsx");
```
A to je vše! Výstupní soubor je nyní uložen, včetně textu v buňce B4 a úprav provedených na tvaru.
## Krok 8: Spusťte kód
Ve vašem `Main` metodu, zabalte všechny výše uvedené úryvky kódu a spusťte projekt. Sledujte, jak se změny projeví ve výstupním souboru!
```csharp
Console.WriteLine("RotateTextWithShapeInsideWorksheet executed successfully.");
```
## Závěr
Otáčení textu s tvary v Excelu pomocí Aspose.Cells pro .NET se může zpočátku zdát jako složitý proces, ale jakmile si ho rozeberete, je to docela jednoduché. Dodržováním těchto jednoduchých kroků si můžete přizpůsobit tabulky tak, aby vypadaly profesionálněji a vizuálně atraktivněji. Ať už to děláte pro klienta nebo pro své osobní projekty, všichni budou nadšeně chválit kvalitu vaší práce!
## Často kladené otázky
### Mohu používat Aspose.Cells zdarma?
Ano! Můžete použít [bezplatná zkušební verze](https://releases.aspose.com/) vyzkoušet si knihovnu.
### Jaké verze Excelu podporuje Aspose.Cells?
Aspose.Cells podporuje řadu formátů aplikace Excel, včetně XLS, XLSX, CSV a dalších.
### Je možné otáčet text s tvary ve starších verzích Excelu?
Ano, tuto funkcionalitu lze použít i pro starší formáty podporované službou Aspose.Cells.
### Kde najdu další dokumentaci o Aspose.Cells?
Můžete si prohlédnout komplexní [dokumentace](https://reference.aspose.com/cells/net/) pro více informací.
### Jak získám podporu pro Aspose.Cells?
O podporu můžete požádat na adrese [Fórum Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}