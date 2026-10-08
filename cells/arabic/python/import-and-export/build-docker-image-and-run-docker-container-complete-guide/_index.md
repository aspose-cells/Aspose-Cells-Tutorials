---
category: general
date: 2026-06-21
description: تعلم كيفية إنشاء صورة Docker وتشغيل حاوية Docker مع تعيين المنافذ بشكل
  صحيح. يتضمن تعيين منفذ docker run وتعريض المنفذ في Docker.
draft: false
keywords:
- build docker image
- run docker container
- docker run port mapping
- expose port in docker
- docker build from dockerfile
language: ar
og_description: إنشاء صورة Docker وتشغيل حاوية Docker مع تعيين المنفذ الصحيح. إتقان
  تعيين منفذ تشغيل Docker وتعريض المنفذ في Docker خلال دقائق.
og_title: إنشاء صورة Docker وتشغيل حاوية Docker – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Learn how to build docker image and run docker container with proper
    port mapping. Includes docker run port mapping and expose port in docker.
  headline: Build Docker Image and Run Docker Container – Complete Guide
  type: TechArticle
- description: Learn how to build docker image and run docker container with proper
    port mapping. Includes docker run port mapping and expose port in docker.
  name: Build Docker Image and Run Docker Container – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Docker Engine installed (Desktop or Engine 20.10+). - Basic familiarity
      with the command line. - A tiny web app (we’ll use a one‑line Python Flask server,
      but you can swap it for anything).'
  - name: Verify the Image Exists
    text: 'Run `docker images` and look for `myflaskapp`:'
  - name: Detaching the Container (Optional)
    text: 'If you don’t want the terminal to be blocked, add `-d` to run in the background:'
  - name: Using `docker run` with Different Host Ports
    text: 'Sometimes you might already have something listening on host port 5000.
      No problem—just map to a different host port:'
  - name: Building Multi‑Stage Images (Advanced)
    text: 'If you ever need a smaller final image, you can **build docker image**
      with a multi‑stage Dockerfile:'
  type: HowTo
tags:
- docker
- containers
- devops
title: إنشاء صورة Docker وتشغيل حاوية Docker – دليل كامل
url: /ar/python/import-and-export/build-docker-image-and-run-docker-container-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء صورة Docker وتشغيل حاوية Docker – دليل كامل

هل تساءلت يوماً كيف **build docker image** لتطبيق ويب بسيط ثم تشغيله دون أي مشاكل؟ لست وحدك—الكثير من المطورين يواجهون نفس الصعوبة عندما يبدؤون في التعامل مع الحاويات. في هذا الدرس سنستعرض العملية بالكامل، من كتابة Dockerfile إلى كشف المنفذ الصحيح وأخيرًا استخدام `docker run` لتعيين ذلك المنفذ إلى جهازك. في النهاية ستعرف بالضبط كيف **run docker container** مع تعيين المنفذ بشكل صحيح، وستدرك لماذا يعتبر كشف المنفذ في Docker مهمًا.

سنغطي كل ما تحتاجه: الأمر الدقيق `docker build`، كيفية **docker build from Dockerfile**، تفاصيل `docker run port mapping`، وحتى فحص سريع للتأكد من أن الحاوية تستمع فعليًا حيث تتوقع. لا إطالة، مجرد دليل عملي خطوة بخطوة يمكنك نسخه ولصقه في الطرفية.

## ما ستحققه

- كتابة Dockerfile بسيط لتطبيق Node.js (أو أي تطبيق آخر).  
- **Build docker image** باستخدام صيغة CLI الرسمية.  
- فهم الفرق بين `EXPOSE` في Dockerfile وعلامة `-p` في `docker run`.  
- **Run docker container** مع `docker run port mapping` لتتمكن من الوصول إلى الخدمة عبر `http://localhost:5000`.  
- تشخيص المشكلات الشائعة مثل نسيان المنافذ أو عدم تطابق منافذ المضيف‑الحاوية.

### المتطلبات المسبقة

- تثبيت Docker Engine (Desktop أو Engine 20.10+).  
- إلمام أساسي بسطر الأوامر.  
- تطبيق ويب صغير (سنستخدم خادم Python Flask سطرًا واحدًا، لكن يمكنك استبداله بأي شيء).  

إذا كان لديك كل ذلك، فلنبدأ.

---

## الخطوة 1: إنشاء تطبيق بسيط

أولاً، نحتاج إلى شيء لنقوم بحاويته. أنشئ مجلدًا باسم `myapp` وضع ملفًا واحدًا اسمه `app.py` داخله:

