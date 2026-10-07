---
category: general
date: 2026-06-21
description: Programowo kopiuj zakres arkusza w Javie przy użyciu Aspose.Cells. Dowiedz
  się, jak efektywnie skopiować zakres Excela do innego skoroszytu.
draft: false
keywords:
- programmatically copy worksheet range
- how to copy excel range to another workbook
- Aspose.Cells copy range Java
- copy pivot table between workbooks
- Java Excel automation
language: pl
og_description: Programowo kopiuj zakres arkusza w Javie. Ten przewodnik pokazuje,
  jak skopiować zakres Excela do innego skoroszytu, zawierając pełny kod i wskazówki.
og_title: Programowo kopiowanie zakresu arkusza – Java krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Programmatically copy worksheet range in Java using Aspose.Cells. Learn
    how to copy excel range to another workbook efficiently.
  headline: Programmatically Copy Worksheet Range – Complete Java Guide
  type: TechArticle
- description: Programmatically copy worksheet range in Java using Aspose.Cells. Learn
    how to copy excel range to another workbook efficiently.
  name: Programmatically Copy Worksheet Range – Complete Java Guide
  steps:
  - name: 1. Copying Across Different Excel Versions
    text: Aspose.Cells works with `.xls`, `.xlsx`, `.xlsb`, and even `.csv`. If the
      source and destination use different formats, the library automatically converts
      them. Just ensure the file extensions match your desired output.
  - name: 2. Preserving External Data Sources in Pivot Tables
    text: If the pivot table in the source references an external data source (e.g.,
      a database connection), the copied pivot will retain the connection string but
      **won’t automatically refresh**. Call `pivotTable.refreshData()` after copying
      if you need up‑to‑date results.
  - name: 3. Large Ranges and Memory Consumption
    text: Copying massive ranges (hundreds of thousands of rows) can spike memory
      usage. Use `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` before
      loading large files to keep the footprint low.
  - name: 4. Multiple Sheets or Ranges
    text: If you need to copy several non‑contiguous ranges, repeat steps 4‑6 for
      each range, or use `copyRange` with a union range (`Cells.createRange("A1:B10,C1:D10")`).
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Workbook
- Automation
title: Programowe kopiowanie zakresu arkusza – kompletny przewodnik Java
url: /pl/java/range-management/programmatically-copy-worksheet-range-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Programowo kopiowanie zakresu arkusza – kompletny przewodnik Java

Zastanawiałeś się kiedyś, jak **programowo kopiować zakres arkusza** bez ręcznego otwierania Excela? Nie jesteś jedyny. Niezależnie od tego, czy musisz zduplikować raport, sklonować pulpit nawigacyjny oparty na tabeli przestawnej, czy po prostu przenieść dane między plikami, wykonanie tego w kodzie oszczędza czas i eliminuje błędy ludzkie.

W tym samouczku przeprowadzimy Cię przez czyste, kompleksowe rozwiązanie, które pokazuje **jak skopiować zakres Excel do innego skoroszytu** przy użyciu Javy i biblioteki Aspose.Cells. Po zakończeniu będziesz mieć gotowy do uruchomienia program, zrozumiesz powody poszczególnych kroków i poznasz pułapki, na które trzeba uważać.

---

## Czego będziesz potrzebować

- **Java Development Kit (JDK) 11+** – kod kompiluje się na dowolnym aktualnym JDK.
- **Aspose.Cells for Java** (bezpłatna wersja próbna lub licencjonowana). Dodaj zależność Maven lub pobierz plik JAR.
- Dwa pliki Excel: `input.xlsx` zawierający zakres źródłowy (w tym tabelę przestawną) oraz pusty `output.xlsx`, do którego zostanie skopiowany zakres.
- Dowolne IDE, które lubisz – IntelliJ IDEA, Eclipse lub nawet prosty edytor tekstu.

To wszystko. Bez dodatkowych usług, bez interfejsu COM, po prostu czysta Java.

---

![Diagram ilustrujący programowe kopiowanie zakresu arkusza między dwoma skoroszytami](image.png)

*Tekst alternatywny obrazu: ilustracja programowego kopiowania zakresu arkusza*

---

## Krok 1: Konfiguracja projektu i import Aspose.Cells

Na początek potrzebujemy biblioteki w classpath. Jeśli używasz Maven, dodaj:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

Jeśli wolisz ręcznie używać pliku JAR, umieść go w folderze `libs` i dodaj do ścieżki kompilacji.

Dlaczego to ważne: Aspose.Cells udostępnia bogaty model obiektowy (`Workbook`, `Worksheet`, `Range`), który pozwala kopiować dane **w tym tabele przestawne, formuły i formatowanie** w jednym wywołaniu — coś, czego zwykła biblioteka Apache POI nie potrafi zrobić tak elegancko.

