---
category: general
date: 2026-08-20
description: Naucz się eksportować Excel do TXT, ograniczając liczbę miejsc po przecinku,
  zachowując istotne cyfry i zapisując skoroszyt jako TXT przy użyciu Javy.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- limit decimal places
- keep significant digits
- save workbook as txt
language: pl
lastmod: 2026-08-20
og_description: Eksportuj Excel do TXT za pomocą Aspose.Cells. Ten przewodnik pokazuje,
  jak ograniczyć liczbę miejsc po przecinku, zachować istotne cyfry i zapisać skoroszyt
  jako TXT w Javie.
og_image_alt: Result of export excel to txt showing limited decimal places and kept
  significant digits
og_title: Eksportuj Excel do TXT w Javie – kontroluj miejsca dziesiętne i cyfry znaczące
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn to export Excel to TXT while limiting decimal places, keeping
    significant digits, and saving workbook as TXT using Java.
  headline: How to export Excel to TXT with Aspose.Cells and control decimal precision
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Text export
title: Jak wyeksportować Excel do TXT przy użyciu Aspose.Cells i kontrolować precyzję
  dziesiętną
url: /pl/java/excel-import-export/how-to-export-excel-to-txt-with-aspose-cells-and-control-dec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wyeksportować Excel do TXT przy użyciu Aspose.Cells i kontrolować precyzję dziesiętną

Jeśli potrzebujesz **export Excel to TXT** i zapewnić, że wynik respektuje określoną liczbę miejsc po przecinku, ten przewodnik oferuje pełne rozwiązanie. Zobaczysz, jak ograniczyć miejsca po przecinku, zachować istotne cyfry oraz **save workbook as TXT** przy użyciu biblioteki Aspose.Cells dla Javy.

Samouczek przeprowadza przez tworzenie skoroszytu, wstawianie wartości o wysokiej precyzji, konfigurowanie opcji zapisu TXT oraz zapisywanie pliku na dysku. Po zakończeniu będziesz mógł wygenerować plik tekstowy zawierający dokładnie wymaganą precyzję, bez ręcznego przetwarzania.

## Czego będziesz potrzebować

- Java 17 (lub dowolny obsługiwany JDK)
- Aspose.Cells for Java 23.10 lub nowszy
- IDE lub narzędzie budujące (Maven/Gradle) do zarządzania zależnościami
- Uprawnienia do zapisu w katalogu wyjściowym

## Krok 1: Utwórz skoroszyt i uzyskaj dostęp do pierwszego arkusza

Utworzenie skoroszytu jest pierwszym krokiem, gdy chcesz **export Excel to TXT**. Klasa `Workbook` reprezentuje cały plik Excel, a `Worksheet` daje dostęp do komórek.

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
```

*Dlaczego to ważne*: Obiekt workbook zawiera wszystkie dane, style i metadane. Rozpoczęcie od nowego skoroszytu gwarantuje, że żadne ukryte formatowanie nie zakłóci eksportu tekstu.

## Krok 2: Dodaj wartość numeryczną i ogranicz miejsca po przecinku

Wstaw liczbę z wieloma miejscami po przecinku, aby móc pokazać, jak **limit decimal places** podczas eksportu.

```java
        // Put a high‑precision number into cell A1
        sheet.getCells().putValue("A1", 0.000123456789);
```

*Dlaczego to ważne*: Excel przechowuje pełną precyzję, ale przy późniejszym eksporcie możesz chcieć przyciąć lub zaokrąglić wartość. Ustawienie `limit decimal places` obsłuży to automatycznie.

## Krok 3: Skonfiguruj opcje zapisu TXT, aby zachować istotne cyfry

Aspose.Cells udostępnia `TxtSaveOptions`. Ustawienie `significantDigits` instruuje eksportera, aby zachował tylko wymaganą liczbę istotnych cyfr, ignorując wiodące zera.

```java
        // Configure TXT export options
        TxtSaveOptions txtOptions = new TxtSaveOptions();

        // Keep exactly 5 significant digits (e.g., 0.00012346)
        txtOptions.setSignificantDigits(5);
