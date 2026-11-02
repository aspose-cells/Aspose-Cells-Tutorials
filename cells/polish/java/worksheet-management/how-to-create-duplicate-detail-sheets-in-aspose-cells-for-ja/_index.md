---
category: general
date: 2026-08-17
description: Dowiedz się, jak tworzyć duplikaty arkuszy szczegółowych przy użyciu
  Aspose.Cells dla Javy oraz zezwalać na duplikaty nazw arkuszy za pomocą SmartMarkerProcessor.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicate detail sheets
- allow duplicate sheet names
language: pl
lastmod: 2026-08-17
og_description: Utwórz duplikaty arkuszy szczegółowych w Aspose.Cells dla Javy i zezwól
  na duplikowanie nazw arkuszy. Skorzystaj z tego pełnego poradnika, aby uzyskać natychmiastowe
  wyniki.
og_image_alt: Generated Excel workbook showing multiple detail sheets with the same
  name
og_title: Tworzenie duplikatów arkuszy szczegółowych w Aspose.Cells dla Javy – przewodnik
  krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Learn how to create duplicate detail sheets with Aspose.Cells for Java
    and allow duplicate sheet names using SmartMarkerProcessor.
  headline: How to create duplicate detail sheets in Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create duplicate detail sheets with Aspose.Cells for Java
    and allow duplicate sheet names using SmartMarkerProcessor.
  name: How to create duplicate detail sheets in Aspose.Cells for Java
  steps:
  - name: Load the master template workbook.
    text: Load the master template workbook.
  - name: Configure `SmartMarkerProcessor` to **allow duplicate sheet names**.
    text: Configure `SmartMarkerProcessor` to **allow duplicate sheet names**.
  - name: Process the workbook so that a new detail sheet is created for each data
      group.
    text: Process the workbook so that a new detail sheet is created for each data
      group.
  - name: Save the resulting workbook that now contains duplicated detail sheets.
    text: Save the resulting workbook that now contains duplicated detail sheets.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Jak utworzyć zduplikowane arkusze szczegółowe w Aspose.Cells dla Javy
url: /pl/java/worksheet-management/how-to-create-duplicate-detail-sheets-in-aspose-cells-for-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak tworzyć duplikaty arkuszy szczegółowych w Aspose.Cells dla Javy

Jeśli potrzebujesz **tworzyć duplikaty arkuszy szczegółowych** w skoroszycie Excel, Aspose.Cells dla Javy umożliwia to w prosty sposób. Ten tutorial pokazuje dokładnie, jak zezwolić na duplikaty nazw arkuszy podczas generowania arkuszy szczegółowych przy użyciu SmartMarkerProcessor, abyś mógł uzyskać skoroszyt zawierający kilka arkuszy o tej samej nazwie.

Zobaczysz pełny, gotowy do uruchomienia przykład, szczegółowy opis każdej opcji konfiguracyjnej oraz wskazówki dotyczące obsługi typowych przypadków brzegowych, takich jak kolizje nazw i duże zestawy danych. Nie są wymagane żadne zewnętrzne odwołania — wszystko, co potrzebne, znajduje się w poniższym kodzie.

## Wymagania wstępne

* Java Development Kit (JDK) 8 lub nowszy.
* Maven lub Gradle do zarządzania zależnościami.
* Biblioteka Aspose.Cells for Java (wersja 23.9 lub późniejsza). Dodaj następującą zależność Maven do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

* Szablonowy skoroszyt główny (`master_template.xlsx`) zawierający region Smart Marker dla danych szczegółowych.

## Przegląd rozwiązania

Rozwiązanie składa się z czterech logicznych kroków:

1. Załaduj szablonowy skoroszyt główny.
2. Skonfiguruj `SmartMarkerProcessor`, aby **zezwalał na duplikaty nazw arkuszy**.
3. Przetwórz skoroszyt, aby dla każdej grupy danych został utworzony nowy arkusz szczegółowy.
4. Zapisz wynikowy skoroszyt, który teraz zawiera zduplikowane arkusze szczegółowe.

