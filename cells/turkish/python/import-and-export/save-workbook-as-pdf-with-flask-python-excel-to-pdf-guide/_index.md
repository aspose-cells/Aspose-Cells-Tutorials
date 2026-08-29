---
category: general
date: 2026-06-21
description: Python’da Flask ve Aspose.Cells kullanarak çalışma kitabını PDF olarak
  kaydedin – XLSX’i PDF’e nasıl dönüştüreceğinizi, Excel sütunlarını otomatik olarak
  nasıl sığdıracağınızı ve dosyayı Flask send_file ile PDF olarak nasıl döndüreceğinizi
  öğrenin.
draft: false
keywords:
- save workbook as pdf
- convert xlsx to pdf
- python excel to pdf
- auto fit excel columns
- flask send_file pdf
language: tr
og_description: Flask kullanarak Python’da çalışma kitabını PDF olarak kaydedin. Bu
  adım adım öğretici, XLSX dosyasını PDF’ye nasıl dönüştüreceğinizi, Excel sütunlarını
  otomatik olarak nasıl sığdıracağınızı ve sonucu Flask send_file pdf ile nasıl sunacağınızı
  gösterir.
og_title: Flask ile Çalışma Kitabını PDF Olarak Kaydet – Tam Python Rehberi
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
title: Flask ile Çalışma Kitabını PDF Olarak Kaydet – Python Excel'den PDF'ye Kılavuz
url: /tr/python/import-and-export/save-workbook-as-pdf-with-flask-python-excel-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Flask ile Çalışma Kitabını PDF Olarak Kaydet – Python Excel'ten PDF'ye Rehberi

Bir web servisinden **çalışma kitabını PDF olarak kaydetmek** mi istiyorsunuz? Yüklenen bir Excel dosyasını anında şık bir PDF'e dönüştürmek isteyen tek kişi siz değilsiniz. Bu rehberde, Flask ve Aspose.Cells kullanarak bir çalışma kitabını PDF olarak kaydetmeyi adım adım inceleyecek, ayrıca **XLSX'i PDF'ye dönüştürme**, Excel sütunlarını otomatik sığdırma ve son olarak sonucu `flask send_file pdf` ile teslim etme konularına değineceğiz.

Temiz bir Flask projesiyle başlayıp birkaç en iyi uygulama ipucu ekleyecek ve sonunda herhangi bir istemcinin çağırabileceği tam işlevsel bir uç nokta elde edeceğiz. Bu bölümü tamamladığınızda, herhangi bir elektronik tabloyu sadece birkaç Python satırıyla PDF'e dönüştürebileceksiniz.

## Gereksinimler

- **Python 3.8+** (kod 3.9, 3.10 ve daha yeni sürümlerde de çalışır)
- **Flask** (`pip install flask`) – API'mizi besleyen hafif web çerçevesi
- **Aspose.Cells for Python via .NET** (`pip install aspose-cells`) – XLSX'i okuyup PDF olarak yazan kütüphane
- HTTP `POST` istekleri hakkında temel bilgi (karmaşık bir şey değil)

Bu bileşenlere zaten sahipseniz harika—hadi başlayalım. Yoksa, “Bağımlılıkları Yükleme” adımı sizi kurulum aşamasına getirecek.

## Adım 1 – Flask Projesini Kurun

İlk olarak proje için yeni bir klasör oluşturun ve bir sanal ortam başlatın. Bu, bağımlılıklarımızı düzenli tutar.

```bash
mkdir flask_excel_pdf && cd flask_excel_pdf
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate
pip install flask aspose-cells
```

Şimdi `app.py` adlı bir dosya oluşturun. Bu dosya **çalışma kitabını pdf olarak kaydet** mantığını barındıracak.

## Adım 2 – Flask Uygulamasını Başlatın

İhtiyacımız olan parçaları içe aktarıp Flask uygulama nesnesini oluşturuyoruz. İçe aktarma bloğunun ne kadar özlü olduğuna dikkat edin—kullanılmayan modüller yok, bu da başlangıç süresini düşük tutar.

```python
# app.py
from flask import Flask, request, send_file
import aspose.cells as cells
import io

app = Flask(__name__)
```

> **Pro ipucu:** `app = Flask(__name__)` satırını dosyanın en üstünde tutun; bu, `pytest-flask` gibi araçlarla daha sonraki testleri çok kolaylaştırır.

## Adım 3 – Dönüştürme Uç Noktasını Oluşturun (xlsx to pdf)

İşte eğitimin kalbi: `POST` ile bir elektronik tablo kabul eden, Aspose.Cells çalışma kitabına yükleyen ve PDF dışa aktarımı için hazırlayan bir uç nokta.

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

### Her Parçanın Önemi

- **`request.files.get("file")`** – Yüklenen dosyayı güvenli bir şekilde alır; `.get` kullanmak alan eksikse `KeyError` oluşmasını engeller.
- **`io.BytesIO`** – Her şeyi RAM'de tutar, böylece geçici dosyalar diske yazılmaz. Bu, ölçeklenebilirlik için kritiktir.
- **`auto_fit_columns()`** – Bu olmadan PDF'teki sütun genişlikleri genellikle sıkışık görünür. Metod, her sütunu en uzun hücresine göre genişleterek profesyonel bir görünüm sağlar.
- **`workbook.save(..., cells.SaveFormat.PDF)`** – Bu tek çağrı XLSX'i PDF'ye dönüştürmenin ağır işini yapar. Aspose.Cells formülleri, grafikleri ve birleştirilmiş hücreleri bile işler.
- **`flask send_file pdf`** – PDF'i uygun başlıklarla istemciye gönderir, `output.pdf` adıyla indirilmesini sağlar.

