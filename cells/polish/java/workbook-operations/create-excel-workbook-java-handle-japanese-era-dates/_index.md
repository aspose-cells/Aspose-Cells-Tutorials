---
category: general
date: 2026-08-04
description: Utwórz skoroszyt Excel w Javie i parsuj daty w japońskich erach, a następnie
  zapisz skoroszyt jako xlsx przy użyciu Aspose.Cells dla Javy.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- save workbook as xlsx
- java excel date conversion
- Aspose.Cells Java
- japanese era date parsing
language: pl
lastmod: 2026-08-04
og_description: Utwórz skoroszyt Excela w Javie i automatycznie konwertuj japońskie
  daty z ery na kalendarz gregoriański, a następnie zapisz skoroszyt jako xlsx przy
  użyciu Aspose.Cells.
og_image_alt: Java code creating an Excel workbook and converting a Japanese era date
  to Gregorian
og_title: Utwórz skoroszyt Excel w Javie – przewodnik konwersji japońskich dat
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create excel workbook java and parse Japanese era dates, then save
    workbook as xlsx using Aspose.Cells for Java.
  headline: 'Create excel workbook java: handle Japanese era dates'
  type: TechArticle
tags:
- java
- excel
- Aspose.Cells
- date conversion
- xlsx
title: 'Utwórz skoroszyt Excel w Javie: obsługa japońskich dat ery'
url: /pl/java/workbook-operations/create-excel-workbook-java-handle-japanese-era-dates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie skoroszytu Excel w Javie: obsługa dat w japońskim systemie ery

Jeśli potrzebujesz **tworzyć skoroszyt Excel w Javie** i pracować z datami w japońskim systemie ery, ten tutorial pokaże Ci dokładnie, jak to zrobić. Nauczysz się wprowadzać datę w formacie „R3/05/01”, aby Aspose.Cells zinterpretował ją jako datę gregoriańską, a następnie **zapisz skoroszyt jako xlsx**.

Praca z kalendarzami opartymi na erze może być myląca, szczególnie gdy domyślny parser Excela oczekuje standardowego formatu gregoriańskiego. Włączając parsowanie japońskich er, unikniesz ręcznej manipulacji łańcuchami znaków i pozwolisz bibliotece wykonać konwersję za Ciebie. Ten przewodnik obejmuje także ostateczny krok zapisu pliku jako `.xlsx`.

## Wymagania wstępne

Zanim rozpoczniesz, upewnij się, że masz:

* Java 17 lub nowszą.
* Maven 3.6+ (lub Gradle) do zarządzania zależnościami.
* IDE, takie jak IntelliJ IDEA lub Eclipse.
* Bibliotekę Aspose.Cells for Java (przykład używa wersji 23.10, ale działa każda nowsza wersja).

## Krok 1: Dodaj Aspose.Cells do projektu

Biblioteka udostępnia klasy `Workbook`, `Worksheet` i `WorkbookSettings`, które są używane w całym tutorialu.

**Maven**

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

**Gradle**

```gradle
implementation 'com.aspose:aspose-cells:23.10:jdk17'
```

> **Pro tip:** Użyj pliku JAR `javadoc`, aby mieć pod ręką dokumentację inline podczas kodowania.

## Krok 2: Utwórz skoroszyt i uzyskaj dostęp do pierwszego arkusza

Teraz tworzymy nowy obiekt skoroszytu i pobieramy domyślny pierwszy arkusz.

```java
import com.aspose.cells.*;

public class JapaneseEraExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();                // create an empty workbook
        Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet (index 0)
```

*Dlaczego ten krok jest ważny:* `Workbook` reprezentuje cały plik Excel, natomiast `Worksheet` jest płótnem, na którym umieszczasz komórki. Rozpoczęcie od czystego skoroszytu zapewnia, że żadne ukryte formatowanie nie zakłóci parsowania dat.

## Krok 3: Wprowadź japońską datę ery do komórki

Daty w japońskim systemie ery mają wzór „<EraLetter><Year>/<Month>/<Day>”. W tym przykładzie używamy „R3” (Reiwa 3 = 2021).

```java
        // Step 3: Put a Japanese era date into cell A1
        Cell dateCell = worksheet.getCells().get("A1");
        dateCell.putValue("R3/05/01");   // Reiwa 3, May 1st
```

*Dlaczego ten krok jest ważny:* Wpisując łańcuch ery bezpośrednio, pozwalasz Aspose.Cells wykonać konwersję później. Unikasz konieczności ręcznego przeliczania „R3” na „2021”.

