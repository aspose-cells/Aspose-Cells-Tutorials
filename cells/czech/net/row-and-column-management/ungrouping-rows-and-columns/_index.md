---
title: Oddělte seskupení řádků a sloupců v aplikaci Excel pomocí Aspose.Cells
linktitle: Oddělte seskupení řádků a sloupců v aplikaci Excel pomocí Aspose.Cells
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak oddělit řádky a sloupce v Excelu pomocí Aspose.Cells for .NET, pomocí tohoto komplexního průvodce. Zjednodušte si manipulaci s daty v Excelu.
weight: 15
url: /cs/net/row-and-column-management/ungrouping-rows-and-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Oddělte seskupení řádků a sloupců v aplikaci Excel pomocí Aspose.Cells

## Zavedení
Pokud jde o práci se soubory aplikace Excel, můžete se dostat do situací, kdy potřebujete oddělit řádky a sloupce. Ať už čistíte tabulku nebo přeformátujete data pro lepší prezentaci, Aspose.Cells for .NET je fantastický nástroj, který celý proces zjednodušuje. V tomto tutoriálu vás provedu kroky k oddělení řádků a sloupců v Excelu pomocí Aspose.Cells. Na konci budete dobře rozumět tomu, jak programově pracovat se soubory Excelu.
## Předpoklady
Než se ponoříte do kódu, ujistěte se, že máte vše nastaveno. Zde je to, co budete potřebovat:
1.  Visual Studio: Měli byste mít na svém počítači nainstalovanou pracovní verzi sady Visual Studio. Pokud ji ještě nemáte, můžete si ji stáhnout z[Web Visual Studia](https://visualstudio.microsoft.com/).
2. Aspose.Cells for .NET: Budete si muset stáhnout knihovnu Aspose.Cells. Můžete to vzít z[Stránka Aspose Releases](https://releases.aspose.com/cells/net/) . Ujistěte se, že máte potřebné licence, které lze zakoupit nebo získat prostřednictvím a[dočasná licence](https://purchase.aspose.com/temporary-license/).
3. Základní znalost C#: Základní znalost programování v C# vám pomůže snadněji se orientovat.
Jakmile budete mít vše připraveno, můžeme se vrhnout na zábavnější část: kód!
## Importujte balíčky
Chcete-li začít, musíte do svého projektu C# importovat potřebné balíčky. Postup je následující:
1. Otevřete projekt v sadě Visual Studio.
2. Přidejte odkaz na knihovnu Aspose.Cells. Můžete to udělat kliknutím pravým tlačítkem myši na reference ve vašem projektu a výběrem Přidat referenci. Přejděte do umístění, kam jste uložili Aspose.Cells DLL.
3. V horní části souboru C# přidejte následující pomocí direktiv:
```csharp
using System.IO;
using Aspose.Cells;
```
Nyní, když je vše nastaveno, pojďme si projít kroky k oddělení řádků a sloupců v listu aplikace Excel. 
## Krok 1: Definujte adresář dokumentů
Nejprve musíte určit adresář, kde se nachází váš soubor Excel. Můžete to nastavit následovně:
```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
```
 Nahradit`"Your Document Directory"` se skutečnou cestou ve vašem počítači, kde je soubor Excel uložen. 
## Krok 2: Vytvořte stream souborů
Dále je třeba vytvořit datový proud souboru pro otevření souboru aplikace Excel. Můžete to udělat takto:
```csharp
// Vytvoření datového proudu souboru obsahujícího soubor Excel, který se má otevřít
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
 Zde otevíráte soubor s názvem`book1.xls`. Ujistěte se, že tento soubor existuje ve vašem zadaném adresáři, jinak narazíte na chybu nenalezen soubor.
## Krok 3: Vytvořte instanci objektu sešitu
Nyní načteme soubor aplikace Excel do objektu Workbook. To vám umožní programově manipulovat se sešitem:
```csharp
// Vytvoření instance objektu sešitu
// Otevření souboru aplikace Excel prostřednictvím datového proudu souborů
Workbook workbook = new Workbook(fstream);
```
Pomocí tohoto řádku kódu jste úspěšně načetli soubor Excel do paměti a jste připraveni s ním pracovat.
## Krok 4: Otevřete sešit
Poté, co budete mít sešit, je dalším krokem přístup ke konkrétnímu listu, kde chcete oddělit řádky a sloupce. Postup:
```csharp
// Přístup k prvnímu listu v souboru aplikace Excel
Worksheet worksheet = workbook.Worksheets[0];
```
V tomto případě přistupujeme k prvnímu listu. Pokud jsou vaše data na jiném listu, můžete index odpovídajícím způsobem změnit.
## Krok 5: Zrušte seskupení řádků
Nyní přichází ta vzrušující část! Rozdělme prvních šest řad (od řady 0 do řady 5). Použijte následující kód:
```csharp
// Oddělení prvních šesti řádků (od 0 do 5)
worksheet.Cells.UngroupRows(0, 5);
```
Tato metoda odstraní všechna seskupení, která byla použita na zadané řádky. Je to tak snadné!
## Krok 6: Zrušte seskupení sloupců
Stejně jako řádky můžete oddělit i sloupce. Zde je návod, jak oddělit první tři sloupce (od sloupce 0 do sloupce 2):
```csharp
// Oddělení prvních tří sloupců (od 0 do 2)
worksheet.Cells.UngroupColumns(0, 2);
```
## Krok 7: Uložte upravený soubor Excel
 Jakmile zrušíte seskupení řádků a sloupců, dalším krokem je uložit změny zpět do souboru aplikace Excel. Můžete to udělat pomocí`Save` metoda:
```csharp
// Uložení upraveného souboru Excel
workbook.Save(dataDir + "output.xls");
```
 V tomto příkladu ukládáme upravený soubor jako`output.xls`. Název souboru můžete změnit na libovolný.
## Krok 8: Zavřete Stream souborů
Nakonec, abyste uvolnili zdroje, měli byste zavřít datový proud souboru:
```csharp
// Zavřením datového proudu souborů uvolníte všechny zdroje
fstream.Close();
```
To je dobrá praxe, abyste zajistili, že vaše aplikace nebude držet úchyty souborů déle, než je nutné.
## Závěr
tady to máte! Úspěšně jste se naučili, jak oddělit řádky a sloupce v souboru aplikace Excel pomocí Aspose.Cells for .NET. Pomocí několika řádků kódu můžete programově provádět významné změny v souborech aplikace Excel. Ať už automatizujete sestavy nebo připravujete data pro analýzu, zvládnutí těchto technik vám může ušetřit spoustu času.
## FAQ
### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna pro práci se soubory aplikace Excel v aplikacích .NET, která umožňuje snadnou manipulaci, konverzi a vytváření tabulek.
### Mohu oddělit řádky a sloupce v Excelu pomocí jiných knihoven?
Ano, pro manipulaci s Excelem v .NET jsou k dispozici další knihovny, ale Aspose.Cells nabízí rozsáhlé funkce a snadné použití.
### Existuje způsob, jak vrátit změny po uložení?
Jakmile uložíte soubor aplikace Excel, nelze předchozí stav obnovit, pokud nemáte zálohu původního souboru.
### Jak získám podporu pro Aspose.Cells?
 Podporu najdete na stránce[Fórum podpory Aspose](https://forum.aspose.com/c/cells/9), kde můžete klást otázky a hledat řešení.
### Mohu používat Aspose.Cells bez licence?
Ano, Aspose.Cells můžete používat zdarma s určitými omezeními a můžete začít s a[dočasná licence](https://purchase.aspose.com/temporary-license/) pro plnou funkčnost.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