```

*Dlaczego to ważne*: Opcja **keep significant digits** zapewnia, że plik wyjściowy zawiera przewidywalną ilość precyzji, co jest niezbędne dla systemów downstream oczekujących stałej szerokości formatu liczbowego.

## Krok 4: Zapisz skoroszyt jako TXT

Na koniec zapisz skoroszyt do pliku tekstowego. Metoda `save` respektuje skonfigurowane opcje, więc wynikowy plik będzie zawierał ograniczoną reprezentację dziesiętną.

```java
        // Define the output path (replace with your own directory)
        String outputPath = "output/SignificantDigits.txt";

        // Export the workbook to TXT using the configured options
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

*Dlaczego to ważne*: Użycie **save workbook as txt** z przygotowanymi `TxtSaveOptions` gwarantuje, że wyeksportowany plik spełnia ograniczenia precyzji ustawione w poprzednim kroku.

### Oczekiwana zawartość pliku `SignificantDigits.txt`

```
0.00012346
```

Wartość pokazuje pięć istotnych cyfr (`12346`) po zaokrągleniu, a wiodące zera są zachowane zgodnie z formatem TXT.

## Warianty i przypadki brzegowe

| Scenariusz | Dostosowanie |
|----------|------------|
| **Inna liczba istotnych cyfr** | Call `txtOptions.setSignificantDigits(n)` where `n` is 1‑15. |
| **Eksportowanie zakresu zamiast całego arkusza** | Use `txtOptions.setExportRange("A1:B10")` before saving. |
| **Zachowanie separatorów kolumn** | Set `txtOptions.setSeparator('\t')` for tab‑delimited output. |
| **Duże arkusze** | Increase `txtOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCES)` to avoid `OutOfMemoryError`. |

## Częste pułapki i profesjonalne wskazówki

- **Nie myl istotnych cyfr z miejscami po przecinku**. Wiodące zera nie są liczone jako istotne; użyj `setSignificantDigits` dla znaczącej precyzji i `setDecimalPlaces`, jeśli potrzebujesz stałej liczby cyfr po przecinku.
- **Zawsze podawaj bezwzględną ścieżkę wyjściową** podczas uruchamiania z IDE, aby uniknąć błędów uprawnień.
- **Zweryfikuj wygenerowany plik** przy użyciu prostego wywołania `java.nio.file.Files.readAllLines(Paths.get(outputPath))`, aby upewnić się, że zawartość spełnia oczekiwania przed przekazaniem go do procesów downstream.

## Pełny kod źródłowy jako odniesienie

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Step 2: Insert a high‑precision number (will be limited later)
        sheet.getCells().putValue("A1", 0.000123456789);

        // Step 3: Set TXT options – keep 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(5);   // keep significant digits

        // Step 4: Save the workbook as TXT
        String outputPath = "output/SignificantDigits.txt";
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

Uruchomienie programu generuje `SignificantDigits.txt` zawierający jedną linię `0.00012346`, co pokazuje, że proces **export excel to txt** respektuje zarówno wymagania **limit decimal places**, jak i **keep significant digits**.

## Zakończenie

Teraz wiesz, jak **export Excel to TXT** przy użyciu Aspose.Cells dla Javy, kontrolując precyzję liczb. Konfigurując `TxtSaveOptions`, możesz **limit decimal places**, **keep significant digits** i niezawodnie **save workbook as txt** bez dodatkowego przetwarzania.

Następnie możesz zbadać:

- Eksportowanie wielu arkuszy do osobnych plików TXT (`save workbook as txt` per sheet)
- Użycie `setSeparator` do tworzenia wyjścia kompatybilnego z CSV
- Automatyzacja konwersji wsadowych dla dużych zestawów danych

Śmiało eksperymentuj z różnymi liczbami cyfr i separatorami, aby dopasować je do dokładnych potrzeb Twojego projektu. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletny działający kod z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Save Excel as Text – Complete C# Guide to Export Excel to TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}