```python
# app.py
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello from Docker!"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

> **نصيحة احترافية:** السطر `host="0.0.0.0"` يخبر Flask بالاستماع على جميع الواجهات، وهو ما يلزم لكي يقوم Docker بتمرير الحركة من المضيف.

الآن لديك خدمة ويب صغيرة تستمع على المنفذ 5000 داخل الحاوية.

## الخطوة 2: كتابة ملف Dockerfile (Docker Build from Dockerfile)

بعد ذلك، نحتاج إلى **Dockerfile** يخبر Docker كيف يبني الصورة. ضع هذا الملف بجوار `app.py`:

```dockerfile
# Dockerfile
FROM python:3.11-slim

# Install Flask
RUN pip install flask

# Copy our app into the image
COPY app.py /app/app.py

WORKDIR /app

# Expose the internal port (does NOT publish it yet)
EXPOSE 5000

# Default command to run the app
CMD ["python", "app.py"]
```

بعض النقاط التي يجب ملاحظتها:

- `FROM python:3.11-slim` يزودنا بصورة أساسية خفيفة الوزن.  
- `EXPOSE 5000` **expose port in docker** – هو مجرد تلميح لأي شخص يقرأ Dockerfile، لكنه لا يفتح المنفذ فعليًا على المضيف.  
- سطر `CMD` يشغل خادم Flask عندما تبدأ الحاوية.

## الخطوة 3: **Build Docker Image** من ملف Dockerfile

افتح الطرفية، `cd` إلى المجلد الذي يحتوي على Dockerfile، ثم نفّذ:

```bash
docker build -t myflaskapp .
```

لنشرح هذا الأمر:

- `docker build` هو الفعل الذي **builds docker image** الطبقات بناءً على تعليمات Dockerfile.  
- `-t myflaskapp` يضع علامة على الصورة الناتجة باسم سهل يمكنك الرجوع إليه لاحقًا.  
- النقطة `.` في النهاية تخبر Docker باستخدام الدليل الحالي كسياق بناء (المكان الذي يبحث فيه عن Dockerfile وأي ملفات تقوم بـ `COPY`).

من المفترض أن ترى مخرجات مشابهة لـ:

```
Sending build context to Docker daemon  3.072kB
Step 1/6 : FROM python:3.11-slim
 ---> 3b6c0f...
Step 2/6 : RUN pip install flask
 ---> Using cache
 ---> 9e2b7a...
...
Successfully built 1c2d3e4f5g6h
Successfully tagged myflaskapp:latest
```

إذا صادفت أي أخطاء، تحقق مرة أخرى من صياغة Dockerfile وتأكد من وجود ملف `app.py` في نفس المجلد.

### التحقق من وجود الصورة

نفّذ `docker images` وابحث عن `myflaskapp`:

```bash
docker images | grep myflaskapp
```

ستظهر لك نتيجة مشابهة لـ:

```
myflaskapp   latest   1c2d3e4f5g6h   2 minutes ago   120MB
```

مبروك—لقد **built docker image** بنجاح!

## الخطوة 4: **Run Docker Container** مع تعيين المنفذ

الآن بعد أن أصبحت الصورة جاهزة، حان الوقت لـ **run docker container** وجعل تطبيق Flask قابل للوصول من جهازك. استخدم العلامة `-p` لتنفيذ **docker run port mapping**:

```bash
docker run -p 5000:5000 myflaskapp
```

**Explanation:**

- الـ `5000` الأول (الجانب الأيسر) هو **host port**.  
- الـ `5000` الثاني (الجانب الأيمن) هو **container port** الذي كشفناه مسبقًا.  
- سيقوم Docker بتمرير الحركة من `localhost:5000` على جهازك إلى المنفذ 5000 داخل الحاوية.

من المفترض أن ترى سجلات بدء تشغيل Flask:

```
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

افتح المتصفح وتوجه إلى `http://localhost:5000`. سترى “Hello from Docker!”—الحاوية تقدم الحركة تمامًا كما توقعنا.

### فصل الحاوية (اختياري)

إذا لا تريد أن يبقى الطرفية محجوبة، أضف `-d` لتشغيلها في الخلفية:

```bash
docker run -d -p 5000:5000 myflaskapp
```

يمكنك إيقافها لاحقًا باستخدام `docker stop <container-id>`.

## الخطوة 5: الغوص بعمق – **Expose Port in Docker** مقابل **Docker Run Port Mapping**

من السهل الخلط بين تعليمة `EXPOSE` والعلامة `-p`، لكنهما يخدمان أغراضًا مختلفة:

| المفهوم | ما يفعله | هل يفتح المنفذ على المضيف؟ |
|---------|----------|----------------------------|
| `EXPOSE` (في Dockerfile) | يوثّق المنافذ التي يعتزم الحاوية الاستماع عليها. | **لا** – مجرد بيانات وصفية. |
| `-p host:container` (docker run) | ينشئ قاعدة NAT تُحوّل الحركة من منفذ المضيف إلى منفذ الحاوية. | **نعم** – تحويل فعلي للمنفذ. |

