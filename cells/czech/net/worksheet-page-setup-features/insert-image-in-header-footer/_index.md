---
"description": "V tomto komplexním průvodci se naučíte, jak snadno vložit obrázek do záhlaví/zápatí pomocí Aspose.Cells pro .NET."
"linktitle": "Vložit obrázek do záhlaví a zápatí pracovního listu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Vložit obrázek do záhlaví a zápatí pracovního listu"
"url": "/cs/net/worksheet-page-setup-features/insert-image-in-header-footer/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Vložit obrázek do záhlaví a zápatí pracovního listu

## Zavedení
Pokud jde o vytváření profesionálně vypadajících tabulek v Excelu, i malé detaily mohou mít obrovský význam. Jedním z takových detailů je přidání obrázků do záhlaví nebo zápatí vašich listů. Je to jistý způsob, jak označit vaše dokumenty a dodat jim nádech profesionality. I když se to může zdát složité, zvláště pokud nejste technicky zdatní, použití Aspose.Cells pro .NET proces výrazně zjednodušuje. Pojďme se tedy do toho pustit a naučit se, jak na to krok za krokem!
## Předpoklady
Než se pustíte do vkládání obrázků do záhlaví a zápatí, ujistěte se, že máte připraveno několik věcí:
1. Visual Studio: Ujistěte se, že máte v počítači nainstalované Visual Studio. Toto IDE je skvělým nástrojem pro vývoj v .NET.
2. Aspose.Cells pro .NET: Pokud to s maximalizací možností Excelu myslíte vážně, můžete si aplikaci zakoupit nebo získat bezplatnou zkušební verzi. Stáhněte si ji. [zde](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: Základní znalost C# a způsobu spouštění .NET aplikací bude výhodou.
4. Soubor s obrázkem: Připravte si soubor s obrázkem, například logo společnosti. V tomto příkladu jej budeme označovat jako `aspose-logo.jpg`.
## Importovat balíčky
Abychom mohli začít s programováním, ujistěte se, že máte do svého projektu v C# importovány potřebné balíčky. Potřebujete jmenný prostor Aspose.Cells, který obsahuje všechny třídy a metody, se kterými budete pracovat.
Zde je návod, jak to zahrnout do kódu:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Nyní, když máme vše nastavené, pojďme si celý proces projít snadno sledovatelnými kroky.
## Krok 1: Nastavení adresáře
Definujte, kam budou vaše soubory uloženy.
Nejprve musíme zadat cestu k adresáři s dokumenty, kde se nachází soubor Excel a obrázek. Cestu můžete nastavit libovolnou, stačí ji nahradit `"Your Document Directory"` s vaší skutečnou cestou k adresáři.
```csharp
string dataDir = "Your Document Directory";
```
## Krok 2: Vytvoření objektu sešitu
Vytvořte instanci sešitu aplikace Excel.
Po nastavení cesty nyní musíme vytvořit novou instanci listu, kam budeme vkládat náš obrázek. 
```csharp
Workbook workbook = new Workbook();
```
## Krok 3: Načtěte obrázek
Otevřete a načtěte soubor s obrázkem a převeďte ho do bajtového pole pro zpracování.
Dále nastavíme cestu k našemu obrázku (v tomto případě k logu) a inicializujeme `FileStream` objekt pro čtení obrázku. Zde je návod, jak to udělat:
```csharp
string logo_url = dataDir + "aspose-logo.jpg";
// Deklarace objektu FileStream
FileStream inFile;
byte[] binaryData;
// Vytvoření instance objektu FileStream
inFile = new FileStream(logo_url, FileMode.Open, FileAccess.Read);
```
## Krok 4: Načtení obrazu do bajtového pole
Převeďte data obrazového souboru do bajtového pole.
Abychom mohli s obrázkem pracovat, musíme ho načíst do bajtového pole. To je nezbytné, protože nám to umožňuje manipulovat s obrázkem v aplikaci.
```csharp
// Vytvoření instance bajtového pole o velikosti objektu FileStream
binaryData = new byte[inFile.Length];
// Přečte blok bajtů ze streamu a zapíše data do dané vyrovnávací paměti bajtového pole.
long bytesRead = inFile.Read(binaryData, 0, (int)inFile.Length);
```
## Krok 5: Konfigurace nastavení stránky pro záhlaví/zápatí
Pro manipulaci se záhlavím a zápatím použijte objekt PageSetup.
Pro vložení obrázku musíme nakonfigurovat objekt nastavení stránky. To nám umožní přizpůsobit záhlaví našeho listu:
```csharp
PageSetup pageSetup = workbook.Worksheets[0].PageSetup;
```
## Krok 6: Vložte logo do záhlaví
Vložte obrázek do záhlaví listu.
Tohle je ten magický okamžik! Vložíme naše logo do střední části záhlaví:
```csharp
// Umístěte logo/obrázek do střední části záhlaví stránky.
pageSetup.SetHeaderPicture(1, binaryData);
// Nastavení skriptu pro logo/obrázek
pageSetup.SetHeader(1, "&G");
// Pomocí skriptu nastavte název listu v pravé části záhlaví stránky
pageSetup.SetHeader(2, "&A");
```
## Krok 7: Uložte si sešit
Uložte změny do nového souboru aplikace Excel.
Po konfiguraci všeho je čas uložit náš sešit. Nezapomeňte zadat nový název výstupního souboru:
```csharp
workbook.Save(dataDir + "InsertImageInHeaderFooter_out.xls");
```
## Krok 8: Vyčištění zdrojů
Zavřete FileStream pro uvolnění zdrojů.
Nakonec, po všech manipulacích, nezapomeňte uklidit zavřením `FileStream`!
```csharp
inFile.Close();
```
## Závěr
A tady to máte! Úspěšně jste vložili obrázek do záhlaví/zápatí listu aplikace Excel pomocí Aspose.Cells pro .NET. Je to jednoduché, že? Jakmile pochopíte kroky, můžete si jej dále přizpůsobit svým specifickým potřebám. Ať už chcete pro svou firmu vytvořit brandingové sestavy, nebo jim jednoduše dodat osobní nádech, tato technika je neuvěřitelně užitečná. 
## Často kladené otázky
### Mohu použít jakýkoli formát obrázku?
Ano, Aspose.Cells podporuje různé obrazové formáty včetně JPEG, PNG a BMP pro obrázky záhlaví a zápatí.
### Je Aspose.Cells zdarma k použití?
Aspose.Cells nabízí bezplatnou zkušební verzi, ale pro další používání si budete muset zakoupit licenci. Zjistěte více o cenách. [zde](https://purchase.aspose.com/buy).
### Jak získám přístup k dokumentaci k Aspose.Cells?
Do funkcí a funkcí Aspose.Cells se můžete ponořit hlouběji na webových stránkách [dokumentace](https://reference.aspose.com/cells/net/).
### Mohu používat Aspose.Cells bez Visual Studia?
Ano, pokud máte běhové prostředí .NET, můžete Aspose.Cells používat v jakémkoli vývojovém prostředí kompatibilním s .NET.
### Co mám dělat, když narazím na problémy?
Pokud narazíte na nějaké problémy nebo potřebujete podporu, podívejte se na [Fórum podpory Aspose](https://forum.aspose.com/c/cells/9) za pomoc od komunity a vývojářů.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}