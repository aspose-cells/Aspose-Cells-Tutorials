---
category: general
date: 2026-04-07
description: Zapište datum a čas do Excelu pomocí C#. Naučte se, jak vložit datum
  do listu, pracovat s hodnotou data v buňce Excelu a převést datum japonského kalendáře
  během několika kroků.
draft: false
keywords:
- write datetime to excel
- excel cell date value
- insert date into worksheet
- convert japanese calendar date
language: cs
og_description: Rychle zapisujte datum a čas do Excelu. Tento návod ukazuje, jak vložit
  datum do listu, spravovat hodnotu data v buňce Excelu a převést datum japonského
  kalendáře pomocí C#.
og_title: Zapsat datum a čas do Excelu – krok za krokem C# tutoriál
tags:
- C#
- Excel automation
- Aspose.Cells
title: Zapsat datum a čas do Excelu – Kompletní průvodce pro vývojáře C#
url: /cs/net/excel-custom-number-date-formatting/write-datetime-to-excel-complete-guide-for-c-developers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zapisování data a času do Excelu – Kompletní průvodce pro vývojáře C#

Už jste někdy potřebovali **zapsat datum a čas do Excelu**, ale nebyli jste si jisti, která volání API skutečně uloží správné datum v Excelu? Nejste v tom sami. V mnoha firemních nástrojích musíme vložit C# `DateTime` do tabulky a výsledek by se měl chovat jako skutečné datum v Excelu – řaditelný, filtrovatelný a připravený pro kontingenční tabulky.  

V tomto tutoriálu projdeme přesné kroky, jak *vložit datum do listu* pomocí Aspose.Cells, vysvětlíme, proč je nastavení kultury důležité, a dokonce ukážeme, jak **převést datum z japonského kalendáře** na běžný `DateTime` před jeho zápisem. Na konci budete mít samostatný úryvek, který můžete zkopírovat a vložit do libovolného .NET projektu.

## Co budete potřebovat

- **.NET 6+** (nebo jakákoli recentní verze .NET; kód funguje i na .NET Frameworku)  
- **Aspose.Cells for .NET** – NuGet balíček, který umožňuje manipulovat se soubory Excel bez nainstalovaného Office.  
- Základní znalost C# `DateTime` a kultur.  

Žádné další knihovny, žádné COM interop a žádná instalace Excelu nejsou potřeba. Pokud už máte instanci listu (`ws`), můžete rovnou pokračovat.

## Krok 1: Nastavení japonské kultury (Převod data z japonského kalendáře)

Když obdržíte datum jako `"R02/05/01"` (Reiwa 2, 1. května), musíte .NETu říct, jak má interpretovat symboly éry. Japonský kalendář není výchozím gregoriánským kalendářem, takže vytvoříme `CultureInfo`, který nahradí jeho kalendář za `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;
using Aspose.Cells;   // Make sure Aspose.Cells is referenced

// Assume you already have a worksheet instance named "ws"
Worksheet ws = /* your worksheet instance */;

// 1️⃣ Configure a Japanese culture that uses the Japanese calendar
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

**Proč je to důležité:**  
Pokud řetězec parsujete pomocí výchozí kultury, .NET vyhodí výjimku formátu, protože nedokáže přiřadit `R` (éra Reiwa) k roku. Nahrazením kalendáře za `JapaneseCalendar` parser rozumí symbolům éry a přeloží je na správný gregoriánský rok.

## Krok 2: Parsování řetězce založeného na éře do `DateTime`

Nyní, když je kultura připravena, můžeme bezpečně zavolat `DateTime.ParseExact`. Formátovací řetězec `"ggyy/MM/dd"` říká parseru:

- `gg` – designátor éry (např. `R` pro Reiwa)  
- `yy` – dvouciferný rok v rámci éry  
- `MM/dd` – měsíc a den.

```csharp
// 2️⃣ Parse a date string in the Japanese era format (ggyy/MM/dd)
string japaneseDate = "R02/05/01";          // Reiwa 2, May 1st
DateTime parsedDate = DateTime.ParseExact(
    japaneseDate,
    "ggyy/MM/dd",
    japaneseCulture,
    DateTimeStyles.None
);
```

**Tip:** Pokud můžete obdržet data v jiných formátech (např. `"Heisei 30/12/31"`), obalte parsování do `try/catch` a použijte záložní `DateTime.TryParseExact`. Tím zabráníte pádu celého importního úkolu kvůli jedné špatné řádce.

## Krok 3: Zapsání `DateTime` do buňky Excel (Hodnota data v buňce Excel)

Aspose.Cells zachází s .NET `DateTime` jako s nativním datem Excelu, když použijete `PutValue`. Knihovna automaticky převádí tiky na sériové číslo Excelu (počet dní od 1900‑01‑00). To znamená, že buňka zobrazí správnou **excel cell date value** a později ji můžete formátovat pomocí vestavěných stylů data v Excelu.

```csharp
// 3️⃣ Write the resulting DateTime value into cell C1 of the worksheet
Cell targetCell = ws.Cells["C1"];
targetCell.PutValue(parsedDate);

