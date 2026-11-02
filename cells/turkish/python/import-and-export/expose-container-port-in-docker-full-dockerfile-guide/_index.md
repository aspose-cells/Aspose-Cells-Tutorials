---
category: general
date: 2026-06-21
description: Docker'da çalışma dizinini ayarlayıp uygulama kaynak kodunu kopyalarken
  konteyner portunu açın. Python API'sini adım adım dockerize etmeyi öğrenin.
draft: false
keywords:
- expose container port
- set working directory docker
- dockerfile copy app
- copy source into container
- dockerize python api
language: tr
og_description: Docker'da konteyner portunu açın, çalışma dizinini ayarlayın ve kaynak
  kodunuzu konteynere kopyalayın. Bu öğretici, bir Python API'sini Docker'laştırmayı
  gösterir.
og_title: Docker’da Konteyner Portunu Açığa Çıkarma – Tam Rehber
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Expose container port in Docker while setting the working directory
    and copying your app source. Learn how to dockerize a Python API step‑by‑step.
  headline: Expose Container Port in Docker – Full Dockerfile Guide
  type: TechArticle
- description: Expose container port in Docker while setting the working directory
    and copying your app source. Learn how to dockerize a Python API step‑by‑step.
  name: Expose Container Port in Docker – Full Dockerfile Guide
  steps:
  - name: 1. Changing the Host Port
    text: 'Sometimes port 5000 is already in use on your machine. No problem—just
      change the host side of the mapping:'
  - name: 2. Multi‑Stage Builds for Smaller Images
    text: If you don’t need the full Aspose.Cells runtime in production, you can create
      a multi‑stage build that compiles assets in a heavy image then copies only the
      runtime bits into a lightweight `python:3.11-slim` final stage. This reduces
      the final image size dramatically.
  - name: 3. Using Docker Compose
    text: 'For more complex setups (e.g., a database alongside the API), put the same
      instructions into a `docker-compose.yml`:'
  - name: 4. Environment Variables
    text: 'If your API needs configuration (like a secret key), pass them at runtime:'
  type: HowTo
- questions:
  - answer: Check the logs with `docker logs api_container`. A common mistake is forgetting
      `host="0.0.0.0"` in Flask.
    question: Container exits immediately?
  - answer: Verify with `docker ps` and `netstat -tulpn`. Use a different host port
      as shown above.
    question: Port already in use?
  - answer: Ensure your `requirements.txt` is present before the `RUN pip install`
      step, or add the packages directly in the Dockerfile.
    question: Missing dependencies?
  type: FAQPage
tags:
- Docker
- Python
- API
title: Docker'da Konteyner Portunu Açığa Çıkarma – Tam Dockerfile Kılavuzu
url: /tr/python/import-and-export/expose-container-port-in-docker-full-dockerfile-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Docker’da Konteyner Portunu Açma – Tam Dockerfile Rehberi

Python API'nizi konteynerleştirirken **expose container port** nasıl yapılır diye hiç merak ettiniz mi? Tek başınıza değilsiniz. Çoğu geliştirici aynı sorunu yaşıyor: uygulama yerel olarak çalışıyor, ancak Docker içinde dış dünyadan erişilemiyor. Bu öğreticide, sadece **expose container port** değil, aynı zamanda **set working directory docker**, **dockerfile copy app** ve **copy source into container** yapan tam bir Dockerfile üzerinden geçeceğiz—**dockerize python api** yapmanız için ihtiyacınız olan tüm parçalar, zahmetsizce.

Küçük bir Flask uygulamasıyla başlayacağız, ardından sıfırdan bir Docker imajı oluşturacağız, her talimatı açıklayacağız ve sonunda konteyneri çalıştırarak `http://localhost:5000/health` adresine ulaşabileceksiniz. Sonunda, herhangi bir kayıt defterine itebileceğiniz üretim‑hazır bir Docker imajına sahip olacaksınız.

## Önkoşullar

- Docker Engine ≥ 20.10 yüklü (Docker Desktop Windows/macOS'ta, Linux'ta Docker Engine çalışır).
- Python ve Flask (veya herhangi bir WSGI‑uyumlu framework) konusunda temel bilgi.
- Dockerfile ve Python kodunu düzenlemek için bir metin editörü veya IDE (VS Code, PyCharm vb.).

Resmi Aspose.Cells Python.NET temel imajının sağladığı dışındaki ek kütüphanelere gerek yok.

## Adım 1: Minimal Bir Python API Oluşturun

İlk olarak, daha sonra **dockerize python api** yapacağımız küçük bir Flask servisi yazalım. Bunu boş bir klasöre `api_server.py` olarak kaydedin.

```python
# api_server.py
from flask import Flask, jsonify

app = Flask(__name__)

@app.route("/health")
def health():
    return jsonify(status="OK", message="API is running")

if __name__ == "__main__":
    # Listen on all interfaces so Docker can forward the port
    app.run(host="0.0.0.0", port=5000)
```

