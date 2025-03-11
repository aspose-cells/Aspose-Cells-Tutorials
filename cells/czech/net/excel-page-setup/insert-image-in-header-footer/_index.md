---
title: Vložit obrázek do záhlaví, zápatí
linktitle: Vložit obrázek do záhlaví, zápatí
second_title: Aspose.Cells for .NET API Reference
description: Naučte se vkládat obrázky do záhlaví a zápatí pomocí Aspose.Cells for .NET s tímto komplexním průvodcem krok za krokem.
weight: 60
url: /cs/net/excel-page-setup/insert-image-in-header-footer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vložit obrázek do záhlaví, zápatí

## Zavedení

Při práci se soubory Excel hrají záhlaví a zápatí zásadní roli při poskytování kontextu a cenných informací. Představte si, že připravujete zprávu pro svou firmu a logo společnosti musí být přítomno v záhlaví, aby tomu dodalo profesionální nádech. V této příručce vám ukážeme, jak použít Aspose.Cells pro .NET k vložení obrázku do záhlaví nebo zápatí vašich excelových listů.

## Předpoklady

Než se ponoříte do skutečného kódu, musíte mít připraveno několik věcí:

1.  Knihovna Aspose.Cells for .NET: Ujistěte se, že máte ve svém prostředí .NET nainstalovanou knihovnu Aspose.Cells. Pokud ho ještě nemáte, můžete[stáhněte si jej zde](https://releases.aspose.com/cells/net/).
2. Visual Studio nebo jakékoli jiné IDE: K psaní a spouštění kódu C# budete potřebovat integrované vývojové prostředí.
3.  Ukázkový obrázek: Připravte si obrázek, který chcete vložit do záhlaví nebo zápatí. Pro náš příklad použijeme logo společnosti tzv`aspose-logo.jpg`.
4. Základní znalost C#: I když to není povinné, porozumění C# vám usnadní sledování tohoto návodu.
5. Přístup k systému souborů: Ujistěte se, že máte přístup k systému souborů, kde si přečtete obrázek a uložíte soubor Excel.

## Importujte balíčky

Chcete-li začít, musíte do souboru C# importovat potřebné jmenné prostory. Zde je rychlý rozpis:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Tyto importy poskytnou přístup ke všem třídám, které potřebujeme k manipulaci se soubory aplikace Excel a zpracování souborů v systému.

## Krok 1: Nastavení cesty k adresáři

Nejprve budete muset určit adresář, kde jsou umístěny soubory a obrázky aplikace Excel. Aktualizujte cestu, aby odpovídala vaší místní struktuře.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Podle toho aktualizujte
```

 Tento řádek nastavuje`dataDir`proměnná, což je základní cesta pro umístění obrázku, který chcete vložit do záhlaví.

## Krok 2: Vytvoření objektu sešitu

Dále musíte vytvořit nový sešit, kam přidáte svůj obrázek.

```csharp
Workbook workbook = new Workbook();
```

 Tento řádek kódu inicializuje novou instanci souboru`Workbook` třídy, což vám umožní manipulovat s tabulkami aplikace Excel.

## Krok 3: Definování cesty obrazu

 Je čas vytvořit řetězcovou proměnnou, která bude obsahovat cestu k obrázku, který chcete použít. V našem případě používáme`aspose-logo.jpg`.

```csharp
string logo_url = dataDir + "aspose-logo.jpg";
```

Zde zřetězíme cestu k adresáři s názvem souboru loga.

## Krok 4: Čtení obrázku jako binárních dat

Abychom vložili obrázek do záhlaví, musíme soubor obrázku načíst jako binární data.

```csharp
FileStream inFile = new FileStream(logo_url, FileMode.Open, FileAccess.Read);
byte[] binaryData = new byte[inFile.Length];
long bytesRead = inFile.Read(binaryData, 0, (int)inFile.Length);
```

-  The`FileStream` slouží k otevření obrázku v režimu čtení.
-  Poté deklarujeme bajtové pole`binaryData` pro uložení obrazových dat.
-  Nakonec načteme obrazová data z`FileStream`.

## Krok 5: Přístup k objektu Nastavení stránky

 Chcete-li provést změny v záhlaví, musíme získat přístup k`PageSetup` objekt spojený s prvním listem. 

```csharp
PageSetup pageSetup = workbook.Worksheets[0].PageSetup;
```

 Tady, dostáváme`PageSetup` objekt, který nám umožňuje manipulovat s nastavením tisku pro list.

## Krok 6: Vložení obrázku do záhlaví

S binárními daty obrázku je nyní můžeme vložit do záhlaví.

```csharp
pageSetup.SetHeaderPicture(1, binaryData);
```

 Tento řádek umístí obrázek do střední části záhlaví. Parametr`1` určuje sekci záhlaví.

## Krok 7: Nastavení obsahu záhlaví

Nyní, když máme náš obrázek na místě, přidáme do záhlaví nějaký text, abychom zlepšili jeho kontext. 

```csharp
pageSetup.SetHeader(1, "&G"); // Vloží obrázek
pageSetup.SetHeader(2, "&A"); // Vloží název listu
```

- První řádek vloží zástupný symbol obrázku (`&G`).
- Druhý řádek přidá název listu do pravé části záhlaví pomocí zástupného symbolu (`&A`).

## Krok 8: Uložení sešitu

Po provedení všech potřebných změn je čas sešit uložit.

```csharp
workbook.Save(dataDir + "InsertImageInHeaderFooter_out.xls");
```

Tento řádek uloží sešit se zadaným názvem souboru do adresáře, který jste definovali dříve.

## Krok 9: Zavření FileStream

 Nakonec nezapomeňte zavřít svůj`FileStream` uvolnit zdroje.

```csharp
inFile.Close();
```

Vaše aplikace tak bude uklizená a zabrání se únikům paměti.

## Závěr

Gratuluji! Úspěšně jste přidali obrázek do záhlaví souboru aplikace Excel pomocí Aspose.Cells for .NET. Ať už jde o firemní logo nebo inspirativní citát, záhlaví může výrazně zvýšit profesionalitu vašich dokumentů. Nyní můžete tyto znalosti aplikovat na různé projekty – představte si, jak budou vypadat vaše zprávy s přizpůsobenými záhlavími a zápatími!

## FAQ

### Jaké formáty souborů podporuje Aspose.Cells pro obrázky?
Aspose.Cells podporuje různé formáty, včetně JPEG, PNG, BMP, GIF a TIFF.

### Mohu do záhlaví/zápatí vložit více obrázků?
Ano, do různých částí záhlaví nebo zápatí můžete vložit samostatné obrázky pomocí různých zástupných symbolů.

### Je Aspose.Cells zdarma?
 Aspose.Cells nabízí bezplatnou zkušební verzi, ale pro plný přístup a další funkce je k dispozici licencovaná verze. Můžete získat a[dočasná licence zde](https://purchase.aspose.com/temporary-license/).

### Jak mohu vyřešit problémy s nezobrazováním obrázků?
Ujistěte se, že cesta k obrázku je správná a soubor existuje. Zkontrolujte také kompatibilitu formátu obrázku.

### Kde najdu další dokumentaci pro Aspose.Cells?
 Můžete najít podrobnou dokumentaci[zde](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