---

## Krok 2: Załaduj źródłowy skoroszyt

Otworzymy skoroszyt, który zawiera dane, które chcemy sklonować. Konstruktor `Workbook` przyjmuje ścieżkę do pliku, a Aspose odczyta cały plik do pamięci.

```java
import com.aspose.cells.*;

public class CopyWorksheetRange {
    public static void main(String[] args) throws Exception {
        // Load the source workbook containing the data and pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Wskazówka:* Owiń ładowanie w blok try‑catch, jeśli plik może być nieobecny; w przeciwnym razie program zakończy się z czytelnym błędem.

---

## Krok 3: Utwórz pusty docelowy skoroszyt

Nowy skoroszyt zapewnia czyste płótno. Nie musimy wstępnie wypełniać żadnych arkuszy; Aspose doda jeden za nas.

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();
```

Dlaczego nie używać źródła ponownie? Trzymanie ich osobno zapobiega przypadkowym nadpisaniom i sprawia, że kod jest wielokrotnego użytku w operacjach wsadowych.

---

## Krok 4: Zdefiniuj dokładny zakres do skopiowania

Tutaj zaczyna się magia **programowego kopiowania zakresu arkusza**. Wybieramy komórki `A1:D20` z pierwszego arkusza pliku źródłowego. Metoda `createRange` zwraca obiekt `Range`, który dokładnie reprezentuje te komórki, w tym tabele przestawne.

```java
        // Define the range to copy (A1:D20) from the first worksheet of the source
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)               // first sheet (index 0)
                                          .getCells()
                                          .createRange("A1:D20");
```

Jeśli potrzebujesz dynamicznego zakresu (np. „ostatni używany wiersz”), możesz zastąpić sztywno zakodowany adres metodą `Cells.maxDisplayRange` lub obliczyć go przy użyciu `Cells.getMaxDataColumn()` i `Cells.getMaxDataRow()`.

---

## Krok 5: Dodaj docelowy arkusz w skoroszycie docelowym

Aspose tworzy domyślny arkusz o nazwie „Sheet1” przy tworzeniu `Workbook`. Dodamy nowy, aby utrzymać porządek, zwłaszcza jeśli planujesz później kopiować wiele zakresów.

```java
        // Add a new worksheet to the destination workbook where the range will be placed
        Worksheet targetWorksheet = destinationWorkbook.getWorksheets().add();
```

Możesz nadać arkuszowi przyjazną nazwę:

```java
        targetWorksheet.setName("CopiedData");
```

---

## Krok 6: Wykonaj kopiowanie – w tym tabele przestawne

Teraz główna operacja: `copyRange`. Ta metoda kopiuje **wartości, formuły, formatowanie i osadzone obiekty** (np. tabele przestawne) ze źródłowego zakresu do komórki docelowej (`A1` w naszym nowym arkuszu). To najprostszy sposób, aby osiągnąć **jak skopiować zakres Excel do innego skoroszytu** bez manipulacji niskopoziomowymi pętlami komórek.

```java
        // Copy the defined range (including the pivot table) to cell A1 of the new worksheet
        sourceWorkbook.getWorksheets()
                      .get(0)               // source sheet index
                      .getCells()
                      .copyRange(sourceRange, targetWorksheet, "A1");
```

Za kulisami Aspose serializuje źródłowy zakres do formatu pośredniego, a następnie deserializuje go w arkuszu docelowym — dzięki czemu wszystko pozostaje nienaruszone.

---

## Krok 7: Zapisz docelowy skoroszyt i zweryfikuj

Na koniec zapisujemy docelowy skoroszyt na dysku. Otwórz `output.xlsx` w Excelu, aby zobaczyć skopiowany zakres, tabelę przestawną i zachowane formatowanie.

```java
        // (Optional) Save the destination workbook to verify the result
        destinationWorkbook.save("YOUR_DIRECTORY/output.xlsx");
        System.out.println("Range copied successfully!");
    }
}
```

Po otwarciu `output.xlsx` powinieneś zobaczyć arkusz o nazwie „CopiedData” z taką samą strukturą jak `A1:D20` ze źródła, w tym tabelę przestawną, która teraz wskazuje na skopiowane dane.

---

## Obsługa typowych przypadków brzegowych

### 1. Kopiowanie pomiędzy różnymi wersjami Excela

Aspose.Cells obsługuje `.xls`, `.xlsx`, `.xlsb`, a nawet `.csv`. Jeśli źródło i docelowy plik używają różnych formatów, biblioteka automatycznie je konwertuje. Upewnij się tylko, że rozszerzenia plików odpowiadają pożądanemu wynikowi.

