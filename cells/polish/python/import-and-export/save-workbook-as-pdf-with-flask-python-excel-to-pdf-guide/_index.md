---
category: general
date: 2026-06-21
description: Zapisz skoroszyt jako PDF przy użyciu Flask i Aspose.Cells w Pythonie
  – dowiedz się, jak konwertować XLSX na PDF, automatycznie dopasowywać kolumny Excela
  i zwracać plik za pomocą flask send_file pdf.
draft: false
keywords:
- save workbook as pdf
- convert xlsx to pdf
- python excel to pdf
- auto fit excel columns
- flask send_file pdf
language: pl
og_description: Zapisz skoroszyt jako PDF w Pythonie przy użyciu Flask. Ten krok‑po‑kroku
  poradnik pokazuje, jak przekonwertować XLSX na PDF, automatycznie dopasować kolumny
  Excela i udostępnić wynik za pomocą flask send_file pdf.
og_title: Zapisz skoroszyt jako PDF przy użyciu Flask – Kompletny przewodnik Pythona
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Save workbook as PDF using Flask and Aspose.Cells in Python – learn
    how to convert XLSX to PDF, auto‑fit Excel columns, and return the file with flask
    send_file pdf.
  headline: Save Workbook as PDF with Flask – Python Excel to PDF Guide
  type: TechArticle
- description: Save workbook as PDF using Flask and Aspose.Cells in Python – learn
    how to convert XLSX to PDF, auto‑fit Excel columns, and return the file with flask
    send_file pdf.
  name: Save Workbook as PDF with Flask – Python Excel to PDF Guide
  steps:
  - name: Why Each Piece Matters
    text: '- **`request.files.get("file")`** – Safely fetches the uploaded file; using
      `.get` avoids a `KeyError` if the field is missing. - **`io.BytesIO`** – Keeps
      everything in RAM, so we never write temporary files to disk. This is crucial
      for scalability. - **`auto_fit_columns()`** – Without this, column '
  - name: Manual Test with cURL
    text: '```bash curl -X POST http://localhost:5000/convert  -F "file=@sample.xlsx"  -o
      result.pdf ```'
  - name: Automated Test with Python’s `requests`
    text: '```python import requests'
  type: HowTo
tags:
- flask
- python
- excel
- pdf
- aspose-cells
title: 'Zapisz skoroszyt jako PDF z Flask – Przewodnik Python: Excel do PDF'
url: /pl/python/import-and-export/save-workbook-as-pdf-with-flask-python-excel-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zapisz skoroszyt jako PDF przy użyciu Flask – Przewodnik Python Excel do PDF

Potrzebujesz **save workbook as PDF** z usługi webowej? Nie jesteś jedynym, który zastanawia się, jak zamienić przesłany plik Excel w elegancki PDF w locie. W tym przewodniku przeprowadzimy Cię przez zapisywanie skoroszytu jako PDF przy użyciu Flask i Aspose.Cells, a także omówimy, jak **convert XLSX to PDF**, automatycznie dopasować kolumny Excel oraz ostatecznie dostarczyć wynik za pomocą `flask send_file pdf`.

Zaczniemy od świeżego projektu Flask, dodamy kilka wskazówek najlepszych praktyk i zakończymy w pełni funkcjonalnym endpointem, który każdy klient może wywołać. Po zakończeniu będziesz w stanie zamienić dowolny arkusz kalkulacyjny na PDF w zaledwie kilku linijkach kodu Python.

## Czego będziesz potrzebować

- **Python 3.8+** (kod działa na 3.9, 3.10 i nowszych)
- **Flask** (`pip install flask`) – lekki framework webowy napędzający nasze API
- **Aspose.Cells for Python via .NET** (`pip install aspose-cells`) – biblioteka, która rzeczywiście odczytuje XLSX i zapisuje PDF
- Podstawowa znajomość żądań HTTP `POST` (nic skomplikowanego)

Jeśli już masz te elementy, świetnie — zanurzmy się. Jeśli nie, krok „Install Dependencies” przygotuje Cię do pracy.

## Krok 1 – Konfiguracja projektu Flask

Najpierw utwórz nowy folder dla projektu i uruchom wirtualne środowisko. Dzięki temu nasze zależności będą uporządkowane.

```bash
mkdir flask_excel_pdf && cd flask_excel_pdf
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate
pip install flask aspose-cells
```

