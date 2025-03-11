---
title: Nastavení dat kategorie
linktitle: Nastavení dat kategorie
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak nastavit data kategorií v grafech aplikace Excel pomocí Aspose.Cells pro .NET. Pro snadnou implementaci postupujte podle našeho podrobného návodu.
weight: 15
url: /cs/net/advanced-chart-operations/setting-category-data/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nastavení dat kategorie

## Zavedení

Pokud jde o programovou správu a manipulaci se soubory aplikace Excel, může mít ty správné nástroje zásadní význam. Aspose.Cells for .NET vyniká jako jeden takový nástroj, který umožňuje vývojářům snadno vytvářet, upravovat a převádět soubory aplikace Excel. Ať už vytváříte komplexní aplikaci pro analýzu dat nebo jednoduše potřebujete automatizovat generování sestav, Aspose.Cells vás pokryje. 

## Předpoklady 

Než se ponoříme do podrobností, ujistěte se, že máte vše, co potřebujete:

1. Vývojové prostředí: Ujistěte se, že máte nastavené vývojové prostředí .NET. Doporučuje se Visual Studio.
2.  Aspose.Cells for .NET Library: Stáhněte si nejnovější verzi knihovny z[Stránka ke stažení Aspose.Cells](https://releases.aspose.com/cells/net/).
3. Základní porozumění C#: Znalost konceptů C# a Excelu vám pomůže plynuleji uchopit obsah.
4.  Přístup k dokumentaci: Mít přístup k[Dokumentace Aspose.Cells](https://reference.aspose.com/cells/net/) může poskytnout další informace, pokud uvíznete. 

Když je vše na svém místě, odemkněme kouzlo manipulace s Excelem krok za krokem.

## Importujte balíčky 

Než začneme kódovat, je důležité importovat potřebné balíčky. To nám umožňuje přístup k funkcím poskytovaným Aspose.Cells.

## Krok 1: Import jmenného prostoru

Chcete-li začít, importujme jmenný prostor Aspose.Cells do vašeho souboru C#.

```csharp
using System;
using System.IO;
using Aspose.Cells;
```

Zahrnutím tohoto řádku na začátek souboru získáte přístup ke všem relevantním třídám a metodám v knihovně Aspose.Cells.

Nyní, když jsme obeznámeni s předpoklady a importovali jsme potřebnou knihovnu, pojďme prozkoumat, jak nastavit data kategorií v grafu Excel.

## Krok 2: Definujte svůj výstupní adresář

Nejprve musíte určit, kam se soubor Excel uloží. Vytvořte proměnnou pro výstupní adresář. 

```csharp
string outputDir = "Your Output Directory";
```

 Nahradit`"Your Output Directory"` se skutečnou cestou k umístění, kam chcete uložit výstupní soubor Excel. Díky tomu budete přesně vědět, kde svůj hotový produkt najít!

## Krok 3: Vytvoření instance objektu sešitu

Dále vytvoříte novou instanci objektu Sešit. Tento objekt slouží jako kontejner pro váš soubor Excel.

```csharp
Workbook workbook = new Workbook();
```

## Krok 4: Přístup k prvnímu listu

Budete muset pracovat s prvním listem v sešitu. Přístup k pracovnímu listu je stejně snadný jako:

```csharp
Worksheet worksheet = workbook.Worksheets[0];
```

 Index`0` ukazuje na první pracovní list. V Excelu si to představte jako otevření první karty v sešitu.

## Krok 5: Přidání vzorových hodnot do buněk

Vyplníme nějaké údaje, se kterými budeme pracovat. Do prvních dvou sloupců můžete přidat číselné hodnoty. 

```csharp
worksheet.Cells["A1"].PutValue(10);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(170);
worksheet.Cells["A4"].PutValue(200);
worksheet.Cells["B1"].PutValue(120);
worksheet.Cells["B2"].PutValue(320);
worksheet.Cells["B3"].PutValue(50);
worksheet.Cells["B4"].PutValue(40);
```

V tomto úryvku vyplňujeme řádky A1 až A4 různými číselnými hodnotami a vyplňujeme také sloupce B1 až B4. Tato data budou sloužit jako základ pro náš graf.

## Krok 6: Přidání dat kategorie

Nyní označme naše datové kategorie. To se provádí ve třetím sloupci (sloupec C):

```csharp
worksheet.Cells["C1"].PutValue("Q1");
worksheet.Cells["C2"].PutValue("Q2");
worksheet.Cells["C3"].PutValue("Y1");
worksheet.Cells["C4"].PutValue("Y2");
```

Zde označujeme každou sadu dat kategoriemi jako „Q1“ a „Y1“, což usnadňuje pozdější interpretaci našeho grafu.

## Vytvoření grafu

S našimi daty jsme připraveni přidat graf, který bude tato data vizuálně reprezentovat.

## Krok 7: Přidání grafu do listu

Nyní do listu přidáme graf typu „Sloupec“.

```csharp
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Column, 5, 0, 15, 5);
```

Tento řádek vytvoří nový sloupcový graf začínající na řádku 5 a sloupci 0 listu.

## Krok 8: Přístup k instanci grafu

Než budeme moci naplnit graf daty, musíme získat přístup k instanci nově vytvořeného grafu:

```csharp
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

Tímto krokem jsme všichni připraveni přidat naše datové řady do grafu.

## Krok 9: Přidání datových řad do grafu

Dále přidáte kolekci řad, která definuje data, která bude graf zobrazovat. 

```csharp
chart.NSeries.Add("A1:B4", true);
```

Tento řádek určuje, že graf by měl přebírat data z rozsahů A1 až B4, což umožňuje zobrazit tyto hodnoty vizuálně.

## Krok 10: Nastavení dat kategorie

Zde přichází klíčová část – definování údajů o naší kategorii. To je to, co označuje naše datové body na ose x.

```csharp
chart.NSeries.CategoryData = "C1:C4";
```

Přiřazením tohoto rozsahu sdělíme grafu, které buňky odpovídají kategoriím v naší datové řadě. Bez tohoto kroku by váš graf byl pouze souborem čísel!

## Krok 11: Uložení souboru Excel

Když je vše nastaveno, je čas zachránit naši dřinu. 

```csharp
workbook.Save(outputDir + "outputSettingCategoryData.xlsx");
```

Tento příkaz uloží sešit do zadaného výstupního adresáře pod názvem "outputSettingCategoryData.xlsx". 

## Krok 12: Potvrzující zpráva

Nakonec můžeme přidat malou zpětnou vazbu, abychom potvrdili, že vše fungovalo hladce:

```csharp
Console.WriteLine("SettingCategoryData executed successfully.");
```

Tím se na konzole vytiskne zpráva, která vás informuje o dokončení procesu. Jednoduché, že?

## Závěr

A tady to máte! Úspěšně jste nastavili data kategorií pro graf v sešitu aplikace Excel pomocí Aspose.Cells for .NET. Krása tohoto přístupu spočívá v tom, jak vám umožňuje automatizovat manipulaci se soubory Excel, aniž byste měli Excel nainstalovaný na vašem počítači. 

## FAQ

### Co je Aspose.Cells?
Aspose.Cells je knihovna .NET pro správu souborů aplikace Excel bez nutnosti aplikace Microsoft Excel. Umožňuje vytvářet, upravovat a převádět dokumenty aplikace Excel programově.

### Mohu používat Aspose.Cells zdarma?
 Ano, Aspose.Cells můžete vyzkoušet zdarma. Nabízejí bezplatnou zkušební verzi k dispozici[zde](https://releases.aspose.com/).

### Je Aspose.Cells vhodný pro velké datové sady?
Absolutně! Aspose.Cells je navržen tak, aby efektivně zpracovával velké datové sady, což z něj činí spolehlivou volbu pro datově náročné aplikace.

### Jak přidám grafy pomocí Aspose.Cells?
Grafy můžete přidat vytvořením nového objektu grafu a jeho propojením s oblastmi buněk, které obsahují vaše data, jak je ukázáno v tomto kurzu.

### Kde najdu další příklady použití Aspose.Cells?
 Další příklady a podrobnou dokumentaci můžete prozkoumat na adrese[Stránka dokumentace Aspose.Cells](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
