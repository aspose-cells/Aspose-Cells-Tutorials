---
"description": "Naučte se, jak získat rozměry stránky v listu aplikace Excel pomocí Aspose.Cells pro .NET. Podrobný návod k přizpůsobení velikostí papíru A2, A3, A4 a Letter."
"linktitle": "Získejte rozměry stránky pracovního listu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Získejte rozměry stránky pracovního listu"
"url": "/cs/net/worksheet-page-setup-features/get-page-dimensions/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Získejte rozměry stránky pracovního listu

## Zavedení
Pokud pracujete s excelovými soubory programově pomocí nástroje Aspose.Cells pro .NET, může se stát, že budete potřebovat zobrazit rozměry stránky listu a nastavit je. Znalost rozměrů vám může pomoci s rozvržením, tiskem a přizpůsobením excelových listů pro specifické účely. V tomto článku se podíváme na to, jak načíst a zobrazit různé rozměry stránky v Excelu pomocí nástroje Aspose.Cells pro .NET. Projdeme si podrobný návod, abyste se ujistili, že máte všechny podrobnosti pro sebevědomý začátek.
## Předpoklady
Než se do toho pustíme, ujistěte se, že máte vše, co potřebujete k dodržování tohoto tutoriálu.
1. Aspose.Cells pro .NET: Ujistěte se, že máte nainstalovaný Aspose.Cells pro .NET. Můžete [stáhněte si knihovnu zde](https://releases.aspose.com/cells/net/) nebo jej nainstalujte pomocí NuGetu ve vašem .NET projektu.
2. Prostředí .NET: Kompatibilní vývojové prostředí .NET (např. Visual Studio).
3. Nastavení licence: Pro plnou funkčnost Aspose.Cells použijte licenci. Můžete [požádejte o bezplatnou dočasnou licenci](https://purchase.aspose.com/temporary-license/) pro účely hodnocení.
Pokud Aspose.Cells testujete poprvé, začněte s bezplatnou zkušební verzí.
## Importovat balíčky
Než se pustíme do kódu, budete muset do projektu importovat jmenný prostor Aspose.Cells, abyste měli přístup ke všem potřebným třídám a metodám.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Rozdělme si proces na jednoduché kroky. Zde si ukážeme různé velikosti papíru, aplikujeme je na pracovní list a vytiskneme pro každou z nich rozměry.
## Krok 1: Vytvoření instance sešitu
Prvním krokem je vytvoření instance `Workbook` třída. Tento objekt bude sloužit jako náš hlavní sešit obsahující pracovní listy, se kterými můžeme manipulovat.
```csharp
Workbook book = new Workbook();
```
Myslete na `Workbook` jako hlavní kontejner pro váš excelový soubor. Potřebujeme ho pro přístup k jednotlivým listům a jejich správu.
## Krok 2: Přístup k prvnímu pracovnímu listu
Dále si otevřeme první list v sešitu. Ve výchozím nastavení má nový sešit jeden list, takže na něj můžeme přímo odkazovat pomocí indexu `0`.
```csharp
Worksheet sheet = book.Worksheets[0];
```
Ten/Ta/To `Worksheets` sbírka v `Workbook` umožňuje nám přístup ke každému listu pomocí indexu. Zde vezmeme první list pro zahájení nastavení rozměrů stránky.
## Krok 3: Nastavte velikost papíru na A2 a zobrazte rozměry
Nyní, když máme přístup k našemu listu, nastavme jeho velikost papíru na A2. Nastavení velikosti papíru je užitečné pro formátování stránky před jejím tiskem nebo exportem. Jakmile nastavíme velikost papíru, vytiskneme rozměry stránky v palcích.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Zde měníme `PaperSize` majetek `PaperA2`Po nastavení velikosti `PageSetup.PaperWidth` a `PageSetup.PaperHeight` načíst šířku a výšku listu v palcích. To nám poskytne rychlý přehled o rozměrech stránky.
## Krok 4: Nastavte velikost papíru na A3 a zobrazte rozměry
Podle stejných kroků jako výše upravme rozměry stránky na velikost A3. Tato změna je užitečná pro o něco větší výtisky nebo pro umístění většího množství obsahu na jednu stránku.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Formát A3 je dvojnásobný oproti formátu A4, takže je dobrou volbou pro velké tabulky nebo podrobné grafy. Změna velikosti papíru pomáhá přizpůsobit rozvržení pracovního listu.
## Krok 5: Nastavení velikosti papíru na A4 a zobrazení rozměrů
Nyní nastavme velikost papíru na A4. Toto je nejčastěji používaná velikost stránky pro tisk dokumentů. Aktualizované rozměry zobrazíme později.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Pokud je vaším cílem standardní formát dokumentu, obvykle je nejvhodnější velikost A4. Znalost rozměrů může pomoci s úpravou rozvržení obsahu a předejít problémům s tiskem.
## Krok 6: Nastavení velikosti papíru na Letter a zobrazení rozměrů
Nakonec nastavíme velikost papíru na formát Letter, který se běžně používá v Severní Americe. Vytiskněme rozměry ještě naposledy.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Velikost Letter se v Severní Americe široce používá pro dokumenty, takže nastavení této velikosti je užitečné při spolupráci s týmy nebo klienty, kteří tam sídlí.
## Závěr
tomto tutoriálu jsme si prošli, jak nastavit a načíst rozměry stránky pro různé velikosti papíru pomocí Aspose.Cells pro .NET. Konfigurací velikostí stránek, jako jsou A2, A3, A4 a Letter, můžete formátovat listy aplikace Excel tak, aby vyhovovaly specifickým potřebám tisku a rozvržení. Tato kontrola nad rozměry stránky je obzvláště cenná pro profesionální reporting a prezentace, protože zajišťuje, že se váš obsah perfektně vejde na každou velikost stránky.
## Často kladené otázky
### Jak mohu změnit orientaci stránky v Aspose.Cells?  
Orientaci můžete změnit pomocí `PageSetup.Orientation` vlastnost nastavením na jednu z nich `PageOrientationType.Pnebotrait` or `PageOrientationType.Landscape`.
### Mohu v Aspose.Cells nastavit vlastní rozměry stránky?  
Ano, můžete nastavit vlastní rozměry stránky úpravou okrajů a možností měřítka v části `PageSetup` pro větší kontrolu.
### Jaká je výchozí velikost papíru v Aspose.Cells?  
Výchozí velikost papíru je obvykle A4. Může to však záviset na místním nastavení a lze to dle potřeby upravit.
### Je možné zobrazit náhled rozvržení stránek v Aspose.Cells?  
I když Aspose.Cells nenabízí grafický náhled, můžete programově nastavit rozvržení a používat náhledy tisku v Excelu.
### Jak nainstaluji Aspose.Cells pro .NET?  
Aspose.Cells můžete nainstalovat pomocí Správce balíčků NuGet ve Visual Studiu nebo si stáhnout knihovnu DLL z [Stránka ke stažení Aspose.Cells](https://releases.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}