Teraz utwórz plik o nazwie `app.py`. Będzie on zawierał całą logikę **save workbook as pdf**.

## Krok 2 – Inicjalizacja aplikacji Flask

Zaczynamy od zaimportowania potrzebnych elementów i stworzenia obiektu aplikacji Flask. Zauważ, jak zwięzły jest blok importów — nie ma nieużywanych modułów, co utrzymuje niski czas uruchamiania.

```python
# app.py
from flask import Flask, request, send_file
import aspose.cells as cells
import io

app = Flask(__name__)
```

> **Pro tip:** Trzymaj `app = Flask(__name__)` na początku pliku; ułatwia to późniejsze testowanie narzędziami takimi jak `pytest-flask`.

## Krok 3 – Zbuduj endpoint konwersji (convert xlsx to pdf)

Oto serce tutorialu: endpoint, który przyjmuje arkusz kalkulacyjny poprzez `POST`, ładuje go do skoroszytu Aspose.Cells i przygotowuje do eksportu PDF.

```python
@app.route("/convert", methods=["POST"])
def convert():
    # 1️⃣ Grab the uploaded file from the request
    uploaded = request.files.get("file")
    if not uploaded:
        return {"error": "No file provided"}, 400

    # 2️⃣ Read the file into memory (binary)
    file_bytes = uploaded.read()

    # 3️⃣ Load the spreadsheet into a workbook object
    workbook = cells.Workbook(io.BytesIO(file_bytes))

    # 4️⃣ Auto‑fit all columns in the first sheet (auto fit excel columns)
    workbook.worksheets[0].auto_fit_columns()

    # 5️⃣ Save the workbook as PDF into an in‑memory stream
    pdf_stream = io.BytesIO()
    workbook.save(pdf_stream, cells.SaveFormat.PDF)
    pdf_stream.seek(0)

    # 6️⃣ Return the PDF using flask send_file pdf
    return send_file(
        pdf_stream,
        mimetype="application/pdf",
        as_attachment=True,
        download_name="output.pdf"
    )
```

### Dlaczego każdy element ma znaczenie

- **`request.files.get("file")`** – Bezpiecznie pobiera przesłany plik; użycie `.get` zapobiega `KeyError`, jeśli pole jest nieobecne.
- **`io.BytesIO`** – Przechowuje wszystko w RAM, więc nigdy nie zapisujemy plików tymczasowych na dysku. To kluczowe dla skalowalności.
- **`auto_fit_columns()`** – Bez tego szerokości kolumn często wyglądają na zbyt wąskie w PDF. Metoda rozszerza każdą kolumnę, aby dopasować ją do najdłuższej komórki, zapewniając profesjonalny wygląd.
- **`workbook.save(..., cells.SaveFormat.PDF)`** – To pojedyncze wywołanie wykonuje ciężką pracę konwersji XLSX do PDF. Aspose.Cells obsługuje formuły, wykresy i nawet scalone komórki.
- **`flask send_file pdf`** – Wysyła PDF z powrotem do klienta z odpowiednimi nagłówkami, wywołując pobranie pliku o nazwie `output.pdf`.

## Krok 4 – Uruchom serwer Flask

Dodaj typowy „run guard” na końcu `app.py`, aby skrypt mógł być uruchamiany bezpośrednio.

```python
if __name__ == "__main__":
    # Listening on all interfaces makes testing from Docker or another machine easy
    app.run(host="0.0.0.0", port=5000, debug=True)
```

Uruchomienie `python app.py` spowoduje start serwera pod adresem `http://localhost:5000`. Flaga `debug=True` jest przydatna w trakcie rozwoju; pamiętaj, aby wyłączyć ją w produkcji.

## Krok 5 – Testuj endpoint (ręcznie i automatycznie)

### Test ręczny przy użyciu cURL

```bash
curl -X POST http://localhost:5000/convert \
  -F "file=@sample.xlsx" \
  -o result.pdf
```

Jeśli wszystko poszło dobrze, `result.pdf` będzie zawierać ładnie sformatowaną wersję `sample.xlsx`, ze wszystkimi kolumnami automatycznie dopasowanymi.

### Test automatyczny przy użyciu `requests` w Pythonie

```python
import requests

with open("sample.xlsx", "rb") as f:
    response = requests.post(
        "http://localhost:5000/convert",
        files={"file": f}
    )
    response.raise_for_status()
    with open("downloaded.pdf", "wb") as out:
        out.write(response.content)

print("PDF saved as downloaded.pdf")
```

