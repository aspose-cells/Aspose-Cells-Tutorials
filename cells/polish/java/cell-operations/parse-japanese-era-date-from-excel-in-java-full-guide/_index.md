---
category: general
date: 2026-10-07
description: Odczytaj datę z Excel w Java przy użyciu Aspose.Cells. Ten przewodnik
  pokazuje, jak parsować japońskie daty ery, odczytywać daty z komórek Excel oraz
  szybko wyodrębniać datetime z komórek Excel.
draft: false
keywords:
- read date from excel
- extract datetime from excel
- java excel date conversion
- japanese era date parsing
- aspose.cells java
lastmod: 2026-10-07
og_description: Odczytaj datę z Excel w Java przy użyciu Aspose.Cells. Ten przewodnik
  pokazuje, jak parsować japońskie daty ery, odczytywać daty z komórek Excel oraz
  wyodrębniać datetime z komórek Excel w kilku prostych krokach.
og_image_alt: 'Developer guide: Read date from Excel in Java using Aspose.Cells'
og_title: Odczyt daty z Excel w Java przy użyciu Aspose.Cells – pełny przewodnik
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Read date from Excel in Java with Aspose.Cells. This guide shows you
    how to parse Japanese era dates, read date from Excel cells, and extract datetime
    from Excel cells quickly.
  headline: Read date from Excel in Java with Aspose.Cells – full guide
  type: TechArticle
- description: Read date from Excel in Java with Aspose.Cells. This guide shows you
    how to parse Japanese era dates, read date from Excel cells, and extract datetime
    from Excel cells quickly.
  name: Read date from Excel in Java with Aspose.Cells – full guide
  steps:
  - name: Multiple Eras
    text: Japan has had several eras (Meiji, Taishō, Shōwa, Heisei, Reiwa). The `setParseDateUsingJapaneseEra(true)`
      flag covers all of them automatically, but be aware that older dates may fall
      outside the library’s supported range (typically 1868‑present). If you encounter
      a date like “昭和45年12月31日”, the sam
  - name: Blank or Invalid Cells
    text: 'If a cell is empty or contains a malformed string, `cell.getDateTime()`
      throws a `CellsException`. Guard against this with a simple check:'
  - name: Time Component
    text: The example only includes a date, but if your Excel file also stores time
      (e.g., “令和3年5月10日 14:30”), Aspose.Cells will preserve the time portion. The
      `LocalDateTime` you receive will include hours, minutes, and seconds.
  type: HowTo
tags:
- Java
- Excel
- DateTime
- read date from excel
- java excel date conversion
title: Odczyt daty z Excel w Java przy użyciu Aspose.Cells – pełny przewodnik
url: /pl/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Odczyt daty z Excela w Javie przy użyciu Aspose.Cells – pełny przewodnik

Jeśli potrzebujesz **odczytać datę z Excela** arkusze zawierające japońskie ciągi epok, trafiłeś we właściwe miejsce. W wielu starszych arkuszach księgowych lub rządowych data jest zapisana jako „令和3年5月10日”, a konwersja na standardowy gregoriański `LocalDateTime` może być podatna na błędy. Ten samouczek pokazuje, krok po kroku, jak włączyć parsowanie uwzględniające epoki, odczytać wartość komórki i **wyodrębnić datę i czas z Excela** przy użyciu Aspose.Cells dla Javy.

## Szybkie odpowiedzi
- **Która biblioteka obsługuje japońskie daty epokowe?** Aspose.Cells for Java.
- **Jaką wersję Javy wymaga?** Java 17 lub nowsza (Java 8 działa również).
- **Czy potrzebuję licencji do testowania?** Darmowa wersja próbna wystarczy do rozwoju.
- **Czy ten sam kod może odczytać daty gregoriańskie?** Tak, API automatycznie wykrywa format.
- **Czy informacja o czasie jest zachowana?** Absolutnie – godziny, minuty i sekundy przetrwają konwersję.

## Co to jest odczyt daty z Excela?
Wyrażenie „odczyt daty z Excela” odnosi się do pobierania wartości daty z komórki i konwertowania jej na obiekt daty‑czasu Javy, taki jak `java.time.LocalDateTime`. Aspose.Cells abstrahuje niskopoziomowy format binarny Excela, dzięki czemu możesz pracować z datami bez ręcznego parsowania łańcuchów.

## Dlaczego warto używać Aspose.Cells do parsowania japońskich epok?
Aspose.Cells obsługuje **ponad 50 formatów wejścia i wyjścia** i może przetwarzać wielostronicowe skoroszyty bez ładowania całego pliku do pamięci. Wbudowany parser uwzględniający epoki konwertuje każdą japońską epokę (Meiji, Taishō, Shōwa, Heisei, Reiwa) na daty gregoriańskie w jednym wywołaniu API, eliminując kruchy kod oparty na wyrażeniach regularnych.

