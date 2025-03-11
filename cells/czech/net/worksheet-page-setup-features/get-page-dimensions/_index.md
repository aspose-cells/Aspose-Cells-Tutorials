---
title: Získejte rozměry stránky listu
linktitle: Získejte rozměry stránky listu
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak získat rozměry stránky v excelovém listu pomocí Aspose.Cells for .NET. Podrobný průvodce přizpůsobením velikostí papíru A2, A3, A4 a Letter.
weight: 13
url: /cs/net/worksheet-page-setup-features/get-page-dimensions/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Získejte rozměry stránky listu

## Zavedení
Pokud pracujete se soubory aplikace Excel programově pomocí Aspose.Cells for .NET, může se stát, že budete potřebovat získat přístup a nastavit rozměry stránky listu. Znalost rozměrů může pomoci s rozvržením, tiskem a přizpůsobením listů aplikace Excel pro konkrétní účely. V tomto článku prozkoumáme, jak načíst a zobrazit různé rozměry stránky v Excelu pomocí Aspose.Cells for .NET. Projdeme si návod krok za krokem, abychom se ujistili, že máte všechny podrobnosti, abyste mohli začít sebevědomě.
## Předpoklady
Než se ponoříte, ujistěte se, že máte vše, co potřebujete, abyste spolu s tímto tutoriálem dodrželi.
1.  Aspose.Cells for .NET: Ujistěte se, že máte nainstalovaný Aspose.Cells for .NET. Můžete[stáhněte si knihovnu zde](https://releases.aspose.com/cells/net/) nebo jej nainstalujte přes NuGet ve svém .NET projektu.
2. .NET Environment: Kompatibilní vývojové prostředí .NET (např. Visual Studio).
3.  Nastavení licence: Pro plnou funkčnost Aspose.Cells použijte licenci. Můžete[požádat o bezplatnou dočasnou licenci](https://purchase.aspose.com/temporary-license/) pro účely hodnocení.
Začněte s bezplatnou zkušební verzí Aspose.Cells, pokud ji hodnotíte poprvé.
## Importujte balíčky
Než se pustíme do kódu, budete muset do svého projektu importovat jmenný prostor Aspose.Cells, abyste získali přístup ke všem potřebným třídám a metodám.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Pojďme si tento proces rozdělit do jednoduchých kroků. Zde budeme mít přístup k různým velikostem papíru, použijeme je na pracovní list a vytiskneme rozměry pro každý z nich.
## Krok 1: Vytvořte instanci sešitu
 Prvním krokem je vytvoření instance souboru`Workbook` třída. Tento objekt bude fungovat jako náš hlavní sešit obsahující listy, se kterými můžeme manipulovat.
```csharp
Workbook book = new Workbook();
```
 Myslete na to`Workbook` jako hlavní kontejner pro váš soubor Excel. Potřebujeme ho pro přístup a ovládání jednotlivých pracovních listů.
## Krok 2: Otevřete první list
 Dále se dostaneme k prvnímu listu v sešitu. Ve výchozím nastavení je nový sešit dodáván s jedním listem, takže na něj můžeme přímo odkazovat pomocí indexu`0`.
```csharp
Worksheet sheet = book.Worksheets[0];
```
 The`Worksheets` sběr v`Workbook` nám umožňuje přistupovat ke každému listu podle indexu. Zde vezmeme první list a začneme nastavovat rozměry stránky.
## Krok 3: Nastavte Paper Size na A2 a Display Dimensions
Nyní, když máme přístup k našemu listu, nastavíme jeho velikost papíru na A2. Nastavení velikosti papíru je užitečné pro formátování stránky před tiskem nebo exportem. Jakmile nastavíme velikost papíru, vytiskneme rozměry stránky v palcích.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
 Zde změníme`PaperSize` majetek do`PaperA2` . Po nastavení velikosti,`PageSetup.PaperWidth` a`PageSetup.PaperHeight` načíst šířku a výšku listu v palcích. Získáme tak rychlý přehled o rozměrech stránky.
## Krok 4: Nastavte Paper Size na A3 a Display Dimensions
Podle stejných kroků jako výše upravíme rozměry stránky na velikost A3. Tato změna je užitečná pro mírně větší výtisky nebo pro umístění více obsahu na jednu stránku.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Formát A3 je dvojnásobný oproti formátu A4, takže je dobrou volbou pro velké tabulky nebo podrobné tabulky. Změna velikosti papíru pomáhá odpovídajícím způsobem přizpůsobit rozvržení listu.
## Krok 5: Nastavte Paper Size na A4 a Display Dimensions
Nyní nastavíme velikost papíru na A4. Toto je nejčastěji používaná velikost stránky pro tisk dokumentů. Aktualizované rozměry zobrazíme později.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Pokud je vaším cílem standardní formát dokumentu, je obvykle nejvhodnější formát A4. Znalost rozměrů může pomoci při úpravě rozvržení obsahu, abyste se vyhnuli problémům s tiskem.
## Krok 6: Nastavte Paper Size na Letter a Display Dimensions
Nakonec nastavíme velikost papíru na formát Letter, který se běžně používá v Severní Americe. Ještě naposledy vytiskneme rozměry.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Velikost Letter je široce používána pro dokumenty v Severní Americe, takže nastavení této velikosti pomáhá při spolupráci s týmy nebo klienty, kteří tam sídlí.
## Závěr
tomto tutoriálu jsme si prošli, jak nastavit a načíst rozměry stránky pro různé velikosti papíru pomocí Aspose.Cells pro .NET. Nakonfigurováním velikostí stránek, jako jsou A2, A3, A4 a Letter, můžete formátovat listy aplikace Excel tak, aby vyhovovaly specifickým potřebám tisku a rozvržení. Tato kontrola nad rozměry stránky je zvláště cenná pro profesionální vytváření sestav a prezentaci, protože zajišťuje, že se váš obsah dokonale vejde na každou velikost stránky.
## FAQ
### Jak mohu změnit orientaci stránky v Aspose.Cells?  
 Orientaci můžete změnit pomocí`PageSetup.Orientation` vlastnost, nastavte ji na buď`PageOrientationType.Portrait` nebo`PageOrientationType.Landscape`.
### Mohu nastavit vlastní rozměry stránky v Aspose.Cells?  
 Ano, můžete nastavit vlastní rozměry stránky úpravou okrajů a možností změny velikosti pod`PageSetup` pro větší kontrolu.
### Jaká je výchozí velikost papíru v Aspose.Cells?  
Výchozí velikost papíru je obvykle A4. To však může záviset na regionálním nastavení a lze jej upravit podle potřeby.
### Je možné zobrazit náhled rozvržení stránky v Aspose.Cells?  
Zatímco Aspose.Cells nenabízí grafický náhled, můžete programově nastavit rozvržení a používat náhledy tisku v Excelu.
### Jak nainstaluji Aspose.Cells pro .NET?  
 Aspose.Cells můžete nainstalovat pomocí NuGet Package Manager ve Visual Studiu nebo si stáhnout DLL z[Stránka ke stažení Aspose.Cells](https://releases.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
