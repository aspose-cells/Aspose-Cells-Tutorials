---
category: general
date: 2026-02-28
description: Szybko usuwaj wiersze w tabeli Excel w C#. Dowiedz się, jak dodać nazwany
  zakres w Excelu, uzyskać dostęp do arkusza po nazwie i uniknąć błędów duplikatów
  nazw.
draft: false
keywords:
- delete rows excel table
- add named range excel
- access worksheet by name
- how to add defined name
- named range on another sheet
language: pl
og_description: Usuwanie wierszy w tabeli Excel przy użyciu C#. Ten samouczek pokazuje
  również, jak dodać nazwany zakres w Excelu i uzyskać dostęp do arkusza po nazwie.
og_title: Usuwanie wierszy w tabeli Excel przy użyciu C# – Kompletny przewodnik
tags:
- C#
- Excel
- DevExpress Spreadsheet
title: Usuwanie wierszy w tabeli Excel przy użyciu C# – Przewodnik krok po kroku
url: /pl/net/row-and-column-management/delete-rows-excel-table-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Usuwanie wierszy z tabeli Excel przy użyciu C# – Kompletny samouczek programistyczny

Czy kiedykolwiek potrzebowałeś **delete rows excel table** z skoroszytu, ale nie byłeś pewien, którego wywołania API użyć? Nie jesteś jedyny — większość programistów napotyka tę samą przeszkodę, gdy po raz pierwszy próbuje programowo zmniejszyć tabelę.

W tym przewodniku przeprowadzimy Cię przez pełny, działający przykład, który nie tylko usuwa wiersze z tabeli Excel, ale także pokazuje **how to add defined name** (znany jako *named range*), jak **access worksheet by name**, oraz dlaczego dodanie zduplikowanej nazwy na innym arkuszu powoduje `InvalidOperationException`.

Do końca artykułu będziesz w stanie:

* Pobrać arkusz przy użyciu jego nazwy zakładki.  
* Bezpiecznie usunąć wiersze danych z pierwszej tabeli na tym arkuszu.  
* Utworzyć zakres nazwany wskazujący na konkretny adres.  
* Zrozumieć pułapki związane z duplikatami nazw w różnych arkuszach.

Nie potrzebujesz żadnej zewnętrznej dokumentacji — wszystko, co potrzebne, znajduje się tutaj.

---

## Czego będziesz potrzebować

* **DevExpress Spreadsheet** (lub dowolna biblioteka udostępniająca obiekty `Workbook`, `Worksheet`, `ListObject` i `Names`).  
* Projekt .NET targetujący **.NET 6** lub nowszy (kod kompiluje się również w .NET Framework 4.8).  
* Podstawowa znajomość C# — jeśli potrafisz napisać pętlę `foreach`, jesteś gotowy.

> **Pro tip:** Jeśli używasz darmowej edycji Community Edition DevExpress, API użyte poniżej są identyczne jak w wersji komercyjnej.

---

## Krok 1 – Dostęp do arkusza po nazwie

Pierwszą rzeczą, którą musisz zrobić, jest zlokalizowanie arkusza zawierającego tabelę, którą chcesz zmodyfikować.  
Większość programistów sięga po `Worksheets[0]` z przyzwyczajenia, ale to wiąże Twój kod z kolejnością arkuszy i psuje się, gdy ktoś zmieni nazwę zakładki.

```csharp
using DevExpress.Spreadsheet;

// Assume 'workbook' is an already‑loaded Workbook instance
Worksheet worksheet = workbook.Worksheets["Sheet1"];   // <-- access worksheet by name
```

*Dlaczego to ważne:* Używając **name** arkusza zamiast jego indeksu, unikasz przypadkowych modyfikacji niewłaściwego arkusza, gdy skoroszyt się zmienia.  

Jeśli podana nazwa nie istnieje, biblioteka rzuca `KeyNotFoundException`, który możesz przechwycić, aby wyświetlić przyjazny komunikat o błędzie.

---

## Krok 2 – Usuwanie wierszy z tabeli Excel (bezpieczny sposób)

Teraz, gdy masz właściwy arkusz, usuńmy wiersze danych z pierwszej tabeli.  
Częstym błędem jest wywołanie `DeleteRows(1, rowCount‑1)`. Od **DevExpress 22.2** ta przeciążona metoda jest **zabroniona** i rzuca `InvalidOperationException`. Biblioteka oczekuje, że usuniesz wiersze **w obrębie zakresu danych tabeli**, a nie wiersz nagłówka.

```csharp
// Grab the first table (ListObject) on the sheet
var table = worksheet.ListObjects[0];

// Calculate how many data rows we actually have (excluding the header)
int dataRowCount = table.DataRange.RowCount;

// Delete only the data rows – keep the header intact
if (dataRowCount > 0)
{
    // DeleteRows(startRow, rowCount) – startRow is zero‑based within the table
    table.DeleteRows(0, dataRowCount);
}
```

> **Co jeśli tabela jest pusta?** Warunek `if` zapobiega wywołaniu z `rowCount = 0`, co w przeciwnym razie spowodowałoby wyjątek.

### Przegląd wizualny  