// Optional: apply a standard date format so users see "yyyy-MM-dd"
targetCell.Style.Number = 14;   // built‑in Excel format ID for "m/d/yy"
```

**Co uvidíte v Excelu:**  
Buňka C1 nyní obsahuje sériové číslo `44796`, které Excel vykreslí jako `2020‑05‑01` (nebo jakýkoli formát, který použijete). Podkladová hodnota je skutečné datum, ne řetězec, takže řazení funguje podle očekávání.

## Krok 4: Uložení sešitu (Závěr)

Pokud jste ještě neuložili sešit, udělejte to nyní. Tento krok není striktně o zápisu data a času, ale dokončuje celý pracovní postup.

```csharp
// Save the workbook to a file (or a MemoryStream if you need it in‑memory)
Workbook workbook = ws.Workbook;   // get the parent workbook
workbook.Save("Output.xlsx", SaveFormat.Xlsx);
```

A to je vše—čtyři stručné kroky a úspěšně jste **zapsali datum a čas do Excelu**, přičemž jste během toho zpracovali japonskou era datum.

---

![příklad zápisu data a času do excelu](/images/write-datetime-to-excel.png "Snímek obrazovky ukazující C# projekt zapisující DateTime do buňky Excel C1")

*Obrázek výše ilustruje finální soubor Excel s datem správně zobrazeným v buňce C1.*

## Časté otázky a okrajové případy

### Co když proměnná worksheet ještě není připravena?

Můžete vytvořit nový sešit za běhu:

```csharp
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];   // default first sheet
```

### Jak zachovat původní řetězec japonské éry v listu?

Pokud potřebujete jak původní řetězec, tak parsované datum, zapište je do sousedních buněk:

```csharp
ws.Cells["B1"].PutValue(japaneseDate);   // original text
ws.Cells["C1"].PutValue(parsedDate);     // parsed DateTime
```

### Funguje to se staršími verzemi .NET?

Ano. `JapaneseCalendar` existuje od .NET 2.0 a Aspose.Cells podporuje .NET Framework 4.5+. Jen se ujistěte, že odkazujete na správný assembly.

### Co s časovými pásmy?

`DateTime.ParseExact` vrací **Kind** `Unspecified`. Pokud jsou vaše zdrojová data v UTC, nejprve je převedete:

```csharp
DateTime utcDate = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
DateTime localDate = utcDate.ToLocalTime();
targetCell.PutValue(localDate);
```

### Můžu nastavit vlastní formát data (např. “yyyy年MM月dd日”)?

Určitě. Použijte vlastnost `Style.Custom`:

```csharp
targetCell.Style.Custom = "yyyy\"年\"mm\"月\"dd\"日\"";
```

Excel nyní zobrazí `2020年05月01日`, přičemž stále ukládá skutečnou hodnotu data.

## Shrnutí

Probrali jsme vše, co potřebujete k **zapsání data a času do Excelu** z C#:

1. **Nastavte** japonskou kulturu s `JapaneseCalendar` pro **převod data z japonského kalendáře**.  
2. **Parsujte** řetězec založený na éře pomocí `DateTime.ParseExact`.  
3. **Vložte** výsledný `DateTime` do buňky, čímž zajistíte správnou **excel cell date value**.  
4. **Uložte** sešit, aby data přetrvala.

S těmito čtyřmi kroky můžete bezpečně **vložit datum do listu** bez ohledu na formát zdroje. Kód je plně spustitelný, vyžaduje jen Aspose.Cells a funguje na jakémkoli moderním .NET runtime.

## Co dál?

- **Hromadný import:** Procházet řádky v CSV, parsovat každé japonské datum a zapisovat je do po sobě jdoucích buněk.  
- **Styling:** Použít podmíněné formátování pro zvýraznění prošlých termínů.  
- **Výkon:** Použít `WorkbookDesigner` nebo kešování `CellStyle` při práci s tisíci řádky.  

Klidně experimentujte – zaměňte japonskou éru za gregoriánský kalendář, změňte cílovou buňku nebo výstup do jiného formátu souboru (CSV, ODS). Hlavní myšlenka zůstává stejná: parsovat, převést a **zapsat datum a čas do Excelu** s jistotou.

Šťastné programování a ať se vaše tabulky vždy řadí správně!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}