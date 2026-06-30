---
category: general
date: 2026-06-30
description: Szybko utwórz liniowy sparkline w Excelu przy użyciu C#. Dowiedz się,
  jak dodać sparkline, utworzyć skoroszyt Excel w C# i dodać sparkline do komórki
  w kilku krokach.
draft: false
keywords:
- create line sparkline
- how to add sparkline
- add line sparkline
- create excel workbook c#
- add sparkline to cell
language: pl
og_description: Utwórz liniowy sparkline w Excelu przy użyciu C#. Ten samouczek pokazuje,
  jak dodać sparkline, utworzyć skoroszyt Excel w C# oraz osadzić sparkline w komórce.
og_title: Tworzenie wykresu liniowego typu sparkline w Excelu przy użyciu C# – Przewodnik
  krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create line sparkline in Excel with C# quickly. Learn how to add sparkline,
    create Excel workbook C#, and add sparkline to cell in a few steps.
  headline: Create line sparkline in Excel with C# – Complete Programming Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Utwórz wykres liniowy sparkline w Excelu przy użyciu C# – Kompletny przewodnik
  programistyczny
url: /pl/net/charts/create-line-sparkline-in-excel-with-c-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie wykresu liniowego sparkline w Excelu przy użyciu C# – Kompletny przewodnik programistyczny

Zastanawiałeś się kiedyś, jak **utworzyć wykres liniowy sparkline** w pliku Excel przy pomocy C#? Nie jesteś jedyny – programiści często pytają: „jak dodać sparkline do raportu bez ręcznego otwierania Excela?”. Dobra wiadomość: wystarczy kilka linii kodu, aby wygenerować elegancki wykres liniowy sparkline bezpośrednio w skoroszycie, bez interfejsu użytkownika.

W tym tutorialu przejdziemy przez wszystko, co musisz wiedzieć: od podstaw **create Excel workbook C#**, przez wypełnianie danymi, po dokładne kroki **add line sparkline** i **add sparkline to cell**. Na końcu będziesz mieć gotowy plik *.xlsx*, który wizualizuje miesięczne trendy sprzedaży w jednym spojrzeniu. Bez zbędnych wstępów, tylko praktyczne, gotowe do uruchomienia rozwiązanie.

---

## Co zbudujesz

- Nowy skoroszyt Excel o nazwie *KPI_Sparklines.xlsx*  
- Arkusz o nazwie **KPI** zawierający przykładowe liczby sprzedaży  
- **Wykres liniowy sparkline** umieszczony w komórce **D2**, odwołujący się do zakresu danych **B2:B13**  
- Podstawowe formatowanie (kolor, grubość linii), aby sparkline wyróżniał się  

Wymagania wstępne? Tylko .NET SDK (3.1+ lub .NET 6) oraz darmowa biblioteka Aspose.Cells for .NET (dostępna przez NuGet). Jeśli nigdy nie używałeś Aspose.Cells, wyobraź sobie potężny silnik Excel, którego możesz wywoływać z kodu – bez COM interop, bez konieczności instalacji Excela.

---

