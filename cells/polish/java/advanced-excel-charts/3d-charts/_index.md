---
date: 2026-08-21
description: Dowiedz się, jak wyeksportować chart jako image i tworzyć 3D pie charts
  w Java przy użyciu Aspose.Cells. Generuj 3D bar charts, dodawaj 3D charts do Excel
  i zapisuj workbooks jako XLSX.
keywords:
- export chart as image
- 3d pie chart java
- 3d bar chart java
- save workbook as xlsx
- add 3d chart excel
lastmod: 2026-08-21
linktitle: Utwórz 3D Pie Chart w Java
og_description: Export chart jako image i twórz 3D pie charts w Java przy użyciu Aspose.Cells.
  Przewodnik krok po kroku dotyczący generowania 3D bar i pie charts, ich dostosowywania
  oraz zapisywania workbooks jako XLSX.
og_image_alt: Developer guide showing how to export a 3D chart as an image with Aspose.Cells
  for Java
og_title: Export chart jako image i utwórz 3D pie chart w Java
schemas:
- author: Aspose
  dateModified: '2026-08-21'
  description: Learn how to export chart as image and create 3D pie charts in Java
    with Aspose.Cells. Generate 3D bar charts, add 3D charts to Excel, and save workbooks
    as XLSX.
  headline: How to export chart as image and create 3D pie chart in Java
  type: TechArticle
