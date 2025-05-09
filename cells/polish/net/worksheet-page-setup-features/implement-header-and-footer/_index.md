---
"description": "Dowiedz się, jak skonfigurować nagłówki i stopki w arkuszach kalkulacyjnych programu Excel za pomocą pakietu Aspose.Cells dla platformy .NET, korzystając z samouczka krok po kroku, praktycznych przykładów i przydatnych wskazówek."
"linktitle": "Wdrażanie nagłówka i stopki w arkuszu kalkulacyjnym"
"second_title": "Aspose.Cells .NET API przetwarzania programu Excel"
"title": "Wdrażanie nagłówka i stopki w arkuszu kalkulacyjnym"
"url": "/pl/net/worksheet-page-setup-features/implement-header-and-footer/"
"weight": 22
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Wdrażanie nagłówka i stopki w arkuszu kalkulacyjnym

## Wstęp

Podczas pracy z arkuszami kalkulacyjnymi programu Excel nagłówki i stopki odgrywają kluczową rolę w dostarczaniu odbiorcom ważnych informacji kontekstowych, takich jak nazwy plików, daty lub numery stron. Niezależnie od tego, czy automatyzujesz raporty, czy generujesz pliki dynamiczne, Aspose.Cells for .NET ułatwia programowe dostosowywanie nagłówków i stopek w arkuszach kalkulacyjnych. Ten przewodnik zagłębia się w kompleksowe, krok po kroku podejście do dodawania nagłówków i stopek za pomocą Aspose.Cells for .NET, nadając plikom programu Excel dodatkowy szlif i profesjonalizm.

## Wymagania wstępne

Zanim zaczniesz, upewnij się, że masz przygotowane następujące rzeczy:

