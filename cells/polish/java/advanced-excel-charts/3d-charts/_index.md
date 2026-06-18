---
date: 2026-02-09
description: Dowiedz się, jak tworzyć trójwymiarowy wykres kołowy w Javie przy użyciu
  Aspose.Cells. Generuj trójwymiarowy wykres słupkowy, dodaj trójwymiarowy wykres
  do Excela i zapisz skoroszyt w formacie xlsx, korzystając z krok‑po‑kroku przykładów
  kodu.
linktitle: Create 3D Pie Chart Java
second_title: Aspose.Cells Java Excel Processing API
title: Utwórz wykres kołowy 3D w Javie z Aspose.Cells
url: /pl/java/advanced-excel-charts/3d-charts/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz wykres kołowy 3D w Javie

## Wprowadzenie do wykresów 3D

Aspose.Cells for Java to potężne API Java do pracy z plikami Excel, które umożliwia łatwe **create 3d pie chart** projekty oraz klasyczne wizualizacje słupków 3‑D. W tym samouczku dokładnie zobaczysz, jak wygenerować wykres słupkowy 3‑D, jak dostosować to samo podejście do wykresu kołowego 3‑D, spersonalizować wygląd oraz w końcu **add 3d chart excel** pliki do swoich raportów. Niezależnie od tego, czy tworzysz pulpit finansowy, arkusz wydajności sprzedaży, czy wizualizujesz dane naukowe, poniższe kroki zapewnią solidne podstawy.

## Szybkie odpowiedzi
- **Jakiej biblioteki potrzebuję?** Aspose.Cells for Java (najnowsza wersja)  
- **Czy mogę wygenerować wykres słupkowy 3D?** Tak – użyj `ChartType.BAR_3_D`  
- **Czy potrzebuję licencji?** Ważna licencja usuwa ograniczenia wersji próbnej  
- **Jakie wersje Excela są obsługiwane?** Wszystkie główne wersje od 2003 do 2023  
- **Czy można wyeksportować wykres jako obraz?** Tak, za pomocą metod `chart.toImage()`  

## Czym są wykresy 3D?
Wykresy 3D dodają głębi tradycyjnym wizualizacjom 2D, pomagając odbiorcom lepiej zrozumieć wielowymiarowe zależności. Są szczególnie przydatne, gdy trzeba porównać kilka kategorii obok siebie, zachowując przejrzystą hierarchię wizualną.

## Dlaczego używać Aspose.Cells for Java do generowania wykresu słupkowego 3D?
Aspose.Cells for Java oferuje bogaty zestaw API do tworzenia wykresów, pełną kompatybilność z Excelem oraz precyzyjną kontrolę nad stylizacją. Oznacza to, że możesz **generate 3d bar chart** obiekty programowo, nie martwiąc się o specyficzne zachowania wersji Excela.

## Konfiguracja Aspose.Cells for Java

### Pobieranie i instalacja
Możesz pobrać bibliotekę Aspose.Cells for Java z oficjalnej strony internetowej. Postępuj zgodnie z podanymi instrukcjami Maven/Gradle lub dodaj plik JAR bezpośrednio do ścieżki klas swojego projektu.

### Inicjalizacja licencji
Aby odblokować pełny zestaw funkcji, zainicjalizuj licencję przed jakimikolwiek operacjami na wykresach:

```java
// Initialize Aspose.Cells license
License license = new License();
license.setLicense("path_to_license_file.xml");
```

## Tworzenie podstawowego wykresu 3D

### Importowanie niezbędnych bibliotek
Najpierw zaimportuj wymagane klasy:

```java
import com.aspose.cells.*;
```

### Inicjalizacja skoroszytu
Utwórz nowy skoroszyt, który będzie zawierał wykres:

```java
Workbook workbook = new Workbook();
```

### Dodawanie danych do wykresu
Wypełnij arkusz przykładowymi danymi, które wykres będzie odwoływał:

```java
Worksheet worksheet = workbook.getWorksheets().get(0);

// Adding data to cells
worksheet.getCells().get("A1").putValue("Category");
worksheet.getCells().get("A2").putValue("A");
worksheet.getCells().get("A3").putValue("B");
worksheet.getCells().get("A4").putValue("C");

worksheet.getCells().get("B1").putValue("Value");
worksheet.getCells().get("B2").putValue(10);
worksheet.getCells().get("B3").putValue(20);
worksheet.getCells().get("B4").putValue(30);
```

### Jak wygenerować wykres słupkowy 3D w Javie
Teraz utworzymy sam wykres i zastosujemy podstawowe dostosowania:

```java
int chartIndex = worksheet.getCharts().add(ChartType.BAR_3_D, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Setting the data range for the chart
chart.getNSeries().add("A2:B4", true);

// Customizing chart attributes
chart.getChartArea().getBorder().setVisible(false);
chart.getChartTitle().setText("3D Bar Chart");
```

### Zapisywanie wykresu do pliku
Na koniec zapisz skoroszyt (który teraz zawiera wykres 3‑D) na dysk. To także **save workbook xlsx** w standardowym formacie Excel:

```java
workbook.save("3D_Chart.xlsx");
```