- questions:
  - answer: Use `chart.getNSeries().add()` for each series range and ensure the chart
      type remains 3‑D (e.g., `ChartType.BAR_3_D` or `ChartType.PIE_3_D`).
    question: How can I add multiple data series to a 3D chart?
  - answer: Yes, you can save the chart as PNG, JPEG, or PDF by calling the appropriate
      `chart.toImage()` overload or `workbook.save()` with an image or PDF format,
      satisfying the **convert chart png** requirement.
    question: Can I export 3D charts created with Aspose.Cells for Java to other formats?
  - answer: Aspose.Cells focuses on static Excel charts. For interactive web‑based
      3‑D visualizations, consider coupling Excel data with JavaScript libraries such
      as Three.js.
    question: Is it possible to create interactive 3D charts with Aspose.Cells for
      Java?
  - answer: Absolutely. Load new data into the worksheet programmatically and refresh
      the chart range; the next time the workbook is opened, the chart reflects the
      updated values.
    question: Can I automate the process of updating data in my 3D charts?
  - answer: 'You can find comprehensive documentation and resources for Aspose.Cells
      for Java at the website: [Aspose.Cells for Java Documentation](https://reference.aspose.com/cells/java/).'
    question: Where can I find more resources and documentation for Aspose.Cells for
      Java?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- export chart as image
- 3d pie chart
- Aspose.Cells Java
- Excel chart automation
title: Jak wyeksportować chart jako image i utworzyć 3D pie chart w Java
url: /pl/java/advanced-excel-charts/3d-charts/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz wykres kołowy 3D w Javie

## Wprowadzenie do wykresów 3D

Aspose.Cells for Java to potężne API Java do pracy z plikami Excel, które umożliwia łatwe **create 3d pie chart** projekty oraz klasyczne wizualizacje słupków 3‑D. W tym samouczku zobaczysz dokładnie, jak **export chart as image**, wygenerować wykres słupkowy 3‑D, dostosować to samo podejście do wykresu kołowego 3‑D, spersonalizować wygląd i w końcu **add 3d chart excel** do swoich raportów. Niezależnie od tego, czy tworzysz finansowy pulpit nawigacyjny, arkusz wydajności sprzedaży, czy wizualizujesz dane naukowe, poniższe kroki zapewnią solidne podstawy.

## Szybkie odpowiedzi
- **Jakiej biblioteki potrzebuję?** Aspose.Cells for Java (latest version)  
- **Czy mogę wygenerować wykres słupkowy 3D?** Tak – użyj `ChartType.BAR_3_D`  
- **Czy potrzebuję licencji?** Ważna licencja usuwa ograniczenia wersji próbnej  
- **Jakie wersje Excela są obsługiwane?** Wszystkie główne wersje od 2003 do 2023  
- **Czy można wyeksportować wykres jako obraz?** Tak – wywołaj `chart.toImage()` po utworzeniu wykresu  

## Czym są wykresy 3D?

Wykresy 3D dodają głębi tradycyjnym wizualizacjom 2D, pomagając odbiorcom lepiej zrozumieć wielowymiarowe zależności. Są szczególnie przydatne, gdy trzeba porównać kilka kategorii obok siebie, zachowując przejrzystą hierarchię wizualną. Dodanie trzeciego wymiaru pozwala wykresom uwydatnić różnice w wielkościach, które w płaskich reprezentacjach mogą być mniej widoczne, co ułatwia interpretację złożonych danych interesariuszom biznesowym.

## Dlaczego używać Aspose.Cells for Java do generowania wykresu słupkowego 3D?

Aspose.Cells for Java oferuje ponad 150 wbudowanych typów wykresów i obsługuje ponad 100 funkcji Excela, zapewniając w pełni funkcjonalny silnik działający we wszystkich wersjach Excela od 2003 do 2023 bez konieczności posiadania Microsoft Office. Oznacza to, że możesz **generate 3d bar chart** obiekty programowo, uzyskując przewidywalne wyniki i minimalny narzut.

## Konfiguracja Aspose.Cells for Java

### Pobieranie i instalacja

Możesz pobrać bibliotekę Aspose.Cells for Java z oficjalnej strony. Postępuj zgodnie z podanymi instrukcjami Maven/Gradle lub dodaj plik JAR bezpośrednio do classpathu swojego projektu.

### Inicjalizacja licencji

Klasa `License` służy do zastosowania licencji Aspose.Cells i odblokowania pełnej funkcjonalności.  
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

Wypełnij arkusz przykładowymi danymi, do których będzie się odnosił wykres:  
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

## Jak wygenerować wykres słupkowy 3D w Javie

Aby utworzyć wykres słupkowy 3D, dodajesz obiekt wykresu do arkusza, ustawiasz jego typ na `ChartType.BAR_3_D`, a następnie wiążesz serię danych z komórkami zawierającymi wartości. Po skonfigurowaniu wyglądu wykresu możesz go renderować lub wyeksportować w razie potrzeby.  
```java
int chartIndex = worksheet.getCharts().add(ChartType.BAR_3_D, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Setting the data range for the chart
chart.getNSeries().add("A2:B4", true);

// Customizing chart attributes
chart.getChartArea().getBorder().setVisible(false);
chart.getChartTitle().setText("3D Bar Chart");
```

## Zapisywanie wykresu do pliku

Na koniec zapisz skoroszyt (który teraz zawiera wykres 3‑D) na dysku. To także **save workbook xlsx** w standardowym formacie Excel:  
```java
workbook.save("3D_Chart.xlsx");
```

## Jak utworzyć wykres kołowy 3D przy użyciu Aspose.Cells for Java

Jeśli potrzebujesz wizualizacji w stylu kołowym, przepływ pracy jest prawie identyczny — zmienia się tylko enum `ChartType`. Zastąp `ChartType.BAR_3_D` przez `ChartType.PIE_3_D` przy dodawaniu wykresu i wskaż serię na ten sam zakres danych. Po utworzeniu wykresu możesz ustawić opisowy tytuł, dostosować kolory kawałków i wyeksportować wynik jako obraz. Takie podejście pozwala ponownie wykorzystać ten sam kod przygotowujący dane, jednocześnie dostarczając innej perspektywy wizualnej.

## Jak wyeksportować wykres jako obraz w Javie

Metoda `toImage` obiektu `Chart` zapisuje wykres jako plik obrazu. Możesz wyeksportować dowolny wykres 3D do obrazu rastrowego jednym wywołaniem: `chart.toImage("myChart.png", ImageFormat.getPng())`. Metoda ta renderuje wykres dokładnie tak, jak wygląda w Excelu, zachowując głębię 3‑D, kolory i legendy, i zapisuje wynik w określonej ścieżce pliku. Użyj PNG dla jakości bezstratnej lub JPEG dla mniejszych rozmiarów plików przy osadzaniu obrazu w raportach internetowych.

## Różne typy wykresów 3D

Aspose.Cells for Java obsługuje kilka rodzajów wykresów 3D, które możesz **add 3d chart excel** plikami:

- **Wykresy słupkowe** – idealne do porównywania kategorii.  
- **Wykresy kołowe** – pokazują proporcjonalny udział (w tym kołowy 3D).  
- **Wykresy liniowe** – ilustrują trendy w czasie.  
- **Wykresy obszarowe** – podkreślają wielkość zmian.  

Możesz przełączyć enum `ChartType` na dowolny z powyższych, zachowując ten sam wzorzec tworzenia.

## Zaawansowana personalizacja wykresów

### Dodawanie tytułów i etykiet

Nadaj wykresowi kontekst, ustawiając opisowy tytuł i etykiety osi.

### Dostosowywanie kolorów i stylów

Użyj metody `chart.getSeries().get(i).getArea().setForegroundColor(Color.getRGB(...))`, aby dopasować kolory do identyfikacji wizualnej firmy.

### Praca z osiami wykresu

Dopracuj skale osi, interwały i znaczniki, aby poprawić czytelność.

### Dodawanie legend

Włącz legendy za pomocą `chart.getLegend().setVisible(true)`, aby odbiorcy mogli zidentyfikować każdą serię danych.

### Eksportowanie wykresów jako obrazy

Gdy potrzebujesz statycznego obrazu do raportu internetowego, wywołaj `chart.toImage("chart.png", ImageFormat.getPng())`. Spełnia to przypadek użycia **convert chart png** bez opuszczania skoroszytu.

## Integracja danych

Aspose.Cells for Java może pobierać dane z baz danych, plików CSV lub żywych API. Po prostu wypełnij komórki arkusza pobranymi danymi przed połączeniem zakresu z wykresem. To utrzymuje Twój przepływ pracy **add 3d chart excel** dynamiczny i aktualny.

## Podsumowanie

W tym przewodniku przeprowadziliśmy Cię przez proces tworzenia projektów **create 3d pie chart** i **create 3d bar chart** od początku do końca — konfigurację biblioteki, dodawanie danych, generowanie wykresu słupkowego 3‑D, dostosowanie tych samych kroków do wykresu kołowego 3‑D oraz zastosowanie zaawansowanego stylu. Dzięki Aspose.Cells for Java masz niezawodny, niezależny od wersji sposób na osadzanie bogatych wizualizacji 3‑D bezpośrednio w skoroszytach Excel oraz **export chart as image** do użycia w pulpitach nawigacyjnych lub raportach.

## Najczęściej zadawane pytania

**Q: Jak mogę dodać wiele serii danych do wykresu 3D?**  
A: Użyj `chart.getNSeries().add()` dla każdego zakresu serii i upewnij się, że typ wykresu pozostaje 3‑D (np. `ChartType.BAR_3_D` lub `ChartType.PIE_3_D`).

**Q: Czy mogę wyeksportować wykresy 3D stworzone przy użyciu Aspose.Cells for Java do innych formatów?**  
A: Tak, możesz zapisać wykres jako PNG, JPEG lub PDF, wywołując odpowiednie przeciążenie `chart.toImage()` lub `workbook.save()` z formatem obrazu lub PDF, spełniając wymóg **convert chart png**.

**Q: Czy można tworzyć interaktywne wykresy 3D przy użyciu Aspose.Cells for Java?**  
A: Aspose.Cells koncentruje się na statycznych wykresach Excel. Do interaktywnych wizualizacji 3‑D w sieci rozważ połączenie danych z Excela z bibliotekami JavaScript, takimi jak Three.js.

**Q: Czy mogę zautomatyzować proces aktualizacji danych w moich wykresach 3D?**  
A: Oczywiście. Ładuj nowe dane do arkusza programowo i odśwież zakres wykresu; przy następnym otwarciu skoroszytu wykres odzwierciedli zaktualizowane wartości.

**Q: Gdzie mogę znaleźć więcej zasobów i dokumentacji dla Aspose.Cells for Java?**  
A: Kompletną dokumentację i zasoby dla Aspose.Cells for Java znajdziesz na stronie: [Dokumentacja Aspose.Cells for Java](https://reference.aspose.com/cells/java/).

---

**Ostatnia aktualizacja:** 2026-08-21  
**Testowano z:** Aspose.Cells for Java 24.12 (latest)  
**Autor:** Aspose

## Powiązane samouczki

- [Utwórz wykresy kołowe w Excelu przy użyciu Aspose.Cells for Java: Kompletny przewodnik](/cells/java/charts-graphs/master-pie-chart-creation-excel-aspose-cells-java/)
- [aspose cells java – Tworzenie wykresu Excel z adnotacjami](/cells/java/advanced-excel-charts/chart-annotations/)
- [Dodaj etykiety danych do wykresu Excel przy użyciu Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}