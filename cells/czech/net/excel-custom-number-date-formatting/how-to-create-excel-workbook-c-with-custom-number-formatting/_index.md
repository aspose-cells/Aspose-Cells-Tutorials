---
category: general
date: 2026-10-01
description: Naučte se, jak v C# vytvořit sešit Excel, použít vlastní formát čísel,
  nastavit desetinná místa buňky a uložit sešit jako XLSX v kompletním krok‑za‑krokem
  průvodci.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- apply custom number format
- how to format numbers excel
- set cell decimal places
- save workbook as xlsx
language: cs
lastmod: 2026-10-01
og_description: Vytvořte Excel sešit v C# s vlastním číselným formátem, nastavte počet
  desetinných míst buňky a uložte sešit jako XLSX. Postupujte podle tohoto kompletního
  průvodce pro přesný číselný výstup.
og_image_alt: Screenshot of an Excel sheet showing numbers rounded to four significant
  digits
og_title: Vytvořte Excel sešit v C# – vlastní formát čísel a export do XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  headline: How to create Excel workbook C# with custom number formatting
  type: TechArticle
- description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  name: How to create Excel workbook C# with custom number formatting
  steps:
  - name: Run the program (`dotnet run`).
    text: Run the program (`dotnet run`).
  - name: Open `SigDigits.xlsx`.
    text: Open `SigDigits.xlsx`.
  - name: Confirm that **A1** reads `123.5`.
    text: Confirm that **A1** reads `123.5`.
  - name: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
    text: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Jak vytvořit Excel sešit v C# s vlastním formátováním čísel
url: /cs/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-c-with-custom-number-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vytvořit Excel sešit C# s vlastním formátováním čísel

Pokud potřebujete **vytvořit Excel sešit C#**, který zobrazuje čísla přesně tak, jak chcete, tento průvodce vám ukáže, jak to provést v několika jasných krocích. Naučíte se použít vlastní formát čísel, nastavit počet desetinných míst buňky a nakonec **uložit sešit jako xlsx** pro další využití.

Práce s číselnými daty často vyžaduje vyvážení přesnosti a čitelnosti. Na konci tohoto tutoriálu budete mít znovupoužitelný vzor, který omezuje zobrazované číslice na konkrétní počet významných číslic a zároveň zachovává původní hodnotu v souboru. Nepotřebujete žádné externí skripty – stačí C# a knihovna Aspose.Cells.

## Prerequisites