`host="0.0.0.0"` neden? Bir konteyner içinde `localhost` konteynerin kendisini ifade eder. `0.0.0.0`'a bağlamak, Flask'in herhangi bir ağ arayüzünden gelen bağlantıları kabul etmesini sağlar; bu, sonraki **expose container port** adımı için kritiktir.

## Adım 2: Doğru Temel İmajı Seçin

Bu örnek için Aspose'un resmi **Aspose.Cells Python.NET base image** (`aspose/cells-pythonnet:6.22`) imajını kullanacağız. İçinde .NET runtime, Python 3.9 ve Aspose.Cells kütüphanesi bulunur—API'nizin Excel işlemlerine ihtiyacı varsa mükemmeldir.

```dockerfile
# Use the official Aspose.Cells Python.NET base image
FROM aspose/cells-pythonnet:6.22
```

Aspose'a ihtiyacınız yoksa, bunu `python:3.11-slim` ile değiştirebilirsiniz. Dockerfile'ın geri kalanı aynı kalır.

## Adım 3: **Dockerfile Copy App** – Kaynağınızı Konteynere Kopyalayın

Sonra kodumuzu imaja getirmemiz gerekiyor. İşte **dockerfile copy app** talimatının devreye girdiği yer.

```dockerfile
# Copy the entire current directory (your app) into /app inside the container
COPY . /app
```

`.` build context'i temsil eder—`docker build` komutunu çalıştırdığınız klasör. Her şeyi kopyalayarak `requirements.txt` (varsa) ve statik varlıkları da dahil etmiş olursunuz. Daha sıkı bir imaj isterseniz, yalnızca gerçekten ihtiyaç duyduğunuz dosyaları listeleyin.

## Adım 4: **Set Working Directory Docker** – Çalışma Dizini Tanımlayın

Kopyalama sonrası Docker'a sonraki komutların nerede çalıştırılacağını söyleriz. Bu, **set working directory docker** adımıdır.

```dockerfile
# Set /app as the working directory for the rest of the build
WORKDIR /app
```

Neden? Sonradan tam yolları yazmaktan kurtarır (örneğin `python api_server.py` yerine `python /app/api_server.py`). Ayrıca, imajı daha sonra inceleyecek kişiler için konteynerin dosya sistemi düzenini daha net hâle getirir.

## Adım 5: Python Bağımlılıklarını Kurun (Opsiyonel ama Tavsiye Edilir)

API'niz harici paketlere bağımlıysa, bir `requirements.txt` oluşturun ve bunları ayrı bir katmanda kurun. Bu, önbellekleme performansını artırır.

```dockerfile
# Install Python dependencies (if requirements.txt exists)
RUN if [ -f requirements.txt ]; then pip install --no-cache-dir -r requirements.txt; fi
```

Koşul, `requirements.txt` yoksa derlemenin başarısız olmamasını sağlar—yukarıdaki minimal örnek için kullanışlıdır.

## Adım 6: **Expose Container Port** – API'yi Dışarıdan Erişilebilir Hale Getirin

Şimdi gösterinin yıldızına geliyoruz: **expose container port**. Bu, Docker'a konteynerin hangi portu dinleyeceğini söyler ve çalışma zamanında port eşlemesini etkinleştirir.

```dockerfile
# Expose the Flask port (5000) so the host can forward traffic
EXPOSE 5000
```

`EXPOSE` sadece bir dokümantasyon ipucu; gerçek eşleme `docker run -p` komutuyla gerçekleşir. Yine de portu tanımlamak en iyi uygulamadır ve Docker Compose gibi araçların doğru portları otomatik yönlendirmesine yardımcı olur.

## Adım 7: Başlangıç Komutunu Tanımlayın

Son olarak Docker'a API'yi nasıl başlatacağını söyleriz. Bu, `CMD` talimatıdır.

```dockerfile
# Start the Flask API when the container launches
CMD ["python", "api_server.py"]
```

JSON dizi biçimini kullanmak, kabuk yorumlama sorunlarından kaçınır ve komutu daha taşınabilir hâle getirir.

## Tam Dockerfile Özeti

Tüm parçaları bir araya getirerek, kopyalayıp yapıştırabileceğiniz tam Dockerfile şu şekildedir:

```dockerfile
# Step 1: Use the official Aspose.Cells Python.NET base image
FROM aspose/cells-pythonnet:6.22

# Step 2: Copy your application source code into the container
COPY . /app

# Step 3: Set the working directory to the application folder
WORKDIR /app

# Optional: Install Python dependencies if you have a requirements file
RUN if [ -f requirements.txt ]; then pip install --no-cache-dir -r requirements.txt; fi

# Step 4: Expose the port your API server will listen on
EXPOSE 5000

# Step 5: Define the command to start the API server
CMD ["python", "api_server.py"]
```

> **Pro ipucu:** Çok sayıda bağımlılığınız varsa `COPY` satırını `RUN pip install` satırından *önce* tutun. Docker, kurulu paketlerle katmanı önbelleğe alır, böylece kod değişikliğinden sonra yeniden inşa ettiğinizde her şeyi yeniden kurmaz.

