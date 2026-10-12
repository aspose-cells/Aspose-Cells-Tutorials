---
category: general
date: 2026-06-18
description: Parsuj japońską datę w erze w Javie przy użyciu Aspose.Cells. Dowiedz
  się, jak szybko odczytać datę z komórki Excel i wyodrębnić datę i czas z komórki
  Excel.
draft: false
keywords:
- parse japanese era date
- read date from excel cell
- extract datetime from excel cell
language: pl
og_description: Parsuj japońską datę ery w Javie przy użyciu Aspose.Cells. Ten przewodnik
  pokazuje, jak odczytać datę z komórki Excel i wyodrębnić datę i czas z komórki Excel
  w kilku prostych krokach.
og_title: Parsowanie japońskiej daty ery z Excela w Javie – Kompletny poradnik
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Parse Japanese era date in Java using Aspose.Cells. Learn how to read
    date from Excel cell and extract datetime from Excel cell quickly.
  headline: Parse Japanese Era Date from Excel in Java – Full Guide
  type: TechArticle
- description: Parse Japanese era date in Java using Aspose.Cells. Learn how to read
    date from Excel cell and extract datetime from Excel cell quickly.
  name: Parse Japanese Era Date from Excel in Java – Full Guide
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
title: Parsowanie japońskiej daty ery z Excela w Javie – pełny przewodnik
url: /pl/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Parsowanie daty japońskiej ery z Excela w Javie – Pełny przewodnik

Kiedykolwiek potrzebowałeś **parse Japanese era date** przechowywaną w skoroszycie Excel, ale nie byłeś pewien, jak przekształcić ją w zwykły gregoriański `DateTime`? Nie jesteś sam — wielu programistów napotyka ten problem przy pracy z legacyjskimi japońskimi arkuszami księgowymi lub formularzami rządowymi. Dobrą wiadomością jest to, że kilka linijek Javy i odpowiednia biblioteka pozwalają **read date from Excel cell** i **extract datetime from Excel cell** bez ręcznego manipulowania łańcuchami.

W tym samouczku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który dokładnie pokazuje, jak **parse Japanese era date** ciągi takie jak „令和3年5月10日” zamienić na `java.time.LocalDateTime` w Javie. Omówimy wymaganą zależność Maven, wyjaśnimy, dlaczego musisz włączyć parsowanie z uwzględnieniem ery, oraz wskażemy typowe pułapki, na które możesz natrafić. Po zakończeniu będziesz mieć solidny, gotowy do produkcji fragment kodu, który możesz wkleić do dowolnego projektu Java.

## Wymagania wstępne

- Java 17 lub nowszy (kod działa również na Java 8+)
- System budowania Maven lub Gradle
- Podstawowa znajomość plików Excel
- Biblioteka **Aspose.Cells for Java** (darmowa wersja próbna działa do testów)

Jeśli któreś z nich jest Ci nieznane, nie martw się — pokażę dokładnie, jak dodać bibliotekę i rozpocząć.

## Krok 1: Dodaj Aspose.Cells do swojego projektu

Na początek: potrzebujesz biblioteki, która rozumie daty japońskiej ery. Aspose.Cells wykona za Ciebie ciężką pracę.

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

Gdy zależność zostanie rozwiązana, możesz rozpocząć pisanie kodu, który *reads date from Excel cell* i *extracts datetime from Excel cell*.

## Krok 2: Utwórz skoroszyt i skieruj się do pierwszego arkusza

Zaczniemy od utworzenia nowego skoroszytu w pamięci i pobrania pierwszego arkusza. To odzwierciedla pierwsze dwie linie oryginalnego przykładu.

```java
import com.aspose.cells.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize workbook and worksheet
        Workbook workbook = new Workbook();               // creates a blank workbook
        Worksheet sheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

Dlaczego zaczynamy od nowego skoroszytu? Gwarantuje to czyste środowisko, w którym możemy kontrolować każde ustawienie — co jest kluczowe, gdy później włączysz parsowanie z uwzględnieniem ery.

## Krok 3: Wstaw ciąg daty japońskiej ery do komórki A1

Teraz symulujemy plik Excel, który już zawiera datę japońskiej ery. W rzeczywistości prawdopodobnie wczytywałbyś istniejący plik `.xlsx`, ale dla ilustracji **zapiszemy** wartość sami.

```java
        // Step 3: Insert a Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日"); // Reiwa 3rd year = 2021-05-10
```

Ciąg jest zgodny ze standardową japońską notacją: *Era* + *Year* + *Month* + *Day*. Bez dodatkowej konfiguracji Aspose.Cells potraktuje to jako zwykły tekst, a nie datę.

## Krok 4: Włącz parsowanie dat z uwzględnieniem ery

Oto kluczowa część: poinformuj skoroszyt, aby **parse Japanese era date** ciągi, gdy je napotka. Robi się to za pomocą flagi `ParseDateUsingJapaneseEra`.

```java
        // Step 4: Turn on era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);