![Utwórz wykres liniowy sparkline w Excelu przy użyciu C#](https://example.com/images/create-line-sparkline.png "Utwórz wykres liniowy sparkline w Excelu przy użyciu C#")

*Tekst alternatywny obrazu: utwórz wykres liniowy sparkline w Excelu przy użyciu przykładu kodu C#*

---

## Krok 1: **Create Excel workbook C#** – Utwórz plik i arkusz

Na początek potrzebujemy obiektu workbook oraz arkusza, w którym będą przechowywane dane. To podstawa każdej automatyzacji Excela, niezależnie od tego, czy później **add line sparkline**, czy zapiszesz formuły.

```csharp
using Aspose.Cells;
using System.Drawing;

// Initialize a new workbook
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0) and give it a meaningful name
Worksheet worksheet = workbook.Worksheets[0];
worksheet.Name = "KPI";   // “KPI” will hold our key performance indicators
```

> **Dlaczego to ważne:** Klasa `Workbook` reprezentuje cały plik, natomiast `Worksheet` jest płótnem dla wierszy, kolumn i w końcu naszego sparkline. Nadanie nazwy arkuszowi od razu utrzymuje plik w porządku i zapewnia samodokumentację.

---

## Krok 2: Wypełnij dane – Źródłowy zakres dla sparkline

Sparkline potrzebuje danych do wykreślenia. Zasymulujmy 12 miesięcy wyników sprzedaży. Można je pobrać z bazy danych, ale dla przejrzystości wygenerujemy je w locie.

```csharp
// Fill column B (index 1) with monthly sales numbers
for (int month = 0; month < 12; month++)
{
    // Example pattern: start at 5,000 and increase by 750 each month
    worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
}
```

> **Wskazówka:** `PutValue` automatycznie wykrywa typ danych, więc nie musisz rzutować na `double` czy `int`. Jeśli kiedykolwiek będziesz potrzebował sformatować komórki (waluta, separator tysięcy), możesz później zastosować obiekt `Style`.

---

## Krok 3: **Create line sparkline** – Dodaj sparkline do konkretnej komórki

Teraz najważniejszy element: **wykres liniowy sparkline**. Aspose.Cells grupuje sparkline, więc najpierw tworzymy `SparklineGroup` typu `Line`, a potem określamy, gdzie ma się pojawić wizualizacja.

```csharp
// Add a new SparklineGroup of type Line
int groupIndex = worksheet.SparklineGroups.Add(SparklineType.Line);
SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIndex];

// Add a sparkline that lives in D2 (row 1, column 3) and reads data from B2:B13
// Parameters: firstRow, firstColumn, lastRow, lastColumn, firstDataRow, lastDataRow
sparklineGroup.Add(1, 3, 1, 3, 1, 12);   // D2 ↔ B2:B13
```

> **Jak to działa:**  
> - `firstRow/firstColumn` i `lastRow/lastColumn` definiują *komórkę docelową* (gdzie pojawi się sparkline).  
> - `firstDataRow/lastDataRow` wskazują na zakres źródłowy.  
> Ponieważ używamy **line sparkline**, wizualizacja będzie prostą, cienką linią odzwierciedlającą trend liczb.

### Opcjonalnie: **How to add sparkline** z niestandardowym stylowaniem

Jeśli chcesz, aby sparkline się wyróżniał, dostosuj kilka właściwości:

```csharp
sparklineGroup.LineWeight = 1.0;               // Thickness of the line
sparklineGroup.SeriesColor = Color.DarkBlue;  // Color of the sparkline line
sparklineGroup.ShowMarkers = true;             // Show data markers (optional)
sparklineGroup.MarkerColor = Color.OrangeRed;  // Marker color
```

> **Dlaczego stylizować?** Ciemnoniebieska linia na białym tle jest przyjemna dla oka, a znaczniki dają szybki podgląd poszczególnych punktów danych – przydatne podczas prezentacji.

---

## Krok 4: Zapisz skoroszyt – Zweryfikuj wynik

Po dodaniu sparkline wystarczy zapisać plik na dysku. Wybierz folder, do którego masz prawo zapisu; w przykładzie użyto ścieżki zastępczej, którą powinieneś zamienić na własną.

```csharp
// Save the workbook as an .xlsx file
string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
workbook.Save(outputPath);
```

> **Weryfikacja:** Otwórz wygenerowany plik w Excelu (lub w dowolnym podglądzie obsługującym .xlsx). Powinieneś zobaczyć **wykres liniowy sparkline** w komórce **D2**, odzwierciedlający rosnące liczby sprzedaży w kolumnie **B**. Najazd kursorem na sparkline wyświetli podpowiedź z wartościami źródłowymi.

---

## Krok 5: Typowe pułapki przy **add sparkline to cell**

Nawet prosty przykład może sprawić trudności początkującym. Oto kilka rzeczy, na które warto zwrócić uwagę:

| Problem | Dlaczego się pojawia | Rozwiązanie |
|-------|----------------|-----|
| Nieprawidłowe współrzędne komórki | Cel sparkline używa indeksu kolumny zerowego, ale indeksu wiersza jedynkowego. | Pamiętaj, że `Cells[row, column]` ma zerowy indeks zarówno dla wiersza, jak i kolumny. W `SparklineGroup.Add` wiersze i kolumny są **jedynkowe**. |
| Brak wyświetlanych danych | Zakres źródłowy jest pusty lub zawiera wartości nienumeryczne. | Upewnij się, że zakres (np. `B2:B13`) zawiera liczby. Użyj `PutValue` z typami numerycznymi. |
| Sparkline znika po zapisaniu | Niekompatybilna wersja biblioteki lub brak licencji. | Użyj najnowszej wersji pakietu Aspose.Cells i podaj ważną licencję, jeśli przekraczasz limity wersji ewaluacyjnej. |
| Styl nie zastosowano | Zmiany stylu wykonano przed dodaniem sparkline. | Ustaw styl **po** utworzeniu grupy, tak jak pokazano powyżej. |

---

## Pełny kod źródłowy – Kopiuj i wklej

Poniżej znajduje się kompletny, gotowy do uruchomienia program. Wklej go do nowego projektu konsolowego, dodaj pakiet NuGet Aspose.Cells i naciśnij **F5**.

```csharp
using Aspose.Cells;
using System.Drawing;

namespace SparklineDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create Excel workbook C#
            // -------------------------------------------------
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "KPI";

            // -------------------------------------------------
            // Step 2: Populate monthly sales data (B2:B13)
            // -------------------------------------------------
            for (int month = 0; month < 12; month++)
            {
                worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
            }

            // -------------------------------------------------
            // Step 3: Create line sparkline and add it to D2
            // -------------------------------------------------
            int groupIdx = worksheet.SparklineGroups.Add(SparklineType.Line);
            SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIdx];
            sparklineGroup.Add(1, 3, 1, 3, 1, 12); // D2 ↔ B2:B13

            // -------------------------------------------------
            // Step 4: Optional formatting (how to add sparkline with style)
            // -------------------------------------------------
            sparklineGroup.LineWeight = 1.0;
            sparklineGroup.SeriesColor = Color.DarkBlue;
            sparklineGroup.ShowMarkers = true;
            sparklineGroup.MarkerColor = Color.OrangeRed;

            // -------------------------------------------------
            // Step 5: Save the workbook
            // -------------------------------------------------
            string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
            workbook.Save(outputPath);

            System.Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Oczekiwany rezultat:** Po otwarciu *KPI_Sparklines.xlsx* kolumna **B** zawiera dwanaście liczb (5 000 → 13 250), a komórka **D2** posiada płynną, ciemnoniebieską linię sparkline, która stopniowo rośnie. Jeśli włączyłeś `ShowMarkers`, znaczniki pojawią się jako małe pomarańczowo‑czerwone kropki.

---

## Co dalej? Rozwijanie umiejętności pracy ze sparkline

Po opanowaniu **create line sparkline** w Aspose.Cells możesz zgłębiać następujące tematy:

- **Add column sparkline** – idealny do prezentacji danych skumulowanych.  
- **Create multi‑sparkline groups** w tym samym arkuszu, aby porównać je obok siebie.  
- **Export to PDF** zachowując sparkline (Aspose.Cells obsługuje konwersję do PDF).  
- **Dynamic data sources** – pobieraj rzeczywiste dane sprzedaży z bazy SQL zamiast wartości stałych.  

Wszystkie te zagadnienia opierają się na tych samych podstawowych koncepcjach: **create Excel workbook C#**, wypełnianie danymi oraz **add sparkline to cell** w wybranym stylu.

---

### TL;DR

Pokazaliśmy, jak **create line sparkline** w skoroszycie Excel przy użyciu C#. Kroki – *utwórz workbook, wypełnij danymi, dodaj sparkline, sformatuj go i zapisz* – są zawarte w jednym, samodzielnym programie. Śmiało modyfikuj kolory, grubość linii lub zakres źródłowy, aby dopasować je do własnych potrzeb raportowych.

Masz własny pomysł, którym chcesz się podzielić? zostaw komentarz poniżej i powodzenia w kodowaniu!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz szczegółowe wyjaśnienia, pomagające opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Excel Automation: Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Excel Automation Create Workbook Add Listbox Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Excel Automation Create Workbook Add Listbox Aspose Cells](/cells/french/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}