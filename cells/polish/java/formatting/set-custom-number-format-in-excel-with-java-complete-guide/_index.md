---
category: general
date: 2026-06-30
description: Ustaw niestandardowy format liczby w Excelu przy użyciu Javy. Dowiedz
  się, jak tworzyć skoroszyt Excel w Javie, pobierać datę i godzinę z komórki, obliczać
  formuły w skoroszycie i wyświetlać wartość daty i godziny.
draft: false
keywords:
- set custom number format
- get datetime from cell
- create excel workbook java
- calculate workbook formulas
- output datetime value
language: pl
og_description: Ustaw niestandardowy format liczby w Excelu przy użyciu Javy. Ten
  przewodnik pokazuje, jak stworzyć skoroszyt Excel w Javie, pobrać datę i godzinę
  z komórki, obliczyć formuły w skoroszycie i wyświetlić wartość daty i godziny.
og_title: Ustaw niestandardowy format liczb w Excelu przy użyciu Javy – pełny poradnik
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  headline: Set Custom Number Format in Excel with Java – Complete Guide
  type: TechArticle
- description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  name: Set Custom Number Format in Excel with Java – Complete Guide
  steps:
  - name: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
    text: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
  - name: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
    text: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
  - name: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
    text: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- DateTime
title: Ustaw własny format liczby w Excelu za pomocą Javy – Kompletny przewodnik
url: /pl/java/formatting/set-custom-number-format-in-excel-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ustaw niestandardowy format liczby w Excelu przy użyciu Java – Kompletny przewodnik

Czy kiedykolwiek potrzebowałeś **ustawić niestandardowy format liczby** w arkuszu Excel podczas pracy w Javie? Nie jesteś jedyny. Niezależnie od tego, czy tworzysz silnik raportowy, czy po prostu chcesz poprawnie wyświetlać daty w japońskim erze, opanowanie tej sztuczki oszczędza niezliczone godziny post‑przetwarzania. W tym samouczku przeprowadzimy Cię przez rzeczywisty przykład, który **creates Excel workbook Java**, stosuje format specyficzny dla lokalizacji, przelicza formuły i w końcu **pobiera DateTime z komórki**, aby **wyświetlić wartość datetime**.

Użyjemy popularnej biblioteki Aspose.Cells for Java, ponieważ obsługuje formaty liczb i daty zależne od kultury od razu po instalacji. Po zakończeniu przewodnika będziesz mieć samodzielny, uruchamialny program, który możesz wstawić do dowolnego projektu Maven lub Gradle. Bez niejasnych skrótów typu „zobacz dokumentację” — tylko solidny kod i jasne wyjaśnienia.

---

## Czego się nauczysz

- Jak programowo **create Excel workbook Java**.
- Dokładne kroki, aby **set custom number format** dla dat w japońskiej erze.
- Dlaczego wywołanie **calculate workbook formulas** jest niezbędne przed wyodrębnieniem wartości.
- Właściwy sposób, aby **get datetime from cell** i **output datetime value**.
- Typowe pułapki (brak lokalizacji, nieaktualne formuły) oraz szybkie rozwiązania.

---

## Wymagania wstępne

- Java 8 lub nowsza zainstalowana na Twoim komputerze.  
- Aspose.Cells for Java 23.11 (lub dowolna nowsza wersja).  
- Podstawowe IDE lub edytor tekstu — IntelliJ IDEA, Eclipse, VS Code, cokolwiek wolisz.  

Jeśli jeszcze nie dodałeś Aspose.Cells do swojego projektu, wklej poniższy fragment Maven do pliku `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.11</version>
</dependency>
```

Użytkownicy Gradle mogą dodać:

```gradle
implementation 'com.aspose:aspose-cells:23.11'
```

Teraz, gdy środowisko jest gotowe, przejdźmy do kodu.

---

## Krok 1: Ustaw niestandardowy format liczby – Przegląd

Zanim napiszemy jakikolwiek kod Java, warto zwizualizować, co chcemy osiągnąć. Wyobraź sobie komórkę w Excelu, która powinna wyświetlać **„令和2年4月1日”** zamiast ciągu ISO‑8601 „2020‑04‑01”. Wartość podstawowa pozostaje prawdziwą datą (więc formuły nadal działają), ale *wyświetlanie* używa formatu japońskiej ery. To właśnie operacja **set custom number format** realizuje.