## Wymagania wstępne
- Java 17 (lub Java 8+) zainstalowana na Twoim komputerze.
- System budowania Maven lub Gradle.
- Podstawowa znajomość plików Excel.
- Biblioteka Aspose.Cells for Java (wersja trial lub licencjonowana).

Jeśli któreś z nich jest Ci nieznane, nie martw się — pokażemy dokładnie, jak dodać bibliotekę w następnym kroku.

## Jak odczytać datę z Excela w Javie?

Wczytaj swój skoroszyt, włącz parsowanie uwzględniające epoki i poproś komórkę o jej wartość `DateTime`. Cały proces zajmuje **dwie linie funkcjonalnego kodu**, gdy biblioteka znajduje się w classpath.

### Krok 1: dodaj Aspose.Cells do swojego projektu

**Maven**:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- check for latest version -->
</dependency>
```

**Gradle**:

```groovy
implementation 'com.aspose:aspose-cells:24.9'
```

Po rozwiązaniu zależności możesz rozpocząć używanie API do **odczytu daty z Excela** komórek.

### Krok 2: utwórz skoroszyt i skieruj się do pierwszego arkusza

Klasa `Workbook` reprezentuje cały plik Excel w pamięci. Utworzenie nowej instancji zapewnia czyste środowisko dla kolejnych kroków parsowania.

```java
import com.aspose.cells.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize workbook and worksheet
        Workbook workbook = new Workbook();               // creates a blank workbook
        Worksheet sheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

### Krok 3: wstaw japoński ciąg daty epoki do komórki A1

Dla demonstracji zapisujemy ciąg epoki sami; w produkcji wczytałbyś istniejący plik `.xlsx`.

```java
        // Step 3: Insert a Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日"); // Reiwa 3rd year = 2021-05-10
```

Tekst podąża za konwencjonalnym japońskim wzorcem: *Era* + *Year* + *Month* + *Day*.

### Krok 4: włącz parsowanie dat uwzględniające epokę

Powiedz Aspose.Cells, aby traktował ciągi epok jako daty, ustawiając flagę `ParseDateUsingJapaneseEra`.  
`ParseDateUsingJapaneseEra` to właściwość, która przy wartości true włącza automatyczną konwersję japońskich ciągów epokowych na daty gregoriańskie.

```java
        // Step 4: Turn on era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);
```

Bez tej flagi biblioteka potraktowałaby „令和3年5月10日” jako zwykły tekst i utraciłaby automatyczną konwersję.

### Krok 5: pobierz sparsowaną wartość DateTime

Teraz poproś komórkę o jej reprezentację daty. `cell.getDateTime()` zwraca wartość komórki jako obiekt `java.util.Date`. Metoda zwraca `java.util.Date`, który natychmiast konwertujemy na nowoczesny `java.time.LocalDateTime`. `LocalDateTime` to klasa Javy reprezentująca datę i czas bez strefy czasowej.

```java
        // Step 5: Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime(); // returns java.util.Date
        // Convert to java.time.LocalDateTime for modern APIs
        java.time.Instant instant = javaDate.toInstant();
        java.time.ZoneId zone = java.time.ZoneId.systemDefault();
        java.time.LocalDateTime dateTime = java.time.LocalDateTime.ofInstant(instant, zone);
```

Spełnia to wymaganie **wyodrębnienia daty i czasu z Excela** w sposób typowo‑bezpieczny.

### Krok 6: zweryfikuj wynik

Wydrukuj datę gregoriańską, aby potwierdzić, że konwersja się powiodła.

```java
        // Step 6: Output the Gregorian date
        System.out.println(dateTime); // Expected output: 2021-05-10T00:00
    }
}
```

Po uruchomieniu programu powinieneś zobaczyć:

```
2021-05-10T00:00
```

Wynik dowodzi, że pomyślnie **odczytaliśmy datę z Excela**, sparsowaliśmy japońską epokę i **wyodrębniliśmy datę i czas z Excela** w jednym przepływie.

## Obsługa rzeczywistych przypadków brzegowych

### Wiele epok

Japonia miała kilka epok (Meiji, Taishō, Shōwa, Heisei, Reiwa). Flaga `setParseDateUsingJapaneseEra(true)` obejmuje je wszystkie automatycznie, ale pamiętaj, że starsze daty mogą znajdować się poza zakresem obsługiwanym przez bibliotekę (zazwyczaj 1868‑obecnie). Jeśli napotkasz datę taką jak „昭和45年12月31日”, ten sam kod przekonwertuje ją na 1970‑12‑31.

### Puste lub nieprawidłowe komórki

