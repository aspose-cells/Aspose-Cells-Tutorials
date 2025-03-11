---
title: Walidacja danych dziesiętnych w programie Excel
linktitle: Walidacja danych dziesiętnych w programie Excel
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Dowiedz się, jak wdrożyć walidację danych dziesiętnych w programie Excel przy użyciu Aspose.Cells dla .NET dzięki naszemu łatwemu w użyciu przewodnikowi. Zwiększ integralność danych bez wysiłku.
weight: 11
url: /pl/net/excel-autofilter-validation/decimal-data-validation-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Walidacja danych dziesiętnych w programie Excel

## Wstęp

Tworzenie arkuszy kalkulacyjnych z dokładnymi danymi jest niezbędne do jasnej komunikacji w każdej firmie. Jednym ze sposobów zapewnienia dokładności danych jest użycie walidacji danych w programie Excel. W tym samouczku wykorzystamy moc Aspose.Cells dla .NET, aby utworzyć mechanizm walidacji danych dziesiętnych, który zapewni niezawodność i czystość danych. Jeśli chcesz ulepszyć swoją grę w programie Excel, jesteś we właściwym miejscu!

## Wymagania wstępne

Zanim zagłębisz się w kod, upewnij się, że wszystko jest skonfigurowane, aby zapewnić płynne działanie:

