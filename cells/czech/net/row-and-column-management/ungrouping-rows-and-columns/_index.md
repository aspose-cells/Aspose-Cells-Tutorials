---
"description": "Naučte se, jak v Excelu pomocí Aspose.Cells pro .NET rozdělit seskupení řádků a sloupců v tomto komplexním průvodci. Zjednodušte si manipulaci s daty v Excelu."
"linktitle": "Rozdělení řádků a sloupců v Excelu pomocí Aspose.Cells"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Rozdělení řádků a sloupců v Excelu pomocí Aspose.Cells"
"url": "/cs/net/row-and-column-management/ungrouping-rows-and-columns/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Rozdělení řádků a sloupců v Excelu pomocí Aspose.Cells

## Zavedení
Pokud jde o práci se soubory Excelu, můžete se ocitnout v situacích, kdy potřebujete oddělit seskupení řádků a sloupců. Ať už čistíte tabulku nebo přeformátujete data pro lepší prezentaci, Aspose.Cells pro .NET je fantastický nástroj, který tento proces zjednodušuje. V tomto tutoriálu vás provedu kroky k oddělování seskupení řádků a sloupců v Excelu pomocí Aspose.Cells. Na konci budete mít důkladné znalosti o tom, jak programově pracovat se soubory Excelu.
## Předpoklady
Než se pustíme do kódu, ujistěte se, že máte vše nastavené. Zde je to, co budete potřebovat:
1. Visual Studio: Měli byste mít na svém počítači nainstalovanou funkční verzi Visual Studia. Pokud ji ještě nemáte, můžete si ji stáhnout z [Webové stránky Visual Studia](https://visualstudio.microsoft.com/).
2. Aspose.Cells pro .NET: Budete si muset stáhnout knihovnu Aspose.Cells. Můžete si ji stáhnout z [Stránka s vydáními Aspose](https://releases.aspose.com/cells/net/)Ujistěte se, že máte potřebné licence, které lze zakoupit nebo získat prostřednictvím [dočasná licence](https://purchase.aspose.com/temporary-license/).
3. Základní znalost C#: Základní znalost programování v C# vám pomůže snáze se orientovat.
Jakmile budete mít vše připravené, můžeme se pustit do té zábavné části: kódu!
## Importovat balíčky
Chcete-li začít, musíte do svého projektu C# importovat potřebné balíčky. Postupujte takto:
1. Otevřete svůj projekt ve Visual Studiu.
2. Přidejte odkaz na knihovnu Aspose.Cells. To provedete kliknutím pravým tlačítkem myši na odkazy ve vašem projektu a výběrem možnosti Přidat odkaz. Přejděte do umístění, kam jste uložili knihovnu DLL Aspose.Cells.
3. Na začátek souboru C# přidejte pomocí direktiv následující:
```csharp
using System.IO;
using Aspose.Cells;
```
Nyní, když je vše nastaveno, pojďme si projít kroky k oddělování řádků a sloupců v excelovém listu. 
## Krok 1: Definování adresáře dokumentů
Nejprve je třeba zadat adresář, kde se nachází váš soubor Excel. Můžete to nastavit takto:
```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "Your Document Directory";
```
Nahradit `"Your Document Directory"` se skutečnou cestou v počítači, kde je uložen soubor Excel. 
## Krok 2: Vytvoření souborového streamu
Dále je třeba vytvořit souborový proud pro otevření souboru Excelu. Postupujte takto:
```csharp
// Vytvoření proudu souborů obsahujícího soubor Excel, který se má otevřít
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
Zde otevíráte soubor s názvem `book1.xls`Ujistěte se, že tento soubor existuje ve vámi zadaném adresáři, jinak se zobrazí chyba „soubor nebyl nalezen“.
## Krok 3: Vytvoření instance objektu Workbook
Nyní načtěme soubor aplikace Excel do objektu Workbook. To vám umožní programově manipulovat se sešitem:
```csharp
// Vytvoření instance objektu Workbook
// Otevření souboru Excelu prostřednictvím souborového proudu
Workbook workbook = new Workbook(fstream);
```
S tímto řádkem kódu jste úspěšně načetli soubor aplikace Excel do paměti a jste připraveni s ním pracovat.
## Krok 4: Přístup k pracovnímu listu
Jakmile máte sešit, dalším krokem je přístup ke konkrétnímu listu, ve kterém chcete oddělit seskupení řádků a sloupců. Postupujte takto:
```csharp
// Přístup k prvnímu listu v souboru aplikace Excel
Worksheet worksheet = workbook.Worksheets[0];
```
V tomto případě přistupujeme k prvnímu listu. Pokud jsou vaše data na jiném listu, můžete index odpovídajícím způsobem změnit.
## Krok 5: Rozdělení řádků
A teď přichází ta vzrušující část! Pojďme rozdělit prvních šest řádků (od řádku 0 do řádku 5). Použijeme následující kód:
```csharp
// Rozdělení prvních šesti řádků (od 0 do 5)
worksheet.Cells.UngroupRows(0, 5);
```
Tato metoda odstraní jakékoli seskupení, které bylo použito na zadané řádky. Je to tak jednoduché!
## Krok 6: Rozdělení sloupců
Stejně jako u řádků můžete rozdělit seskupení i u sloupců. Zde je návod, jak rozdělit seskupení prvních tří sloupců (od sloupce 0 do sloupce 2):
```csharp
// Rozdělení prvních tří sloupců (od 0 do 2)
worksheet.Cells.UngroupColumns(0, 2);
```
## Krok 7: Uložení upraveného souboru aplikace Excel
Jakmile rozdělíte seskupení řádků a sloupců, dalším krokem je uložení změn zpět do souboru aplikace Excel. To můžete provést pomocí `Save` metoda:
```csharp
// Uložení upraveného souboru aplikace Excel
workbook.Save(dataDir + "output.xls");
```
V tomto příkladu ukládáme upravený soubor jako `output.xls`Název souboru můžete změnit na libovolný název.
## Krok 8: Zavřete souborový stream
Nakonec, abyste uvolnili zdroje, měli byste zavřít souborový proud:
```csharp
// Uzavření souborového proudu pro uvolnění všech zdrojů
fstream.Close();
```
Toto je dobrý postup, který zajistí, že vaše aplikace nebude uchovávat popisovače souborů déle, než je nutné.
## Závěr
A tady to máte! Úspěšně jste se naučili, jak oddělit řádky a sloupce v souboru aplikace Excel pomocí Aspose.Cells pro .NET. S pouhými několika řádky kódu můžete programově provádět významné změny v souborech aplikace Excel. Ať už automatizujete sestavy nebo připravujete data k analýze, zvládnutí těchto technik vám může ušetřit spoustu času.
## Často kladené otázky
### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna pro práci s excelovými soubory v .NET aplikacích, která umožňuje snadnou manipulaci, konverzi a vytváření tabulek.
### Mohu v Excelu rozdělit seskupení řádků a sloupců pomocí jiných knihoven?
Ano, pro manipulaci s Excelem v .NET jsou k dispozici i jiné knihovny, ale Aspose.Cells nabízí rozsáhlé funkce a snadné použití.
### Existuje způsob, jak vrátit změny po uložení?
Po uložení souboru aplikace Excel nelze předchozí stav obnovit, pokud nemáte zálohu původního souboru.
### Jak získám podporu pro Aspose.Cells?
Podporu můžete najít na adrese [Fórum podpory Aspose](https://forum.aspose.com/c/cells/9), kde můžete klást otázky a hledat řešení.
### Mohu používat Aspose.Cells bez licence?
Ano, Aspose.Cells můžete používat zdarma s určitými omezeními a můžete začít s [dočasná licence](https://purchase.aspose.com/temporary-license/) pro plnou funkčnost.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}