```

Dlaczego to konieczne? Domyślnie Aspose.Cells zakłada kalendarz gregoriański, więc „令和3年5月10日” pozostałby jako ciąg znaków. Włączenie flagi instruuje silnik, aby przekształcił go w `java.util.Date` (lub odpowiednik `java.time`) w tle.

## Krok 5: Pobierz sparsowaną wartość DateTime

Teraz, gdy skoroszyt wie, jak interpretować erę, możemy poprosić komórkę o jej reprezentację `DateTime`.

```java
        // Step 5: Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime(); // returns java.util.Date
        // Convert to java.time.LocalDateTime for modern APIs
        java.time.Instant instant = javaDate.toInstant();
        java.time.ZoneId zone = java.time.ZoneId.systemDefault();
        java.time.LocalDateTime dateTime = java.time.LocalDateTime.ofInstant(instant, zone);
```

Zauważ, że **read date from Excel cell** przy użyciu `cell.getDateTime()`. Metoda zwraca `java.util.Date`, który od razu konwertujemy na `LocalDateTime` dla lepszej bezpieczeństwa typów. Spełnia to wymaganie **extract datetime from excel cell** w czysty, idiomatyczny sposób.

## Krok 6: Zweryfikuj wynik

Na koniec wydrukujmy datę gregoriańską, aby potwierdzić, że konwersja się powiodła.

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

Ten wynik dowodzi, że pomyślnie **parse Japanese era date**, **read date from Excel cell** i **extract datetime from Excel cell** w jednym przebiegu.

## Obsługa rzeczywistych przypadków brzegowych

### Wiele er

Japonia miała kilka er (Meiji, Taishō, Shōwa, Heisei, Reiwa). Flaga `setParseDateUsingJapaneseEra(true)` obejmuje je wszystkie automatycznie, ale pamiętaj, że starsze daty mogą wykraczać poza zakres obsługiwany przez bibliotekę (zwykle 1868‑obecnie). Jeśli napotkasz datę taką jak „昭和45年12月31日”, ten sam kod przekształci ją na 1970‑12‑31.

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

Przykład zawiera tylko datę, ale jeśli Twój plik Excel przechowuje także czas (np. „令和3年5月10日 14:30”), Aspose.Cells zachowa część czasową. `LocalDateTime`, który otrzymasz, będzie zawierał godziny, minuty i sekundy.

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

## Porady profesjonalne i typowe pułapki

- **Pro tip:** Zawsze ustaw `setParseDateUsingJapaneseEra(true)` **przed** odczytaniem jakichkolwiek wartości komórek. Zmiana flagi po odczytaniu komórki nie spowoduje retroaktywniej konwersji wartości.
- **Watch out for locale:** Biblioteka parsuje ciągi er na podstawie znaków Unicode, więc nie musisz explicite ustawiać japońskiej lokalizacji.
- **Performance note:** Włączenie parsowania er dodaje niewielkie obciążenie. Jeśli potrzebujesz go tylko dla kilku komórek, możesz tymczasowo przełączyć flagę, odczytać komórki, a potem wyłączyć ją ponownie.
- **Testing:** Skorzystaj z darmowej wersji próbnej Aspose, aby zweryfikować rzeczywisty plik Excel zawierający wiele dat er. To zapewnia, że Twój kod produkcyjny zachowuje się zgodnie z oczekiwaniami.

## Podsumowanie

Właśnie pokazaliśmy, jak **parse Japanese era date** wartości bezpośrednio z skoroszytu Excel przy użyciu Javy i Aspose.Cells. Włączając parsowanie z uwzględnieniem ery, możesz **read date from Excel cell** i **extract datetime from Excel cell** w czysty, typowo‑bezpieczny sposób. Podejście działa dla każdej nowoczesnej japońskiej ery, obsługuje składniki czasu i elegancko radzi sobie z nieprawidłowymi danymi.

Gotowy na kolejne wyzwanie? Spróbuj wczytać rzeczywisty plik `.xlsx`, który zawiera mieszankę dat gregoriańskich i japońskich er, lub poeksperymentuj z formatowaniem otrzymanego `LocalDateTime` do ciągów pasujących do Twojej lokalizacji. Możesz także zbadać zapis przekształconych dat z powrotem do Excela dla systemów downstream, które rozumieją tylko daty gregoriańskie.

Masz pytania lub natrafiłeś na dziwny przypadek brzegowy? zostaw komentarz poniżej i szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Opanuj system daty 1904 w Excelu przy użyciu Aspose.Cells Java dla efektywnych operacji na komórkach](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Efektywne konwertowanie Excela do PDF z niestandardowymi formatami dat przy użyciu Aspose.Cells for Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Jak wybrać zakresy komórek w Excelu przy użyciu Aspose.Cells for Java (przewodnik 2023)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}