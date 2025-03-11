---
title: Přidat Combo Box do listu v Excelu
linktitle: Přidat Combo Box do listu v Excelu
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak přidat pole se seznamem do listu aplikace Excel programově pomocí Aspose.Cells for .NET. Tento podrobný průvodce vás provede každým detailem.
weight: 21
url: /cs/net/excel-shapes-controls/add-combo-box-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidat Combo Box do listu v Excelu

## Zavedení
Vytváření interaktivních tabulek Excelu může výrazně zlepšit uživatelské prostředí, zvláště když přidáte prvky formuláře, jako jsou pole se seznamem. Rozbalovací seznamy umožňují uživatelům vybrat si možnosti z předdefinovaného seznamu, což usnadňuje a zefektivňuje zadávání dat. S Aspose.Cells for .NET můžete programově vytvářet pole se seznamem v listech aplikace Excel bez přímého použití aplikace Excel. Tato výkonná knihovna umožňuje vývojářům manipulovat se soubory Excel různými způsoby, včetně schopnosti automatizovat ovládací prvky formulářů.
V tomto tutoriálu vás provedeme procesem přidání pole se seznamem do listu v aplikaci Excel pomocí Aspose.Cells pro .NET. Pokud chcete vytvářet dynamické a uživatelsky přívětivé tabulky, tato příručka vám pomůže začít.
## Předpoklady
Než se ponoříme do kódu, ujistěte se, že máte vše, co potřebujete:
- Aspose.Cells for .NET: Stáhněte si a nainstalujte knihovnu Aspose.Cells for .NET z[stránka ke stažení](https://releases.aspose.com/cells/net/).
- .NET Framework: Ujistěte se, že máte na svém počítači nainstalované rozhraní .NET Framework. Jakákoli verze podporovaná Aspose.Cells bude fungovat.
- Vývojové prostředí: Ke správě projektu a psaní kódu použijte IDE, jako je Visual Studio.
-  Aspose License: Ve zkušebním režimu můžete pracovat bez licence, ale pro plnou verzi budete muset použít licenci. Získejte a[dočasná licence](https://purchase.aspose.com/temporary-license/) v případě potřeby.
## Importujte balíčky
Chcete-li začít, musíte do projektu importovat požadované jmenné prostory. Zde je to, co potřebujete:
```csharp
using System.IO;
using Aspose.Cells;
```
Ty jsou nezbytné pro interakci se soubory aplikace Excel a manipulaci s prvky formuláře, jako jsou pole se seznamem v sešitu.
Pojďme si proces přidání pole se seznamem rozdělit do několika jednoduchých kroků pro snadné pochopení.
## Krok 1: Nastavte adresář dokumentů
Prvním krokem je vytvoření adresáře, kam se budou ukládat vaše excelové soubory. Můžete vytvořit novou složku, pokud ještě neexistuje.
```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
// Vytvořte adresář, pokud ještě není přítomen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- dataDir: Určuje umístění, kam bude výstupní soubor uložen.
- System.IO.Directory.Exists: Zkontroluje, zda adresář již existuje.
- System.IO.Directory.CreateDirectory: Vytvoří adresář, pokud chybí.
## Krok 2: Vytvořte nový sešit
Nyní vytvořte nový sešit aplikace Excel, kam přidáte pole se seznamem.

```csharp
// Vytvořte nový sešit.
Workbook workbook = new Workbook();
```

- Sešit sešit: Inicializuje novou instanci třídy Sešit představující soubor aplikace Excel.
## Krok 3: Získejte list a buňky
Dále otevřete první list ze sešitu a načtěte kolekci buněk, do které zadáte data.

```csharp
// Získejte první pracovní list.
Worksheet sheet = workbook.Worksheets[0];
// Získejte kolekci buněk listu.
Cells cells = sheet.Cells;
```

- List listu: Načte první list ze sešitu.
- Buňky buněk: Získá kolekci buněk z listu.
## Krok 4: Zadejte hodnoty pro Combo Box
Nyní musíme do buněk vložit nějaké hodnoty. Tyto hodnoty budou sloužit jako možnosti pro pole se seznamem.

```csharp
// Zadejte hodnotu.
cells["B3"].PutValue("Employee:");
// Nastavte to tučně.
cells["B3"].GetStyle().Font.IsBold = true;
// Zadejte některé hodnoty, které označují vstupní rozsah pro pole se seznamem.
cells["A2"].PutValue("Emp001");
cells["A3"].PutValue("Emp002");
cells["A4"].PutValue("Emp003");
cells["A5"].PutValue("Emp004");
cells["A6"].PutValue("Emp005");
cells["A7"].PutValue("Emp006");
```

- buňky["B3"].PutValue: Umístí štítek "Zaměstnanec" do buňky B3.
- Font.IsBold = true: Nastaví text na tučné, aby vynikl.
- Rozsah zadávání: Vloží několik ID zaměstnanců do buněk A2 až A7. Tyto se zobrazí v rozevíracím seznamu.
## Krok 5: Přidejte pole se seznamem do listu
Dalším krokem je přidání ovládacího prvku pole se seznamem do listu. Toto pole se seznamem umožní uživatelům vybrat si jedno z ID zaměstnance, které jste zadali dříve.

```csharp
// Přidat nové pole se seznamem.
Aspose.Cells.Drawing.ComboBox comboBox = sheet.Shapes.AddComboBox(2, 0, 2, 0, 22, 100);
```

- AddComboBox: Přidá do listu nové pole se seznamem. Čísla (2, 0, 2, 0, 22, 100) představují polohu a rozměry pole se seznamem.
## Krok 6: Propojte Combo Box s buňkou a nastavte vstupní rozsah
Aby byl rozbalovací seznam funkční, musíme jej propojit s konkrétní buňkou a definovat rozsah buněk, ze kterých bude čerpat své možnosti.

```csharp
// Nastavte propojenou buňku.
comboBox.LinkedCell = "A1";
// Nastavte vstupní rozsah.
comboBox.InputRange = "A2:A7";
```

- LinkedCell: Propojí výběr pole se seznamem s buňkou A1. V této buňce se objeví vybraná hodnota z rozbalovacího seznamu.
- InputRange: Definuje rozsah buněk (A2:A7) obsahující hodnoty, které vyplní možnosti pole se seznamem.
## Krok 7: Přizpůsobte vzhled Combo Boxu
Rozbalovací seznam můžete dále přizpůsobit zadáním počtu rozevíracích řádků a povolením 3D stínování pro lepší estetiku.

```csharp
// Set č. řádků seznamu zobrazených v části seznamu v poli se seznamem.
comboBox.DropDownLines = 5;
// Nastavte combo box s 3-D stínováním.
comboBox.Shadow = true;
```

- DropDownLines: Řídí, kolik možností bude najednou viditelných v rozevíracím seznamu.
- Stín: Přidá do pole se seznamem efekt 3D stínování.
## Krok 8: Automatické přizpůsobení sloupcům a uložení sešitu
Nakonec automaticky přizpůsobíme sloupce pro čisté rozvržení a uložíme sešit.

```csharp
// Automatické přizpůsobení sloupcům
sheet.AutoFitColumns();
// Uloží soubor.
workbook.Save(dataDir + "book1.out.xls");
```

- AutoFitColumns: Automaticky upraví šířku sloupců tak, aby odpovídala obsahu.
- Uložit: Uloží sešit jako soubor aplikace Excel do určeného adresáře.

## Závěr
Přidání pole se seznamem do listů aplikace Excel pomocí Aspose.Cells for .NET je přímočarý proces, který výrazně zlepšuje flexibilitu zadávání dat. Programovým vytvářením ovládacích prvků formuláře můžete snadno vytvářet interaktivní tabulky. Tento tutoriál vám ukázal, jak přidat pole se seznamem, propojit ho s buňkou a nakonfigurovat jeho vstupní rozsah, to vše pomocí Aspose.Cells.
 Aspose.Cells poskytuje širokou škálu funkcí pro manipulaci se soubory aplikace Excel, takže je ideální volbou pro vývojáře, kteří chtějí automatizovat úlohy v tabulkovém procesoru. Vyzkoušejte to s a[zkušební verze zdarma](https://releases.aspose.com/).
## FAQ
### Mohu používat Aspose.Cells bez nainstalovaného Excelu?
Ano, Aspose.Cells funguje nezávisle na Excelu a nevyžaduje instalaci Excelu.
### Jak mohu uplatnit licenci v Aspose.Cells?
 O licenci můžete požádat tak, že ji získáte od[zde](https://purchase.aspose.com/buy) a volání`License.SetLicense()` ve vašem kódu.
### Jaké formáty Aspose.Cells podporuje pro ukládání souborů?
Aspose.Cells podporuje ukládání souborů v různých formátech, jako jsou XLSX, XLS, CSV, PDF a další.
### Existuje nějaký limit na počet polí se seznamem, které mohu přidat?
Ne, neexistuje žádný přísný limit; můžete přidat tolik rozbalovacích polí, kolik váš projekt vyžaduje.
### Jak získám podporu pro Aspose.Cells?
 Můžete získat podporu od[Aspose fórum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
