---
title: Konwersja wykresu na obraz w .NET
linktitle: Konwersja wykresu na obraz w .NET
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Dowiedz się, jak konwertować wykresy na obrazy w .NET za pomocą Aspose.Cells dzięki temu przewodnikowi krok po kroku. Łatwo konwertuj wykresy Excela na wysokiej jakości obrazy.
weight: 10
url: /pl/net/image-and-chart-operations/chart-to-image-conversion/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konwersja wykresu na obraz w .NET

## Wstęp
Konwersja wykresu z programu Excel na obraz może być kluczowym wymogiem podczas tworzenia systemów raportowania lub udostępniania wizualnych reprezentacji danych. Na szczęście dzięki Aspose.Cells dla .NET ten proces jest dziecinnie prosty! Niezależnie od tego, czy generujesz raporty, czy po prostu konwertujesz wykresy programu Excel na obrazy w celu lepszego wyświetlania, ten przewodnik przeprowadzi Cię przez ten proces krok po kroku.
## Wymagania wstępne
Zanim zaczniemy, upewnijmy się, że masz wszystko, czego potrzebujesz, aby móc skorzystać z tego samouczka.
### Biblioteka Aspose.Cells dla .NET
Najpierw musisz pobrać i odwołać się do biblioteki Aspose.Cells for .NET w swoim projekcie. Możesz pobrać najnowszą wersję tutaj:
- [Pobierz Aspose.Cells dla .NET](https://releases.aspose.com/cells/net/)
### Środowisko .NET
Upewnij się, że masz zainstalowany .NET Framework w swoim systemie. Możesz użyć Visual Studio lub dowolnego innego środowiska programistycznego .NET, aby uruchomić ten przykład.
### Konfiguracja licencji (opcjonalnie)
 Chociaż możesz używać Aspose.Cells w ramach bezpłatnej wersji próbnej, aby uzyskać pełną funkcjonalność bez ograniczeń, rozważ złożenie wniosku o[licencja tymczasowa](https://purchase.aspose.com/temporary-license/) lub kup jeden z[Tutaj](https://purchase.aspose.com/buy).

## Importuj pakiety
Na początek zaimportujmy niezbędne przestrzenie nazw do pracy z biblioteką Aspose.Cells. Pozwoli nam to manipulować plikami Excela i generować obrazy.
```csharp
using System.IO;
using System.Drawing;
using Aspose.Cells;
```
Upewnij się, że masz te pakiety gotowe zanim zaczniesz kodować.

Teraz przedstawimy proces konwersji wykresu na obraz w kilku prostych krokach.
## Krok 1: Skonfiguruj katalog swojego projektu
Potrzebujesz miejsca do zapisywania wygenerowanych obrazów, prawda? Najpierw utwórzmy katalog, w którym będą zapisywane obrazy wyjściowe.

Zaczynamy od zdefiniowania ścieżki do naszego katalogu dokumentów i upewnienia się, że folder istnieje. Jeśli nie istnieje, utworzymy go.
```csharp
// Zdefiniuj katalog, w którym będą zapisywane obrazy
string dataDir = "Your Document Directory";
//Sprawdź czy katalog istnieje
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Po wykonaniu tego kroku możesz wygenerować i zapisać obrazy wykresów w tym katalogu.
## Krok 2: Utwórz nowy skoroszyt
Tutaj utworzymy obiekt Workbook. Będzie on reprezentował nasz plik Excel, w którym zostanie osadzony wykres.

Skoroszyt jest jak plik Excela zawierający arkusze. Tworząc nowy skoroszyt, zaczynamy od nowa z pustym plikiem Excela.
```csharp
// Utwórz nowy obiekt skoroszytu
Workbook workbook = new Workbook();
```
## Krok 3: Dodaj nowy arkusz kalkulacyjny
Każdy plik Excela ma arkusze kalkulacyjne (lub zakładki). Dodajmy jeden do naszego skoroszytu.

Dodanie nowego arkusza jest niezbędne, ponieważ będziemy wstawiać nasze dane i wykresy do tego arkusza. Po dodaniu arkusza pobieramy jego odniesienie.
```csharp
// Dodaj nowy arkusz do skoroszytu
int sheetIndex = workbook.Worksheets.Add();
// Pobierz nowo dodany arkusz kalkulacyjny
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
## Krok 4: Wypełnij arkusz danymi
Aby utworzyć sensowny wykres, potrzebujemy danych, prawda? Wypełnijmy kilka komórek przykładowymi wartościami.

Dodamy dane do określonych komórek w arkuszu kalkulacyjnym. Dane te zostaną później wykorzystane do wygenerowania naszego wykresu.
```csharp
// Dodaj przykładowe dane do komórek
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```
## Krok 5: Dodaj wykres do arkusza kalkulacyjnego
Teraz utwórzmy wykres kolumnowy, który będzie wizualizował dodane właśnie dane.

Określamy typ wykresu (wykres kolumnowy) oraz definiujemy jego rozmiar i pozycję w arkuszu kalkulacyjnym.
```csharp
// Dodaj wykres kolumnowy do arkusza kalkulacyjnego
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Column, 5, 0, 15, 5);
```
## Krok 6: Zdefiniuj źródło danych wykresu
I tu właśnie dzieje się magia: połączenie wykresu z danymi w arkuszu kalkulacyjnym!

Łączymy wykres z danymi w kolumnach A1 do B3. Dzięki temu wykres będzie wiedział, skąd ma pobierać dane.
```csharp
// Połącz wykres z danymi w zakresie od A1 do B3
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
chart.NSeries.Add("A1:B3", true);
```
## Krok 7: Konwersja wykresu na obraz
Chwila prawdy: zamierzamy przekonwertować ten wykres na plik graficzny!

 Tutaj używamy`ToImage` metoda konwersji wykresu do wybranego formatu obrazu. W tym przypadku konwertujemy go do formatu EMF (Enhanced Metafile).
```csharp
// Przekonwertuj wykres na obraz i zapisz go w katalogu
chart.ToImage(dataDir + "Chart.emf", ImageFormat.Emf);
```
I to wszystko! Twój wykres został zapisany jako obraz. Czas poklepać się po plecach.
## Krok 8: Wyświetl komunikat o powodzeniu
Na zakończenie wyświetlmy komunikat potwierdzający wygenerowanie obrazu.
```csharp
// Wyświetl komunikat informujący o powodzeniu
System.Console.WriteLine("Image generated successfully.");
```
## Wniosek
Bum! Tak łatwo jest przekonwertować wykres z Excela na obraz za pomocą Aspose.Cells dla .NET. Ten proces nie tylko upraszcza prezentację danych, ale także zwiększa elastyczność raportów lub pulpitów nawigacyjnych, w których obrazy są preferowane od osadzonych wykresów.
Postępując zgodnie z instrukcjami zawartymi w tym przewodniku, możesz teraz przekonwertować dowolny wykres programu Excel na obraz, co umożliwi bezproblemową integrację danych wizualnych z różnymi aplikacjami.
## Najczęściej zadawane pytania
### Czy mogę konwertować różne typy wykresów za pomocą tej metody?
Tak, możesz konwertować dowolny typ wykresu obsługiwany przez Aspose.Cells, w tym wykresy kołowe, słupkowe, liniowe i inne!
### Czy można zmienić format obrazu?
 Oczywiście! Podczas gdy w tym przykładzie użyliśmy EMF, możesz zmienić format obrazu na PNG, JPEG, BMP i inne, po prostu modyfikując`ImageFormat` parametr.
### Czy Aspose.Cells obsługuje obrazy o wysokiej rozdzielczości?
Tak, Aspose.Cells pozwala kontrolować rozdzielczość obrazu i ustawienia jakości podczas eksportowania wykresów do obrazów.
### Czy mogę przekonwertować wiele wykresów na obrazy na raz?
Tak, możesz przeglądać wiele wykresów w skoroszycie i konwertować je wszystkie na obrazy za pomocą zaledwie kilku linijek kodu.
### Czy liczba wykresów, które mogę przekonwertować, jest ograniczona?
Aspose.Cells nie nakłada żadnych ograniczeń, ale przetwarzanie dużych ilości danych może zależeć od pamięci i wydajności systemu.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
