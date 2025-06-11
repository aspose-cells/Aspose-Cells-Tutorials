---
"description": "Naučte se, jak programově přidat pole se seznamem do listu aplikace Excel pomocí Aspose.Cells pro .NET. Tato podrobná příručka vás provede každým detailem."
"linktitle": "Přidání pole se seznamem do listu v Excelu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Přidání pole se seznamem do listu v Excelu"
"url": "/cs/net/excel-shapes-controls/add-combo-box-to-worksheet-excel/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přidání pole se seznamem do listu v Excelu

## Zavedení
Vytváření interaktivních tabulek v Excelu může výrazně vylepšit uživatelský zážitek, zejména pokud přidáte prvky formuláře, jako jsou například seznamovací pole. Seznamovací pole umožňují uživatelům vybírat možnosti z předdefinovaného seznamu, což usnadňuje a zefektivňuje zadávání dat. S Aspose.Cells pro .NET můžete programově vytvářet seznamovací pole v tabulkách Excelu bez nutnosti přímého použití Excelu. Tato výkonná knihovna umožňuje vývojářům manipulovat s excelovými soubory různými způsoby, včetně možnosti automatizovat ovládací prvky formulářů.
V tomto tutoriálu vás provedeme procesem přidání pole se seznamem do listu v Excelu pomocí Aspose.Cells pro .NET. Pokud chcete vytvářet dynamické a uživatelsky přívětivé tabulky, tato příručka vám pomůže začít.
## Předpoklady
Než se pustíme do kódu, ujistěme se, že máte vše potřebné:
- Aspose.Cells pro .NET: Stáhněte a nainstalujte knihovnu Aspose.Cells pro .NET z [stránka ke stažení](https://releases.aspose.com/cells/net/).
- .NET Framework: Ujistěte se, že máte na svém počítači nainstalovaný .NET Framework. Fungovat bude jakákoli verze podporovaná službou Aspose.Cells.
- Vývojové prostředí: Pro správu projektu a psaní kódu použijte IDE, jako je Visual Studio.
- Licence Aspose: V zkušebním režimu můžete pracovat bez licence, ale pro plnou verzi budete muset licenci získat. Získejte [dočasná licence](https://purchase.aspose.com/temporary-license/) v případě potřeby.
## Importovat balíčky
Chcete-li začít, musíte do projektu importovat požadované jmenné prostory. Zde je to, co potřebujete:
```csharp
using System.IO;
using Aspose.Cells;
```
Tyto prvky jsou nezbytné pro interakci se soubory aplikace Excel a manipulaci s prvky formulářů, jako jsou například pole se seznamem v sešitu.
Pro snadné pochopení si rozdělme proces přidání pole se seznamem do několika jednoduchých kroků.
## Krok 1: Nastavení adresáře dokumentů
Prvním krokem je vytvoření adresáře, kam budou uloženy vaše soubory aplikace Excel. Pokud ještě neexistuje, můžete vytvořit novou složku.
```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "Your Document Directory";
// Vytvořte adresář, pokud ještě neexistuje.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- dataDir: Určuje umístění, kam bude uložen výstupní soubor.
- System.IO.Directory.Exists: Zkontroluje, zda adresář již existuje.
- System.IO.Directory.CreateDirectory: Vytvoří adresář, pokud chybí.
## Krok 2: Vytvořte nový sešit
Nyní vytvořte nový sešit aplikace Excel, do kterého přidáte pole se seznamem.

```csharp
// Vytvořte nový sešit.
Workbook workbook = new Workbook();
```

- Sešit Workbook: Inicializuje novou instanci třídy Workbook, která představuje soubor aplikace Excel.
## Krok 3: Získejte pracovní list a buňky
Dále otevřete první list ze sešitu a načtěte kolekci buněk, do které budete zadávat data.

```csharp
// Vezměte si první pracovní list.
Worksheet sheet = workbook.Worksheets[0];
// Získejte kolekci buněk pracovního listu.
Cells cells = sheet.Cells;
```

- Pracovní list: Načte první list ze sešitu.
- Buňky buňky: Získá kolekci buněk z listu.
## Krok 4: Zadání hodnot pro pole se seznamem
Nyní musíme do buněk zadat nějaké hodnoty. Tyto hodnoty budou sloužit jako možnosti pro pole se seznamem.

```csharp
// Zadejte hodnotu.
cells["B3"].PutValue("Employee:");
// Nastavte to tučně.
cells["B3"].GetStyle().Font.IsBold = true;
// Zadejte hodnoty, které označují vstupní rozsah pro pole se seznamem.
cells["A2"].PutValue("Emp001");
cells["A3"].PutValue("Emp002");
cells["A4"].PutValue("Emp003");
cells["A5"].PutValue("Emp004");
cells["A6"].PutValue("Emp005");
cells["A7"].PutValue("Emp006");
```

- buňky["B3"].PutValue: Umístí popisek „Zaměstnanec“ do buňky B3.
- Font.IsBold = true: Nastaví text na tučné písmo, aby vynikl.
- Vstupní rozsah: Zadá několik ID zaměstnanců do buněk A2 až A7. Tato čísla se zobrazí v rozbalovacím seznamu.
## Krok 5: Přidání rozbalovacího seznamu do pracovního listu
Dalším krokem je přidání ovládacího prvku pole se seznamem do listu. Toto pole se seznamem umožní uživatelům vybrat jedno z ID zaměstnanců, které jste zadali dříve.

```csharp
// Přidejte nové pole se seznamem.
Aspose.Cells.Drawing.ComboBox comboBox = sheet.Shapes.AddComboBox(2, 0, 2, 0, 22, 100);
```

- AddComboBox: Přidá do listu nové pole se seznamem. Čísla (2, 0, 2, 0, 22, 100) představují polohu a rozměry pole se seznamem.
## Krok 6: Propojení rozbalovacího seznamu s buňkou a nastavení vstupního rozsahu
Aby byl seznam funkční, musíme ho propojit s konkrétní buňkou a definovat rozsah buněk, ze kterých bude načítat své možnosti.

```csharp
// Nastavte propojenou buňku.
comboBox.LinkedCell = "A1";
// Nastavte vstupní rozsah.
comboBox.InputRange = "A2:A7";
```

- Propojená buňka: Propojí výběr ze seznamu s buňkou A1. Vybraná hodnota ze seznamu se zobrazí v této buňce.
- Vstupní rozsah: Definuje oblast buněk (A2:A7) obsahující hodnoty, které budou naplňovat možnosti pole se seznamem.
## Krok 7: Přizpůsobení vzhledu pole se seznamem
Rozbalovací seznam si můžete dále přizpůsobit zadáním počtu rozbalovacích řádků a povolením 3D stínování pro lepší estetiku.

```csharp
// Nastavte počet řádků seznamu zobrazených v části seznamu v rozbalovacím seznamu.
comboBox.DropDownLines = 5;
// Nastavte pole se seznamem s 3D stínováním.
comboBox.Shadow = true;
```

- DropDownLines: Určuje, kolik možností bude najednou viditelných v rozevíracím seznamu.
- Stín: Přidá do pole se seznamem efekt 3D stínování.
## Krok 8: Automatické přizpůsobení sloupců a uložení sešitu
Nakonec automaticky přizpůsobíme sloupce pro přehledné rozvržení a uložíme sešit.

```csharp
// Automatické přizpůsobení sloupců
sheet.AutoFitColumns();
// Uloží soubor.
workbook.Save(dataDir + "book1.out.xls");
```

- AutoFitColumns: Automaticky upraví šířku sloupců tak, aby odpovídala obsahu.
- Uložit: Uloží sešit jako soubor aplikace Excel do zadaného adresáře.

## Závěr
Přidání pole se seznamem do listů aplikace Excel pomocí Aspose.Cells pro .NET je přímočarý proces, který výrazně zlepšuje flexibilitu zadávání dat. Programovým vytvářením ovládacích prvků formuláře můžete snadno vytvářet interaktivní tabulky. Tento tutoriál vám ukázal, jak přidat pole se seznamem, propojit ho s buňkou a nakonfigurovat jeho vstupní rozsah, to vše pomocí Aspose.Cells.
Aspose.Cells nabízí širokou škálu funkcí pro manipulaci s Excelovými soubory, což z něj činí ideální volbu pro vývojáře, kteří chtějí automatizovat úlohy s tabulkami. Vyzkoušejte si to s... [bezplatná zkušební verze](https://releases.aspose.com/).
## Často kladené otázky
### Mohu používat Aspose.Cells bez nainstalovaného Excelu?
Ano, Aspose.Cells funguje nezávisle na Excelu a nevyžaduje instalaci Excelu.
### Jak požádám o licenci v Aspose.Cells?
Licenci můžete získat od [zde](https://purchase.aspose.com/buy) a volání `License.SetLicense()` ve vašem kódu.
### Jaké formáty Aspose.Cells podporuje pro ukládání souborů?
Aspose.Cells podporuje ukládání souborů v různých formátech, jako jsou XLSX, XLS, CSV, PDF a další.
### Existuje omezení počtu rozbalovacích seznamů, které můžu přidat?
Ne, neexistuje žádné striktní omezení; můžete přidat tolik seznamů, kolik váš projekt vyžaduje.
### Jak získám podporu pro Aspose.Cells?
Podporu můžete získat od [Fórum Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}