## Adım 4 – Flask Sunucusunu Çalıştırın

`app.py` dosyasının altına tipik “run guard” ekleyin, böylece script doğrudan çalıştırılabilir.

```python
if __name__ == "__main__":
    # Listening on all interfaces makes testing from Docker or another machine easy
    app.run(host="0.0.0.0", port=5000, debug=True)
```

`python app.py` komutunu çalıştırmak, sunucuyu `http://localhost:5000` adresinde başlatır. `debug=True` bayrağı geliştirme sırasında kullanışlıdır; üretimde kapatmayı unutmayın.

## Adım 5 – Uç Noktayı Test Edin (Manuel & Otomatik)

### cURL ile Manuel Test

```bash
curl -X POST http://localhost:5000/convert \
  -F "file=@sample.xlsx" \
  -o result.pdf
```

Her şey yolunda giderse, `result.pdf` dosyası `sample.xlsx`'in güzel biçimlendirilmiş bir sürümünü, tüm sütunlar otomatik sığdırılmış şekilde içerir.

### Python `requests` ile Otomatik Test

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

Her iki yaklaşım da **python excel to pdf** iş akışını—yüklemeden indirmeye—sunucu tarafında dosya sistemine dokunmadan gösterir.

## Adım 6 – Kenar Durumları & Yaygın Tuzaklar

| Durum | Dikkat Edilmesi Gereken | Çözüm |
|-----------|-------------------|-----|
| Büyük XLSX dosyaları ( > 50 MB ) | Sunucuda bellek baskısı | Yüklemeyi geçici bir dosyaya akıtın ve `Workbook(file_path)` kullanın, `BytesIO` yerine. |
| Şifre korumalı çalışma kitabı | `Workbook` bir istisna fırlatır | Şifreyi `Workbook` yapıcıya geçirin: `Workbook(io.BytesIO(file_bytes), cells.LoadOptions(password="secret"))`. |
| `auto_fit_columns()` eksik | PDF sütunları kesik görünür | `save()` çağrısından **önce** her zaman `auto_fit_columns()` çağırın. |
| İstemci JSON hata bekliyor | Flask HTML hata sayfası döner | Uç noktada gösterildiği gibi JSON sözlüğü ve uygun durum kodu döndürün (`return {"error": "No file provided"}, 400`). |

Bu senaryoları önceden tahmin ederek API'niz sağlam ve kullanıcı dostu kalır.

## Adım 7 – Üretime Dağıtma

Canlıya geçmeye hazır olduğunuzda, aşağıdaki üretim‑ağırlıklı ayarları göz önünde bulundurun:

- **WSGI sunucusu** kullanın; örneğin `gunicorn` (`gunicorn -w 4 app:app`) Flask’ın yerleşik sunucusu yerine.
- **HTTPS**'i ters proxy (NGINX) üzerinden etkinleştirerek dosya yüklemelerini koruyun.
- **İstek boyutu sınırı** belirleyin (`app.config["MAX_CONTENT_LENGTH"] = 20 * 1024 * 1024`) servis reddi saldırılarını önlemek için.
- **Yapılandırılmış bir logger** (örn. `structlog`) ile hataları kaydedin, böylece dönüşüm hatalarını izleyebilirsiniz.

Tüm bu adımlar, temel **save workbook as pdf** mantığını korurken hizmeti üretim‑hazır hâle getirir.

## Beklenen Çıktı

`/convert` uç noktasına geçerli bir XLSX dosyası gönderdiğinizde yanıt:

1. `Content-Type: application/pdf` başlığına sahip olur.
2. Tarayıcıyı (veya istemciyi) `output.pdf` adıyla bir dosya indirmeye zorlar.
3. `auto fit excel columns` çağrısı sayesinde sütunlar içeriğe göre otomatik boyutlandırılmış şekilde elektronik tabloyu render eder.

İndirilen PDF'i açtığınızda her sütunun tamamen göründüğünü, formüllerin değerlendirilmiş olduğunu ve gömülü resimlerin korunduğunu görmelisiniz.

## Sonuç

Artık Flask, Aspose.Cells ve saf Python kullanarak **save workbook as pdf** yapan eksiksiz, üretim‑hazır bir örneğe sahipsiniz. Eğitim, ortam kurulumundan **convert xlsx to pdf**, sütunları otomatik sığdırmaya ve `flask send_file pdf` ile sonucu teslim etmeye kadar her şeyi kapsadı.

Sonraki adım olarak **özel stil ekleme**, hücre birleştirme veya birden fazla çalışma sayfasını tek çok‑sayfalı PDF'e dönüştürme gibi konuları keşfedebilirsiniz. Aynı desen diğer dosya tipleri için de çalışır—tek yapmanız gereken `SaveFormat` enum'ını değiştirmek.

Kenarlık durumları veya dağıtım hakkında sorularınız mı var? Aşağıya yorum bırakın, kodlamanın tadını çıkarın!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki eğitimler, bu rehberde gösterilen tekniklere yakın konuları kapsar ve kendi projelerinizde ek API özellikleri öğrenmenize ve alternatif uygulama yaklaşımları keşfetmenize yardımcı olacak tam çalışan kod örnekleri içerir.

- [How to Save Specific Pages of an Excel File as PDF Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/save-specific-excel-pages-pdf-aspose-cells-net/)
- [Save Excel Workbook as PDF with Custom Fonts using Aspose.Cells for .NET](/cells/english/net/workbook-operations/save-excel-workbook-pdf-custom-fonts-aspose-cells-net/)
- [Convert Excel to PDF with Fit Columns in Java using Aspose.Cells](/cells/english/java/workbook-operations/convert-excel-to-pdf-fit-columns-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}