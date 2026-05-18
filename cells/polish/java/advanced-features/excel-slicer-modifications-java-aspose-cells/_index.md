---
date: '2026-05-18'
description: Dowiedz się, jak dodać slicer do tabeli przestawnej w Excel przy użyciu
  Aspose.Cells for Java — wczytywać skoroszyty, dostosowywać slicery i efektywnie
  zapisywać pliki Excel.
keywords:
- add slicer to pivot
- save excel file java
- load excel workbook java
- Aspose.Cells Java
- Excel slicer automation
schemas:
- author: Aspose
  dateModified: '2026-05-18'
  description: Learn how to add slicer to pivot in Excel using Aspose.Cells for Java—load
    workbooks, customize slicers, and save Excel files efficiently.
  headline: How to Add Slicer to Pivot in Excel Using Aspose.Cells for Java
  type: TechArticle
- questions:
  - answer: Yes, it handles formulas, charts, pivot tables, conditional formatting,
      and more across 50+ formats.
    question: Does Aspose.Cells support other Excel features besides slicers?
  - answer: Absolutely. Aspose.Cells works with Java 8, 11, 17, and 21.
    question: Is the library compatible with Java 11 and newer?
  - answer: Yes. Because Aspose.Cells is pure Java, it runs on any OS with a compatible
      JVM.
    question: Can I run this code on a Linux server?
  - answer: Call `slicer.setStyleType(SlicerStyleType.YOUR_CHOSEN_STYLE);` where the
      enum provides dozens of predefined styles.
    question: How do I apply a custom style to a slicer?
  - answer: The Aspose.Cells documentation and the official GitHub repository contain
      extensive examples for slicers, pivot tables, and chart automation.
    question: Where can I find more code samples?
  type: FAQPage
title: Jak dodać slicer do tabeli przestawnej w Excel przy użyciu Aspose.Cells for
  Java
url: /pl/java/advanced-features/excel-slicer-modifications-java-aspose-cells/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj segmentator do tabeli przestawnej w Excelu przy użyciu Aspose.Cells dla Javy

## Wprowadzenie

Jeśli chcesz **dodać segmentator do tabeli przestawnej** programowo, Aspose.Cells dla Javy zapewnia czysto‑Java API, które obsługuje segmentatory bez potrzeby Microsoft Office. W wielu projektach raportowych programiści spędzają godziny na ręcznym dostosowywaniu segmentatorów; dzięki tej bibliotece możesz zautomatyzować te zmiany w ciągu kilku sekund, poprawić spójność i utrzymać swoje pulpity na bieżąco we wszystkich środowiskach. Ten przewodnik przeprowadzi Cię przez wyświetlanie informacji o wersji, **ładowanie skoroszytu Excel w Javie**, dostęp do arkuszy, dostosowywanie właściwości segmentatora oraz ostatecznie **zapisywanie pliku Excel w Javie** z wprowadzonymi aktualizacjami.

## Szybkie odpowiedzi
- **Jaka biblioteka umożliwia automatyzację segmentatora?** Aspose.Cells for Java  
- **Czy mogę dodać segmentator do tabeli przestawnej programowo?** Tak – użyj klasy `Slicer`  
- **Czy wymagana jest licencja do produkcji?** Bezpłatna wersja próbna działa w ocenie; licencja jest potrzebna do użytku komercyjnego  
- **Jakie wersje Javy są wspierane?** JDK 8 i nowsze (w tym 11, 17, 21)  
- **Gdzie znaleźć zależność Maven?** W Maven Central pod `com.aspose:aspose-cells`

## Co oznacza „dodaj segmentator do tabeli przestawnej” w tym kontekście?

**Dodaj segmentator do tabeli przestawnej** oznacza programowe tworzenie lub modyfikowanie segmentatora, który kontroluje kryteria filtrowania tabeli przestawnej, umożliwiając użytkownikom końcowym interaktywne segmentowanie danych. Korzystając z API Aspose.Cells, możesz określić pozycję segmentatora, styl i powiązane pola, a następnie podłączyć go do jednej lub wielu tabel przestawnych, tak aby zmiany wprowadzone przez segmentator natychmiast filtrowały podstawowe dane bez ręcznej interwencji.