* .NET 6.0 SDK nebo novější nainstalováno  
* Visual Studio 2022 (nebo jakékoli C# IDE)  
* Balíček **Aspose.Cells for .NET** NuGet (`Install-Package Aspose.Cells`) – tato knihovna poskytuje třídy `Workbook`, `Worksheet` a `ExportTableOptions` používané v příkladech.  

Tyto požadavky jsou minimální; stejný kód funguje v .NET Core, .NET Framework i v Azure Functions.

## Krok 1: Vytvořit Excel sešit C# – inicializace souboru

První operací je vytvořit novou instanci objektu `Workbook`. Tento objekt představuje celý Excel soubor v paměti a automaticky obsahuje výchozí list.

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // creates an empty .xlsx container
            Worksheet sheet = workbook.Worksheets[0];         // reference to the default sheet
```

**Proč je to důležité:**  
Vytvoření sešitu předem vám poskytne čisté plátno. Výchozí list (`Worksheets[0]`) je připravený pro zadání dat, takže nemusíte přidávat nový list, pokud váš scénář nevyžaduje více záložek.

## Krok 2: Zapsat číselnou hodnotu do buňky

Nyní vložte ukázkové číslo do buňky **A1**. Hodnota, kterou používáme (`123.456789`), obsahuje více desetinných míst, než nakonec chceme zobrazit, což nám umožní později demonstrovat zaokrouhlování.

```csharp
            // Step 2: Write a numeric value to cell A1
            sheet.Cells[0, 0].PutValue(123.456789); // row 0, column 0 = A1
```

**Tip:** `PutValue` automaticky detekuje datový typ, takže nemusíte číslo převádět na řetězec.

## Krok 3: Použít vlastní formát čísel – omezit viditelné desetinné místo

Abychom kontrolovali, jak Excel číslo zobrazuje, vytvoříme `Style` s **custom number format**. Vzor `"0.######"` říká Excelu, aby zobrazil až šest desetinných míst, ale vynechal koncové nuly.

```csharp
            // Step 3: Define a custom number format (up to 6 decimal places) and apply it
            Style customStyle = workbook.CreateStyle();
            customStyle.Custom = "0.######";               // up to 6 decimals, no trailing zeros
            sheet.Cells[0, 0].SetStyle(customStyle);
```

**Jak to funguje:**  
Formátovací řetězec následuje syntaxi vlastního formátu Excelu. `0` vynutí číslici, zatímco `#` zobrazí číslici jen pokud je významná. Kombinací získáte flexibilní zobrazení, které stále respektuje původní přesnost.

## Krok 4: Nastavit počet desetinných míst buňky – pomocí ExportTableOptions

Pokud potřebujete **set cell decimal places** pro exportovaná data (např. při převodu na DataTable), Aspose.Cells vám umožní specifikovat počet **significant digits**. Tento krok zajistí, že exportovaný CSV nebo DataTable bude respektovat stejná pravidla zaokrouhlování, jaká jste použili v sešitu.

```csharp
            // Step 4: Configure export options to limit the output to 4 significant digits
            ExportTableOptions exportOptions = new ExportTableOptions();
            exportOptions.SignificantDigits = 4;           // round to 4 significant figures
```

**Proč použít `SignificantDigits`?**  
Na rozdíl od pevného počtu desetinných míst zachovávají významné číslice velikost čísla při omezení přesnosti, což analytikům často vyhovuje při sumarizaci dat.

## Krok 5: Exportovat data listu a **uložit sešit jako xlsx**

Nakonec exportujte data (pokud potřebujete DataTable) a uložte sešit na disk. Volání `ExportDataTable` respektuje `ExportTableOptions`, které jsme nakonfigurovali, a `workbook.Save` zapíše standardní soubor XLSX.

```csharp
            // Step 5: Export the worksheet data using the configured options and save the workbook
            sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
            workbook.Save("SigDigits.xlsx");               // saves to the application’s working folder
        }
    }
}
```

**Očekávaný výsledek:**  
Když otevřete *SigDigits.xlsx* v Excelu, buňka **A1** zobrazí `123.5`. Podkladová hodnota zůstane `123.456789`, ale zobrazené číslo respektuje pravidlo 4‑významných‑číslic. Pokud exportujete list do DataTable, hodnota v tabulce bude také zaokrouhlena na `123.5`.

---

## Použít vlastní formát čísel na další buňky

Pokud potřebujete formátovat rozsah místo jedné buňky, znovu použijte objekt `Style`:

```csharp
// Apply the same custom style to B2:C5
Range range = sheet.Cells.CreateRange("B2:C5");
range.ApplyStyle(customStyle, new StyleFlag { NumberFormat = true });
```

**Pro tip:** Znovupoužití objektu stylu snižuje paměťovou zátěž a zaručuje konzistentní formátování napříč listem.

## Jak formátovat čísla v Excelu pomocí C# – běžné varianty

| Scénář | Formátovací řetězec | Výsledek |
|----------|---------------------|----------|
| Pevné dvě desetinná místa | `"0.00"` | `123.46` |
| Měna (US) | `"$#,##0.00"` | `$123.46` |
| Procenta s jedním desetinným místem | `"0.0%"` | `12,346.0%` |
| Vědecká notace | `"0.00E+00"` | `1.23E+02` |

Vyberte vzor, který odpovídá vašim požadavkům na reportování. Všechny vzory jsou kompatibilní s vlastností `Style.Custom`, kterou jsme demonstrovali dříve.

## Dynamicky nastavit počet desetinných míst buňky na základě vstupu uživatele

Někdy není požadovaná přesnost známá při kompilaci. Formátovací řetězec můžete vytvořit za běhu:

```csharp
int decimals = 3; // could come from a UI textbox
string format = "0." + new string('#', decimals);
customStyle.Custom = format;
sheet.Cells["A2"].PutValue(987.654321);
sheet.Cells["A2"].SetStyle(customStyle);
```

**Hraniční případ:** Pokud je `decimals` nula, formát se změní na `"0"` (zobrazení celých čísel). Vždy validujte vstup uživatele, aby nedošlo k poškození formátovacího řetězce.

## Uložit sešit jako XLSX – osvědčené postupy

* **Používejte absolutní cesty** při zápisu do známého adresáře (`Path.Combine(Environment.CurrentDirectory, "output.xlsx")`).  
* **Uvolněte** (`Dispose`) objekt `Workbook`, pokud jej obalíte do `using` bloku, aby se rychle uvolnily neřízené prostředky:

```csharp
using (Workbook wb = new Workbook())
{
    // ...populate workbook...
    wb.Save(Path.Combine(@"C:\Exports", "Report.xlsx"));
}
```

* **Kompatibilita verzí:** Aspose.Cells zapisuje soubory kompatibilní s Excel 2010‑2023, takže koncoví uživatelé nebudou mít problémy s formátem.

---

## Kompletní funkční příklad

Níže je celý program, který můžete zkopírovat, vložit a okamžitě spustit. Obsahuje všechny potřebné `using` direktivy, komentáře a ošetření chyb.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Create workbook and get the first worksheet
                Workbook workbook = new Workbook();
                Worksheet sheet = workbook.Worksheets[0];

                // 2️⃣ Write a high‑precision number to A1
                sheet.Cells[0, 0].PutValue(123.456789);

                // 3️⃣ Apply a custom number format (up to 6 decimals)
                Style customStyle = workbook.CreateStyle();
                customStyle.Custom = "0.######";
                sheet.Cells[0, 0].SetStyle(customStyle);

                // 4️⃣ Configure export options for 4 significant digits
                ExportTableOptions exportOptions = new ExportTableOptions
                {
                    SignificantDigits = 4
                };

                // 5️⃣ Export data (optional) and save the workbook as XLSX
                sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
                string outputPath = Path.Combine(Environment.CurrentDirectory, "SigDigits.xlsx");
                workbook.Save(outputPath);

                Console.WriteLine($"Workbook saved successfully at: {outputPath}");
                Console.WriteLine("Cell A1 displays: " + sheet.Cells["A1"].StringValue);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error creating workbook: {ex.Message}");
            }
        }
    }
}
```

**Kroky ověření**

1. Spusťte program (`dotnet run`).  
2. Otevřete `SigDigits.xlsx`.  
3. Potvrďte, že **A1** zobrazuje `123.5`.  
4. Pokud otevřete XML souboru (`.xlsx` je zip archiv), uvidíte vlastní formát `"0.######"` uložený v atributu `s` elementu `<c>`.

## Závěr

V tomto tutoriálu jste se naučili, jak **vytvořit Excel sešit C#**, **použít vlastní formát čísel**, **nastavit počet desetinných míst buňky** a **uložit sešit jako xlsx** pomocí Aspose.Cells. Řešení ukazuje jak vizuální formátování uvnitř Excelu, tak zaokrouhlování při exportu dat prostřednictvím `ExportTableOptions`.  

Odtud můžete:

* Rozšířit přístup na celé rozsahy nebo tabulky.  
* Kombinovat více stylů (písma, okraje) pomocí `StyleFlag`.  
* Automatizovat generování reportů pomocí smyčky přes zdroje dat a aplikování stejné logiky formátování.  

Neváhejte experimentovat s různými formátovacími řetězci, počty desetinných míst nebo možnostmi exportu, aby vyhovovaly vašim konkrétním potřebám reportování. Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, která vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Vytvořit Excel sešit C# – Použít formát měny a importovat DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Vytvořit Excel sešit C# – Průvodce krok za krokem s podmíněným formátováním](/cells/english/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/)
- [Vytvořit Excel sešit C# – Přidat komentář a uložit jako XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}