## Adım 8: Docker İmajını Oluşturun

`Dockerfile` ve `api_server.py` dosyalarının bulunduğu klasörde bir terminal açın ve şu komutu çalıştırın:

```bash
docker build -t my-python-api .
```

Docker her adımı akış olarak gösterecek, mümkün olduğunda önbelleklenmiş katmanları gösterecek. Her şey sorunsuz giderse `Successfully tagged my-python-api:latest` mesajını göreceksiniz.

## Adım 9: Konteyneri Çalıştırın ve Port Eşlemesini Doğrulayın

Şimdi konteyneri başlatın, iç `5000` portunu ana makinenizin `5000` portuna (veya tercih ettiğiniz başka bir ana portuna) eşleştirerek:

```bash
docker run -d -p 5000:5000 --name api_container my-python-api
```

- `-d` konteyneri ayrık (detached) modda çalıştırır.
- `-p 5000:5000` Docker'a ana makine port 5000'i konteyner port 5000'e yönlendirmesini söyler—tam olarak **expose container port** yönergesinin hazırladığı şey.

Uç noktayı `curl` ile test edebilirsiniz:

```bash
curl http://localhost:5000/health
```

Beklenen çıktı:

```json
{
  "status": "OK",
  "message": "API is running"
}
```

Bu JSON çıktısını görürseniz, tebrikler—**dockerized python api** işlemini başarıyla tamamladınız ve portu erişilebilir hâle getirdiniz.

## Yaygın Kenar Durumları ve Nasıl Ele Alınır

### 1. Ana Makine Portunu Değiştirme

Bazen 5000 portu makinenizde zaten kullanımda olabilir. Sorun değil—eşlemenin ana makine tarafını değiştirin:

```bash
docker run -d -p 8080:5000 my-python-api
```

Şimdi konteyner hâlâ `5000` portunu dinlerken `http://localhost:8080/health` çalışacaktır.

### 2. Daha Küçük İmajlar İçin Çok Aşamalı (Multi‑Stage) Build'ler

Üretimde tam Aspose.Cells çalışma zamanına ihtiyacınız yoksa, ağır bir imajda varlıkları derleyen ve ardından sadece çalışma zamanı parçalarını hafif bir `python:3.11-slim` son aşamaya kopyalayan çok aşamalı bir build oluşturabilirsiniz. Bu, son imaj boyutunu büyük ölçüde azaltır.

### 3. Docker Compose Kullanımı

Daha karmaşık kurulumlar için (ör. API ile birlikte bir veritabanı), aynı talimatları bir `docker-compose.yml` dosyasına koyun:

```yaml
version: "3.9"
services:
  api:
    build: .
    ports:
      - "5000:5000"
    restart: unless-stopped
```

Compose, `EXPOSE` yönergesine otomatik olarak uyar, bu yüzden port eşlemesini tekrarlamanıza gerek kalmaz.

### 4. Çevre Değişkenleri

API'nizin bir yapılandırmaya (ör. gizli anahtar) ihtiyacı varsa, bunları çalışma zamanında geçirin:

```bash
docker run -d -p 5000:5000 -e SECRET_KEY=supersecret my-python-api
```

Python içinde `os.getenv("SECRET_KEY")` ile okuyabilirsiniz.

## Hata Ayıklama İpuçları

- **Konteyner hemen çıkıyor mu?** `docker logs api_container` ile günlükleri kontrol edin. Yaygın bir hata, Flask'te `host="0.0.0.0"` eklemeyi unutmaktır.
- **Port zaten kullanımda mı?** `docker ps` ve `netstat -tulpn` komutlarıyla doğrulayın. Yukarıda gösterildiği gibi farklı bir ana port kullanın.
- **Bağımlılıklar eksik mi?** `RUN pip install` adımından önce `requirements.txt` dosyanızın mevcut olduğundan emin olun veya paketleri doğrudan Dockerfile içine ekleyin.

## Özet

Basit bir Flask uygulamasıyla başladık, sağlam bir temel imaj seçtik, kodu içeriye getirmek için **dockerfile copy app** kullandık, temiz çalıştırma için **set working directory docker** belirledik, `EXPOSE 5000` ile **expose container port** ilan ettik ve hizmeti başlatan bir `CMD` ile bitirdik. İmajı oluşturup çalıştırmak, herkesin çekip çalıştırabileceği tam işlevsel bir **dockerize python api** sağladı.

## Sıradaki Adım Ne?

- **Dockerfile içinde bir health‑check ekleyin** (`HEALTHCHECK CMD curl -f http://localhost:5000/health || exit 1`).
- **stdout'a logging uygulayın** böylece Docker yakalayabilir.
- **API'yi HTTPS ile güvenceye alın**

## Sonra Ne Öğrenmeli?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Copy Sheets Within Workbook Using Aspose.Cells for .NET - Step-by-Step Guide](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)
- [Copy Data in Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}