Każdy krok jest wyjaśniony szczegółowo poniżej, a pełny plik źródłowy znajduje się na końcu przewodnika.

## Krok 1: Załaduj szablonowy skoroszyt główny

Pierwsza operacja tworzy instancję `Workbook`, która reprezentuje plik szablonu. Szablon musi zawierać placeholder Smart Marker (np. `&=DetailData`), który instruuje procesor, gdzie wstawić dane.

```java
import com.aspose.cells.*;

public class DuplicateDetailSheet {
    public static void main(String[] args) throws Exception {
        // Load the master template workbook from the file system
        Workbook workbook = new Workbook("YOUR_DIRECTORY/master_template.xlsx");
```

**Dlaczego to ważne:** Ładowanie szablonu oddziela układ i formatowanie od logiki generowania danych, co utrzymuje kod w czystości i ułatwia ponowne użycie tego samego szablonu dla różnych zestawów danych.

## Krok 2: Skonfiguruj SmartMarkerProcessor, aby zezwalał na duplikaty nazw arkuszy

Domyślnie Aspose.Cells generuje unikalne nazwy arkuszy przy tworzeniu arkuszy szczegółowych. Aby **zezwolić na duplikaty nazw arkuszy**, ustaw opcję `DetailSheetNewName` na stałą wartość. Procesor będzie ponownie używał tej nazwy dla każdego wygenerowanego arkusza.

```java
        // Create a SmartMarkerProcessor instance
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // Enable duplicate detail sheet names by assigning a fixed name
        processor.getOptions().setDetailSheetNewName("DetailSheet");

        // Optional: if you want to keep the original sheet after processing, set this flag
        // processor.getOptions().setKeepOriginalDetailSheet(true);
```

**Dlaczego to ważne:** Ustawienie `DetailSheetNewName` informuje silnik, aby używał tej samej nazwy dla każdego arkusza szczegółowego, co bezpośrednio spełnia wymaganie **zezwolenia na duplikaty nazw arkuszy**. To podejście jest przydatne, gdy narzędzia downstream identyfikują arkusze po ich pozycji, a nie po nazwie.

## Krok 3: Przetwórz skoroszyt, aby wygenerować arkusze szczegółowe

Po skonfigurowaniu wywołaj `process` na skoroszycie. Procesor odczytuje region Smart Marker, tworzy nowy arkusz dla każdej grupy danych i wypełnia go odpowiednimi wierszami.

```java
        // Process the workbook; this creates the duplicate detail sheets
        processor.process(workbook);
```

**Dlaczego to ważne:** Wywołanie `process` wykonuje ciężką pracę — parsowanie Smart Markerów, klonowanie arkusza szablonu i wstawianie danych. Ponieważ opcja `DetailSheetNewName` jest już ustawiona, każdy nowy arkusz otrzymuje tę samą nazwę, co skutkuje duplikatami nazw arkuszy w finalnym pliku.

## Krok 4: Zapisz wynikowy skoroszyt

Na koniec zapisz zmodyfikowany skoroszyt do nowego pliku. Plik wyjściowy będzie zawierał tyle kart „DetailSheet”, ile jest grup danych.

```java
        // Save the workbook with duplicated detail sheets
        workbook.save("YOUR_DIRECTORY/duplicate_detail.xlsx");
    }
}
```

**Dlaczego to ważne:** Zapisanie pliku finalizuje zmiany wprowadzone przez procesor. Wynikowy skoroszyt może być otwarty w Microsoft Excel, LibreOffice lub dowolnej innej aplikacji arkuszy kalkulacyjnych obsługującej format XLSX.

## Pełny kod źródłowy

Łącząc wszystkie elementy, oto pełny program, który możesz skopiować, wkleić i uruchomić:

```java
import com.aspose.cells.*;

public class DuplicateDetailSheet {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the master template workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/master_template.xlsx");

        // Step 2: Create a SmartMarkerProcessor and allow duplicate detail sheet names
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.getOptions().setDetailSheetNewName("DetailSheet"); // same name allowed for each detail sheet

        // Step 3: Process the workbook to generate the detail sheets
        processor.process(workbook);

        // Step 4: Save the resulting workbook with duplicated detail sheets
        workbook.save("YOUR_DIRECTORY/duplicate_detail.xlsx");
    }
}
```