إذا نسيت تضمين `EXPOSE`، فإن أمر `docker run -p` سيظل يعمل، لكنك ستفقد الوثائق المفيدة للمستخدمين اللاحقين. وعلى العكس، إذا قمت فقط بـ `EXPOSE` دون استخدام `-p`، فستظل الخدمة غير قابلة للوصول من المضيف.

### استخدام `docker run` مع منافذ مضيف مختلفة

أحيانًا قد يكون لديك شيء بالفعل يستمع على منفذ المضيف 5000. لا مشكلة—فقط عيّن إلى منفذ مضيف مختلف:

```bash
docker run -p 8080:5000 myflaskapp
```

الآن يمكن الوصول إلى التطبيق عبر `http://localhost:8080`، بينما يظل يستمع على 5000 داخل الحاوية. هذه المرونة هي إحدى القوي الأساسية لـ **docker run port mapping**.

## الخطوة 6: المشكلات الشائعة وحالات الحافة

| المشكلة | العرض | الحل |
|---------|-------|------|
| نسيان `EXPOSE` | لا يستطيع المطورون الجدد معرفة أي منفذ يجب تعيينه. | أضف `EXPOSE 5000` (أو أي منفذ يستخدمه تطبيقك). |
| استخدام منفذ مضيف خاطئ | المتصفح يُظهر “connection refused”. | تأكد أن الجانب الأيسر من `-p` يطابق المنفذ الذي تحاول الوصول إليه. |
| تعطل الحاوية عند البدء | لا توجد سجلات، الحاوية تنتهي فورًا. | نفّذ `docker logs <container-id>` لرؤية رسائل الخطأ؛ غالبًا ما يكون السبب نقص تبعيات أو `CMD` غير صحيح. |
| المنفذ مستخدم بالفعل على المضيف | Docker يطبع “bind: address already in use”. | اختر منفذ مضيف مختلف (`-p 8080:5000`). |
| عدم الربط إلى `0.0.0.0` | الخدمة لا يمكن الوصول إليها إلا من داخل الحاوية. | في Flask، اضبط `host="0.0.0.0"`؛ للأطر الأخرى إعدادات مماثلة. |

### بناء صور متعددة المراحل (متقدم)

إذا احتجت يومًا إلى صورة نهائية أصغر، يمكنك **build docker image** باستخدام Dockerfile متعدد المراحل:

```dockerfile
# Stage 1: Build
FROM python:3.11-slim AS builder
RUN pip install --target=/app flask
COPY app.py /app/

# Stage 2: Runtime
FROM python:3.11-slim
COPY --from=builder /app /app
WORKDIR /app
EXPOSE 5000
CMD ["python", "app.py"]
```

هذه التقنية تزيل طبقات وقت البناء، مما ينتج صورة أخف—مثالية للإنتاج.

## الخطوة 7: التنظيف

عند الانتهاء من التجارب، قم بتنظيف البيئة:

```bash
# Stop all running containers derived from the image
docker ps --filter "ancestor=myflaskapp" -q | xargs -r docker stop

# Remove the image
docker rmi myflaskapp
```

التنظيف يمنع امتلاء القرص ويحافظ على بيئة Docker مرتبة.

## الخلاصة

أصبح لديك الآن سير عمل متكامل من البداية للنهاية لـ **build docker image** و **run docker container** مع **docker run port mapping** الصحيح. بفهمك لكيفية **expose port in docker** وكيفية عمل علامة `-p` في تحويل الحركة، يمكنك حاوية أي خدمة بثقة وجعلها قابلة للوصول من مضيفك أو الشبكة الأوسع.

ما الخطوة التالية؟ جرّب استبدال تطبيق Flask بملف تنفيذي Go، أضف متغيرات بيئية باستخدام `-e`، أو ادفع الصورة التي بنيتها حديثًا إلى Docker Hub باستخدام `docker push`. السماء هي الحد، وقد اكتسبت الآن قدرة جديدة في عالم DevOps.

حاوية سعيدة

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشروعاتك الخاصة.

- [إتقان عرض الصور في Excel باستخدام Aspose.Cells لـ .NET: دليل شامل](/cells/english/net/images-shapes/master-image-rendering-excel-aspose-cells-net/)
- [كيفية إضافة صورة إلى مخطط باستخدام Aspose.Cells لـ .NET: دليل خطوة بخطوة](/cells/english/net/charts-graphs/add-image-chart-aspose-cells-dotnet/)
- [كيفية إضافة روابط تشعبية للصور في دفاتر عمل .NET باستخدام Aspose.Cells لتعزيز التفاعل](/cells/english/net/images-shapes/adding-image-hyperlinks-net-workbooks-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}