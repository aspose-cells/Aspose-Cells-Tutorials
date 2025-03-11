---
title: Sortowanie niestandardowe tabeli przestawnej programowo w .NET
linktitle: Sortowanie niestandardowe tabeli przestawnej programowo w .NET
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Dowiedz się, jak programowo sortować tabele przestawne w .NET przy użyciu Aspose.Cells. Przewodnik krok po kroku obejmujący konfigurację, sortowanie i zapisywanie wyników jako pliki Excel i PDF.
weight: 29
url: /pl/net/creating-and-configuring-pivot-tables/pivot-table-custom-sort/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sortowanie niestandardowe tabeli przestawnej programowo w .NET

## Wstęp
Jeśli chodzi o pracę z programem Excel w środowisku .NET, jedna biblioteka wyróżnia się spośród pozostałych: Aspose.Cells. Czyż nie uwielbiasz, gdy narzędzie pozwala programowo manipulować arkuszami kalkulacyjnymi? Dokładnie to robi Aspose.Cells! W dzisiejszym samouczku zagłębiamy się w świat tabel przestawnych i pokazujemy, jak programowo implementować niestandardowe sortowanie przy użyciu tej wszechstronnej biblioteki.
## Wymagania wstępne
Zanim zakasamy rękawy i zaczniemy pisać kod, upewnij się, że masz przygotowane kilka rzeczy:
1. Visual Studio: Będziesz potrzebować działającej wersji Visual Studio. To plac zabaw, na którym dzieje się cała magia.
2. .NET Framework: Znajomość programowania .NET jest niezbędna. Niezależnie od tego, czy jesteś entuzjastą .NET Core czy .NET Framework, jesteś gotowy do działania.
3.  Biblioteka Aspose.Cells: Musisz zainstalować bibliotekę Aspose.Cells. Możesz ją pobrać z[Link do pobrania](https://releases.aspose.com/cells/net/) i dodaj do swojego projektu.
4. Podstawowa wiedza na temat tabel przestawnych: Chociaż nie musisz być ekspertem, odrobina wiedzy na temat działania tabel przestawnych okaże się pomocna w trakcie przechodzenia przez ten samouczek.
5.  Przykładowy plik programu Excel: Utwórz przykładowy plik programu Excel o nazwie`SamplePivotSort.xlsx` gotowe do przetestowania w Twoim katalogu roboczym.
## Importuj pakiety
Gdy już wszystkie wymagania wstępne zostaną posortowane, pierwszym krokiem jest zaimportowanie niezbędnych pakietów. Aby to zrobić, umieść następujące wiersze na górze kodu:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells;
using Aspose.Cells.Pivot;
```
Pakiet ten udostępnia wszystkie funkcje niezbędne do manipulowania plikami Excela za pomocą Aspose.Cells.

No dobrze, przejdźmy do zabawy! Rozłożymy proces tworzenia tabeli przestawnej i stosowania sortowania niestandardowego na łatwe do opanowania kroki.
## Krok 1: Skonfiguruj skoroszyt
Aby zacząć, musimy skonfigurować nasz skoroszyt. Oto, jak to zrobić:
```csharp
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
Workbook wb = new Workbook(sourceDir + "SamplePivotSort.xlsx");
```
 W tym kroku inicjujemy nowy`Workbook` wystąpienie ze ścieżką do naszego pliku Excel. Działa to jak płótno, na którym nasza tabela przestawna ożyje.
## Krok 2: Uzyskaj dostęp do arkusza kalkulacyjnego
Następnie musimy uzyskać dostęp do arkusza kalkulacyjnego, w którym dodamy tabelę przestawną.
```csharp
Worksheet sheet = wb.Worksheets[0];
PivotTableCollection pivotTables = sheet.PivotTables;
```
 Tutaj bierzemy pierwszy arkusz roboczy w naszym skoroszycie i wywołujemy`PivotTableCollection`Ta kolekcja pozwala nam zarządzać wszystkimi tabelami przestawnymi w tym arkuszu.
## Krok 3: Utwórz swoją pierwszą tabelę przestawną
Teraz czas utworzyć tabelę przestawną.
```csharp
int index = pivotTables.Add("=Sheet1!A1:C10", "E3", "PivotTable1");
PivotTable pivotTable = pivotTables[index];
```
Dodajemy nową tabelę przestawną do naszego arkusza kalkulacyjnego, określając zakres danych i jego lokalizację. „E3” wskazuje, gdzie chcemy, aby nasza tabela przestawna się zaczynała. Następnie odwołujemy się do tej nowej tabeli przestawnej, używając jej indeksu.
## Krok 4: Skonfiguruj ustawienia tabeli przestawnej
Skonfigurujmy naszą tabelę przestawną! Oznacza to kontrolowanie takich aspektów, jak sumy całkowite i układy pól.
```csharp
pivotTable.RowGrand = false;
pivotTable.ColumnGrand = false;
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
PivotField rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
Upewniamy się, że sumy całkowite dla wierszy i kolumn nie są wyświetlane, co może sprawić, że dane będą czystsze. Następnie dodajemy pierwsze pole do obszaru wiersza, umożliwiając automatyczne sortowanie i sortowanie rosnące.
## Krok 5: Dodaj kolumny i pola danych
Po ustawieniu wierszy dodajmy kolumny i pola danych.
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Column,0);
PivotField colField = pivotTable.ColumnFields[0];
colField.NumberFormat = "dd/mm/yyyy";
colField.IsAutoSort = true;
colField.IsAscendSort = true;
```
Dodajemy drugie pole jako kolumnę i formatujemy je jako datę. Ponownie włączamy automatyczne sortowanie i kolejność rosnącą, aby zachować porządek. Na koniec musimy dodać trzecie pole do naszego obszaru danych:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Data,2);
```
## Krok 6: Odśwież i oblicz tabelę przestawną
Po dodaniu wszystkich niezbędnych pól upewnijmy się, że nasza tabela przestawna jest aktualna i gotowa.
```csharp
pivotTable.RefreshData();
pivotTable.CalculateData();
```
Metody te odświeżają dane i przeliczają je, dzięki czemu wszystko jest aktualne i prawidłowo wyświetlane w tabeli przestawnej.
## Krok 7: Sortowanie niestandardowe na podstawie wartości pól wiersza
Dodajmy odrobinę finezji, sortując tabelę przestawną według określonych wartości, np. „Owoce morza”.
```csharp
index = pivotTables.Add("=Sheet1!A1:C10", "E10", "PivotTable2");
pivotTable = pivotTables[index];
```
Powtarzamy proces, tworząc kolejną tabelę przestawną i konfigurując ją podobnie do pierwszej. Teraz możemy ją dalej dostosować:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
## Krok 8: Dodatkowe dostosowywanie sortowaniaWypróbujmy inną metodę sortowania na podstawie określonej daty:
```csharp
// Dodawanie kolejnej tabeli przestawnej do sortowania według daty
index = pivotTables.Add("=Sheet1!A1:C10", "E18", "PivotTable3");
pivotTable = pivotTables[index];
// Powtórz ustawienia wierszy i kolumn podobne do tych z poprzednich kroków
```
Wystarczy, że powtórzysz ten sam proces, tworząc trzecią tabelę przestawną z kryteriami sortowania dostosowanymi do Twoich potrzeb.
## Krok 9: Zapisz skoroszytCzas zapisać całą ciężką pracę, którą włożyliśmy!
```csharp
wb.Save(outputDir + "out.xlsx");
PdfSaveOptions options = new PdfSaveOptions();
options.OnePagePerSheet = true;
wb.Save(outputDir + "out.pdf", options);
```
 Tutaj zapisujesz skoroszyt jako plik Excel i PDF.`PdfSaveOptions` umożliwia lepsze formatowanie, zapewniając, że każdy arkusz pojawi się na osobnej stronie po konwersji.
