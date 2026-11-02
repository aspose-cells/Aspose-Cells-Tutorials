---
category: general
date: 2026-06-30
description: Dynamiczne formuły tablicowe w Javie pozwalają budować potężne arkusze
  Excel. Naucz się tworzyć skoroszyt Excel w Javie i szybko obliczać wszystkie formuły.
draft: false
keywords:
- dynamic array formulas
- calculate all formulas
- use lambda formula
- use expand function
- create excel workbook java
language: pl
og_description: Dynamiczne formuły tablicowe w Javie upraszczają automatyzację Excela.
  Ten przewodnik pokazuje, jak stworzyć skoroszyt Excela w Javie, używać funkcji EXPAND,
  formuły lambda oraz obliczać wszystkie formuły.
og_title: Dynamiczne formuły tablicowe w Javie – Tworzenie skoroszytu i obliczanie
  formuł
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Dynamic array formulas in Java let you build powerful Excel sheets.
    Learn to create Excel workbook Java and calculate all formulas quickly.
  headline: 'Dynamic Array Formulas in Java: Create Excel Workbook and Calculate All
    Formulas'
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: 'Dynamiczne formuły tablicowe w Javie: Tworzenie skoroszytu Excel i obliczanie
  wszystkich formuł'
url: /pl/java/calculation-engine/dynamic-array-formulas-in-java-create-excel-workbook-and-cal/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Formuły dynamicznych tablic w Javie: Tworzenie skoroszytu Excel i obliczanie wszystkich formuł

Zastanawiałeś się kiedyś, jak działają **dynamic array formulas**, gdy automatyzujesz Excel z Javy? Nie jesteś sam — wielu programistów napotyka problem, gdy muszą wstawić zaawansowane formuły takie jak `EXPAND` czy `REDUCE` do skoroszytu bez otwierania samego Excela.  

Dobre wieści? Kilka linii kodu w Javie pozwala **create Excel workbook Java** w stylu, wstawić te nowoczesne funkcje tablicowe, a następnie **calculate all formulas** jednocześnie. W tym samouczku przeprowadzimy Cię przez każdy krok, wyjaśnimy *dlaczego* każdy element ma znaczenie i dostarczymy kompletny, gotowy do uruchomienia przykład, który możesz skopiować‑wkleić bezpośrednio do swojego projektu.

## Czego się nauczysz

- Jak utworzyć nowy skoroszyt Excel przy użyciu Javy (tak, bez interfejsu Excela).  
- Mechanikę działania funkcji `EXPAND` i to, jak zamienia prosty zakres w dynamiczną tablicę.  
- Jak **use lambda formula** z `REDUCE` do własnych agregacji.  
- Dodawanie funkcji trygonometrycznych i hiperbolicznych (`COT`, `COTH`), które wielu zapomina, że istnieją w zestawie formuł Excela.  
- Jednolinijkowy kod potrzebny do **calculate all formulas**, aby skoroszyt odzwierciedlał najnowsze wyniki.  

> **Wymagania wstępne:** Java 8+ (dla obsługi lambd), biblioteka Aspose.Cells for Java oraz podstawowa znajomość formuł Excel. Nie są potrzebne inne zależności.

---

## Formuły dynamicznych tablic: przygotowanie skoroszytu

Na początek — uzyskajmy obiekt skoroszytu. Klasa `Workbook` z Aspose.Cells jest Twoim punktem wejścia; traktuj ją jak czyste płótno, na którym będą umieszczane wszystkie formuły dynamicznych tablic.

```java
import com.aspose.cells.*;

public class DynamicArrayDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.getWorksheets().get(0); // default sheet is Sheet1
```

*Dlaczego to ważne:* Programowe tworzenie skoroszytu daje pełną kontrolę nad formatem pliku, ustawieniami kultury i — co najważniejsze — oceną formuł bez konieczności zapisywania czegokolwiek na dysku.

---

## Użycie funkcji EXPAND do rozszerzania zakresów

