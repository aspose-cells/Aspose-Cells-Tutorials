---
category: general
date: 2026-06-21
description: डॉकर इमेज बनाना और उचित पोर्ट मैपिंग के साथ डॉकर कंटेनर चलाना सीखें।
  इसमें डॉकर रन पोर्ट मैपिंग और डॉकर में पोर्ट एक्सपोज़ करना शामिल है।
draft: false
keywords:
- build docker image
- run docker container
- docker run port mapping
- expose port in docker
- docker build from dockerfile
language: hi
og_description: डॉकर इमेज बनाएं और सही पोर्ट मैपिंग के साथ डॉकर कंटेनर चलाएँ। कुछ
  ही मिनटों में डॉकर रन पोर्ट मैपिंग में निपुण बनें और डॉकर में पोर्ट एक्सपोज़ करें।
og_title: Docker इमेज बनाएं और Docker कंटेनर चलाएँ – पूर्ण गाइड
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
title: Docker इमेज बनाएं और Docker कंटेनर चलाएं – पूर्ण गाइड
url: /hi/python/import-and-export/build-docker-image-and-run-docker-container-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Docker इमेज बनाएं और Docker कंटेनर चलाएँ – पूर्ण गाइड

क्या आपने कभी सोचा है कि **docker image** को एक साधारण वेब ऐप के लिए कैसे **बनाएँ** और फिर बिना किसी समस्या के उसे चलाएँ? आप अकेले नहीं हैं—कई डेवलपर्स को कंटेनराइज़ेशन के साथ पहली बार काम करते समय यही समस्या आती है। इस ट्यूटोरियल में हम पूरी प्रक्रिया को समझेंगे, Dockerfile लिखने से लेकर सही पोर्ट एक्सपोज़ करने और अंत में `docker run` के साथ उस पोर्ट को होस्ट से मैप करने तक। अंत तक आप बिल्कुल जानेंगे कि **docker container** को सही पोर्ट मैपिंग के साथ कैसे **चलाएँ**, और समझेंगे कि Docker में पोर्ट एक्सपोज़ करना क्यों महत्वपूर्ण है।

हम वह सब कवर करेंगे जिसकी आपको ज़रूरत है: सटीक `docker build` कमांड, **docker build from Dockerfile**, `docker run port mapping` के नुअन्स, और एक त्वरित sanity check जिससे आप यह सुनिश्चित कर सकें कि कंटेनर वाकई उस पोर्ट पर सुन रहा है जहाँ आप उम्मीद करते हैं। कोई फालतू बात नहीं, सिर्फ एक हैंड‑ऑन, स्टेप‑बाय‑स्टेप गाइड जिसे आप अपने टर्मिनल में कॉपी‑पेस्ट कर सकते हैं।

## आप क्या हासिल करेंगे

- एक न्यूनतम Dockerfile लिखेंगे Node.js (या किसी भी) ऐप के लिए।  
- आधिकारिक CLI सिंटैक्स का उपयोग करके **docker image** बनाएँगे।  
- Dockerfile में `EXPOSE` और `docker run` में `-p` फ़्लैग के बीच का अंतर समझेंगे।  
- `docker run port mapping` के साथ **docker container** चलाएँगे ताकि आप सेवा को `http://localhost:5000` पर पहुँचा सकें।  
- सामान्य समस्याओं जैसे भूल गए पोर्ट या होस्ट‑कंटेनर पोर्ट का मेल न खाने को पहचानेंगे।

### पूर्वापेक्षाएँ

- Docker Engine स्थापित हो (Desktop या Engine 20.10+)।  
- कमांड लाइन की बुनियादी समझ।  
- एक छोटा वेब ऐप (हम एक‑लाइन Python Flask सर्वर का उपयोग करेंगे, लेकिन आप इसे किसी भी चीज़ से बदल सकते हैं)।  

यदि आपके पास ये सब है, तो चलिए शुरू करते हैं।

---

## चरण 1: एक साधारण एप्लिकेशन बनाएं

पहले, हमें कंटेनराइज़ करने के लिए कुछ चाहिए। `myapp` नाम का एक फ़ोल्डर बनाएं और उसके अंदर एक फ़ाइल `app.py` रखें:

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

> **Pro tip:** `host="0.0.0.0"` लाइन Flask को सभी इंटरफ़ेस पर सुनने के लिए बताती है, जो Docker को होस्ट से ट्रैफ़िक फ़ॉरवर्ड करने के लिए आवश्यक है।

