---
"description": "Dowiedz się, jak kontrolować zasoby zewnętrzne podczas konwersji plików Excel do PDF za pomocą Aspose.Cells dla platformy .NET, korzystając z naszego łatwego w użyciu przewodnika."
"linktitle": "Kontrola zasobów zewnętrznych w programie Excel do pliku PDF w Aspose.Cells"
"second_title": "Aspose.Cells .NET API przetwarzania programu Excel"
"title": "Kontrola zasobów zewnętrznych w programie Excel do pliku PDF w Aspose.Cells"
"url": "/pl/net/rendering-and-export/control-loading-of-external-resources/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Kontrola zasobów zewnętrznych w programie Excel do pliku PDF w Aspose.Cells

## Wstęp
W dzisiejszej erze cyfrowej konwersja arkuszy kalkulacyjnych Excela na dokumenty PDF jest powszechnym zadaniem. Niezależnie od tego, czy przygotowujesz raporty, dane finansowe czy materiały prezentacyjne, chcesz mieć pewność, że Twoje pliki PDF wyglądają dokładnie tak, jak zamierzałeś. Aspose.Cells dla .NET to solidna biblioteka, która pozwala kontrolować ten proces konwersji do ostatniego szczegółu, szczególnie podczas obsługi zasobów zewnętrznych, takich jak obrazy towarzyszące plikom Excela. W tym przewodniku zagłębiamy się w to, jak kontrolować zasoby zewnętrzne podczas procesu konwersji Excela na PDF za pomocą Aspose.Cells. Więc weź swój ulubiony napój i zaczynajmy!
## Wymagania wstępne
Zanim przejdziemy do konkretów, upewnijmy się, że masz wszystko, czego potrzebujesz, aby zacząć. Oto krótka lista kontrolna:
1. Visual Studio lub dowolne środowisko IDE zgodne z platformą .NET: będziesz potrzebować środowiska, w którym będziesz mógł pisać i testować swój kod.
2. Aspose.Cells dla .NET: Jeśli jeszcze tego nie zainstalowałeś, przejdź do [Pobieranie Aspose](https://releases.aspose.com/cells/net/) stronę i pobierz najnowszą wersję.
3. Podstawowa wiedza o C#: Znajomość języka programowania C# będzie pomocna. Jeśli nie jesteś pewien jakichś pojęć, nie wahaj się ich sprawdzić.
4. Przykładowy plik Excela: Przygotuj plik Excela z dowolnymi zewnętrznymi zasobami, które chcesz przekonwertować. Możesz użyć dostarczonego przykładowego pliku „samplePdfSaveOptions_StreamProvider.xlsx”.
5. Plik obrazu do testowania: Będzie on używany jako zasób zewnętrzny podczas konwersji. Plik obrazu „newPdfSaveOptions_StreamProvider.png” jest dobrym symbolem zastępczym.
## Importuj pakiety
Aby zacząć, musisz zaimportować niezbędne przestrzenie nazw z biblioteki Aspose.Cells. Jest to kluczowe dla dostępu do jej funkcjonalności. Upewnij się, że dodałeś następujące dyrektywy using na górze pliku:
```csharp
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Rendering;
using System;
```
Pakiety te zawierają wszystkie niezbędne klasy i metody potrzebne do wykonania zadań.
## Krok 1: Utwórz klasę dostawcy strumienia
Pierwszym krokiem jest utworzenie klasy dostawcy strumienia, która implementuje `IStreamProvider` interfejs. Ta klasa pozwoli Ci kontrolować, jak ładowane są zasoby zewnętrzne.
```csharp
class MyStreamProvider : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        Debug.WriteLine("-----Close Stream-----");
    }
    public void InitStream(StreamProviderOptions options)
    {
        string sourceDir = "Your Document Directory";
        Debug.WriteLine("-----Init Stream-----");
        // Odczytaj nowy obraz w strumieniu pamięci i przypisz go do właściwości strumienia
        byte[] bts = File.ReadAllBytes(sourceDir + "newPdfSaveOptions_StreamProvider.png");
        MemoryStream ms = new MemoryStream(bts);
        options.Stream = ms;
    }
}
```
W tej klasie:
- CloseStream: Ta metoda zostanie wywołana, gdy strumień zostanie zamknięty. Na razie piszemy tylko komunikat debugowania do śledzenia.
- InitStream: Tutaj zaczyna się magia. Tutaj odczytasz swój zewnętrzny obraz jako tablicę bajtów, przekonwertujesz go na strumień pamięci i przypiszesz do `options.Stream` nieruchomość.
## Krok 2: Skonfiguruj katalogi źródłowe i wyjściowe
Teraz, gdy Twój dostawca transmisji strumieniowej jest gotowy, czas ustalić, gdzie znajduje się plik Excel i gdzie chcesz zapisać plik PDF.
```csharp
// Katalog źródłowy
string sourceDir = "Your Document Directory";
// Katalog wyjściowy
string outputDir = "Your Document Directory";
```
Po prostu zamień `"Your Document Directory"` z rzeczywistą ścieżką na twoim komputerze, gdzie znajdują się twoje pliki. Utrzymywanie porządku w twoich plikach jest kluczowe!
## Krok 3: Załaduj plik Excel
Następnie załadujesz plik Excela, z którego chcesz utworzyć plik PDF.
```csharp
// Załaduj plik źródłowy Excel zawierający obrazy zewnętrzne
Workbook wb = new Workbook(sourceDir + "samplePdfSaveOptions_StreamProvider.xlsx");
```
Używamy `Workbook` klasa z Aspose.Cells, która reprezentuje plik Excel. Plik może zawierać różne zasoby zewnętrzne, takie jak obrazy, które chcesz kontrolować podczas konwersji.
## Krok 4: Ustaw opcje zapisywania pliku PDF
Zanim zapiszesz skoroszyt jako PDF, określmy, jak chcesz go zapisać. Możesz dostosować te opcje zgodnie ze swoimi wymaganiami.
```csharp
// Określ opcje zapisu pliku PDF - Dostawca strumienia
PdfSaveOptions opts = new PdfSaveOptions();
opts.OnePagePerSheet = true; // Zapisz każdy arkusz na nowej stronie
```
Tutaj tworzymy nową instancję `PdfSaveOptions`który umożliwia dostosowanie formatowania pliku PDF. `OnePagePerSheet` opcja ta jest przydatna, ponieważ zapewnia, że każdy arkusz programu Excel będzie miał własną stronę w końcowym pliku PDF.
## Krok 5: Przypisz swojego dostawcę strumienia
Po ustawieniu opcji PDF musisz poinformować Aspose, aby używał Twojego niestandardowego dostawcy strumieniowego do obsługi zasobów zewnętrznych.
```csharp
wb.Settings.StreamProvider = new MyStreamProvider();
```
Ta linia łączy Twoje `Workbook` instancja z `MyStreamProvider` klasa, którą utworzyłeś wcześniej. Oznacza to, że kiedykolwiek podczas konwersji napotkasz zasoby zewnętrzne, Twój dostawca obsłuży je zgodnie ze specyfikacją.
## Krok 6: Zapisz skoroszyt jako plik PDF
Gdy wszystko jest już gotowe, nadszedł czas, aby zapisać skoroszyt programu Excel w formacie PDF.
```csharp
// Zapisz skoroszyt w formacie PDF
wb.Save(outputDir + "outputPdfSaveOptions_StreamProvider.pdf", opts);
```
Dzwoniąc do `Save` na obiekcie skoroszytu i przekazując katalog wyjściowy wraz z opcjami PDF, konwertujesz plik Excela do pięknie sformatowanego pliku PDF.
## Krok 7: Potwierdź pomyślne wykonanie
Podsumowując, zawsze miło jest potwierdzić, że Twój proces zakończył się sukcesem!
```csharp
Console.WriteLine("ControlLoadingOfExternalResourcesInExcelToPDF executed successfully.\r\n");
```
Wydrukowanie komunikatu o powodzeniu na konsoli pomaga być na bieżąco ze stanem operacji. Dobrym nawykiem jest umieszczanie tych małych potwierdzeń w kodzie.
## Wniosek
Oto i masz! Postępując zgodnie z tymi prostymi krokami, możesz fachowo kontrolować, jak zasoby zewnętrzne są obsługiwane podczas konwersji Excela do PDF za pomocą Aspose.Cells. Oznacza to, że Twoje dokumenty mogą teraz dokładnie zawierać obrazy i inne elementy zewnętrzne, zapewniając za każdym razem dopracowany produkt końcowy.
## Najczęściej zadawane pytania
### Czym jest Aspose.Cells?  
Aspose.Cells to zaawansowana biblioteka dla programistów .NET umożliwiająca tworzenie, przetwarzanie, konwertowanie i renderowanie plików Excel w różnych formatach.
### Jak pobrać Aspose.Cells?  
Najnowszą wersję Aspose.Cells można pobrać ze strony [Link do pobrania](https://releases.aspose.com/cells/net/).
### Czy mogę wypróbować Aspose.Cells za darmo?  
Tak! Możesz otrzymać bezpłatną wersję próbną, odwiedzając [Bezpłatna strona próbna](https://releases.aspose.com/).
### Gdzie mogę znaleźć pomoc dotyczącą Aspose.Cells?  
przypadku pytań dotyczących wsparcia możesz odwiedzić stronę [Forum wsparcia Aspose](https://forum.aspose.com/c/cells/9).
### Jak mogę uzyskać tymczasową licencję na Aspose.Cells?  
Możesz złożyć wniosek o tymczasową licencję [Tutaj](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}