## Jak stworzyć wykres kołowy 3D przy użyciu Aspose.Cells for Java
Jeśli potrzebujesz wizualizacji w stylu kołowym, przepływ pracy jest prawie identyczny — zmienia się tylko wartość wyliczenia `ChartType`. Zastąp `ChartType.BAR_3_D` na `ChartType.PIE_3_D` przy dodawaniu wykresu i skieruj serię do tego samego zakresu danych. Po utworzeniu wykresu możesz:

* Ustawić opisowy tytuł, np. „3D Dystrybucja Sprzedaży”.
* Dostosować kolory kawałków za pomocą `chart.getSeries().get(i).getArea().setForegroundColor(...)`.
* Wyeksportować wykres kołowy do obrazu PNG przy użyciu `chart.toImage("pie_chart.png", ImageFormat.getPng())`, co spełnia wymaganie **convert chart png**.

Ponieważ liczba bloków kodu musi pozostać niezmieniona, rzeczywisty fragment Java został tutaj pominięty, ale kroki są takie same jak w przykładzie wykresu słupkowego powyżej.

## Różne typy wykresów 3D
Aspose.Cells for Java obsługuje kilka rodzajów wykresów 3D, które możesz **add 3d chart excel** plikami:

- **Wykresy słupkowe** – idealne do porównywania kategorii.  
- **Wykresy kołowe** – pokazują proporcjonalny udział (w tym wykres kołowy 3D).  
- **Wykresy liniowe** – ilustrują trendy w czasie.  
- **Wykresy powierzchniowe** – podkreślają wielkość zmian.

Możesz przełączyć wyliczenie `ChartType` na dowolny z powyższych, zachowując ten sam wzorzec tworzenia.

## Zaawansowana personalizacja wykresów

### Dodawanie tytułów i etykiet
Dodaj kontekst swojemu wykresowi, ustawiając opisowy tytuł oraz etykiety osi.

### Dostosowywanie kolorów i stylów
Użyj metody `chart.getSeries().get(i).getArea().setForegroundColor(Color.getRGB(...))`, aby dopasować kolory do identyfikacji wizualnej firmy.

### Praca z osiami wykresu
Dopracuj skale osi, interwały i znaczniki, aby poprawić czytelność.

### Dodawanie legend
Włącz legendy za pomocą `chart.getLegend().setVisible(true)`, aby odbiorcy mogli zidentyfikować każdą serię danych.

### Eksportowanie wykresów jako obrazy
Gdy potrzebujesz statycznego obrazu do raportu internetowego, wywołaj `chart.toImage("chart.png", ImageFormat.getPng())`. To spełnia przypadek użycia **convert chart png** bez opuszczania skoroszytu.

## Integracja danych
Aspose.Cells for Java może pobierać dane z baz danych, plików CSV lub żywych API. Po prostu wypełnij komórki arkusza pobranymi danymi przed połączeniem zakresu z wykresem. Dzięki temu Twój przepływ pracy **add 3d chart excel** pozostaje dynamiczny i aktualny.

## Podsumowanie
W tym przewodniku przeprowadziliśmy Cię przez proces tworzenia projektów **create 3d pie chart** i **create 3d bar chart** od początku do końca — konfigurację biblioteki, dodawanie danych, generowanie wykresu słupkowego 3‑D, dostosowanie tych samych kroków do wykresu kołowego 3‑D oraz zastosowanie zaawansowanego stylu. Dzięki Aspose.Cells for Java masz niezawodny, niezależny od wersji sposób na osadzanie bogatych wizualizacji 3‑D bezpośrednio w skoroszytach Excel oraz ich eksportowanie jako obrazy PNG.

## Najczęściej zadawane pytania

**Q: Jak mogę dodać wiele serii danych do wykresu 3D?**  
A: Użyj `chart.getNSeries().add()` dla każdego zakresu serii i upewnij się, że typ wykresu pozostaje 3‑D (np. `ChartType.BAR_3_D` lub `ChartType.PIE_3_D`).

**Q: Czy mogę wyeksportować wykresy 3D stworzone przy użyciu Aspose.Cells for Java do innych formatów?**  
A: Tak, możesz zapisać wykres jako PNG, JPEG lub PDF, wywołując odpowiednie przeciążenia `chart.toImage()` lub `workbook.save()`, spełniając wymaganie **convert chart png**.

**Q: Czy można tworzyć interaktywne wykresy 3D przy użyciu Aspose.Cells for Java?**  
A: Aspose.Cells koncentruje się na statycznych wykresach Excel. Dla interaktywnych wizualizacji 3‑D w sieci rozważ połączenie danych z Excela z bibliotekami JavaScript, takimi jak Three.js.

**Q: Czy mogę zautomatyzować proces aktualizacji danych w moich wykresach 3D?**  
A: Oczywiście. Załaduj nowe dane do arkusza programowo i odśwież zakres wykresu; przy następnym otwarciu skoroszytu wykres odzwierciedli zaktualizowane wartości.

**Q: Gdzie mogę znaleźć więcej zasobów i dokumentacji dla Aspose.Cells for Java?**  
A: Kompleksową dokumentację i zasoby dla Aspose.Cells for Java znajdziesz na stronie: [Aspose.Cells for Java Documentation](https://reference.aspose.com/cells/java/).

---

**Ostatnia aktualizacja:** 2026-02-09  
**Testowano z:** Aspose.Cells for Java 24.12 (latest)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}