Funkcja `EXPAND` to odpowiedź Excela na „rozlanie” (spill) zakresu na większy obszar w oparciu o podany rozmiar. Idealna, gdy źródłowe dane mogą zmieniać długość w czasie wykonywania.

```java
        // Step 2: Add a formula that expands B1:B3 into a 5‑row, 1‑column array
        worksheet.getCells().get("A1").setFormula("=EXPAND(B1:B3,5,1)");
```

*Wyjaśnienie:*  
- `B1:B3` to zakres źródłowy.  
- `5` mówi Excelowi, aby wygenerował pięć wierszy, nawet jeśli źródło jest krótsze.  
- `1` wymusza jedną kolumnę.  

Gdy później **calculate all formulas**, wynik w `A1` będzie pionowym rozlanem pięciu wartości, wypełniając puste komórki w razie potrzeby.

---

## Zastosowanie formuły LAMBDA z REDUCE

Jeśli kiedykolwiek chciałeś zsumować kolumnę, ale potrzebujesz własnego akumulatora, `REDUCE` połączony z **lambda formula** jest rozwiązaniem. Składnia może wydawać się nieco nietypowa, ale to po prostu sposób Javy na osadzenie małej anonimowej funkcji wewnątrz formuły Excela.

```java
        // Step 3: Add a REDUCE formula that sums the values in B1:B5
        worksheet.getCells().get("A2").setFormula(
            "=REDUCE(0,B1:B5,LAMBDA(a,b,a+b))"
        );
```

*Dlaczego warto używać?*  
- `0` to początkowa wartość (seed).  
- `B1:B5` to tablica, nad którą „składamy”.  
- `LAMBDA(a,b,a+b)` oznacza „weź akumulator `a` i kolejny element `b`, zwróć ich sumę”.  

Możesz zamienić `a+b` na dowolną własną logikę — średnią, maksymalną wartość, a nawet konkatenację ciągów — co czyni `REDUCE` wszechstronnym elementem konstrukcyjnym.

---

## Dodawanie funkcji trygonometrycznych (COT, COTH)

Excel zawiera kilka pomocniczych funkcji trygonometrycznych, które często są pomijane. Oto jak wstawić prosty cotangens i jego hiperboliczny odpowiednik do arkusza.

```java
        // Step 4: COT of π/4 (equals 1)
        worksheet.getCells().get("A3").setFormula("=COT(PI()/4)");

        // Step 5: COTH of 2 (hyperbolic cotangent)
        worksheet.getCells().get("A4").setFormula("=COTH(2)");
```

*Wskazówka:* Funkcje te automatycznie respektują tryb obliczeń skoroszytu, więc nie musisz dodatkowo konwertować stopni na radiany — `PI()` wykona ciężką pracę.

---

## Obliczanie wszystkich formuł w skoroszycie

Teraz, gdy formuły są już w miejscu, musimy **calculate all formulas**, aby komórki zawierały rzeczywiste wartości, a nie jedynie tekst formuły. Aspose.Cells realizuje to jednym wywołaniem metody.

```java
        // Step 6: Force evaluation of every formula in the workbook
        workbook.calculateFormula();

        // Optional: Save to disk to see the result
        workbook.save("DynamicArrayDemo.xlsx");
    }
}
```

*Co dzieje się pod maską?* Biblioteka przegląda każdą komórkę, rozwiązuje zależności i rozlewa wyniki tablic tam, gdzie jest to potrzebne. Jeśli pracujesz z bardzo dużymi arkuszami, możesz dostosować opcje obliczeń pod kątem wydajności, ale domyślne ustawienia sprawdzają się w większości scenariuszy.

---

## Pełny działający przykład (gotowy do kopiowania)

Poniżej znajduje się cały program, gotowy do wklejenia do IDE. Zawiera importy, metodę `main` oraz końcowe wywołanie `save`, dzięki czemu możesz otworzyć wygenerowany plik w Excelu i zobaczyć rozlania.

