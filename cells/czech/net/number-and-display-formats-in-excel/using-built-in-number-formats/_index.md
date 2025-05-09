---
"description": "Automatizujte formátování čísel v Excelu pomocí Aspose.Cells pro .NET. Naučte se, jak programově používat formáty data, procent a měny."
"linktitle": "Programové používání vestavěných číselných formátů v Excelu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Programové používání vestavěných číselných formátů v Excelu"
"url": "/cs/net/number-and-display-formats-in-excel/using-built-in-number-formats/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Programové používání vestavěných číselných formátů v Excelu

## Zavedení
tomto tutoriálu si ukážeme, jak používat vestavěné formáty čísel v Excelu pomocí Aspose.Cells pro .NET. Probereme vše od nastavení prostředí až po použití různých formátů, jako jsou data, procenta a měny. Ať už jste zkušený profesionál, nebo se teprve seznamujete s ekosystémem .NET, tento průvodce vám pomůže s formátováním buněk v Excelu jako hračka.
## Předpoklady
Než se ponoříte, ujistěte se, že máte následující:
- Je nainstalována knihovna Aspose.Cells pro .NET. Můžete [stáhněte si to zde](https://releases.aspose.com/cells/net/).
- Pracovní znalost C# a základů programování v .NET.
- Visual Studio nebo jakékoli .NET IDE nainstalované na vašem počítači.
- Platná licence Aspose nebo [dočasná licence](https://purchase.aspose.com/temporary-license/).
- Nainstalovaný .NET framework (verze 4.0 nebo vyšší).
  
Pokud vám něco z výše uvedeného chybí, nastavte vše pomocí uvedených odkazů. Jste připraveni? Pojďme se pustit do zábavné části!
## Importovat balíčky
Než začneme s tutoriálem, nezapomeňte importovat potřebné jmenné prostory pro práci s Aspose.Cells pro .NET:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Jakmile je importujete, můžete programově manipulovat s excelovými soubory. Nyní se pojďme ponořit do podrobného návodu!
## Krok 1: Vytvořte nebo zpřístupněte sešit aplikace Excel
V tomto kroku vytvoříte nový sešit. Představte si to jako otevření nového souboru aplikace Excel, ale děláte to pomocí kódu!
```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "Your Document Directory";
// Vytvořte adresář, pokud ještě neexistuje.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Vytvoření instance objektu Workbook
Workbook workbook = new Workbook();
```
Zde jednoduše vytváříme novou instanci `Workbook` objekt. Funguje jako váš soubor aplikace Excel, připravený k manipulaci s daty. Můžete také načíst existující soubor zadáním jeho cesty.
## Krok 2: Přístup k pracovnímu listu
Sešity aplikace Excel mohou obsahovat více listů. V tomto kroku se dostaneme k prvnímu listu ve vašem sešitu:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Nyní přistupujeme k prvnímu listu v sešitu. Pokud potřebujete manipulovat s dalšími listy, můžete se na ně odkazovat pomocí jejich indexu nebo názvu.
## Krok 3: Přidání dat do buněk
Začněme přidávat data do konkrétních buněk. Nejprve vložíme aktuální systémové datum do buňky „A1“:
```csharp
worksheet.Cells["A1"].PutValue(DateTime.Now);
```
Tento řádek vloží aktuální datum do buňky A1. Docela skvělé, že? Představte si, že byste to dělali ručně pro stovky buněk – byla by to noční můra. Teď se přesuneme k formátování!
## Krok 4: Formátování data v buňce „A1“
Dále naformátujeme toto datum do čitelnějšího formátu, například „15. října 2024“. A tady Aspose.Cells skutečně vyniká:
1. Získejte styl buňky:
```csharp
Style style = worksheet.Cells["A1"].GetStyle();
```
Zde bereme styl buňky A1. Představte si to jako vezměte si „módu“ buňky před provedením jakýchkoli úprav.
2. Nastavte formát data:
```csharp
style.Number = 15;
```
Nastavení `Number` Vlastnost na 15 použije požadovaný formát data. Toto je vestavěný kód formátu čísla pro zobrazení data ve formátu „d-mmm-rr“.
3. Aplikujte styl na buňku:
```csharp
worksheet.Cells["A1"].SetStyle(style);
```
Tento řádek aplikuje změny stylu na buňku. Nyní se místo výchozího formátu data zobrazí něco mnohem uživatelsky přívětivějšího, například „15. října 2024“.
## Krok 5: Přidání a formátování procenta v buňce „A2“
Pojďme k formátování procent. Představte si, že chcete vložit hodnotu a zobrazit ji jako procento. V tomto kroku přidáme číselnou hodnotu do buňky „A2“ a naformátujeme ji jako procento:
1. Vložit číselnou hodnotu:
```csharp
worksheet.Cells["A2"].PutValue(20);
```
Tím se do buňky A2 vloží číslo 20. Možná si říkáte: „To je jen obyčejné číslo – jak ho převedu na procenta?“ No, k tomu se brzy dostaneme.
2. Načtěte styl a nastavte procentuální formát:
```csharp
style = worksheet.Cells["A2"].GetStyle();
style.Number = 9;  // Formátovat jako procenta
worksheet.Cells["A2"].SetStyle(style);
    ```
Setting the `Number` property to 9 applies the built-in percentage format. Now the value in A2 will be displayed as "2000%." (Yes, 20 is treated as 2000% in percentage formatting).
## Step 6: Add and Format Currency in Cell "A3"
Now, let’s add a numeric value in cell A3 and format it as currency. This is a common use case for financial reports.
1. Insert Numeric Value:
```csharp
worksheet.Cells["A3"].PutValue(2546);
```
Zde do buňky A3 přidáváme číslo 2546. Dále toto číslo naformátujeme tak, aby se zobrazovalo jako měna.
2. Načtěte styl a nastavte formát měny:
```csharp
style = worksheet.Cells["A3"].GetStyle();
style.Number = 6;  // Formátovat jako měnu
worksheet.Cells["A3"].SetStyle(style);
```
Nastavení `Number` Vlastnost na 6 použije formát měny. Hodnota v buňce A3 se nyní zobrazí jako „2 546,00“ s čárkami a dvěma desetinnými místy.
## Krok 7: Uložte soubor Excel
Nyní, když jsme použili všechna kouzla formátování, je čas soubor uložit:
```csharp
// Uložení souboru aplikace Excel
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
Tento řádek uloží soubor aplikace Excel ve formátu Excel 97-2003. Můžete změnit formát `SaveFormat` aby vyhovoval vašim potřebám. A takhle jste programově vytvořili a naformátovali soubor aplikace Excel!
## Závěr
Gratulujeme! Úspěšně jste se naučili, jak používat Aspose.Cells pro .NET k použití vestavěných číselných formátů na buňky v souboru aplikace Excel. Od dat po procenta a měny jsme probrali některé z nejběžnějších potřeb formátování pro zpracování dat v Excelu. Nyní můžete namísto ručního formátování buněk celý proces automatizovat – ušetříte tak čas a snížíte počet chyb.
## Často kladené otázky
### Mohu použít vlastní formáty čísel pomocí Aspose.Cells pro .NET?
Ano! Kromě vestavěných formátů podporuje Aspose.Cells také vlastní formáty čísel. Můžete vytvářet vysoce specifické formáty pomocí `Custom` nemovitost v `Style` třída.
### Jak mohu formátovat buňku jako měnu s konkrétním symbolem?
Chcete-li použít konkrétní symbol měny, můžete použít vlastní formátování nastavením `Style.Custom` vlastnictví.
### Mohu formátovat celé řádky nebo sloupce?
Rozhodně! Styly můžete použít na celé řádky nebo sloupce pomocí `Rows` nebo `Columns` sbírky v `Worksheet` objekt.
### Jak mohu formátovat více buněk najednou?
Můžete použít `Range` objekt pro výběr více buněk a použití stylů na všechny najednou.
### Potřebuji pro použití Aspose.Cells nainstalovaný Microsoft Excel?
Ne, Aspose.Cells funguje nezávisle na Microsoft Excelu, takže Excel na svém počítači nainstalovaný není.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}