Jeśli komórka jest pusta lub zawiera nieprawidłowy ciąg, `cell.getDateTime()` rzuca `CellsException`. Zabezpiecz się przed tym prostym sprawdzeniem:

```java
if (cell.getType() == CellValueType.IS_DATE) {
    // safe to call getDateTime()
} else {
    System.out.println("Cell does not contain a parsable date.");
}
```

### Składnik czasu

Przykład zawiera tylko datę, ale jeśli Twój plik Excel przechowuje także czas (np. „令和3年5月10日 14:30”), Aspose.Cells zachowa część czasu. `LocalDateTime`, który otrzymasz, będzie zawierał godziny, minuty i sekundy.

## Pełny działający przykład

Łącząc wszystko razem, oto kompletny, gotowy do skopiowania i wklejenia program:

```java
import com.aspose.cells.*;
import java.time.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Insert Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日");

        // Enable era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);

        // Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime();
        LocalDateTime dateTime = javaDate.toInstant()
                                         .atZone(ZoneId.systemDefault())
                                         .toLocalDateTime();

        // Output the Gregorian date
        System.out.println(dateTime); // 2021-05-10T00:00
    }
}
```

Zapisz to jako `JapaneseEraDateParser.java`, skompiluj przy użyciu `javac` i uruchom przy pomocy `java`. Jeśli wszystko jest poprawnie skonfigurowane, zobaczysz wydrukowaną datę gregoriańską w konsoli.

## Porady ekspertów i typowe pułapki

- **Porada:** Włącz `setParseDateUsingJapaneseEra(true)` **przed** odczytaniem jakichkolwiek wartości komórek. Zmiana flagi później nie spowoduje retroaktywniej konwersji już odczytanych komórek.
- **Uwaga dotycząca lokalizacji:** Parser działa na samych znakach Unicode, więc nie musisz explicite ustawiać japońskiej lokalizacji.
- **Wydajność:** Parsowanie epok dodaje znikomy narzut. Jeśli potrzebujesz go tylko dla kilku komórek, włącz flagę tylko przy tych odczytach.
- **Testowanie:** Skorzystaj z darmowej wersji próbnej Aspose, aby zweryfikować rzeczywisty skoroszyt mieszający daty gregoriańskie i epokowe. To zapewnia, że kod produkcyjny zachowuje się zgodnie z oczekiwaniami.

## Najczęściej zadawane pytania

**Q: Czy mogę użyć tego podejścia z istniejącym plikiem .xlsx?**  
A: Tak. Wczytaj plik za pomocą `new Workbook("path/to/file.xlsx")`, a ta sama flaga sparsuje wszystkie znalezione ciągi epokowe.

**Q: Co się stanie, jeśli komórka zawiera datę gregoriańską?**  
A: Biblioteka zwraca niezmienioną wartość gregoriańską; parsowanie epok dotyczy tylko ciągów pasujących do wzorca epoki.

**Q: Czy Aspose.Cells obsługuje daty wcześniejsze niż Meiji (1868)?**  
A: Nie. Daty wcześniejsze niż 1868 są poza zakresem obsługiwanym i będą traktowane jako zwykły tekst.

**Q: Jak obsłużyć duże skoroszyty bez wyczerpania pamięci?**  
A: Użyj konstruktora `Workbook`, który przyjmuje `LoadOptions` z `setMemorySetting(MemorySetting.MemoryPreference)`, aby strumieniować dane zamiast ładować wszystko jednocześnie.

**Q: Czy wymagana jest komercyjna licencja do użytku produkcyjnego?**  
A: Tak, ważna licencja Aspose.Cells usuwa ograniczenia wersji próbnej i zapewnia pełną wydajność.

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i zbadać alternatywne podejścia implementacyjne w własnych projektach.

- [Opanuj system daty 1904 w Excelu przy użyciu Aspose.Cells Java dla efektywnych operacji na komórkach](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Efektywne konwertowanie Excela do PDF z niestandardowymi formatami dat przy użyciu Aspose.Cells dla Javy](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Jak wybrać zakresy komórek w Excelu przy użyciu Aspose.Cells dla Javy (przewodnik 2023)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

---

**Last Updated:** 2026-10-07  
**Tested With:** Aspose.Cells 24.12 for Java  
**Author:** Aspose

## Powiązane samouczki

- [Pełny przewodnik: parsowanie japońskiej daty epoki z Excela w Javie](/cells/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/)
- [Odczyt pliku Excel w Javie z Aspose.Cells – kompletny przewodnik](/cells/java/automation-batch-processing/aspose-cells-java-excel-manipulation/)
- [Zapis skoroszytu Excel przy użyciu Aspose.Cells dla Javy – kompletny przewodnik](/cells/java/automation-batch-processing/excel-workbook-automation-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}