Poniżej znajduje się pełny plik źródłowy. Śmiało skopiuj‑wklej go do `src/main/java/SetCustomNumberFormatDemo.java`.

```java
// File: SetCustomNumberFormatDemo.java
import com.aspose.cells.*;

public class SetCustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Create Excel workbook Java – a fresh workbook
        // -------------------------------------------------
        Workbook workbook = new Workbook();               // in‑memory workbook, no file yet

        // -------------------------------------------------
        // 2️⃣ Access the first worksheet
        // -------------------------------------------------
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // -------------------------------------------------
        // 3️⃣ Retrieve cell A1 where we’ll store the date string
        // -------------------------------------------------
        Cell cellA1 = worksheet.getCells().get("A1");

        // -------------------------------------------------
        // 4️⃣ Insert a Japanese era date string (Reiwa 2‑04‑01)
        // -------------------------------------------------
        // Note: Aspose.Cells will treat this as a text value until we recalc.
        cellA1.putValue("R02-04-01");

        // -------------------------------------------------
        // 5️⃣ Apply the custom number format (our primary goal)
        // -------------------------------------------------
        // [$-ja-JP] tells Excel to use the Japanese locale.
        // ggge年m月d日 renders as "令和2年4月1日".
        cellA1.setNumberFormat("[$-ja-JP]ggge年m月d日");

        // -------------------------------------------------
        // 6️⃣ Calculate workbook formulas – crucial step!
        // -------------------------------------------------
        // Without this, the cell remains a plain string and the
        // DateTime conversion below will fail.
        workbook.calculateFormula();

        // -------------------------------------------------
        // 7️⃣ Get DateTime from cell – now the value is a true date
        // -------------------------------------------------
        // The getDateTime() method returns a java.util.Calendar instance.
        java.util.Calendar dt = cellA1.getDateTime();

        // -------------------------------------------------
        // 8️⃣ Output datetime value – see the result in console
        // -------------------------------------------------
        System.out.println("Converted DateTime: " + dt.getTime()); // → Tue Apr 01 00:00:00 UTC 2020
    }
}
```

### Dlaczego to działa

- `setNumberFormat` informuje Excel, jak *wyświetlać* podstawową wartość numeryczną. Kluczowy jest ciąg formatu `[$-ja-JP]ggge年m月d日`; `ggg` wybiera nazwę ery, `e` rok w ramach ery, a następnie literały miesiąca i dnia.
- `calculateFormula` zmusza Aspose.Cells do interpretacji tekstu „R02-04-01” jako daty zgodnie z japońskim kalendarzem. Pominięcie tego kroku pozostawia komórkę jako zwykły tekst, a `getDateTime()` wyrzuci wyjątek.
- `getDateTime` w końcu wyciąga *rzeczywisty* obiekt `java.util.Calendar`, który możesz manipulować, formatować lub przechowywać w innym miejscu.

---

## Krok 2: Tworzenie Excel workbook Java – Szczegółowy przegląd

Kiedy **create Excel workbook Java**, nie tylko przydzielasz pamięć; tworzysz także domyślne style, domyślny arkusz i domyślną kulturę (zazwyczaj locale systemu). Jeśli potrzebujesz innego domyślnego locale, możesz przekazać obiekt `LoadOptions`:

```java
LoadOptions opts = new LoadOptions(LoadFormat.XLSX);
opts.setLocale(new java.util.Locale("ja", "JP"));
Workbook workbook = new Workbook(opts);
```

W większości scenariuszy prosty konstruktor jest wystarczający, ale warto znać alternatywę — szczególnie gdy pracujesz z wieloma locale w jednej aplikacji.

*Pro tip:* Zawsze trzymaj skoroszyt w pamięci, dopóki nie zakończysz formatowania. Zapisywanie na dysk po każdej zmianie generuje niepotrzebny narzut I/O.

---

## Krok 3: Pobieranie DateTime z komórki – Obsługa wyniku

Linia `java.util.Calendar dt = cellA1.getDateTime();` wykonuje ciężką pracę. W tle Aspose.Cells konwertuje wewnętrzny numer seryjny (liczbę dni od 1899‑12‑31) na obiekt `Calendar`. Ta konwersja respektuje locale skoroszytu, więc otrzymujesz poprawną datę gregoriańską, mimo że wyświetlanie używa japońskiej ery.

