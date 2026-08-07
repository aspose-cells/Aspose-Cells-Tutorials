---
category: general
date: 2026-06-21
description: افتح منفذ الحاوية في Docker أثناء تعيين دليل العمل ونسخ مصدر تطبيقك.
  تعلم كيفية تحويل واجهة برمجة تطبيقات Python إلى Docker خطوة بخطوة.
draft: false
keywords:
- expose container port
- set working directory docker
- dockerfile copy app
- copy source into container
- dockerize python api
language: ar
og_description: قم بفتح منفذ الحاوية في Docker، حدد دليل العمل، وانسخ المصدر الخاص
  بك إلى الحاوية. يوضح هذا الدرس كيفية تحويل واجهة برمجة تطبيقات Python إلى Docker.
og_title: كشف منفذ الحاوية في Docker – دليل كامل
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
title: كشف منفذ الحاوية في Docker – دليل كامل لملف Dockerfile
url: /ar/python/import-and-export/expose-container-port-in-docker-full-dockerfile-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# فتح منفذ الحاوية في Docker – دليل كامل لملف Dockerfile

هل تساءلت يومًا كيف **expose container port** عندما تقوم بحاوية (containerizing) واجهة برمجة تطبيقات Python؟ لست وحدك. يواجه معظم المطورين نفس المشكلة: التطبيق يعمل محليًا، ولكن بمجرد وضعه داخل Docker، لا يمكن للعالم الخارجي الوصول إليه. في هذا الدرس سنستعرض ملف Dockerfile كامل لا يقتصر فقط على **expose container port** بل يشمل أيضًا **set working directory docker**، **dockerfile copy app**، و **copy source into container** — جميع العناصر التي تحتاجها لت **dockerize python api** دون عناء.

سنبدأ بتطبيق Flask صغير، ثم نبني صورة Docker من الصفر، نشرح كل تعليمة، وأخيرًا نشغل الحاوية حتى تتمكن من الوصول إلى `http://localhost:5000/health`. بنهاية الدرس ستحصل على صورة Docker جاهزة للإنتاج يمكنك دفعها إلى أي سجل.

## المتطلبات المسبقة

- Docker Engine ≥ 20.10 مثبت (Docker Desktop يعمل جيدًا على Windows/macOS، Docker Engine على Linux).
- إلمام أساسي بـ Python و Flask (أو أي إطار عمل متوافق مع WSGI).
- محرر نصوص أو بيئة تطوير متكاملة (VS Code، PyCharm، إلخ) لتعديل Dockerfile وكود Python.

لا توجد مكتبات إضافية مطلوبة بخلاف ما توفره صورة الأساس الرسمية Aspose.Cells Python.NET.

## الخطوة 1: إنشاء واجهة برمجة تطبيقات Python بسيطة

أولاً، لنكتب خدمة Flask صغيرة سنقوم لاحقًا **dockerize python api** لها. احفظ هذا كملف `api_server.py` في مجلد فارغ.

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

لماذا `host="0.0.0.0"`؟ داخل الحاوية، `localhost` يشير إلى الحاوية نفسها. الربط بـ `0.0.0.0` يخبر Flask بقبول الاتصالات من أي واجهة شبكة، وهو أمر أساسي لخطوة **expose container port** لاحقًا.

## الخطوة 2: اختيار صورة الأساس المناسبة

في هذا المثال سنستخدم **Aspose.Cells Python.NET base image** الرسمي من Aspose (`aspose/cells-pythonnet:6.22`). هذه الصورة تتضمن بالفعل .NET runtime، Python 3.9، ومكتبة Aspose.Cells — مثالية إذا كانت واجهة برمجة تطبيقاتك تحتاج إلى معالجة Excel.

```dockerfile
# Use the official Aspose.Cells Python.NET base image
FROM aspose/cells-pythonnet:6.22
```

إذا لم تكن بحاجة إلى Aspose، يمكنك استبدالها بـ `python:3.11-slim`. باقي محتوى Dockerfile يبقى كما هو.

## الخطوة 3: **Dockerfile Copy App** – نسخ الشيفرة المصدرية إلى داخل الحاوية

بعد ذلك، نحتاج إلى جلب الشيفرة إلى الصورة. هنا يتألق توجيه **dockerfile copy app**.