### 2. Zachowanie zewnętrznych źródeł danych w tabelach przestawnych

Jeśli tabela przestawna w źródle odwołuje się do zewnętrznego źródła danych (np. połączenia bazodanowego), skopiowana tabela zachowa ciąg połączenia, ale **nie odświeży się automatycznie**. Wywołaj `pivotTable.refreshData()` po skopiowaniu, jeśli potrzebujesz aktualnych wyników.

```java
        PivotTable pt = targetWorksheet.getPivotTables().get(0);
        pt.refreshData();
        pt.calculateData();
```

### 3. Duże zakresy i zużycie pamięci

Kopiowanie ogromnych zakresów (setki tysięcy wierszy) może zwiększyć zużycie pamięci. Użyj `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` przed ładowaniem dużych plików, aby utrzymać niski ślad pamięciowy.

### 4. Wiele arkuszy lub zakresów

Jeśli musisz skopiować kilka nieciągłych zakresów, powtórz kroki 4‑6 dla każdego zakresu lub użyj `copyRange` z zakresem unii (`Cells.createRange("A1:B10,C1:D10")`).

---

## Wskazówki profesjonalne dla solidnej automatyzacji

- **Sprawdź poprawność zakresu źródłowego** przed kopiowaniem. Użyj `sourceRange.isValid()`, aby uniknąć błędów w czasie wykonywania.
- **Zablokuj plik docelowy** przy pomocy `FileInfo.setReadOnly(false)`, jeśli nadpisujesz istniejący skoroszyt.
- **Loguj działania** przy użyciu lekkiego loggera (SLF4J) – szczególnie przydatne przy przetwarzaniu wsadów.
- **Zwolnij zasoby skoroszytów** (`sourceWorkbook.dispose(); destinationWorkbook.dispose();`) w długotrwałych usługach, aby uwolnić zasoby natywne.

---

## Pełny działający przykład – podsumowanie

Poniżej znajduje się kompletny, samodzielny kod klasy Java, który możesz wkleić do swojego IDE i uruchomić. Pamiętaj, aby zamienić `YOUR_DIRECTORY` na rzeczywistą ścieżkę folderu na swoim komputerze.

```java
import com.aspose.cells.*;

public class CopyWorksheetRange {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook containing the data and pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2️⃣ Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // 3️⃣ Define the range to copy (A1:D20) from the first worksheet of the source
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)
                                          .getCells()
                                          .createRange("A1:D20");

        // 4️⃣ Add a new worksheet to the destination workbook where the range will be placed
        Worksheet targetWorksheet = destinationWorkbook.getWorksheets().add();
        targetWorksheet.setName("CopiedData");

        // 5️⃣ Copy the defined range (including the pivot table) to cell A1 of the new worksheet
        sourceWorkbook.getWorksheets()
                      .get(0)
                      .getCells()
                      .copyRange(sourceRange, targetWorksheet, "A1");

        // 6️⃣ (Optional) Save the destination workbook to verify the result
        destinationWorkbook.save("YOUR_DIRECTORY/output.xlsx");

        System.out.println("Programmatically copy worksheet range completed successfully.");
    }
}
```

**Oczekiwany wynik:** Plik `output.xlsx` z arkuszem o nazwie „CopiedData”. Komórki `A1:D20` będą odzwierciedlały źródło, a każda tabela przestawna w tym bloku będzie w pełni funkcjonalna, wskazując na skopiowane dane.

---

## Zakończenie

Właśnie zaprezentowaliśmy czyste rozwiązanie **programowego kopiowania zakresu arkusza** w Javie, odpowiadające na powszechne pytanie **jak skopiować zakres Excel do innego skoroszytu**. Dzięki wykorzystaniu wysokopoziomowego API Aspose.Cells uniknęliśmy niskopoziomowych pętli komórek, zachowaliśmy tabele przestawne i utrzymaliśmy czytelność kodu.

Co dalej? Spróbuj rozszerzyć ten wzorzec o:
- Kopiowanie całych arkuszy zamiast pojedynczego zakresu.
- Przetwarzanie wsadowe dziesiątek skoroszytów w folderze.
- Eksport skopiowanego zakresu do CSV lub PDF w celu tworzenia raportów.

Śmiało eksperymentuj, a jeśli napotkasz problem, zostaw komentarz. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak skopiować wiele kolumn w Excelu przy użyciu Aspose.Cells Java: kompletny przewodnik](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Efektywne kopiowanie kolumn Excel przy użyciu Aspose.Cells for Java: kompleksowy przewodnik](/cells/english/java/range-management/copy-excel-columns-aspose-cells-java/)
- [Kopiowanie obrazów między arkuszami w Excelu przy użyciu Aspose.Cells for Java: kompleksowy przewodnik](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}