![przykład usuwania wierszy z tabeli Excel w kodzie C#](image.png "Zrzut ekranu pokazujący usuwanie wierszy z tabeli Excel")  

---

## Krok 3 – Jak dodać zdefiniowaną nazwę (utworzyć zakres nazwany)

Po wyczyszczeniu tabeli możesz chcieć odwołać się później do konkretnego zakresu — np. do wykresu lub listy walidacji danych. Wtedy przydaje się **add named range excel**.

```csharp
// Define a name that points to A1:C5 on Sheet1
workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

// Verify that the name exists
Name definedName = workbook.Names["MyTable"];
Console.WriteLine($"Defined name '{definedName.Name}' points to {definedName.RefersTo}");
```

Metoda `Names.Add` przyjmuje dwa parametry: identyfikator oraz adres w stylu A1.  
Ponieważ wcześniej użyliśmy **access worksheet by name**, ciąg adresowy może bezpiecznie odwoływać się do dowolnego arkusza, nie martwiąc się o zmiany indeksów.

---

## Krok 4 – Zakres nazwany na innym arkuszu – unikanie błędów duplikatów nazw

Możesz pomyśleć, że możesz ponownie użyć tego samego identyfikatora na innym arkuszu, tak:

```csharp
// Attempt to add the same name on Sheet2 – this will throw
workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

Niestety, zakres nazewnictwa w Excelu jest **workbook‑wide**, a nie per‑sheet. Powyższe wywołanie generuje `InvalidOperationException` z komunikatem *„A name with the same identifier already exists.”*  

### Jak obejść problem

1. **Pick a unique name** (`MyTable_Sheet2`).  
2. **Delete the existing name** before re‑adding it (only if you truly want to replace it).  

```csharp
// Option A – use a unique name
workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");

// Option B – replace the existing name (use with caution)
if (workbook.Names.Contains("MyTable"))
    workbook.Names.Remove("MyTable");

workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

---

## Pełny, działający przykład

Łącząc wszystko razem, oto samodzielna aplikacja konsolowa, którą możesz wrzucić do Visual Studio i uruchomić na przykładowym pliku `sample.xlsx`.

```csharp
using System;
using DevExpress.Spreadsheet;

class Program
{
    static void Main()
    {
        // Load an existing workbook (replace with your file path)
        Workbook workbook = new Workbook();
        workbook.LoadDocument("sample.xlsx");

        // -------------------------------------------------
        // Step 1 – Access the worksheet by its tab name
        // -------------------------------------------------
        Worksheet worksheet = workbook.Worksheets["Sheet1"]; // primary sheet

        // -------------------------------------------------
        // Step 2 – Delete rows excel table (safe method)
        // -------------------------------------------------
        var table = worksheet.ListObjects[0];
        int dataRows = table.DataRange.RowCount;
        if (dataRows > 0)
            table.DeleteRows(0, dataRows); // removes only data rows

        // -------------------------------------------------
        // Step 3 – Add a defined name (named range) on Sheet1
        // -------------------------------------------------
        workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

        // -------------------------------------------------
        // Step 4 – Demonstrate duplicate‑name handling
        // -------------------------------------------------
        try
        {
            workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
        }
        catch (InvalidOperationException ex)
        {
            Console.WriteLine("Duplicate name error: " + ex.Message);
            // Use a unique identifier instead
            workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");
        }

        // Save the modified workbook
        workbook.SaveDocument("sample_modified.xlsx");
        Console.WriteLine("Workbook updated successfully.");
    }
}
```

**Oczekiwany rezultat**

* Wszystkie wiersze danych z pierwszej tabeli na **Sheet1** znikają, pozostawiając tylko wiersz nagłówka.  
* Nazwa **MyTable** teraz wskazuje na `Sheet1!$A$1:$C$5`.  
* Druga nazwa **MyTable_Sheet2** bezpiecznie odwołuje się do zakresu na **Sheet2** bez wyrzucania wyjątku.

---

## Częste pytania i przypadki brzegowe

| Question | Answer |
|----------|--------|
| *What if the workbook has multiple tables?* | Grab the correct `ListObject` by index (`worksheet.ListObjects[1]`) or by name (`worksheet.ListObjects["MyTable"]`). |
| *Can I delete rows from a table that spans multiple worksheets?* | No—tables are confined to a single sheet. You must repeat the delete logic for each sheet. |
| *Is there a way to delete only a subset of rows?* | Yes—use `table.DeleteRows(startRow, count)` where `startRow` is zero‑based within the table’s data area. |
| *Do named ranges survive after saving?* | Absolutely. Once you call `SaveDocument`, the names become part of the workbook’s XML. |
| *How do I list all defined names in the workbook?* | Iterate `foreach (var name in workbook.Names) Console.WriteLine(name.Name);`. |

---

## Zakończenie

Omówiliśmy **delete rows excel table** przy użyciu C#, zaprezentowaliśmy **add named range excel** oraz pokazaliśmy właściwy sposób **access worksheet by name**, unikając przy tym niechcianego wyjątku z duplikatem nazwy.  

Pełne rozwiązanie znajduje się w powyższym fragmencie kodu — skopiuj, wklej i uruchom je na własnych plikach. Stąd możesz rozbudować logikę, aby obsługiwać wiele tabel, dynamiczne obliczenia zakresów lub nawet zintegrować ją z interfejsem użytkownika.

**Kolejne kroki**, które możesz rozważyć:

* Użyj **named range on another sheet**, aby zasilić serie wykresu.  
* Połącz logikę usuwania z **ExcelDataReader**, aby zaimportować dane przed ich czyszczeniem.  
* Zautomatyzuj masowe aktualizacje w dziesiątkach skoroszytów, używając prostej pętli `foreach (var file in Directory.GetFiles(...))`.

Masz więcej pytań o automatyzację Excela w C#? Dodaj komentarz i kontynuujmy dyskusję. Szczęśliwego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}