1. Aspose.Cells dla .NET: Musisz zainstalować Aspose.Cells dla .NET. [Pobierz tutaj](https://releases.aspose.com/cells/net/).
2. Konfiguracja IDE: Visual Studio (lub preferowane środowisko IDE) z zainstalowanym środowiskiem .NET Framework.
3. Licencja: Choć możesz zacząć od bezpłatnej wersji próbnej, uzyskanie pełnej lub tymczasowej licencji pozwoli Ci w pełni wykorzystać potencjał Aspose.Cells. [Uzyskaj tymczasową licencję](https://purchase.aspose.com/temporary-license/).

Dokumentacja Aspose.Cells jest przydatnym źródłem informacji w trakcie całego procesu. Możesz ją znaleźć [Tutaj](https://reference.aspose.com/cells/net/).

## Importowanie pakietów

W swoim projekcie zaimportuj wymagane przestrzenie nazw:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Importując ten pakiet, uzyskasz dostęp do klas i metod potrzebnych do pracy z nagłówkami, stopkami i innymi funkcjonalnościami programu Excel w Aspose.Cells.

W tym przewodniku szczegółowo opiszemy każdy krok, tak aby łatwo było Ci z nim pracować, nawet jeśli dopiero zaczynasz przygodę z Aspose.Cells lub .NET.

## Krok 1: Skonfiguruj skoroszyt i ustawienia strony

Po pierwsze: utwórz nowy skoroszyt i uzyskaj dostęp do ustawień strony arkusza. Dzięki temu uzyskasz narzędzia potrzebne do modyfikacji nagłówka i stopki arkusza.

```csharp
// Zdefiniuj ścieżkę do zapisania dokumentu
string dataDir = "Your Document Directory";

// Utwórz obiekt skoroszytu
Workbook excel = new Workbook();
```

Tutaj stworzyliśmy `Workbook` obiekt, który reprezentuje nasz plik Excel. `PageSetup` arkusza kalkulacyjnego, gdzie możemy modyfikować opcje nagłówka i stopki.


## Krok 2: Uzyskaj dostęp do właściwości arkusza kalkulacyjnego i ustawień strony

W Aspose.Cells każdy arkusz ma `PageSetup` właściwość, która kontroluje funkcje układu, w tym nagłówki i stopki. Zdobądźmy `PageSetup` obiekt dla naszego arkusza kalkulacyjnego.

```csharp
// Uzyskaj odniesienie do PageSetup pierwszego arkusza kalkulacyjnego
PageSetup pageSetup = excel.Worksheets[0].PageSetup;
```

Dzięki temu, `pageSetup` zawiera teraz wszystkie ustawienia potrzebne do dostosowania nagłówków i stopek.


## Krok 3: Ustaw lewą sekcję nagłówka

Nagłówki w programie Excel są podzielone na trzy sekcje: lewą, środkową i prawą. Zacznijmy od ustawienia lewej sekcji, aby wyświetlała nazwę arkusza kalkulacyjnego.

```csharp
// Ustaw nazwę arkusza roboczego w lewej części nagłówka
pageSetup.SetHeader(0, "&A");
```

Używanie `&A` pozwala na dynamiczne wyświetlanie nazwy arkusza. Jest to szczególnie pomocne, jeśli masz wiele arkuszy w skoroszycie i chcesz, aby każdy nagłówek odzwierciedlał tytuł arkusza.


## Krok 4: Dodaj datę i godzinę do środka nagłówka

Następnie dodajmy bieżącą datę i godzinę do środkowej sekcji nagłówka. Dodatkowo użyjemy niestandardowej czcionki do stylizacji.

```csharp
// Ustaw datę i godzinę w środkowej części nagłówka za pomocą pogrubionej czcionki
pageSetup.SetHeader(1, "&\"Times New Roman,Bold\"&D-&T");
```

W tym kodzie:
- `&D` wstawia bieżącą datę.
- `&T` wstawia aktualny czas.
- `"Times New Roman,Bold"` stosuje do tych elementów czcionkę Times New Roman pogrubioną.


## Krok 5: Wyświetl nazwę pliku w prawej części nagłówka

Aby dokończyć nagłówek, pokażmy po prawej stronie nazwę pliku i dostosujmy czcionkę.

```csharp
// Wyświetl nazwę pliku w prawej części nagłówka z niestandardowym rozmiarem czcionki
pageSetup.SetHeader(2, "&\"Times New Roman,Bold\"&12&F");
```

- `&F` reprezentuje nazwę pliku, dzięki czemu wiadomo, do którego pliku należą wydrukowane strony.
- `&12` zmienia rozmiar czcionki na 12 dla tej sekcji.


## Krok 6: Dodaj tekst z niestandardową czcionką do sekcji lewej stopki

Przejdźmy do stopek! Zaczniemy od skonfigurowania lewej sekcji stopki z niestandardowym tekstem i określonym stylem czcionki.

```csharp
// Dodaj niestandardowy tekst ze stylem czcionki do lewej części stopki
pageSetup.SetFooter(0, "Hello World! &\"Courier New\"&14 123");
```

Ten `&\"Courier New\"&14` ustawienie w powyższym kodzie stosuje czcionkę „Courier New” o rozmiarze 14 do określonego tekstu (`123`). Reszta tekstu pozostaje w domyślnej czcionce stopki.


## Krok 7: Wstaw numer strony na środku stopki

Umieszczenie numerów stron w stopce to świetny sposób, aby ułatwić czytelnikom śledzenie dokumentów wielostronicowych.

```csharp
// Wstaw numer strony w środkowej części stopki
pageSetup.SetFooter(1, "&P");
```

Tutaj, `&P` dodaje bieżący numer strony do środkowej sekcji stopki. To mały szczegół, ale kluczowy dla profesjonalnie wyglądających dokumentów.


## Krok 8: Wyświetl całkowitą liczbę stron w prawej stopce

Na koniec uzupełnijmy stopkę, wyświetlając w prawej sekcji całkowitą liczbę stron.

```csharp
// Wyświetl całkowitą liczbę stron w prawej części stopki
pageSetup.SetFooter(2, "&N");
```

- `&N` podaje całkowitą liczbę stron, pozwalając czytelnikom zorientować się, jak długi jest dokument.


## Krok 9: Zapisz skoroszyt

Po skonfigurowaniu nagłówków i stopek nadszedł czas na zapisanie skoroszytu. To ostatni krok w celu wygenerowania pliku Excel z całkowicie dostosowanymi nagłówkami i stopkami.

```csharp
// Zapisz skoroszyt
excel.Save(dataDir + "SetHeadersAndFooters_out.xls");
```

Ten wiersz zapisuje plik w wyznaczonym katalogu z ustawionymi niestandardowymi nagłówkami i stopkami.


## Wniosek

Dodawanie nagłówków i stopek do arkuszy kalkulacyjnych programu Excel to cenna umiejętność tworzenia uporządkowanych, profesjonalnych dokumentów. Dzięki Aspose.Cells dla .NET masz pełną kontrolę nad nagłówkami i stopkami plików programu Excel, od wyświetlania nazwy arkusza kalkulacyjnego po wstawianie niestandardowego tekstu, daty, godziny, a nawet dynamicznych numerów stron. Teraz, gdy widziałeś każdy krok w akcji, możesz przenieść automatyzację programu Excel na wyższy poziom.

## Najczęściej zadawane pytania

### Czy mogę używać różnych czcionek w różnych sekcjach nagłówka i stopki?  
Tak, Aspose.Cells for .NET pozwala na określenie czcionek dla każdej sekcji nagłówka i stopki za pomocą specjalnych znaczników czcionek.

### Jak usunąć nagłówki i stopki?  
Możesz wyczyścić nagłówki i stopki, ustawiając tekst nagłówka lub stopki na pusty ciąg za pomocą `SetHeader` Lub `SetFooter`.

### Czy mogę wstawiać obrazy do nagłówków i stopek za pomocą Aspose.Cells dla .NET?  
Obecnie Aspose.Cells obsługuje głównie tekst w nagłówkach i stopkach. Obrazy mogą wymagać obejścia, takiego jak wstawianie obrazów do samego arkusza kalkulacyjnego.

### Czy Aspose.Cells obsługuje dynamiczne dane w nagłówkach i stopkach?  
Tak, możesz używać różnych kodów dynamicznych (takich jak `&D` na datę lub `&P` (w celu uzyskania numeru strony) w celu dodania dynamicznej zawartości.

### Jak mogę dostosować wysokość nagłówka lub stopki?  
Aspose.Cells zapewnia opcje w ramach `PageSetup` Klasa umożliwiająca dostosowanie marginesów nagłówka i stopki, co daje Ci kontrolę nad odstępami.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}