Oba podejścia demonstrują pełny **python excel to pdf** workflow — od uploadu po pobranie — bez konieczności dotykania systemu plików po stronie serwera.

## Krok 6 – Przypadki brzegowe i typowe pułapki

| Situation | What to Watch For | Fix |
|-----------|-------------------|-----|
| Duże pliki XLSX ( > 50 MB ) | Obciążenie pamięci na serwerze | Strumieniuj upload do pliku tymczasowego i użyj `Workbook(file_path)` zamiast `BytesIO`. |
| Zabezpieczony hasłem skoroszyt | `Workbook` zgłasza wyjątek | Przekaż hasło do konstruktora `Workbook`: `Workbook(io.BytesIO(file_bytes), cells.LoadOptions(password="secret"))`. |
| Brak wywołania `auto_fit_columns()` | Kolumny w PDF są przycięte | Zawsze wywołuj `auto_fit_columns()` **przed** `save()`. |
| Klient oczekuje błędu w formacie JSON | Flask zwraca stronę błędu w HTML | Zwróć słownik JSON z odpowiednim kodem statusu, jak pokazano w endpointzie (linia `return {"error": "No file provided"}, 400`). |

## Krok 7 – Wdrożenie do produkcji

Gdy jesteś gotowy, aby wystartować, rozważ następujące zmiany klasy produkcyjnej:

- **Użyj serwera WSGI** takiego jak `gunicorn` (`gunicorn -w 4 app:app`) zamiast wbudowanego serwera Flask.
- **Włącz HTTPS** za pośrednictwem reverse proxy (NGINX), aby chronić przesyłane pliki.
- **Ustaw limit rozmiaru żądania** (`app.config["MAX_CONTENT_LENGTH"] = 20 * 1024 * 1024`) aby uniknąć ataków typu denial‑of‑service.
- **Loguj błędy** przy użyciu strukturalnego loggera (np. `structlog`), aby móc śledzić niepowodzenia konwersji.

Wszystkie te kroki zachowują rdzeń logiki **save workbook as pdf**, jednocześnie przygotowując usługę do środowiska produkcyjnego.

## Oczekiwany wynik

Gdy wywołasz endpoint `/convert` z prawidłowym plikiem XLSX, odpowiedź:

1. Zawierać nagłówek `Content-Type: application/pdf`.
2. Wywołać w przeglądarce (lub kliencie) pobranie pliku o nazwie `output.pdf`.
3. Wyświetlić arkusz kalkulacyjny z kolumnami automatycznie dopasowanymi do ich zawartości, dzięki wywołaniu `auto fit excel columns`.

Otwórz pobrany PDF — powinieneś zobaczyć każdą kolumnę w pełni widoczną, formuły obliczone i wszelkie osadzone obrazy zachowane.

## Zakończenie

Masz teraz kompletny, gotowy do produkcji przykład, który **save workbook as pdf** przy użyciu Flask, Aspose.Cells i czystego Pythona. Tutorial obejmował wszystko: od konfiguracji środowiska, **convert xlsx to pdf**, automatycznego dopasowywania kolumn, po dostarczenie wyniku za pomocą `flask send_file pdf`.

Następnie możesz zbadać dodawanie **custom styling**, scalanie komórek lub nawet konwersję wielu arkuszy do jednego wielostronicowego PDF. Ten sam wzorzec działa dla innych typów plików — wystarczy zamienić enum `SaveFormat`.

Masz pytania dotyczące przypadków brzegowych lub wdrożenia? zostaw komentarz poniżej i powodzenia w kodowaniu!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak zapisać konkretne strony pliku Excel jako PDF przy użyciu Aspose.Cells dla .NET](/cells/english/net/workbook-operations/save-specific-excel-pages-pdf-aspose-cells-net/)
- [Zapisz skoroszyt Excel jako PDF z własnymi czcionkami przy użyciu Aspose.Cells dla .NET](/cells/english/net/workbook-operations/save-excel-workbook-pdf-custom-fonts-aspose-cells-net/)
- [Konwertuj Excel do PDF z dopasowaniem kolumn w Javie przy użyciu Aspose.Cells](/cells/english/java/workbook-operations/convert-excel-to-pdf-fit-columns-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}