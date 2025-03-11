---
title: Otevírání souborů CSV pomocí preferovaného analyzátoru
linktitle: Otevírání souborů CSV pomocí preferovaného analyzátoru
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se otevírat a analyzovat soubory CSV pomocí vlastních analyzátorů v Aspose.Cells for .NET. Zpracovávejte text a data bez námahy. Ideální pro vývojáře.
weight: 11
url: /cs/net/csv-file-handling/csv-file-opening-csv-files-with-preferred-parser/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Otevírání souborů CSV pomocí preferovaného analyzátoru

## Zavedení
Při práci se soubory CSV někdy chcete zpracovávat různé typy dat pomocí vlastních analyzátorů. Tento tutoriál vás provede tím, jak otevřít soubory CSV pomocí preferovaného analyzátoru pomocí Aspose.Cells for .NET. Ať už chcete pracovat s textem, daty nebo jinými vlastními formáty, tento průvodce vás provede každým krokem s jasným vysvětlením.
## Předpoklady
Než se ponoříme do kódu, pojďme si pokrýt základní položky, které potřebujete, abyste mohli začít.
1.  Aspose.Cells for .NET Library: Ujistěte se, že máte nainstalovanou knihovnu Aspose.Cells. Můžete si jej stáhnout[zde](https://releases.aspose.com/cells/net/) . Můžete také použít bezplatnou zkušební verzi[zde](https://releases.aspose.com/).
2. Vývojové prostředí .NET: Doporučuje se Visual Studio, ale bude fungovat jakékoli IDE kompatibilní s .NET.
3. Základní znalost C#: Tento tutoriál předpokládá, že jste obeznámeni s C# a objektově orientovaným programováním.
## Importujte balíčky
Chcete-li používat Aspose.Cells, budete muset importovat potřebné jmenné prostory v horní části souboru C#:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Nyní, když jsme připravili scénu, pojďme si projít, jak otevřít soubor CSV pomocí preferovaného analyzátoru, který pracuje s různými datovými formáty, jako je text a data.
## Krok 1: Definujte vlastní analyzátory
 Chcete-li zpracovávat různé typy dat, jako je text nebo konkrétní formáty data, musíte definovat vlastní analyzátory. V Aspose.Cells implementují vlastní analyzátory`ICustomParser` rozhraní.
### 1.1 Vytvořte analyzátor textu
Tento analyzátor zpracovává běžné textové hodnoty. Nemění formát, takže hodnota je vrácena tak, jak je.
```csharp
class TextParser : ICustomParser
{
    public object ParseObject(string value)
    {
        return value;
    }
    public string GetFormat()
    {
        return "";
    }
}
```
 The`ParseObject` metoda jednoduše vrátí vstupní hodnotu. Je to jako říct: "Nic neměň, jen mi dej text!"
### 1.2 Vytvořte analyzátor data
 U dat budete chtít zajistit, aby byla data CSV správně analyzována`DateTime` objektů. Zde je návod, jak vytvořit analyzátor data:
```csharp
class DateParser : ICustomParser
{
    public object ParseObject(string value)
    {
        DateTime myDate = DateTime.ParseExact(value, "dd/MM/yyyy", 
            System.Globalization.CultureInfo.InvariantCulture);
        return myDate;
    }
    public string GetFormat()
    {
        return "dd/MM/yyyy";
    }
}
```
 V tomto parseru používáme`ParseExact` abyste zajistili správnou interpretaci data na základě předem definovaného formátu (`"dd/MM/yyyy"`). Tímto způsobem bude jakékoli datum ve vašem CSV v tomto formátu zpracováno bez problémů.
## Krok 2: Nakonfigurujte možnosti načítání
 Dále je třeba nakonfigurovat způsob načítání souboru CSV. To se provádí pomocí`TxtLoadOptions` class, která vám umožňuje určit možnosti analýzy, včetně kódování a vlastních analyzátorů.
### 2.1 Nastavení možností načítání
 Začneme inicializací`TxtLoadOptions` a definování klíčových parametrů, jako je oddělovač a kódování:
```csharp
TxtLoadOptions oTxtLoadOptions = new TxtLoadOptions(LoadFormat.Csv);
oTxtLoadOptions.Separator = Convert.ToChar(",");
oTxtLoadOptions.Encoding = Encoding.UTF8;
oTxtLoadOptions.ConvertDateTimeData = true;
```
- Oddělovač: Definuje znak použitý k oddělení hodnot v souboru CSV (v tomto případě čárkami).
- Kódování: Ke zpracování široké škály znaků používáme kódování UTF-8.
-  ConvertDateTimeData: Nastavení na hodnotu true zajistí, že hodnoty data budou automaticky převedeny na`DateTime` předměty, pokud je to možné.
### 2.2 Použít vlastní analyzátory
Dále přiřadíme analyzátory, které jsme vytvořili dříve, aby zpracovávaly hodnoty v CSV:
```csharp
oTxtLoadOptions.PreferredParsers = new ICustomParser[] 
{ 
    new TextParser(), 
    new DateParser() 
};
```
 To říká Aspose.Cells, aby použilo`TextParser` pro obecné textové hodnoty a`DateParser`pro všechna pole data, na která narazí v souboru CSV.
## Krok 3: Načtěte a přečtěte si soubor CSV
 Nyní, když jsou nakonfigurovány možnosti načítání, můžete načíst soubor CSV do souboru`Aspose.Cells.Workbook` objekt.
### 3.1 Načtěte soubor CSV
 Soubor CSV načteme předáním cesty k souboru a nakonfigurovaným`TxtLoadOptions` k`Workbook` konstruktér:
```csharp
string sourceDir = "Your Document Directory";
Workbook oExcelWorkBook = new Aspose.Cells.Workbook(sourceDir + "samplePreferredParser.csv", oTxtLoadOptions);
```
Tento krok převede vaše data CSV do plně funkčního sešitu aplikace Excel s každou hodnotou analyzovanou podle vašich preferovaných pravidel.
## Krok 4: Přístup k datům buněk a jejich zobrazení
Jakmile je CSV načten do sešitu, můžete začít pracovat s daty. Můžete například chtít vytisknout typ a hodnotu konkrétních buněk.
### 4.1 Načtení a zobrazení buňky A1
Pojďme načíst první buňku (A1) a zobrazit její hodnotu a typ:
```csharp
Cell oCell = oExcelWorkBook.Worksheets[0].Cells["A1"];
Console.WriteLine("A1: " + oCell.Type.ToString() + " - " + oCell.DisplayStringValue);
```
 Tady,`Type` vlastnost zobrazuje datový typ (jako např`String` nebo`DateTime` ), a`DisplayStringValue` vám dává formátovanou hodnotu.
### 4.2 Načtení a zobrazení buňky B1
Podobně můžeme načíst a zobrazit další buňku, například B1:
```csharp
oCell = oExcelWorkBook.Worksheets[0].Cells["B1"];
Console.WriteLine("B1: " + oCell.Type.ToString() + " - " + oCell.DisplayStringValue);
```
Tento proces lze opakovat pro tolik buněk, kolik potřebujete zkontrolovat.
## Krok 5: Uložte sešit
 Po práci s daty můžete chtít uložit sešit do nového souboru. Aspose.Cells to usnadňuje pomocí jednoduchého`Save` metoda:
```csharp
string outputDir = "Your Document Directory";
oExcelWorkBook.Save(outputDir + "outputsamplePreferredParser.xlsx");
```
Tím se sešit uloží jako soubor aplikace Excel a zachová veškeré formátování a analýzu dat, které jste použili.
## Závěr
Otevírání souborů CSV pomocí preferovaného analyzátoru v Aspose.Cells for .NET je flexibilní a výkonný způsob, jak zpracovávat různé typy dat. Vytvořením vlastních analyzátorů a konfigurací možností načítání můžete zajistit, že vaše soubory CSV budou analyzovány přesně tak, jak je potřebujete, ať už pracujete s textem, daty nebo jinými vlastními formáty. S tímto výukovým programem jste nyní připraveni zvládnout složitější scénáře analýzy dat ve vašich projektech.
## FAQ
### Jaký je účel vlastních analyzátorů v Aspose.Cells pro .NET?
Vlastní analyzátory umožňují definovat, jak by měly být při načítání souboru CSV analyzovány konkrétní typy dat, jako je text nebo data.
### Mohu v souboru CSV použít jiný oddělovací znak?
 Ano, můžete zadat jakýkoli znak jako oddělovač v`TxtLoadOptions.Separator` vlastnictví.
### Jak zvládnu kódování v Aspose.Cells při načítání CSV?
 Můžete nastavit`Encoding` vlastnictví`TxtLoadOptions` do libovolného schématu kódování, jako je UTF-8, ASCII atd.
### Co se stane, když je formát data v CSV jiný?
Konkrétní formát data můžete definovat pomocí vlastního analyzátoru a zajistit tak správnou analýzu hodnot data.
### Mohu uložit sešit v jiných formátech?
Ano, Aspose.Cells vám umožňuje uložit sešit v různých formátech, jako je XLSX, CSV, PDF a další.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
