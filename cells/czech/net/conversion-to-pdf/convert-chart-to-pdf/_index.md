---
title: Převést graf do PDF v .NET
linktitle: Převést graf do PDF v .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak převést grafy Excel do PDF v .NET pomocí Aspose.Cells s tímto podrobným průvodcem! Ideální pro programátory všech úrovní.
weight: 11
url: /cs/net/conversion-to-pdf/convert-chart-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převést graf do PDF v .NET

## Zavedení
Chcete převést grafy z tabulek aplikace Excel do formátu PDF pomocí .NET? Tak to jste na správném místě! V této příručce prozkoumáme výhody a nevýhody použití Aspose.Cells, abychom toho dosáhli. Ať už jste ostřílený programátor nebo nováček, náš postup krok za krokem vám pomůže se v tomto procesu snadno orientovat.

## Předpoklady
Než se vydáme na tuto poučnou cestu, je zde několik předpokladů, které musíte zaškrtnout ze svého seznamu:
### 1. Nainstalované rozhraní .NET Framework nebo .NET Core
Ujistěte se, že máte na počítači nainstalováno rozhraní .NET Framework nebo .NET Core. Tato příručka je použitelná pro obě prostředí, takže se nemusíte bát, pokud preferujete jedno před druhým!
### 2. Aspose.Cells Library
 Kouzlo se děje díky knihovně Aspose.Cells, kterou musíte zahrnout do svého projektu. Můžete si jej stáhnout z[Aspose webové stránky](https://releases.aspose.com/cells/net/).
### 3. Základní porozumění programování v C#
Pokud máte základní znalosti C#, je to fantastické! Spolu s příklady, které poskytujeme, zjistíte, že je snadné sledovat. Pokud jste začátečník, příliš se netrápte; udržujeme věci jednoduché a přímočaré.
### 4. Nastavení sady Visual Studio
Ať už používáte Visual Studio nebo jakékoli jiné IDE, ujistěte se, že vaše vývojové prostředí je nastaveno pro psaní a spouštění aplikací .NET.
## Importujte balíčky
Chcete-li začít s konverzí, musíte do projektu importovat potřebné balíčky. Jak na to:
### Otevřete svůj projekt
Spusťte Visual Studio a otevřete projekt, kde chcete implementovat tuto funkci.
### Nainstalujte balíček NuGet Aspose.Cells
Knihovnu Aspose.Cells můžete snadno přidat přes NuGet Package Manager. Zde je postup:
- Klepněte pravým tlačítkem myši na svůj projekt v Průzkumníku řešení.
- Vyberte „Spravovat balíčky NuGet“.
- Vyhledejte „Aspose.Cells“ a stiskněte tlačítko Instalovat.
To zajistí, že budete mít všechny třídy a metody, které potřebujete, k dispozici na dosah ruky!

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Charts;
```

Nyní se pustíme do hrubšího převodu grafu do formátu PDF pomocí Aspose.Cells. Každý krok projdeme metodicky, takže budete přesně vědět, co se děje.
## Krok 1: Nastavení adresáře dokumentů
První věci jako první! Musíte zadat cestu, kde je uložen váš dokument Excel. Zde nasměrujete knihovnu Aspose.Cells, abyste našli svůj soubor .xls.
```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
```
 Tento řádek nastavuje`dataDir` proměnnou k umístění vašeho souboru Excel. Nezapomeňte vyměnit`"Your Document Directory"` s vaší skutečnou cestou.
## Krok 2: Načtěte soubor Excel
Nyní, když jste nastavili adresář, je čas načíst soubor Excel, který obsahuje grafy. Postup:
```csharp
// Načtěte soubor Excel obsahující grafy
Workbook workbook = new Workbook(dataDir + "Sample1.xls");
```
 Tímto způsobem vytvoříte novou instanci`Workbook` a řeknete mu, aby načetl váš ukázkový soubor Excel. Ujistěte se, že název souboru a přípona odpovídají skutečnému souboru.
## Krok 3: Otevřete správný pracovní list
Soubory Excel mohou mít více listů, takže musíte určit, se kterým chcete pracovat. Zde se dostáváme k prvnímu pracovnímu listu:
```csharp
// Otevřete první pracovní list
Worksheet worksheet = workbook.Worksheets[0];
```
 Pomocí indexu`0` vyzvedne první pracovní list. Pokud je graf na jiném listu, upravte index.
## Krok 4: Přístup k grafu
Nyní, když máte list, vezměte graf, který chcete převést:
```csharp
// Otevřete první graf v listu
Chart chart = worksheet.Charts[0];
```
Tento řádek přistupuje k prvnímu grafu obsaženému v listu. Pokud máte více grafů a chcete převést další, stačí zvýšit index.
## Krok 5: Převeďte graf do PDF
S grafem v ruce je čas převést jej do formátu PDF. Zde je postup:
```csharp
// Uložte graf do formátu PDF
chart.ToPdf(dataDir + "Output-Chart_out.pdf");
```
Tento ověřovací příkaz říká Aspose.Cells, aby uložil graf jako PDF do zadané výstupní cesty. A voilà! Váš graf je nyní ve formátu PDF.
## Krok 6: Uložte graf do Memory Stream
Pokud dáváte přednost uložení grafu nikoli do souboru, ale do paměťového toku (například pokud jej plánujete dynamicky stahovat), můžete tak učinit pomocí následujícího kódu:
```csharp
// Uložte graf do formátu PDF ve streamu
MemoryStream ms = new MemoryStream();
chart.ToPdf(ms);
```
 Tímto způsobem uložíte graf do a`MemoryStream` spíše než přímo do souboru. To může být užitečné zejména pro webové aplikace, které vyžadují dynamické generování souborů.
## Závěr
A tady to máte! Právě jste se naučili, jak převést graf Excel do souboru PDF pomocí Aspose.Cells v .NET. Tento proces zahrnuje nejen jednoduché příkazy, ale také vám dává flexibilitu v tom, jak a kam chcete své grafy uložit. Ať už používáte souborový systém nebo paměťový tok, volba je na vás!
Nyní byste měli mít jistotu při převodu grafů do PDF ve svých budoucích aplikacích .NET. Neváhejte experimentovat s dalšími funkcemi Aspose.Cells, protože toho můžete objevit mnohem víc!
## FAQ
### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna .NET, která umožňuje vývojářům vytvářet, manipulovat, převádět a vykreslovat soubory aplikace Excel programově.
### Mohu používat Aspose.Cells zdarma?
 Ano! Aspose.Cells můžete vyzkoušet zdarma stažením zkušební verze z jejich[místo](https://releases.aspose.com/).
### Jak mohu odstraňovat chyby při používání Aspose.Cells?
 Pokud narazíte na nějaké problémy, můžete navštívit[Aspose fórum podpory](https://forum.aspose.com/c/cells/9) o pomoc.
### Podporuje Aspose.Cells jiné formáty dokumentů?
Ano, kromě XLS/XLSX podporuje Aspose.Cells řadu formátů, včetně CSV, PDF, HTML a dalších.
### Mohu si zakoupit licenci pro Aspose.Cells?
 Absolutně! Můžete[zakoupit licenci](https://purchase.aspose.com/buy) na webu Aspose, kde najdete výhody plné verze.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