## Krok 10: Zakończenie Podsumuj wszystko, informując użytkownika, że wszystko jest w porządku.
```csharp
Console.WriteLine("PivotTableCustomSort executed successfully.");
```
## Wniosek
Do tej pory nauczyłeś się, jak wykorzystać moc Aspose.Cells do tworzenia i dostosowywania tabel przestawnych w aplikacjach .NET. Od początkowej konfiguracji do sortowania niestandardowego, każdy krok łączy się, aby zapewnić płynne działanie. Niezależnie od tego, czy musisz przedstawić roczne dane sprzedaży, czy śledzić statystyki zapasów, te umiejętności będą dla Ciebie przydatne!
## Najczęściej zadawane pytania
### Czym jest tabela przestawna?
Tabela przestawna to narzędzie do przetwarzania danych w programie Excel, które umożliwia podsumowywanie i analizowanie danych, zapewniając elastyczny sposób łatwego wyciągania wniosków.
### Jak zainstalować Aspose.Cells?
 Można go zainstalować za pomocą NuGet w programie Visual Studio lub pobrać bezpośrednio z witryny[Link do pobrania](https://releases.aspose.com/cells/net/).
### Czy istnieje wersja próbna Aspose.Cells?
 Tak! Możesz wypróbować za darmo odwiedzając[Link do bezpłatnej wersji próbnej](https://releases.aspose.com/).
### Czy mogę sortować wiele pól w tabeli przestawnej?
Oczywiście! Możesz dodać i sortować wiele pól w zależności od swoich wymagań.
### Gdzie mogę znaleźć pomoc dotyczącą Aspose.Cells?
 Społeczność jest bardzo aktywna, a pytania możesz zadawać na ich forum[Tutaj](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