### Oczekiwany wynik

Po otwarciu `duplicate_detail.xlsx` zobaczysz wiele kart o nazwie **DetailSheet**. Każda karta zawiera zestaw danych odpowiadający konkretnej grupie Smart Marker w szablonie. Układ, formatowanie i formuły z szablonu głównego są zachowane w każdym zduplikowanym arkuszu.

## Radzenie sobie z typowymi problemami

| Problem | Wyjaśnienie | Rozwiązanie |
|-------|-------------|--------|
| Excel wyświetla ostrzeżenie o duplikatach nazw arkuszy | Excel zezwala na duplikaty nazw, ale może wyświetlić ostrzeżenie przy otwieraniu pliku. | Ostrzeżenie jest nieszkodliwe; skoroszyt działa poprawnie. Jeśli chcesz je wyeliminować, zmień nazwy arkuszy po przetworzeniu, używając `Workbook.getWorksheets().get(i).setName("DetailSheet" + i);`. |
| Duże zestawy danych powodują wysokie zużycie pamięci | Każdy zduplikowany arkusz tworzy pełną kopię szablonu, co może zużywać pamięć RAM. | Włącz tryb strumieniowy za pomocą `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);` przed załadowaniem szablonu. |
| Nie znaleziono regionu Smart Marker | Procesor nie może znaleźć `&=DetailData` w szablonie. | Sprawdź, czy składnia placeholdera odpowiada źródłu danych oraz czy arkusz szablonu nie jest ukryty. |

## Porada profesjonalna: dostosowywanie schematu nazewnictwa duplikatów

Jeśli potrzebujesz przewidywalnego wzorca nazewnictwa, jednocześnie zezwalając na duplikaty, połącz nazwę bazową z indeksem:

```java
processor.getOptions().setDetailSheetNewName("DetailSheet_{0}");
```

Placeholder `{0}` jest zastępowany indeksem arkusza, tworząc nazwy takie jak `DetailSheet_1`, `DetailSheet_2` itd. To nadal spełnia wymaganie **zezwolenia na duplikaty nazw arkuszy**, ponieważ nazwa bazowa pozostaje stała.

## Kolejne kroki

Teraz, gdy możesz **tworzyć duplikaty arkuszy szczegółowych**, możesz zgłębić następujące tematy:

* **Wypełnianie arkuszy szczegółowych obrazami** – użyj obiektów `Picture`, aby osadzić loga lub wykresy.
* **Zastosowanie formatowania warunkowego** – dodaj reguły `FormatCondition`, aby podświetlać wiersze w zależności od wartości.
* **Eksport do PDF** – wywołaj `workbook.save("output.pdf", SaveFormat.PDF);`, aby wygenerować wersję PDF zduplikowanych arkuszy.

Każde z tych rozszerzeń opiera się na tym samym przepływie pracy Smart Marker przedstawionym tutaj, pozwalając automatyzować złożone zadania raportowania w Excelu z pewnością.

---

*Nauczyłeś się, jak tworzyć duplikaty arkuszy szczegółowych w Aspose.Cells dla Javy oraz jak zezwalać na duplikaty nazw arkuszy przy użyciu SmartMarkerProcessor. Zastosuj kod, dostosuj szablon i zintegrować technikę w swoich pipeline'ach raportowania.*

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera pełne działające przykłady kodu z krok po kroku wyjaśnieniami, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Utwórz i uzyskaj dostęp do arkuszy Excel, dodaj zakładki PDF przy użyciu Aspose.Cells dla Java](/cells/english/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [Utwórz i uzyskaj dostęp do arkuszy Excel, dodaj zakładki PDF Aspose Cells Java](/cells/german/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [Utwórz i uzyskaj dostęp do arkuszy Excel, dodaj zakładki PDF Aspose Cells Java](/cells/french/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}