Jeśli potrzebujesz `java.time.LocalDate` (nowsze API), skonwertuj w ten sposób:

```java
java.time.LocalDate localDate = dt.toInstant()
        .atZone(java.time.ZoneId.systemDefault())
        .toLocalDate();
System.out.println("LocalDate: " + localDate); // 2020-04-01
```

To spełnia wymaganie **output datetime value**, pozostając przy nowoczesnym podejściu.

---

## Krok 4: Przeliczanie formuł w skoroszycie – Kiedy ma to znaczenie

Możesz się zastanawiać: *„Czy naprawdę muszę wywoływać `calculateFormula()`?”* Odpowiedź brzmi zdecydowane tak, chyba że od samego początku wstawiasz do komórki natywny obiekt Java `Date`. Kiedy **set custom number format** na ciągu tekstowym, Excel (i Aspose.Cells) traktuje go jako wyrażenie podobne do formuły, które wymaga oceny. Bez przeliczenia, `getDateTime()` zwróci domyślną wartość `1900‑01‑00` lub wyrzuci `CellValueException`.

Jeśli Twój skoroszyt już zawiera złożone formuły odwołujące się do nowo sformatowanej komórki, wywołaj `calculateFormula()` *jednokrotnie* po wszystkich zmianach. Wielokrotne wywołania są kosztowne.

---

## Krok 5: Wyświetlanie wartości DateTime – Weryfikacja wyniku

Uruchomienie demo wypisuje coś w rodzaju:

```
Converted DateTime: Tue Apr 01 00:00:00 UTC 2020
```

Ta linia potwierdza trzy rzeczy:

1. Został zastosowany **set custom number format** (możesz otworzyć wygenerowany plik `.xlsx` w Excelu, aby zobaczyć „令和2年4月1日”).
2. Krok **calculate workbook formulas** zakończył się sukcesem, przekształcając ciąg ery w rzeczywistą datę.
3. Wywołanie **get datetime from cell** zwróciło prawidłowy obiekt `Calendar`, który następnie **output datetime value** na konsoli.

Jeśli otworzysz skoroszyt w programie arkusza kalkulacyjnego, zobaczysz sformatowany tekst, ale podstawowa wartość komórki pozostaje numerem seryjnym `43831` (reprezentacja Excel daty 2020‑04‑01). Ta dwoistość to właśnie siła Excela.

---

## Typowe pułapki i przypadki brzegowe

| Problem | Dlaczego się dzieje | Rozwiązanie |
|-------|----------------|-----|
| `cellA1.getDateTime()` throws `CellValueException` | Komórka jest nadal ciągiem znaków, ponieważ pominięto `calculateFormula()`. | Zawsze wywołuj `workbook.calculateFormula()` po ustawieniu tekstowej daty, która wymaga konwersji. |
| Japanese era not displayed correctly | Brak lub nieprawidłowy kod lokalizacji. | Użyj `[$-ja-JP]` w ciągu formatu lub ustaw locale skoroszytu poprzez `LoadOptions`. |
| Format shows “#VALUE!” in Excel | Ciąg formatu jest niepoprawny. | Sprawdź ponownie nawiasy i znaki; wzorzec `ggge年m月d日` jest wymagany dla roku ery. |
| Time component appears (e.g., “00:00:00”) | Źródłowy ciąg zawiera czas lub styl komórki go dodaje. | Przytnij źródłowy ciąg lub dostosuj format do `ggge年m月d日;@`. |

---

## Pełny działający przykład – jednorazowe uruchomienie

Jeśli wolisz pojedynczy plik bez dodatkowych komentarzy, oto wersja minimalna:



## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z krok po kroku wyjaśnieniami, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Utwórz skoroszyt Excel przy użyciu Aspose.Cells w Java: przewodnik krok po kroku](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Mistrzostwo prezentacji danych w Excelu: formatowanie liczb i niestandardowych dat przy użyciu Aspose.Cells for Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Jak tworzyć i formatować komórki Excel przy użyciu Aspose.Cells for Java: przewodnik krok po kroku](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}