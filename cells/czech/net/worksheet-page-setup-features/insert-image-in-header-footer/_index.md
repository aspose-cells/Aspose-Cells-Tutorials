---
title: Vložit obrázek do záhlaví Zápatí listu
linktitle: Vložit obrázek do záhlaví Zápatí listu
second_title: Aspose.Cells .NET Excel Processing API
description: V tomto komplexním průvodci se dozvíte, jak snadno vložit obrázek do záhlaví/zápatí pomocí Aspose.Cells for .NET.
weight: 15
url: /cs/net/worksheet-page-setup-features/insert-image-in-header-footer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vložit obrázek do záhlaví Zápatí listu

## Zavedení
Pokud jde o vytváření profesionálně vypadajících tabulek Excelu, malé detaily mohou znamenat obrovský rozdíl. Jedním z takových detailů je přidávání obrázků do záhlaví nebo zápatí vašich listů. Je to spolehlivý způsob, jak označit své dokumenty a dodat jim nádech profesionality. I když to může znít složitě, zvláště pokud nejste techničtí technici, použití Aspose.Cells pro .NET tento proces výrazně zjednodušuje. Pojďme se tedy ponořit a naučit se, jak to udělat krok za krokem!
## Předpoklady
Než se pustíte do vkládání obrázků do sekcí záhlaví a zápatí, ujistěte se, že máte připraveno několik věcí:
1. Visual Studio: Ujistěte se, že máte v počítači nainstalované Visual Studio. Toto IDE je výkonným nástrojem pro vývoj .NET.
2.  Aspose.Cells for .NET: Můžete získat bezplatnou zkušební verzi nebo si ji zakoupit, pokud to myslíte vážně s maximalizací možností aplikace Excel. Stáhněte si to[zde](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: Základní znalost C# a toho, jak provozovat aplikaci .NET, bude prospěšná.
4. Soubor s obrázkem: Připravte si obrázkový soubor jako logo společnosti. V tomto příkladu to budeme označovat jako`aspose-logo.jpg`.
## Importujte balíčky
Chcete-li zahájit naši cestu kódování, ujistěte se, že máte do svého projektu C# importovány potřebné balíčky. Potřebujete jmenný prostor Aspose.Cells, který obsahuje všechny třídy a metody, se kterými budete pracovat.
Zde je návod, jak jej zahrnout do kódu:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Nyní, když máme vše nastaveno, pojďme si projít proces pomocí snadno srozumitelných kroků.
## Krok 1: Nastavte svůj adresář
Definujte, kde budou soubory uloženy.
 Nejprve musíme zadat cestu k adresáři s dokumenty, kde se nachází soubor Excel a obrázek. Můžete nastavit libovolnou cestu; jen nahradit`"Your Document Directory"` s vaší skutečnou cestou k adresáři.
```csharp
string dataDir = "Your Document Directory";
```
## Krok 2: Vytvořte objekt sešitu
Vytvořte instanci sešitu aplikace Excel.
S nastavenou cestou nyní musíme vytvořit novou instanci listu, kam budeme vkládat náš obrázek. 
```csharp
Workbook workbook = new Workbook();
```
## Krok 3: Načtěte svůj obrázek
Otevřete a přečtěte si soubor s obrázkem a převeďte jej na bajtové pole pro zpracování.
Dále nastavíme cestu pro náš obrázek (v tomto případě logo) a inicializujeme a`FileStream` objekt ke čtení obrázku. Jak na to:
```csharp
string logo_url = dataDir + "aspose-logo.jpg";
// Deklarace objektu FileStream
FileStream inFile;
byte[] binaryData;
// Vytvoření instance objektu FileStream
inFile = new FileStream(logo_url, FileMode.Open, FileAccess.Read);
```
## Krok 4: Načtěte obrázek do pole Byte
Převeďte data souboru obrázku do bajtového pole.
Abychom mohli s obrázkem pracovat, musíme jej načíst do bajtového pole. To je nezbytné, protože nám to umožňuje manipulovat s obrázkem v aplikaci.
```csharp
// Instantování bajtového pole velikosti objektu FileStream
binaryData = new byte[inFile.Length];
// Čte blok bajtů z proudu a zapisuje data do dané vyrovnávací paměti nebo pole bajtů.
long bytesRead = inFile.Read(binaryData, 0, (int)inFile.Length);
```
## Krok 5: Nakonfigurujte nastavení stránky pro záhlaví/zápatí
Otevřete objekt PageSetup, abyste mohli manipulovat se sekcemi záhlaví a zápatí.
Abychom vložili náš obrázek, musíme nakonfigurovat objekt nastavení stránky. To nám umožňuje přizpůsobit záhlaví našeho listu:
```csharp
PageSetup pageSetup = workbook.Worksheets[0].PageSetup;
```
## Krok 6: Vložte logo do záhlaví
Vložte obrázek do sekce záhlaví listu.
Tohle je kouzelný okamžik! Naše logo vložíme do střední části záhlaví:
```csharp
// Nastavte logo/obrázek do střední části záhlaví stránky.
pageSetup.SetHeaderPicture(1, binaryData);
// Nastavte skript pro logo/obrázek
pageSetup.SetHeader(1, "&G");
// Nastavte název listu v pravé části záhlaví stránky pomocí skriptu
pageSetup.SetHeader(2, "&A");
```
## Krok 7: Uložte sešit
Uložte změny do nového souboru aplikace Excel.
Po konfiguraci všeho je čas uložit náš sešit. Nezapomeňte zadat nový název výstupního souboru:
```csharp
workbook.Save(dataDir + "InsertImageInHeaderFooter_out.xls");
```
## Krok 8: Vyčistěte zdroje
Zavřete FileStream a uvolněte prostředky.
 Nakonec po veškeré manipulaci nezapomeňte uklidit zavřením vašeho`FileStream`!
```csharp
inFile.Close();
```
## Závěr
A tady to máte! Úspěšně jste vložili obrázek do záhlaví/zápatí listu aplikace Excel pomocí Aspose.Cells for .NET. Je to jednoduché, že? Jakmile porozumíte jednotlivým krokům, můžete jej dále upravit tak, aby vyhovoval vašim konkrétním potřebám. Tato technika je neuvěřitelně užitečná, ať už hledáte zprávy o značce pro vaši firmu, nebo prostě chcete přidat osobní kontakt. 
## FAQ
### Mohu použít jakýkoli formát obrázku?
Ano, Aspose.Cells podporuje různé formáty obrázků včetně JPEG, PNG a BMP pro obrázky záhlaví a zápatí.
### Je Aspose.Cells zdarma k použití?
 Aspose.Cells nabízí bezplatnou zkušební verzi, ale pro další používání si budete muset zakoupit licenci. Zjistěte více o cenách[zde](https://purchase.aspose.com/buy).
### Jak se dostanu k dokumentaci Aspose.Cells?
 Můžete se ponořit hluboko do funkcí a funkcí Aspose.Cells návštěvou[dokumentace](https://reference.aspose.com/cells/net/).
### Mohu používat Aspose.Cells bez sady Visual Studio?
Ano, pokud máte běhové prostředí .NET, můžete Aspose.Cells používat v jakémkoli vývojovém prostředí kompatibilním s .NET.
### Co mám dělat, když narazím na problémy?
 Pokud narazíte na nějaké problémy nebo potřebujete podporu, zkontrolujte[Aspose fórum podpory](https://forum.aspose.com/c/cells/9) za pomoc od komunity a vývojářů.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