```dockerfile
# Copy the entire current directory (your app) into /app inside the container
COPY . /app
```

`.` يمثل سياق البناء — المجلد الذي تنفذ فيه `docker build`. بنسخ كل شيء، ستجلب أيضًا `requirements.txt` (إن وجد) وأي أصول ثابتة. إذا كنت تفضل صورة أصغر، قم بسرد الملفات التي تحتاجها فقط.

## الخطوة 4: **Set Working Directory Docker** – تحديد دليل العمل

بعد النسخ، نخبر Docker أين ينفذ الأوامر التالية. هذه هي خطوة **set working directory docker**.

```dockerfile
# Set /app as the working directory for the rest of the build
WORKDIR /app
```

لماذا نهتم بذلك؟ يوفر عليك كتابة المسارات الكاملة لاحقًا (مثلاً `python api_server.py` بدلاً من `python /app/api_server.py`). كما يجعل هيكل نظام ملفات الحاوية أكثر وضوحًا لأي شخص يقرأ الصورة لاحقًا.

## الخطوة 5: تثبيت تبعيات Python (اختياري لكن موصى به)

إذا كانت واجهة برمجة تطبيقاتك تعتمد على حزم خارجية، أنشئ ملف `requirements.txt` وقم بتثبيتها في طبقة منفصلة. هذا يحسن التخزين المؤقت.

```dockerfile
# Install Python dependencies (if requirements.txt exists)
RUN if [ -f requirements.txt ]; then pip install --no-cache-dir -r requirements.txt; fi
```

الشرط يضمن أن عملية البناء لن تفشل إذا لم يكن لديك `requirements.txt` — مفيد للمثال البسيط أعلاه.

## الخطوة 6: **Expose Container Port** – جعل الواجهة البرمجية قابلة للوصول من الخارج

الآن نصل إلى نجمة العرض: **expose container port**. هذا يخبر Docker أي منفذ ستستمع إليه الحاوية، مما يتيح تعيين المنافذ أثناء التشغيل.

```dockerfile
# Expose the Flask port (5000) so the host can forward traffic
EXPOSE 5000
```

لاحظ أن `EXPOSE` هو مجرد إشارة توثيقية؛ التعيين الفعلي يحدث عندما تشغل `docker run -p`. ومع ذلك، إعلان المنفذ يُعد ممارسة جيدة ويساعد أدوات مثل Docker Compose على توجيه المنافذ الصحيحة تلقائيًا.

## الخطوة 7: تعريف أمر بدء التشغيل

أخيرًا، نخبر Docker كيف يشغل الواجهة البرمجية. هذا هو توجيه `CMD`.

```dockerfile
# Start the Flask API when the container launches
CMD ["python", "api_server.py"]
```

استخدام صيغة مصفوفة JSON يتجنب مشاكل تفسير القشرة (shell) ويجعل الأمر أكثر قابلية للنقل.

## ملخص كامل لملف Dockerfile

بجمع جميع الأجزاء معًا، إليك ملف Dockerfile الكامل الذي يمكنك نسخه ولصقه:

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

> **نصيحة احترافية:** احتفظ بسطر `COPY` *قبل* سطر `RUN pip install` إذا كان لديك العديد من التبعيات. سيقوم Docker بتخزين الطبقة التي تحتوي على الحزم المثبتة في الذاكرة المؤقتة، لذا عند إعادة بناء الصورة بعد تعديل الشيفرة لن يتم إعادة تثبيت كل شيء.

## الخطوة 8: بناء صورة Docker

افتح طرفية في المجلد الذي يحتوي على `Dockerfile` و `api_server.py`، ثم نفّذ:

```bash
docker build -t my-python-api .
```

سيقوم Docker بتدفق كل خطوة، مع عرض الطبقات المخزنة مؤقتًا حيثما أمكن. إذا سارت الأمور بسلاسة، سترى `Successfully tagged my-python-api:latest`.

## الخطوة 9: تشغيل الحاوية والتحقق من تعيين المنفذ

الآن شغّل الحاوية، مع تعيين المنفذ الداخلي `5000` إلى منفذ المضيف `5000` (أو أي منفذ مضيف آخر تفضله):