## Dlaczego używać Aspose.Cells do automatyzacji segmentatorów w Excelu?

Aspose.Cells obsługuje **ponad 50 formatów wejścia i wyjścia** i może przetwarzać skoroszyty z **do 10 000 wierszy** bez ładowania całego pliku do pamięci, zapewniając wysoką wydajność automatyzacji na Windows, Linux i macOS. Biblioteka daje pełną kontrolę nad wyglądem segmentatora, stylem i powiązanymi tabelami przestawnymi, eliminując zależności COM i zmniejszając obciążenie w czasie działania.

## Wymagania wstępne

- Java Development Kit (JDK) 8 lub wyższy  
- IDE, takie jak IntelliJ IDEA lub Eclipse  
- Maven lub Gradle do zarządzania zależnościami  

### Wymagane biblioteki i zależności

Użyjemy Aspose.Cells dla Javy, potężnej biblioteki umożliwiającej manipulację plikami Excel w aplikacjach Java. Poniżej znajdują się szczegóły instalacji:

**Maven:**

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Uzyskanie licencji

Aspose.Cells dla Javy oferuje bezpłatną wersję próbną, aby rozpocząć. W przypadku intensywnego użycia możesz uzyskać tymczasową licencję lub zakupić pełną licencję. Odwiedź [purchase Aspose](https://purchase.aspose.com/buy), aby poznać dostępne opcje.

## Konfiguracja Aspose.Cells dla Javy

Dodaj niezbędne instrukcje importu na początku swoich plików Java:

```java
import com.aspose.cells.*;
```

Upewnij się, że katalogi danych są poprawnie ustawione:

```java
String dataDir = "YOUR_DATA_DIRECTORY";
String outDir = "YOUR_OUTPUT_DIRECTORY";
```

## Jak dodać segmentator do tabeli przestawnej w Excelu przy użyciu Aspose.Cells?

Aby dodać segmentator, najpierw załaduj skoroszyt, znajdź arkusz zawierający docelową tabelę przestawną, a następnie utwórz obiekt `Slicer` powiązany z tą tabelą. Skonfiguruj jego styl, pozycję oraz pole, które filtruje, i na końcu zapisz skoroszyt. Ta sekwencja zapewnia, że segmentator jest w pełni funkcjonalny i prawidłowo powiązany z tabelą przestawną, oferując użytkownikom końcowym interaktywne filtrowanie.

### Wyświetlanie wersji Aspose.Cells dla Javy

Klasa `VersionInfo` dostarcza aktualną wersję biblioteki Aspose.Cells.  
```java
public class VersionDisplay {
    public static void displayVersion() throws Exception {
        System.out.println("Aspose.Cells for Java Version: " + CellsHelper.getVersion());
    }
}
```

### Ładowanie skoroszytu Excel w Javie

Klasa `Workbook` reprezentuje cały plik Excel załadowany do pamięci.  
```java
public class LoadExcelFile {
    public static Workbook loadWorkbook() throws Exception {
        return new Workbook(dataDir + "/sampleFormattingSlicer.xlsx");
    }
}
```

### Dostęp do arkusza

Obiekt `Worksheet` odpowiada pojedynczemu arkuszowi w skoroszycie.  
```java
public class AccessWorksheet {
    public static Worksheet getFirstWorksheet(Workbook wb) throws Exception {
        return wb.getWorksheets().get(0);
    }
}
```

### Dostosowanie segmentatora w pulpicie Excel

Klasa `Slicer` kapsułkuje segmentator powiązany z tabelą przestawną, umożliwiając dostosowanie filtrów.  
```java
public class ModifySlicerProperties {
    public static void configureSlicer(Worksheet ws) throws Exception {
        Slicer slicer = ws.getSlicers().get(0);
        
        // Set number of columns displayed by the slicer
        slicer.setNumberOfColumns(2);
        
        // Change the style type for better visual appeal
        slicer.setStyleType(SlicerStyleType.SLICER_STYLE_LIGHT_6);
    }
}
```

### Zapisz plik Excel w Javie

Metoda `save` klasy `Workbook` zapisuje zmodyfikowany skoroszyt do pliku.  
```java
public class SaveWorkbook {
    public static void saveModifiedWorkbook(Workbook wb) throws Exception {
        wb.save(outDir + "/outputFormattingSlicer.xlsx", SaveFormat.XLSX);
    }
}
```

## Częste problemy i rozwiązania

- **Segmentator nie pojawia się po zapisaniu:** Upewnij się, że segmentator jest powiązany z istniejącą tabelą przestawną i że `setShowHeader` jest ustawione na `true`.  
- **Opóźnienie wydajności przy dużych plikach:** Przetwarzaj tylko wymagane arkusze i wyłącz automatyczne przeliczanie za pomocą `WorkbookSettings.setRecalcMode(RecalcMode.Manual)`.  
- **Styl nie został zastosowany:** Sprawdź, czy wybrany `SlicerStyleType` jest obsługiwany w docelowej wersji Excela.

## Najczęściej zadawane pytania

**Q: Czy Aspose.Cells obsługuje inne funkcje Excela oprócz segmentatorów?**  
A: Tak, obsługuje formuły, wykresy, tabele przestawne, formatowanie warunkowe i wiele innych w ponad 50 formatach.

**Q: Czy biblioteka jest kompatybilna z Java 11 i nowszymi?**  
A: Zdecydowanie. Aspose.Cells działa z Java 8, 11, 17 i 21.

**Q: Czy mogę uruchomić ten kod na serwerze Linux?**  
A: Tak. Ponieważ Aspose.Cells jest czystą Javą, działa na każdym systemie operacyjnym z kompatybilną JVM.

**Q: Jak zastosować niestandardowy styl do segmentatora?**  
A: Wywołaj `slicer.setStyleType(SlicerStyleType.YOUR_CHOSEN_STYLE);`, gdzie enum dostarcza dziesiątki predefiniowanych stylów.

**Q: Gdzie mogę znaleźć więcej przykładów kodu?**  
A: Dokumentacja Aspose.Cells oraz oficjalne repozytorium GitHub zawierają obszerne przykłady dla segmentatorów, tabel przestawnych i automatyzacji wykresów.

## Zakończenie

W tym samouczku nauczyłeś się, jak **dodać segmentator do tabeli przestawnej** w Excelu przy użyciu Aspose.Cells dla Javy — sprawdzając wersję biblioteki, **ładowanie skoroszytu Excel w Javie**, uzyskując dostęp do właściwego arkusza, **dostosowując segmentator w pulpicie Excel**, oraz ostatecznie **zapisując plik Excel w Javie**. Automatyzując te kroki, możesz tworzyć dynamiczne, interaktywne pulpity bez ręcznego wysiłku.

**Kolejne kroki:**  
- Eksperymentuj z różnymi wartościami `SlicerStyleType`, aby dopasować je do identyfikacji wizualnej Twojej firmy.  
- Połącz automatyzację segmentatorów z odświeżaniem danych tabel przestawnych, aby uzyskać w pełni dynamiczne pipeline'y raportowania.  

Gotowy, aby wdrożyć te techniki w swoim projekcie? Spróbuj już dziś!

---

**Last Updated:** 2026-05-18  
**Tested With:** Aspose.Cells 25.3 for Java  
**Author:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Powiązane samouczki

- [Opanuj Aspose.Cells dla Javy: Efektywne ładowanie i dostęp do tabel przestawnych w Excelu](/cells/java/data-analysis/aspose-cells-java-load-pivot-tables/)
- [Zapisz plik Excel w Javie i zaktualizuj segmentatory przy użyciu Aspose.Cells](/cells/java/advanced-features/update-slicers-java-excel-aspose-cells/)
- [Odśwież segmentator w Excelu i dostosuj go przy użyciu Aspose.Cells dla Javy](/cells/java/advanced-features/customize-slicers-excel-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}