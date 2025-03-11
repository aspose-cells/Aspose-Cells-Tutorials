---
title: Přidejte konce stránek do listu pomocí Aspose.Cells
linktitle: Přidejte konce stránek do listu pomocí Aspose.Cells
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak přidat vodorovné a svislé zalomení stránek v aplikaci Excel pomocí Aspose.Cells for .NET, pomocí tohoto podrobného průvodce. Zajistěte, aby vaše soubory Excel byly vhodné pro tisk.
weight: 10
url: /cs/net/worksheet-value-operations/add-page-breaks/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidejte konce stránek do listu pomocí Aspose.Cells

## Zavedení
V tomto tutoriálu vás provedeme procesem přidávání vodorovných i svislých zalomení stránek do listu aplikace Excel. Uvidíte také podrobný návod, jak používat Aspose.Cells pro .NET ke snadné manipulaci s koncemi stránek, a na konci této příručky budete pohodlně používat tyto techniky ve svých vlastních projektech. Začněme!
## Předpoklady
Než se ponoříme do kódu, ujistíme se, že jste připraveni sledovat tento tutoriál. Zde je několik předpokladů:
- Visual Studio: Budete potřebovat Visual Studio nainstalované ve vašem systému.
-  Aspose.Cells for .NET: Měli byste mít nainstalovanou knihovnu Aspose.Cells. Pokud jste to ještě neudělali, nezoufejte! Chcete-li začít, můžete si stáhnout bezplatnou zkušební verzi. (Můžete to získat[zde](https://releases.aspose.com/cells/net/)).
- .NET Framework: Tento kurz předpokládá, že pracujete s .NET Framework nebo .NET Core. Pokud používáte jiné prostředí, proces se může mírně lišit.
Kromě toho byste měli mít základní znalosti s programováním C# a konceptem zalomení stránek v Excelu.
## Importujte balíčky
Abychom mohli začít pracovat s Aspose.Cells, musíme do našeho projektu importovat příslušné jmenné prostory. To nám umožňuje přístup k funkcím, které poskytuje Aspose.Cells pro manipulaci se soubory Excel.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Jakmile tyto obory názvů importujete, můžete začít pracovat se soubory aplikace Excel a aplikovat různé úpravy, včetně přidávání zalomení stránek.
Nyní, když jste nastavili, pojďme si projít kroky pro přidání zalomení stránek do listu. Rozebereme každou část procesu a podrobně vysvětlíme každý řádek kódu.
## Krok 1: Nastavte svůj sešit
 Nejprve musíte vytvořit nový sešit. The`Workbook` class v Aspose.Cells představuje sešit aplikace Excel a je výchozím bodem pro manipulaci se soubory aplikace Excel.
```csharp
// Definujte cestu k adresáři, kam bude váš soubor uložen
string dataDir = "Your Document Directory";
// Vytvořte nový objekt sešitu
Workbook workbook = new Workbook();
```
V tomto kódu:
- `dataDir` určuje, kam bude váš soubor uložen.
-  The`Workbook` je vytvořen objekt, který bude použit k uložení a manipulaci s vaším souborem Excel.
## Krok 2: Přidejte vodorovný konec stránky
Dále do listu přidáme vodorovný konec stránky. Vodorovný konec stránky rozdělí list vodorovně na dvě části, což znamená, že určuje, kde se obsah při tisku svisle zalomí na novou stránku.
```csharp
//Přidejte vodorovný konec stránky na řádek 30
workbook.Worksheets[0].HorizontalPageBreaks.Add("Y30");
```
V tomto příkladu:
- `Worksheets[0]` odkazuje na první list v sešitu (nezapomeňte, že listy mají nulový index).
- `HorizontalPageBreaks.Add("Y30")` přidá konec stránky na řádek 30. To znamená, že obsah před řádkem 30 se objeví na jedné stránce a vše pod ním začne na nové stránce.
## Krok 3: Přidejte svislý konec stránky
Podobně můžete přidat svislý konec stránky. Tím se list rozdělí na konkrétní sloupec, čímž se zajistí, že obsah vlevo od zalomení se zobrazí na jedné stránce a obsah vpravo na další stránce.
```csharp
// Přidejte svislý konec stránky do sloupce Y
workbook.Worksheets[0].VerticalPageBreaks.Add("Y30");
```
Zde:
-  The`VerticalPageBreaks.Add("Y30")` metoda přidává vertikální konec stránky ve sloupci Y (tj. za 25. sloupcem). Tím se vytvoří zalomení stránky mezi sloupci X a Y.
## Krok 4: Uložte sešit
Po přidání konců stránek je posledním krokem uložení sešitu do souboru. Můžete zadat cestu, kam chcete soubor Excel uložit.
```csharp
// Uložte soubor aplikace Excel
workbook.Save(dataDir + "AddingPageBreaks_out.xls");
```
Tím se sešit s přidanými zalomeními stránek uloží do zadané cesty k souboru (`AddingPageBreaks_out.xls`).
## Závěr
Přidání zalomení stránek v Excelu je zásadní funkcí, když pracujete s velkými datovými sadami nebo připravujete dokumenty k tisku. S Aspose.Cells for .NET můžete snadno automatizovat proces vkládání vodorovných i svislých zalomení stránek do listů aplikace Excel, čímž zajistíte, že vaše dokumenty budou dobře organizované a snadno čitelné.
## FAQ
### Jak do Aspose.Cells pro .NET přidám více konců stránek?
 Můžete přidat více zalomení stránek pouhým zavoláním`HorizontalPageBreaks.Add()` nebo`VerticalPageBreaks.Add()` metody vícekrát s různými odkazy na buňky.
### Mohu přidat konce stránek do konkrétního listu sešitu?
 Ano, můžete zadat list pomocí`Worksheets[index]` nemovitost kde`index` je index listu založený na nule.
### Jak odstraním konec stránky v Aspose.Cells pro .NET?
 Konec stránky můžete odstranit pomocí`HorizontalPageBreaks.RemoveAt()` nebo`VerticalPageBreaks.RemoveAt()` metod zadáním indexu konce stránky, který chcete odstranit.
### Co když chci přidávat konce stránek automaticky na základě velikosti obsahu?
Aspose.Cells neposkytuje automatickou funkci pro přidávání zalomení stránek na základě velikosti obsahu, ale můžete programově vypočítat, kde by se měly zalomení objevit na základě počtu řádků/sloupců.
### Mohu nastavit konce stránek na základě konkrétního rozsahu buněk?
Ano, můžete zadat konce stránek pro libovolnou buňku nebo rozsah poskytnutím příslušného odkazu na buňku, například "A1" nebo "B15".

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