```bash
docker run -d -p 5000:5000 --name api_container my-python-api
```

- `-d` يشغّله في وضعية منفصلة.
- `-p 5000:5000` يخبر Docker بتمرير منفذ المضيف 5000 إلى منفذ الحاوية 5000 — وهو بالضبط ما أعده توجيه **expose container port**.

يمكنك اختبار نقطة النهاية باستخدام `curl`:

```bash
curl http://localhost:5000/health
```

الناتج المتوقع:

```json
{
  "status": "OK",
  "message": "API is running"
}
```

إذا رأيت هذا الـ JSON، تهانينا — لقد نجحت في **dockerized python api** وجعلت المنفذ قابلًا للوصول.

## حالات الحافة الشائعة وكيفية التعامل معها

### 1. تغيير منفذ المضيف

أحيانًا يكون المنفذ 5000 مستخدمًا بالفعل على جهازك. لا مشكلة — فقط غيّر جانب المضيف في التعيين:

```bash
docker run -d -p 8080:5000 my-python-api
```

الآن `http://localhost:8080/health` سيعمل بينما لا تزال الحاوية تستمع على `5000`.

### 2. بناء متعدد المراحل للحصول على صور أصغر

إذا لم تكن بحاجة إلى بيئة تشغيل Aspose.Cells الكاملة في الإنتاج، يمكنك إنشاء بناء متعدد المراحل يقوم بتجميع الأصول في صورة ثقيلة ثم ينسخ فقط أجزاء وقت التشغيل إلى مرحلة نهائية خفيفة الوزن `python:3.11-slim`. هذا يقلل بشكل كبير من حجم الصورة النهائية.

### 3. استخدام Docker Compose

لإعدادات أكثر تعقيدًا (مثل قاعدة بيانات جنبًا إلى جنب مع الواجهة البرمجية)، ضع نفس التعليمات في ملف `docker-compose.yml`:

```yaml
version: "3.9"
services:
  api:
    build: .
    ports:
      - "5000:5000"
    restart: unless-stopped
```

Compose يحترم تلقائيًا توجيه `EXPOSE`، لذا لن تحتاج إلى تكرار تعيين المنفذ.

### 4. المتغيرات البيئية

إذا كانت الواجهة البرمجية تحتاج إلى إعدادات (مثل مفتاح سري)، مرّرها أثناء التشغيل:

```bash
docker run -d -p 5000:5000 -e SECRET_KEY=supersecret my-python-api
```

داخل Python يمكنك قراءة `os.getenv("SECRET_KEY")`.

## نصائح التصحيح

- **هل تخرج الحاوية فورًا؟** تحقق من السجلات باستخدام `docker logs api_container`. خطأ شائع هو نسيان `host="0.0.0.0"` في Flask.
- **هل المنفذ مستخدم بالفعل؟** تحقق باستخدام `docker ps` و `netstat -tulpn`. استخدم منفذ مضيف مختلف كما هو موضح أعلاه.
- **هل هناك تبعيات مفقودة؟** تأكد من وجود `requirements.txt` قبل خطوة `RUN pip install`، أو أضف الحزم مباشرة في Dockerfile.

## ملخص

بدأنا بتطبيق Flask بسيط، اخترنا صورة أساس قوية، استخدمنا **dockerfile copy app** لجلب الشيفرة داخل الصورة، ثم **set working directory docker** لتنفيذ نظيف، أعلنّا `EXPOSE 5000` لـ **expose container port**، واختتمنا بـ `CMD` لتشغيل الخدمة. بناء وتشغيل الصورة منحنا واجهة برمجة تطبيقات **dockerize python api** تعمل بالكامل يمكن لأي شخص سحبها وتشغيلها.

## ما التالي؟

- **إضافة فحص صحة** في Dockerfile (`HEALTHCHECK CMD curl -f http://localhost:5000/health || exit 1`).
- **تنفيذ تسجيل日志** إلى stdout بحيث يستطيع Docker التقاطه.
- **تأمين الواجهة البرمجية** باستخدام HTTPS

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات إضافية للواجهة البرمجية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Copy Sheets Within Workbook Using Aspose.Cells for .NET - Step-by-Step Guide](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)
- [Copy Data in Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}