## Krok 4: Włącz parsowanie japońskich er i przelicz formuły

Powiedz skoroszytowi, aby traktował łańcuchy er jako daty. Po przełączeniu ustawienia wywołaj `calculateFormula()`, aby wszystkie zależne formuły (jeśli dodasz je później) zobaczyły prawidłową wartość gregoriańską.

```java
        // Step 4: Turn on Japanese era parsing
        WorkbookSettings settings = workbook.getSettings();
        settings.setUseJapaneseEra(true);   // enable era conversion
        workbook.calculateFormula();        // refresh any formulas
```

*Dlaczego ten krok jest ważny:* Flaga `setUseJapaneseEra(true)` instruuje Aspose.Cells, aby interpretował łańcuchy takie jak „R3/05/01” jako daty gregoriańskie. Bez niej komórka zachowałaby dosłowny tekst, co zepsułoby dalsze obliczenia.

## Krok 5: Zweryfikuj konwersję i **zapisz skoroszyt jako xlsx**

Wypisz przekonwertowaną wartość na konsolę i zapisz skoroszyt.

```java
        // Step 5: Verify conversion and save the file
        System.out.println("Converted date: " + dateCell.getStringValue()); // → 2021-05-01
        workbook.save("JapaneseEra.xlsx");   // saves as .xlsx by default
    }
}
```

**Oczekiwany wynik w konsoli**

```
Converted date: 2021-05-01
```

Plik `JapaneseEra.xlsx` zawiera teraz datę gregoriańską `2021‑05‑01` w komórce A1, mimo że źródłowy łańcuch używał formatu japońskiej ery.

## Krok 6: Typowe warianty i obsługa przypadków brzegowych

| Scenariusz | Jak dostosować kod |
|------------|--------------------|
| Inna era (np. Heisei) | Użyj „H30/12/31” dla Heisei 30 = 2018‑12‑31. Ta sama flaga `setUseJapaneseEra(true)` działa dla wszystkich obsługiwanych er. |
| Pusty lub niepoprawny łańcuch | Owiń `putValue` w blok try‑catch i zwaliduj przy pomocy wyrażenia regularnego takiego jak `^[RHS][0-9]+/[0-9]{2}/[0-9]{2}$`. |
| Konieczność zachowania oryginalnego łańcucha ery do audytu | Przechowaj surowy łańcuch w ukrytej kolumnie przed konwersją, a następnie ukryj tę kolumnę w finalnym skoroszycie. |
| Duże zestawy danych | Włącz `WorkbookSettings.setEnableThreadedCalculation(true)`, aby przyspieszyć przeliczanie formuł przy wielu wierszach używających dat er. |

> **Uwaga:** Użycie starszej wersji Aspose.Cells, która nie obsługuje japońskich er (przed 2020) spowoduje zignorowanie flagi `setUseJapaneseEra`, pozostawiając komórkę niezmienioną.

## Krok 7: Uruchom przykład

Skompiluj i uruchom klasę w IDE lub z wiersza poleceń:

```bash
javac -cp "path/to/aspose-cells-23.10.jar" JapaneseEraExample.java
java -cp ".:path/to/aspose-cells-23.10.jar" JapaneseEraExample
```

Po wykonaniu otwórz `JapaneseEra.xlsx` w Excelu. Komórka A1 pokazuje `2021-05-01`, potwierdzając, że **konwersja dat w Javie do Excela** zakończyła się sukcesem.

## Podsumowanie

Teraz wiesz, jak **tworzyć skoroszyt Excel w Javie**, wprowadzać daty w japońskim systemie ery, włączać automatyczne parsowanie er oraz **zapisować skoroszyt jako xlsx**. To podejście eliminuje ręczną arytmetykę dat i zapewnia, że Twoje pliki Excel pozostają zgodne ze standardowymi kalendarzami gregoriańskimi.

### Co warto zbadać dalej

* **Formatowanie dat** – zastosuj style komórek (`Style style = workbook.createStyle(); style.setNumber(14);`), aby wyświetlać daty w wybranej lokalizacji.
* **Masowa konwersja** – iteruj po kolumnie łańcuchów er i konwertuj każdą komórkę w pętli.
* **Eksport do innych formatów** – Aspose.Cells obsługuje także PDF, CSV i ODS; wystarczy zmienić rozszerzenie pliku w `workbook.save(...)`.

Śmiało eksperymentuj z innymi erami, własnymi formatami lub łącz tę technikę z raportami opartymi na formułach. Powodzenia w kodowaniu!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletny, działający kod wraz z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/french/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}