---
"description": "Naučte se, jak v Excelu pomocí Aspose.Cells pro .NET přidat vodorovné a svislé zalomení stránek v tomto podrobném návodu. Vytvořte si soubory Excelu pro tisk."
"linktitle": "Přidání zalomení stránek do pracovního listu pomocí Aspose.Cells"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Přidání zalomení stránek do pracovního listu pomocí Aspose.Cells"
"url": "/cs/net/worksheet-value-operations/add-page-breaks/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přidání zalomení stránek do pracovního listu pomocí Aspose.Cells

## Zavedení
V tomto tutoriálu vás provedeme procesem přidávání vodorovných i svislých zalomení stránek do listu aplikace Excel. Také si prohlédněte podrobný návod, jak snadno manipulovat se zalomeními stránek pomocí Aspose.Cells pro .NET. Na konci tohoto průvodce se naučíte tyto techniky používat ve svých vlastních projektech. Pojďme se na to podívat!
## Předpoklady
Než se pustíme do kódu, ujistěme se, že jste připraveni sledovat tento tutoriál. Zde je několik předpokladů:
- Visual Studio: Budete potřebovat Visual Studio nainstalované na vašem systému.
- Aspose.Cells pro .NET: Měli byste mít nainstalovanou knihovnu Aspose.Cells. Pokud jste tak ještě neučinili, nebojte se! Můžete si stáhnout bezplatnou zkušební verzi a začít. (Můžete si ji stáhnout [zde](https://releases.aspose.com/cells/net/)).
- .NET Framework: Tento tutoriál předpokládá, že pracujete s .NET Framework nebo .NET Core. Pokud používáte jiné prostředí, může se postup mírně lišit.
Dále byste měli mít základní znalosti programování v jazyce C# a konceptu zalomení stránek v Excelu.
## Importovat balíčky
Abychom mohli začít pracovat s Aspose.Cells, musíme do našeho projektu importovat příslušné jmenné prostory. To nám umožní přístup k funkcím poskytovaným Aspose.Cells pro manipulaci s excelovými soubory.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Jakmile tyto jmenné prostory importujete, můžete začít pracovat se soubory aplikace Excel a provádět různé úpravy, včetně přidání zalomení stránek.
Nyní, když máte vše nastavené, pojďme si projít kroky pro přidání zalomení stránek do listu. Rozebereme si jednotlivé části procesu a podrobně vysvětlíme každý řádek kódu.
## Krok 1: Nastavení sešitu
Nejprve je třeba vytvořit nový sešit. `Workbook` Třída v Aspose.Cells představuje sešit aplikace Excel a je výchozím bodem pro manipulaci se soubory aplikace Excel.
```csharp
// Definujte cestu k adresáři, kam bude soubor uložen
string dataDir = "Your Document Directory";
// Vytvoření nového objektu sešitu
Workbook workbook = new Workbook();
```
V tomto kódu:
- `dataDir` určuje, kam bude váš soubor uložen.
- Ten/Ta/To `Workbook` Vytvoří se objekt, který bude použit k uchovávání a manipulaci s vaším excelovým souborem.
## Krok 2: Přidání vodorovného zalomení stránky
Dále přidáme do listu vodorovný konec stránky. Vodorovný konec stránky rozdělí list vodorovně na dvě části, což znamená, že určuje, kde se obsah při tisku svisle zalomí na novou stránku.
```csharp
// Přidat vodorovný konec stránky na řádku 30
workbook.Worksheets[0].HorizontalPageBreaks.Add("Y30");
```
V tomto příkladu:
- `Worksheets[0]` odkazuje na první list v sešitu (nezapomeňte, že listy mají nulový index).
- `HorizontalPageBreaks.Add("Y30")` přidá zalomení stránky na řádku 30. To znamená, že obsah před řádkem 30 se zobrazí na jedné stránce a vše pod ním začne na nové stránce.
## Krok 3: Přidání svislého zalomení stránky
Podobně můžete přidat svislý konec stránky. Tím se list zalomí v určitém sloupci, čímž se zajistí, že obsah nalevo od konce se zobrazí na jedné stránce a obsah napravo na další.
```csharp
// Přidat svislý konec stránky ve sloupci Y
workbook.Worksheets[0].VerticalPageBreaks.Add("Y30");
```
Zde:
- Ten/Ta/To `VerticalPageBreaks.Add("Y30")` Metoda přidá svislý konec stránky ve sloupci Y (tj. za 25. sloupec). Tím se vytvoří konec stránky mezi sloupci X a Y.
## Krok 4: Uložení sešitu
Po přidání zalomení stránek je posledním krokem uložení sešitu do souboru. Můžete zadat cestu, kam chcete soubor Excel uložit.
```csharp
// Uložte soubor Excelu
workbook.Save(dataDir + "AddingPageBreaks_out.xls");
```
Tím se sešit s přidanými zalomeními stránek uloží do zadané cesty k souboru (`AddingPageBreaks_out.xls`).
## Závěr
Přidávání zalomení stránek v Excelu je klíčová funkce při práci s velkými datovými sadami nebo při přípravě dokumentů k tisku. S Aspose.Cells pro .NET můžete snadno automatizovat proces vkládání vodorovných i svislých zalomení stránek do listů Excelu, což zajistí, že vaše dokumenty budou dobře organizované a snadno čitelné.
## Často kladené otázky
### Jak přidám více zalomení stránek v Aspose.Cells pro .NET?
Více zalomení stránek můžete přidat pouhým voláním funkce `HneboizontalPageBreaks.Add()` or `VerticalPageBreaks.Add()` metody několikrát s různými odkazy na buňky.
### Mohu přidat zalomení stránek do konkrétního listu sešitu?
Ano, pracovní list můžete zadat pomocí `Worksheets[index]` nemovitost, kde `index` je index listu založený na nule.
### Jak odstraním zalomení stránky v Aspose.Cells pro .NET?
Zalomení stránky můžete odstranit pomocí `HneboizontalPageBreaks.RemoveAt()` or `VerticalPageBreaks.RemoveAt()` metody zadáním indexu zalomení stránky, které chcete odstranit.
### Co když chci automaticky přidávat zalomení stránek na základě velikosti obsahu?
Aspose.Cells neposkytuje automatickou funkci pro přidání zalomení stránek na základě velikosti obsahu, ale můžete programově vypočítat, kde by se zalomení mělo objevit na základě počtu řádků/sloupců.
### Mohu nastavit zalomení stránek na základě určitého rozsahu buněk?
Ano, můžete zadat zalomení stránek pro libovolnou buňku nebo oblast zadáním odpovídajícího odkazu na buňku, například „A1“ nebo „B15“.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}