अब आपके पास एक छोटा वेब सर्विस है जो कंटेनर के अंदर पोर्ट 5000 पर सुनता है।

## चरण 2: Dockerfile लिखें (Docker Build from Dockerfile)

अब हमें एक **Dockerfile** चाहिए जो Docker को इमेज बनाने की प्रक्रिया बताए। इस फ़ाइल को `app.py` के बगल में रखें:

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

ध्यान देने योग्य कुछ बातें:

- `FROM python:3.11-slim` हमें एक हल्का बेस इमेज देता है।  
- `EXPOSE 5000` **expose port in docker** – यह Dockerfile पढ़ने वाले किसी भी व्यक्ति के लिए एक संकेत है, लेकिन यह वास्तव में होस्ट पर पोर्ट नहीं खोलता।  
- `CMD` लाइन कंटेनर शुरू होने पर हमारा Flask सर्वर चलाती है।

## चरण 3: Dockerfile से **Docker Image बनाएं**

एक टर्मिनल खोलें, Dockerfile वाले फ़ोल्डर में `cd` करें, और चलाएँ:

```bash
docker build -t myflaskapp .
```

आइए इस कमांड को विस्तार से देखें:

- `docker build` वह क्रिया है जो **docker image** लेयर बनाती है Dockerfile निर्देशों के आधार पर।  
- `-t myflaskapp` बनायी गयी इमेज को एक दोस्ताना नाम देता है जिसे आप बाद में रेफ़र कर सकते हैं।  
- अंत में `.` Docker को बताता है कि वर्तमान डायरेक्टरी को बिल्ड कॉन्टेक्स्ट के रूप में उपयोग करे (जहाँ Dockerfile और `COPY` की गई फ़ाइलें मिलेंगी)।

आपको कुछ इस तरह का आउटपुट दिखेगा:

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

यदि कोई त्रुटि दिखे, तो Dockerfile सिंटैक्स को दोबारा जाँचें और सुनिश्चित करें कि `app.py` फ़ाइल उसी फ़ोल्डर में है।

### इमेज मौजूद है या नहीं जांचें

`docker images` चलाएँ और `myflaskapp` देखें:

```bash
docker images | grep myflaskapp
```

आपको कुछ इस तरह दिखेगा:

```
myflaskapp   latest   1c2d3e4f5g6h   2 minutes ago   120MB
```

बधाई—आपने सफलतापूर्वक **docker image** **बना ली** है!

## चरण 4: पोर्ट मैपिंग के साथ **Docker Container चलाएँ**

अब इमेज तैयार है, समय है **docker container** चलाने का और Flask ऐप को आपके होस्ट मशीन से पहुँच योग्य बनाने का। `-p` फ़्लैग का उपयोग करके **docker run port mapping** करें:

```bash
docker run -p 5000:5000 myflaskapp
```

व्याख्या:

- पहला `5000` (बाएँ) **होस्ट पोर्ट** है।  
- दूसरा `5000` (दाएँ) वह **कंटेनर पोर्ट** है जिसे हमने पहले `EXPOSE` किया था।  
- Docker आपके मशीन के `localhost:5000` से कंटेनर के अंदर पोर्ट 5000 तक ट्रैफ़िक फ़ॉरवर्ड करेगा।

आपको Flask के स्टार्टअप लॉग दिखेंगे:

```
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

ब्राउज़र खोलें और `http://localhost:5000` पर जाएँ। आपको “Hello from Docker!” दिखेगा—कंटेनर ने ठीक वैसा ही ट्रैफ़िक सर्व किया जैसा हमने उम्मीद की थी।

### कंटेनर को बैकग्राउंड में चलाएँ (वैकल्पिक)

यदि आप टर्मिनल को ब्लॉक नहीं रखना चाहते, तो `-d` जोड़ें ताकि यह बैकग्राउंड में चले:

```bash
docker run -d -p 5000:5000 myflaskapp
```

बाद में आप इसे `docker stop <container-id>` से रोक सकते हैं।

## चरण 5: गहराई से देखें – **Expose Port in Docker** बनाम **Docker Run Port Mapping**

`EXPOSE` निर्देश को `-p` फ़्लैग के साथ भ्रमित होना आसान है, लेकिन उनका उद्देश्य अलग‑अलग है:

| Concept | What it does | Does it open the port on the host? |
|---------|--------------|------------------------------------|
| `EXPOSE` (in Dockerfile) | Documents which ports the container *intends* to listen on. | **No** – just metadata. |
| `-p host:container` (docker run) | Creates a NAT rule that forwards traffic from the host port to the container port. | **Yes** – actual port forwarding. |

यदि आप `EXPOSE` भूल जाते हैं, तो भी `docker run -p` काम करेगा, लेकिन डाउनस्ट्रीम उपयोगकर्ताओं के लिए दस्तावेज़ीकरण कम हो जाता है। दूसरी ओर, यदि आप केवल `EXPOSE` करते हैं और `-p` नहीं इस्तेमाल करते, तो सेवा होस्ट से पहुँच योग्य नहीं रहेगी।

### विभिन्न होस्ट पोर्ट के साथ `docker run` का उपयोग

कभी‑कभी आपके होस्ट पर पहले से ही पोर्ट 5000 पर कुछ चल रहा हो सकता है। कोई बात नहीं—सिर्फ अलग होस्ट पोर्ट मैप करें:

```bash
docker run -p 8080:5000 myflaskapp
```

अब ऐप `http://localhost:8080` पर पहुँचा जा सकता है, जबकि कंटेनर के अंदर अभी भी पोर्ट 5000 पर सुन रहा है। यह लचीलापन **docker run port mapping** की मुख्य ताकतों में से एक है।

## चरण 6: सामान्य समस्याएँ और किनारे के केस

| Issue | Symptom | Fix |
|-------|---------|-----|
| Forgetting `EXPOSE` | New developers can’t tell which port to map. | Add `EXPOSE 5000` (or whatever your app uses). |
| Using the wrong host port | Browser returns “connection refused”. | Verify the left side of `-p` matches the port you’re trying to reach. |
| Container crashes on start | No logs, container exits instantly. | Run `docker logs <container-id>` to see error messages; often caused by missing dependencies or wrong `CMD`. |
| Port already in use on host | Docker prints “bind: address already in use”. | Choose a different host port (`-p 8080:5000`). |
| Not binding to `0.0.0.0` | Service only reachable from inside container. | In Flask, set `host="0.0.0.0"`; other frameworks have similar settings. |

### मल्टी‑स्टेज इमेज बनाना (एडवांस्ड)

यदि आपको अंतिम इमेज को और छोटा बनाना है, तो आप **docker image** को मल्टी‑स्टेज Dockerfile से बना सकते हैं:

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

यह तकनीक बिल्ड‑टाइम लेयर को हटाकर एक हल्की इमेज बनाती है—प्रोडक्शन के लिए बेहतरीन।

## चरण 7: सफ़ाई (Clean Up)

जब आप प्रयोग समाप्त कर लें, तो साफ‑सफ़ाई करें:

```bash
# Stop all running containers derived from the image
docker ps --filter "ancestor=myflaskapp" -q | xargs -r docker stop

# Remove the image
docker rmi myflaskapp
```

सफ़ाई करने से डिस्क स्पेस बचता है और आपका Docker वातावरण साफ़ रहता है।

---

## निष्कर्ष

अब आपके पास **docker image** बनाना और **docker container** को सही **docker run port mapping** के साथ चलाने का एक ठोस, एंड‑टू‑एंड वर्कफ़्लो है। यह समझकर कि **expose port in docker** क्या करता है और `-p` फ़्लैग ट्रैफ़िक को कैसे फ़ॉरवर्ड करता है, आप किसी भी सर्विस को कंटेनराइज़ कर सकते हैं और उसे अपने होस्ट या व्यापक नेटवर्क से पहुँचा सकते हैं।

अगला क्या? Flask ऐप को Go बाइनरी से बदलें, `-e` के साथ एनवायरनमेंट वेरिएबल जोड़ें, या अपनी नई बनी इमेज को Docker Hub पर `docker push` से पुश करें। संभावनाएँ अनंत हैं, और आपने DevOps की दुनिया में एक नई सुपरपावर हासिल कर ली है।

Happy container


## अगला आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑बाय‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच का अन्वेषण कर सकें।

- [Master Image Rendering in Excel Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/images-shapes/master-image-rendering-excel-aspose-cells-net/)
- [How to Add an Image to a Chart with Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/charts-graphs/add-image-chart-aspose-cells-dotnet/)
- [How to Add Image Hyperlinks in .NET Workbooks Using Aspose.Cells for Enhanced Interactivity](/cells/english/net/images-shapes/adding-image-hyperlinks-net-workbooks-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}