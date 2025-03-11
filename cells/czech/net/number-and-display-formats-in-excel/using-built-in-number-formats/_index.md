---
title: Použití vestavěných formátů čísel v Excelu programově
linktitle: Použití vestavěných formátů čísel v Excelu programově
second_title: Aspose.Cells .NET Excel Processing API
description: Automatizujte formátování čísel v Excelu pomocí Aspose.Cells pro .NET. Naučte se programově používat formáty data, procenta a měny.
weight: 10
url: /cs/net/number-and-display-formats-in-excel/using-built-in-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Použití vestavěných formátů čísel v Excelu programově

## Zavedení
tomto tutoriálu vás provedeme tím, jak používat vestavěné formáty čísel v aplikaci Excel pomocí Aspose.Cells pro .NET. Pokryjeme vše od nastavení vašeho prostředí až po použití různých formátů, jako jsou data, procenta a měny. Ať už jste ostřílený profík nebo jen ponoříte prsty do ekosystému .NET, tato příručka vám umožní formátovat buňky Excelu jako vánek.
## Předpoklady
Před potápěním se ujistěte, že máte následující:
-  Nainstalovaná knihovna Aspose.Cells for .NET. Můžete[stáhněte si jej zde](https://releases.aspose.com/cells/net/).
- Pracovní znalost C# a základního programování .NET.
- Visual Studio nebo jakékoli .NET IDE nainstalované na vašem počítači.
-  Platná licence Aspose nebo[dočasná licence](https://purchase.aspose.com/temporary-license/).
- Nainstalovaný .NET framework (verze 4.0 nebo vyšší).
  
Pokud vám něco z výše uvedeného chybí, postupujte podle uvedených odkazů a vše nastavte. Připraveni? Pojďme skočit do zábavné části!
## Importujte balíčky
Než začneme s výukovým programem, nezapomeňte naimportovat potřebné jmenné prostory pro práci s Aspose.Cells for .NET:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Jakmile je naimportujete, jste připraveni programově manipulovat se soubory Excelu. Nyní se pojďme ponořit do podrobného průvodce!
## Krok 1: Vytvořte nebo otevřete sešit Excel
V tomto kroku vytvoříte nový sešit. Berte to jako otevření nového souboru aplikace Excel, kromě toho, že to děláte pomocí kódu!
```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
// Vytvořte adresář, pokud ještě není přítomen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Vytvoření instance objektu sešitu
Workbook workbook = new Workbook();
```
 Zde jednoduše vytváříme novou instanci`Workbook` objekt. To funguje jako váš soubor Excel připravený pro manipulaci s daty. Můžete také načíst existující soubor zadáním jeho cesty.
## Krok 2: Otevřete sešit
Excelové sešity mohou obsahovat více listů. V tomto kroku přistoupíme k prvnímu listu ve vašem sešitu:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Nyní se dostáváme k prvnímu listu v sešitu. Pokud potřebujete manipulovat s dalšími listy, můžete na ně odkazovat pomocí jejich indexu nebo názvu.
## Krok 3: Přidejte data do buněk
Začněme přidávat nějaká data do konkrétních buněk. Nejprve vložíme aktuální systémové datum do buňky "A1":
```csharp
worksheet.Cells["A1"].PutValue(DateTime.Now);
```
Tento řádek vloží aktuální datum do buňky A1. Docela cool, že? Představte si, že byste to dělali ručně pro stovky buněk – byla by to noční můra. Nyní přejdeme k formátování!
## Krok 4: Formátování data v buňce "A1"
Dále zformátujme toto datum do čitelnějšího formátu, například „15-Oct-24“. Tady Aspose.Cells opravdu září:
1. Načíst styl buňky:
```csharp
Style style = worksheet.Cells["A1"].GetStyle();
```
Zde se chopíme stylu buňky A1. Berte to jako chycení „módy“ buňky před provedením jakýchkoli úprav.
2. Nastavte formát data:
```csharp
style.Number = 15;
```
 Nastavení`Number` vlastnost na 15 použije požadovaný formát data. Toto je vestavěný kód formátu čísel pro zobrazení dat ve formátu "d-mmm-rr".
3. Použijte styl na buňku:
```csharp
worksheet.Cells["A1"].SetStyle(style);
```
Tento řádek aplikuje změny stylu na buňku. Nyní namísto výchozího formátu data uvidíte něco mnohem uživatelsky přívětivějšího, například „15-Oct-24“.
## Krok 5: Přidejte a naformátujte procento v buňce "A2"
Pojďme k formátování procent. Představte si, že chcete vložit hodnotu a zobrazit ji v procentech. V tomto kroku přidáme číselnou hodnotu do buňky „A2“ a naformátujeme ji jako procento:
1. Vložit číselnou hodnotu:
```csharp
worksheet.Cells["A2"].PutValue(20);
```
Tím se do buňky A2 vloží číslo 20. Možná si říkáte: "To je jen obyčejné číslo - jak ho převedu na procenta?" No, už se k tomu dostaneme.
2. Získejte styl a nastavte procentuální formát:
```csharp
style = worksheet.Cells["A2"].GetStyle();
style.Number = 9;  // Formát v procentech
worksheet.Cells["A2"].SetStyle(style);
    ```
Setting the `Number` property to 9 applies the built-in percentage format. Now the value in A2 will be displayed as "2000%." (Yes, 20 is treated as 2000% in percentage formatting).
## Step 6: Add and Format Currency in Cell "A3"
Now, let’s add a numeric value in cell A3 and format it as currency. This is a common use case for financial reports.
1. Insert Numeric Value:
```csharp
worksheet.Cells["A3"].PutValue(2546);
```
Zde přidáváme 2546 do buňky A3. Dále toto číslo naformátujeme, aby se zobrazovalo jako měna.
2. Získejte styl a nastavte formát měny:
```csharp
style = worksheet.Cells["A3"].GetStyle();
style.Number = 6;  // Formát jako měna
worksheet.Cells["A3"].SetStyle(style);
```
 Nastavení`Number` vlastnost na 6 použije formát měny. Nyní se hodnota v buňce A3 zobrazí jako "2 546,00" doplněná čárkami a dvěma desetinnými místy.
## Krok 7: Uložte soubor Excel
Nyní, když jsme použili všechna kouzla s formátováním, je čas soubor uložit:
```csharp
// Uložení souboru Excel
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
 Tento řádek uloží soubor aplikace Excel ve formátu Excel 97-2003. Můžete změnit`SaveFormat`aby vyhovoval vašim potřebám. A právě tak jste programově vytvořili a naformátovali soubor Excel!
## Závěr
Gratuluji! Úspěšně jste se naučili, jak používat Aspose.Cells for .NET k použití vestavěných číselných formátů na buňky v souboru aplikace Excel. Od dat po procenta a měny jsme pokryli některé z nejběžnějších potřeb formátování pro zpracování dat v Excelu. Nyní můžete místo ručního formátování buněk celý proces automatizovat – ušetříte čas a snížíte počet chyb.
## FAQ
### Mohu použít vlastní číselné formáty pomocí Aspose.Cells pro .NET?
 Ano! Kromě vestavěných formátů podporuje Aspose.Cells také vlastní formáty čísel. Můžete vytvořit vysoce specifické formáty pomocí`Custom` nemovitost v`Style` třída.
### Jak mohu naformátovat buňku jako měnu se specifickým symbolem?
 Chcete-li použít konkrétní symbol měny, můžete použít vlastní formátování nastavením`Style.Custom` vlastnictví.
### Mohu formátovat celé řádky nebo sloupce?
 Absolutně! Styly můžete použít na celé řádky nebo sloupce pomocí`Rows` nebo`Columns`sbírky v`Worksheet` objekt.
### Jak mohu naformátovat více buněk najednou?
Můžete použít`Range` objekt vybrat více buněk a aplikovat na ně styly najednou.
### Potřebuji k použití Aspose.Cells nainstalovaný Microsoft Excel?
Ne, Aspose.Cells funguje nezávisle na aplikaci Microsoft Excel, takže nepotřebujete, aby byl na vašem počítači nainstalován Excel.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