```java
import com.aspose.cells.*;

public class DynamicArrayDemo {
    public static void main(String[] args) throws Exception {
        // Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Populate source data for demonstration
        worksheet.getCells().get("B1").putValue(10);
        worksheet.getCells().get("B2").putValue(20);
        worksheet.getCells().get("B3").putValue(30);
        worksheet.getCells().get("B4").putValue(40);
        worksheet.getCells().get("B5").putValue(50);

        // EXPAND: spill B1:B3 into a 5‑row array
        worksheet.getCells().get("A1").setFormula("=EXPAND(B1:B3,5,1)");

        // REDUCE with LAMBDA: sum B1:B5
        worksheet.getCells().get("A2").setFormula("=REDUCE(0,B1:B5,LAMBDA(a,b,a+b))");

        // Trig functions
        worksheet.getCells().get("A3").setFormula("=COT(PI()/4)");
        worksheet.getCells().get("A4").setFormula("=COTH(2)");

        // Evaluate everything
        workbook.calculateFormula();

        // Save the file for inspection
        workbook.save("DynamicArrayDemo.xlsx");
    }
}
```

**Oczekiwany wynik po otwarciu `DynamicArrayDemo.xlsx`:**

| A (Wynik) | B (Źródło) |
|-----------|------------|
| 10        | 10 |
| 20        | 20 |
| 30        | 30 |
| (pusty)   | 40 |
| (pusty)   | 50 |
| 150 (suma)|   |
| 1 (cot)   |   |
| 1.0373… (coth) | |

*Zauważ, że `A1` rozlewa pięć wierszy, mimo że źródło miało tylko trzy wartości. To moc **dynamic array formulas**.*

---

## Częste pułapki i wskazówki dla zaawansowanych

- **Nie zapomnij ustawić trybu obliczeń**, jeśli wyłączyłeś automatyczne obliczanie gdzie indziej; w przeciwnym razie `calculateFormula()` nie zrobi nic.  
- **Kolizje rozlewania tablic:** Jeśli inna komórka już zajmuje zakres rozlania, Excel zwróci błąd `#SPILL!`. W kodzie możesz wcześniej wyczyścić docelowy obszar przy pomocy `worksheet.getCells().clear(0, 0, maxRow, maxColumn)`.  
- **Dziwactwa składni Lambda:** Funkcja `LAMBDA` wymaga parametrów oddzielonych przecinkami, a nie średnikami. Brak przecinka spowoduje, że cała formuła nie zostanie prawidłowo sparsowana.  
- **Wskazówka wydajnościowa:** Przy pracy z tysiącami wierszy wywołaj `workbook.getSettings().setCalculateFormulaOnOpen(false)` przed masowym wstawianiem danych, a następnie ponownie włącz ją przed ostatecznym wywołaniem `calculateFormula()`.

---

## Kolejne kroki

Teraz, gdy opanowałeś **dynamic array formulas**, rozważ zgłębienie:

- funkcji **`FILTER`** i **`SORT`** do kształtowania danych w locie.  
- **`SEQUENCE`** do generowania liczbowych tablic bez potrzeby źródłowego zakresu.  
- używania **nazwanych zakresów** razem z `EXPAND` dla czystszych, wielokrotnego użytku formuł.  

Wszystkie te elementy opierają się na koncepcjach, które omówiliśmy — wystarczy podmienić ciąg formuły i pozwolić Aspose.Cells wykonać ciężką pracę.

---

## Zakończenie

W tym przewodniku pokazaliśmy dokładnie, jak **create Excel workbook Java**,

## Co powinieneś nauczyć się dalej?

Poniższe samouczki dotyczą ściśle powiązanych tematów, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz szczegółowe wyjaśnienia krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Utwórz skoroszyt Excel przy użyciu Aspose.Cells w Javie: przewodnik krok po kroku](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Obliczanie formuł Excel w Javie: optymalizacja z Aspose.Cells](/cells/english/java/calculation-engine/optimize-excel-aspose-cells-java-calculation-chains/)
- [Opanuj formuły tablicowe Excel z Aspose.Cells Java: usprawnij obliczenia i formatowanie](/cells/english/java/formulas-functions/aspose-cells-java-array-formulas-custom-calculations/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}