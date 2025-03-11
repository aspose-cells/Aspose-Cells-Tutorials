---
title: Přidat tlačítko do listu v Excelu
linktitle: Přidat tlačítko do listu v Excelu
second_title: Aspose.Cells .NET Excel Processing API
description: V tomto podrobném návodu se dozvíte, jak přidat tlačítko do listu aplikace Excel pomocí Aspose.Cells for .NET. Vylepšete excelové tabulky pomocí interaktivních tlačítek.
weight: 12
url: /cs/net/excel-shapes-controls/add-button-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidat tlačítko do listu v Excelu

## Zavedení
Tabulky Excelu jsou univerzální a běžně se používají pro správu dat, ale někdy vyžadují další interaktivitu. Jedním z nejlepších způsobů, jak zlepšit uživatelskou zkušenost, je přidání tlačítek do listu. Tato tlačítka mohou spouštět makra nebo navigovat uživatele na užitečné odkazy. Pokud jste .NET vývojář pracující se soubory Excelu, Aspose.Cells for .NET poskytuje snadný způsob, jak programově manipulovat s excelovými sešity, včetně přidávání tlačítek.
V tomto tutoriálu vás provedeme procesem přidání tlačítka do listu v Excelu pomocí Aspose.Cells for .NET. Pokryjeme každý detail, od nastavení nezbytných předpokladů až po pokyny krok za krokem. Pojďme se ponořit!
## Předpoklady
Než budete moci pokračovat v tomto tutoriálu, ujistěte se, že máte nainstalované následující nástroje a balíčky:
-  Aspose.Cells for .NET Library: Můžete si ji stáhnout z[zde](https://releases.aspose.com/cells/net/).
- Vývojové prostředí .NET: Ujistěte se, že máte nainstalované funkční prostředí .NET, jako je Visual Studio.
- Základní porozumění C#: Měli byste být obeznámeni se základy programování v C#.
-  Licence: Budete potřebovat platnou licenci. Pokud žádný nemáte, můžete získat a[zkušební verze zdarma](https://releases.aspose.com/) nebo požádat o a[dočasná licence](https://purchase.aspose.com/temporary-license/).
Přejděme k importu potřebných balíčků.
## Importujte balíčky
Než začnete kódovat, budete muset importovat požadované balíčky do svého .NET projektu. Zde je jednoduchý fragment kódu, který vám pomůže importovat Aspose.Cells do vašeho projektu:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Nyní, když jsme importovali potřebné balíčky, pojďme si příklad rozebrat do podrobného průvodce krok za krokem.
## Krok 1: Nastavte sešit a pracovní list
V tomto prvním kroku vytvoříme nový excelový sešit a získáme odkaz na první list.
```csharp
// Definujte cestu k adresáři dokumentů.
string dataDir = "Your Document Directory";
// Vytvořte adresář, pokud ještě není přítomen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Vytvořte nový sešit.
Workbook workbook = new Workbook();
// Získejte první pracovní list v sešitu.
Worksheet sheet = workbook.Worksheets[0];
```

-  Vytvoření sešitu: Začneme vytvořením nového`Workbook` objekt, který představuje soubor aplikace Excel.
-  Odkaz na pracovní list: The`Worksheets[0]` příkaz načte první list v sešitu, který upravíme.
Tento krok vytvoří základ vytvořením prázdného souboru aplikace Excel s jedním listem.
## Krok 2: Přidejte tlačítko do listu
Dále do listu přidáme tlačítko. Tady se děje kouzlo!
```csharp
// Přidejte do listu nové tlačítko.
Aspose.Cells.Drawing.Button button = sheet.Shapes.AddButton(2, 0, 2, 0, 28, 80);
```

- Metoda AddButton: Tato metoda přidá tlačítko na určené místo v listu. Parametry definují polohu tlačítka (řádek, sloupec, x-posun, y-posun) a velikost (výška, šířka).
- Řádek a sloupec: Tlačítko je umístěno na řádku 2 a sloupci 0, bez dalšího odsazení.
- Velikost: Výška tlačítka je nastavena na 28 a šířka na 80.
Tento krok úspěšně přidá tlačítko do listu, ale ještě jsme neskončili – pojďme si ho přizpůsobit.
## Krok 3: Nastavte vlastnosti tlačítka
Nyní je čas upravit vzhled tlačítka nastavením jeho textu, písma a umístění.
```csharp
// Nastavte titulek tlačítka.
button.Text = "Aspose";
// Nastavte typ umístění, způsob, jakým je tlačítko připojeno k buňkám.
button.Placement = PlacementType.FreeFloating;
```

- Text: Titulek tlačítka jsme nastavili na „Aspose“.
-  Umístění: Definujeme, jak je tlačítko umístěno vzhledem k buňkám listu.`FreeFloating` umožňuje tlačítku pohybovat se nezávisle na buňkách.
Tento krok přizpůsobí popis a umístění tlačítka.
## Krok 4: Upravte písmo tlačítka
Dopřejme tlačítku šmrnc přizpůsobením vlastností písma.
```csharp
// Nastavte název písma.
button.Font.Name = "Tahoma";
// Nastavte řetězec titulků tučně.
button.Font.IsBold = true;
// Nastavte barvu na modrou.
button.Font.Color = Color.Blue;
```

- Název písma: Změníme písmo na „Tahoma“, což je čisté a moderní písmo.
- Tučné: Text tlačítka je pro zvýraznění tučný.
- Barva: Barva písma je nastavena na modrou, takže text tlačítka vynikne.
Tento krok vylepšuje vzhled tlačítka a zajišťuje, že je funkční i vizuálně přitažlivé.
## Krok 5: Přidejte k tlačítku hypertextový odkaz
Přidáním hypertextového odkazu můžete tlačítko učinit ještě užitečnějším.
```csharp
// Nastavte hypertextový odkaz pro tlačítko.
button.AddHyperlink("https://www.aspose.com/");
```

- AddHyperlink: Tuto metodu používáme k přidání klikacího hypertextového odkazu na tlačítko. Po kliknutí na tlačítko přejdete na webovou stránku Aspose.
Tento krok přidává tlačítku interaktivitu, díky čemuž je funkční nad rámec pouhé estetiky.
## Krok 6: Uložte soubor Excel
Jakmile je vše nastaveno, nezapomeňte změny uložit!
```csharp
// Uloží soubor.
workbook.Save(dataDir + "book1.out.xls");
```

-  Metoda uložení: Používáme`Save` metoda zapsat upravený sešit do nového souboru. Soubor bude uložen do určeného adresáře.
Gratuluji! Nyní jste přidali plně přizpůsobené tlačítko do listu aplikace Excel.
## Závěr
Přidání tlačítek do listů aplikace Excel může výrazně zlepšit funkčnost vašich tabulek, díky čemuž budou interaktivnější a uživatelsky přívětivější. S Aspose.Cells for .NET toho můžete dosáhnout pomocí několika řádků kódu, jak jsme si ukázali v tomto tutoriálu.
Aspose.Cells for .NET je výkonná knihovna, která poskytuje nekonečné možnosti pro manipulaci s Excelem. Ať už automatizujete úkoly nebo přidáváte nové funkce do svých tabulek, tato knihovna je vaším řešením.
 Pokud jste to ještě neudělali,[stáhněte si knihovnu Aspose.Cells for .NET](https://releases.aspose.com/cells/net/) a začněte vylepšovat své soubory Excel.
## FAQ
### Mohu v Aspose.Cells pro .NET používat jiné tvary kromě tlačítek?
Ano, Aspose.Cells vám umožňuje přidávat různé tvary, včetně zaškrtávacích políček, přepínačů a dalších.
### Mohu spustit makro z tlačítka přidaného prostřednictvím Aspose.Cells?
Ano, tlačítko můžete propojit s makrem, i když v Excelu budete muset zpracovat kód makra samostatně.
### Jak mohu nastavit, aby se velikost tlačítka automaticky změnila s buňkami?
 Použijte`PlacementType.Move` vlastnost, která umožní tlačítku změnit velikost s buňkami.
### Je možné přidat více tlačítek na jeden list?
 Absolutně! Můžete přidat tolik tlačítek, kolik potřebujete, zavoláním na`AddButton` metodou vícekrát.
### Mohu si vzhled tlačítka dále přizpůsobit?
Ano, můžete upravit mnoho vlastností, včetně barvy pozadí, stylu ohraničení a dalších.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