1. Visual Studio: Pobierz i zainstaluj Visual Studio, jeśli jeszcze tego nie zrobiłeś. To idealne środowisko do tworzenia aplikacji .NET.
2.  Aspose.Cells dla .NET: Musisz dodać bibliotekę Aspose.Cells do swojego projektu. Możesz ją pobrać za pośrednictwem[ten link](https://releases.aspose.com/cells/net/).
3. Podstawowa znajomość języka C#: Chociaż wszystko wyjaśnimy krok po kroku, podstawowa znajomość programowania w języku C# pozwoli Ci lepiej zrozumieć te koncepcje.
4. .NET Framework: Upewnij się, że masz zainstalowaną niezbędną wersję .NET Framework zgodną z Aspose.Cells.
5. Biblioteki: Aby uniknąć błędów kompilacji, odwołuj się do biblioteki Aspose.Cells w swoim projekcie.

Teraz, gdy omówiliśmy już podstawy, możemy przejść do ekscytującej części: kodowania.

## Importuj pakiety

Na początek musisz zaimportować niezbędne pakiety do pliku C#. Umożliwi Ci to dostęp do funkcjonalności Aspose.Cells.

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Dodając ten wiersz na początku pliku, informujesz C#, że ma szukać funkcjonalności Aspose.Cells umożliwiającej manipulowanie plikami Excela.

Teraz, gdy już wszystko mamy gotowe, przeanalizujmy kroki niezbędne do utworzenia funkcji sprawdzania poprawności danych dziesiętnych w arkuszu kalkulacyjnym programu Excel.

## Krok 1: Skonfiguruj katalog dokumentów

Zanim zapiszesz jakiekolwiek pliki, musisz upewnić się, że katalog dokumentów jest poprawnie skonfigurowany:

```csharp
string dataDir = "Your Document Directory";
```

 Zastępować`"Your Document Directory"` ze ścieżką, pod którą chcesz zapisać pliki Excela.

## Krok 2: Sprawdź, czy katalog istnieje

Ten fragment kodu sprawdza, czy katalog istnieje i tworzy go, jeśli nie istnieje:

```csharp
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

Ten krok jest jak upewnienie się, że Twoje miejsce pracy jest gotowe przed rozpoczęciem nowego projektu. Bez bałaganu, bez stresu!

## Krok 3: Utwórz obiekt skoroszytu

Następnie utwórzmy nowy obiekt skoroszytu, który jest w zasadzie plikiem programu Excel:

```csharp
Workbook workbook = new Workbook();
```

Wyobraź sobie skoroszyt jako puste płótno na swoje dane. W tym momencie nie ma on żadnej zawartości, ale jest gotowy do pomalowania.

## Krok 4: Utwórz i uzyskaj dostęp do arkusza kalkulacyjnego


Teraz utwórzmy arkusz kalkulacyjny i uzyskajmy dostęp do pierwszego arkusza w skoroszycie:

```csharp
Worksheet ExcelWorkSheet = workbook.Worksheets[0];
```

Podobnie jak książka ma wiele stron, skoroszyt może mieć wiele arkuszy. Obecnie skupiamy się na pierwszym.

## Krok 5: Uzyskaj kolekcję walidacji

Teraz pobierzmy zbiór walidacji z arkusza kalkulacyjnego, ponieważ to tutaj będziemy zarządzać naszymi regułami walidacji danych:

```csharp
ValidationCollection validations = ExcelWorkSheet.Validations;
```

Ten krok można porównać do sprawdzenia zestawu narzędzi przed rozpoczęciem projektu.

## Krok 6: Zdefiniuj obszar komórki do walidacji

Musimy zdefiniować obszar, w którym obowiązuje walidacja:

```csharp
CellArea ca = new CellArea();
ca.StartRow = 0;
ca.EndRow = 0;
ca.StartColumn = 0;
ca.EndColumn = 0;
```

Tutaj zakładamy, że walidacja danych zostanie zastosowana do pojedynczej komórki, a konkretnie do pierwszej komórki w arkuszu kalkulacyjnym (A1).

## Krok 7: Utwórz i dodaj walidację

Utwórzmy nasz obiekt walidacji i dodajmy go do kolekcji walidacji:

```csharp
Validation validation = validations[validations.Add(ca)];
```

Teraz mamy obiekt walidacji, który skonfigurujemy, aby wymusić nasze warunki dziesiętne.

## Krok 8: Ustaw typ walidacji

Następnie określimy typ walidacji, jaki chcemy uzyskać:

```csharp
validation.Type = ValidationType.Decimal;
```

Ustawiając typ na Dziesiętny, instruujemy program Excel, aby oczekiwał wartości dziesiętnych w sprawdzanej komórce.

## Krok 9: Określ operatora

Teraz określimy warunek dla dopuszczalnych wartości. Chcemy się upewnić, że wprowadzone dane mieszczą się między dwoma zakresami:

```csharp
validation.Operator = OperatorType.Between;
```

Pomyśl o tym jak o narysowaniu linii granicznej. Każda liczba poza tym zakresem zostanie odrzucona, dzięki czemu Twoje dane pozostaną czyste!

## Krok 10: Ustal limity dla walidacji

Następnie ustalimy dolny i górny limit naszej walidacji:

```csharp
validation.Formula1 = Decimal.MinValue.ToString();
validation.Formula2 = Decimal.MaxValue.ToString();
```

Dzięki tym ograniczeniom każda liczba dziesiętna, bez względu na jej wielkość, jest akceptowana, pod warunkiem, że jest prawidłowa!

## Krok 11: Dostosowywanie komunikatu o błędzie

Zadbajmy o to, aby użytkownicy wiedzieli, dlaczego ich dane wejściowe zostały odrzucone, dodając komunikat o błędzie:

```csharp
validation.ErrorMessage = "Please enter a valid integer or decimal number";
```

Dzięki temu użytkownik ma dostęp do przyjaznych dla niego informacji, ponieważ otrzymuje wskazówki dotyczące tego, co należy wprowadzić.

## Krok 12: Zdefiniuj obszar walidacji

Teraz określmy komórki, które będą podlegać tej walidacji:

```csharp
CellArea area;
area.StartRow = 0;
area.EndRow = 9;
area.StartColumn = 0;
area.EndColumn = 0;
```

tej konfiguracji zakładamy, że walidacja dotyczy komórek od A1 do A10.

## Krok 13: Dodaj obszar walidacji

Teraz, gdy zdefiniowaliśmy nasz obszar walidacji, zastosujmy go:

```csharp
validation.AddArea(area);
```

Twoja walidacja jest teraz gotowa, gotowa wychwycić wszelkie nieodpowiednie dane wejściowe!

## Krok 14: Zapisz skoroszyt

Na koniec zapiszmy skoroszyt z włączoną walidacją danych dziesiętnych:

```csharp
workbook.Save(dataDir + "output.out.xls");
```

I masz! Udało Ci się utworzyć skoroszyt z walidacją danych dziesiętnych przy użyciu Aspose.Cells dla .NET.

## Wniosek

Wdrożenie walidacji danych dziesiętnych w programie Excel przy użyciu Aspose.Cells dla .NET jest dziecinnie proste, gdy zastosujesz się do tych prostych kroków. Nie tylko upewnisz się, że dane pozostają czyste i uporządkowane, ale także poprawisz ogólną integralność danych w arkuszach kalkulacyjnych, dzięki czemu będą niezawodne i przyjazne dla użytkownika.
Niezależnie od tego, czy jesteś w finansach, zarządzaniu projektami czy w jakiejkolwiek innej dziedzinie, która wykorzystuje raportowanie danych, opanowanie tych umiejętności znacznie zwiększy Twoją produktywność. Więc śmiało, spróbuj! Twoje arkusze kalkulacyjne Ci za to podziękują.

## Najczęściej zadawane pytania

### Czym jest walidacja danych w programie Excel?
Sprawdzanie poprawności danych w programie Excel to funkcja ograniczająca typ danych, jakie można wprowadzić do określonej komórki lub zakresu, zapewniając w ten sposób integralność danych.

### Czy mogę dostosować komunikat o błędzie podczas sprawdzania poprawności danych?
Tak! Możesz zapewnić niestandardowe komunikaty o błędach, aby pomóc użytkownikom, gdy zostaną wprowadzone nieprawidłowe dane.

### Czy korzystanie z Aspose.Cells jest bezpłatne?
 Aspose.Cells oferuje bezpłatną wersję próbną, ale do długoterminowego użytkowania potrzebna będzie licencja. Więcej informacji na temat uzyskania tymczasowej licencji można znaleźć[Tutaj](https://purchase.aspose.com/temporary-license/).

### Jakie typy danych mogę sprawdzać w programie Excel?
Za pomocą Aspose.Cells można sprawdzać poprawność różnych typów danych, w tym liczb całkowitych, liczb dziesiętnych, dat, list i formuł niestandardowych.

### Gdzie mogę znaleźć więcej dokumentacji Aspose.Cells?
 Możesz zapoznać się z obszerną dokumentacją[Tutaj](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
