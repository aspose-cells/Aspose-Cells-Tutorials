---
category: general
date: 2026-06-21
description: Docker में कंटेनर पोर्ट को एक्सपोज़ करें, साथ ही वर्किंग डायरेक्टरी सेट
  करें और अपने ऐप स्रोत को कॉपी करें। चरण‑दर‑चरण सीखें कि Python API को कैसे Dockerize
  किया जाए।
draft: false
keywords:
- expose container port
- set working directory docker
- dockerfile copy app
- copy source into container
- dockerize python api
language: hi
og_description: Docker में कंटेनर पोर्ट को एक्सपोज़ करें, कार्य निर्देशिका सेट करें,
  और अपने स्रोत को कंटेनर में कॉपी करें। यह ट्यूटोरियल दिखाता है कि Python API को
  कैसे Dockerize किया जाए।
og_title: Docker में कंटेनर पोर्ट को एक्सपोज़ करें – पूर्ण गाइड
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
title: Docker में कंटेनर पोर्ट को एक्सपोज़ करें – पूर्ण Dockerfile गाइड
url: /hi/python/import-and-export/expose-container-port-in-docker-full-dockerfile-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Docker में कंटेनर पोर्ट को एक्सपोज़ करें – पूर्ण Dockerfile गाइड

क्या आपने कभी सोचा है कि **expose container port** कैसे किया जाए जब आप एक Python API को कंटेनराइज़ कर रहे हों? आप अकेले नहीं हैं। अधिकांश डेवलपर्स को यही समस्या आती है: एप्लिकेशन लोकली चलती है, लेकिन Docker के अंदर होने पर बाहरी दुनिया उससे कनेक्ट नहीं कर पाती। इस ट्यूटोरियल में हम एक पूर्ण Dockerfile को चरण‑दर‑चरण देखेंगे जो न केवल **expose container port** करता है बल्कि **set working directory docker**, **dockerfile copy app**, और **copy source into container** भी करता है—वे सभी हिस्से जो आपको **dockerize python api** बिना किसी परेशानी के बनाने में मदद करेंगे।

हम एक छोटा Flask एप से शुरू करेंगे, फिर शून्य से Docker इमेज बनाएँगे, प्रत्येक निर्देश को समझाएँगे, और अंत में कंटेनर चलाएँगे ताकि आप `http://localhost:5000/health` को हिट कर सकें। अंत तक आपके पास एक प्रोडक्शन‑रेडी Docker इमेज होगी जिसे आप किसी भी रजिस्ट्री में पुश कर सकते हैं।

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

- Docker Engine ≥ 20.10 स्थापित (Docker Desktop Windows/macOS पर ठीक काम करता है, Linux पर Docker Engine)।
- Python और Flask (या कोई भी WSGI‑compatible फ्रेमवर्क) की बेसिक समझ।
- एक टेक्स्ट एडिटर या IDE (VS Code, PyCharm, आदि) Dockerfile और Python कोड को एडिट करने के लिए।

आधिकारिक Aspose.Cells Python.NET बेस इमेज में जो भी लाइब्रेरीज़ शामिल हैं, उसके अलावा कोई अतिरिक्त लाइब्रेरी आवश्यक नहीं है।

## Step 1: Create a Minimal Python API

पहले, एक छोटा Flask सर्विस लिखते हैं जिसे हम बाद में **dockerize python api** करेंगे। इसे `api_server.py` के रूप में एक खाली फ़ोल्डर में सेव करें।

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

`host="0.0.0.0"` क्यों? कंटेनर के अंदर `localhost` स्वयं कंटेनर को दर्शाता है। `0.0.0.0` पर बाइंड करने से Flask किसी भी नेटवर्क इंटरफ़ेस से कनेक्शन स्वीकार करता है, जो बाद में **expose container port** चरण के लिए आवश्यक है।

## Step 2: Choose the Right Base Image

इस उदाहरण में हम Aspose की आधिकारिक **Aspose.Cells Python.NET base image** (`aspose/cells-pythonnet:6.22`) का उपयोग करेंगे। इसमें पहले से .NET runtime, Python 3.9, और Aspose.Cells लाइब्रेरी शामिल है—यदि आपका API Excel मैनिपुलेशन करता है तो यह परफेक्ट है।

```dockerfile
# Use the official Aspose.Cells Python.NET base image
FROM aspose/cells-pythonnet:6.22
```

यदि आपको Aspose की ज़रूरत नहीं है, तो आप इसे `python:3.11-slim` से बदल सकते हैं। बाकी Dockerfile समान रहता है।

## Step 3: **Dockerfile Copy App** – Copy Your Source Into the Container

अब हमें कोड को इमेज में लाना है। यही वह जगह है जहाँ **dockerfile copy app** निर्देश काम आता है।

```dockerfile
# Copy the entire current directory (your app) into /app inside the container
COPY . /app
```

`.` बिल्ड कॉन्टेक्स्ट को दर्शाता है—वह फ़ोल्डर जहाँ आप `docker build` चलाते हैं। सब कुछ कॉपी करने से `requirements.txt` (यदि मौजूद है) और कोई भी स्टैटिक एसेट्स भी आ जाते हैं। यदि आप इमेज को हल्का रखना चाहते हैं, तो केवल आवश्यक फ़ाइलों को सूचीबद्ध करें।

## Step 4: **Set Working Directory Docker** – Define the Working Directory

कोड कॉपी करने के बाद, हम Docker को बताते हैं कि आगे के कमांड कहाँ चलेंगे। यही **set working directory docker** चरण है।

```dockerfile
# Set /app as the working directory for the rest of the build
WORKDIR /app
```

क्यों? इससे बाद में पूरे पाथ टाइप करने की ज़रूरत नहीं रहती (जैसे `python api_server.py` बनाम `python /app/api_server.py`)। यह कंटेनर की फ़ाइल‑सिस्टम लेआउट को भी स्पष्ट बनाता है।

## Step 5: Install Python Dependencies (Optional but Recommended)

यदि आपका API बाहरी पैकेजों पर निर्भर है, तो एक `requirements.txt` बनाकर उन्हें अलग लेयर में इंस्टॉल करें। इससे कैशिंग बेहतर होती है।

```dockerfile
# Install Python dependencies (if requirements.txt exists)
RUN if [ -f requirements.txt ]; then pip install --no-cache-dir -r requirements.txt; fi
```

यह कंडीशन सुनिश्चित करता है कि यदि आपके पास `requirements.txt` नहीं है तो बिल्ड फेल नहीं होगा—यह मिनिमल उदाहरण के लिए उपयोगी है।

## Step 6: **Expose Container Port** – Make the API Reachable from Outside

अब हम मुख्य चरण पर आते हैं: **expose container port**। यह Docker को बताता है कि कंटेनर किस पोर्ट पर सुनेंगे, जिससे रन‑टाइम पर पोर्ट‑मैपिंग संभव हो जाती है।

```dockerfile
# Expose the Flask port (5000) so the host can forward traffic
EXPOSE 5000
```

ध्यान दें कि `EXPOSE` केवल एक डॉक्यूमेंटेशन हिन्ट है; वास्तविक मैपिंग तब होती है जब आप `docker run -p` चलाते हैं। फिर भी पोर्ट घोषित करना बेस्ट प्रैक्टिस है और Docker Compose जैसे टूल्स को सही पोर्ट फ़ॉरवर्ड करने में मदद करता है।

## Step 7: Define the Startup Command

अंत में, हम Docker को बताते हैं कि API कैसे लॉन्च करनी है। यह `CMD` निर्देश है।

```dockerfile
# Start the Flask API when the container launches
CMD ["python", "api_server.py"]
```

JSON एरे फ़ॉर्मेट का उपयोग शेल इंटरप्रिटेशन समस्याओं से बचाता है और कमांड को अधिक पोर्टेबल बनाता है।

## Full Dockerfile Recap

सभी हिस्सों को मिलाकर, यहाँ पूरा Dockerfile है जिसे आप कॉपी‑पेस्ट कर सकते हैं:

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

> **Pro tip:** यदि आपके पास कई डिपेंडेंसीज़ हैं तो `COPY` लाइन को `RUN pip install` लाइन से पहले रखें। Docker इंस्टॉल किए गए पैकेजों की लेयर को कैश करेगा, इसलिए कोड बदलने पर पूरी इमेज फिर से बिल्ड नहीं होगी।

## Step 8: Build the Docker Image

उस फ़ोल्डर में टर्मिनल खोलें जिसमें `Dockerfile` और `api_server.py` हैं, फिर चलाएँ:

```bash
docker build -t my-python-api .
```

Docker प्रत्येक स्टेप को स्ट्रीम करेगा और जहाँ संभव होगा कैश्ड लेयर्स दिखाएगा। यदि सब कुछ ठीक रहा तो आपको `Successfully tagged my-python-api:latest` दिखाई देगा।

## Step 9: Run the Container and Verify the Port Mapping

अब कंटेनर लॉन्च करें, अंदरूनी `5000` को होस्ट के `5000` (या कोई अन्य पोर्ट) पर मैप करें:

```bash
docker run -d -p 5000:5000 --name api_container my-python-api
```

- `-d` कंटेनर को डिटैच्ड मोड में चलाता है।
- `-p 5000:5000` Docker को बताता है कि होस्ट पोर्ट 5000 को कंटेनर पोर्ट 5000 पर फ़ॉरवर्ड करे—बिल्कुल वही जो **expose container port** निर्देश ने तैयार किया था।

आप `curl` से एंडपॉइंट टेस्ट कर सकते हैं:

```bash
curl http://localhost:5000/health
```

अपेक्षित आउटपुट:

```json
{
  "status": "OK",
  "message": "API is running"
}
```

यदि यह JSON दिखता है, तो बधाई हो—आपने सफलतापूर्वक **dockerize python api** कर लिया और पोर्ट एक्सेसिबल बना दिया।

## Common Edge Cases & How to Handle Them

### 1. Changing the Host Port

कभी‑कभी पोर्ट 5000 आपके मशीन पर पहले से उपयोग में होता है। कोई बात नहीं—मैपिंग के होस्ट साइड को बदल दें:

```bash
docker run -d -p 8080:5000 my-python-api
```

अब `http://localhost:8080/health` काम करेगा जबकि कंटेनर अभी भी `5000` पर सुन रहा है।

### 2. Multi‑Stage Builds for Smaller Images

यदि प्रोडक्शन में आपको पूरे Aspose.Cells रनटाइम की ज़रूरत नहीं है, तो आप एक मल्टी‑स्टेज बिल्ड बना सकते हैं जहाँ भारी इमेज में एसेट्स कंपाइल हों और फिर केवल रनटाइम बाइट्स को हल्के `python:3.11-slim` फाइनल स्टेज में कॉपी किया जाए। इससे अंतिम इमेज का आकार काफी घट जाता है।

### 3. Using Docker Compose

ज्यादा जटिल सेटअप (जैसे API के साथ डेटाबेस) के लिए, वही निर्देश `docker-compose.yml` में रखें:

```yaml
version: "3.9"
services:
  api:
    build: .
    ports:
      - "5000:5000"
    restart: unless-stopped
```

Compose स्वचालित रूप से `EXPOSE` निर्देश को मानता है, इसलिए आपको पोर्ट मैपिंग दोहराने की ज़रूरत नहीं पड़ेगी।

### 4. Environment Variables

यदि आपके API को कॉन्फ़िगरेशन (जैसे सीक्रेट की) चाहिए, तो उन्हें रन‑टाइम पर पास करें:

```bash
docker run -d -p 5000:5000 -e SECRET_KEY=supersecret my-python-api
```

Python में आप `os.getenv("SECRET_KEY")` से पढ़ सकते हैं।

## Debugging Tips

- **Container exits immediately?** `docker logs api_container` से लॉग देखें। अक्सर Flask में `host="0.0.0.0"` भूल जाना कारण होता है।
- **Port already in use?** `docker ps` और `netstat -tulpn` से जांचें। ऊपर दिखाए अनुसार अलग होस्ट पोर्ट इस्तेमाल करें।
- **Missing dependencies?** सुनिश्चित करें कि `requirements.txt` `RUN pip install` स्टेप से पहले मौजूद है, या पैकेज सीधे Dockerfile में जोड़ें।

## Recap

हमने एक साधारण Flask ऐप से शुरू किया, एक मजबूत बेस इमेज चुनी, **dockerfile copy app** से कोड अंदर लाया, **set working directory docker** से साफ़ एक्सीक्यूशन सेट किया, `EXPOSE 5000` के साथ **expose container port** घोषित किया, और `CMD` के साथ सर्विस लॉन्च की। इमेज को बिल्ड और रन करने से हमें एक पूरी तरह से कार्यशील **dockerize python api** मिला जिसे कोई भी पुल करके चला सकता है।

## What’s Next?

- Dockerfile में **health‑check** जोड़ें (`HEALTHCHECK CMD curl -f http://localhost:5000/health || exit 1`)।
- लॉगिंग को stdout पर इम्प्लीमेंट करें ताकि Docker उसे कैप्चर कर सके।
- API को HTTPS के साथ सुरक्षित करें।

## What Should You Learn Next?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक रिसोर्स में पूर्ण कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकते हैं और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोच को एक्सप्लोर कर सकते हैं।

- [Copy Sheets Within Workbook Using Aspose.Cells for .NET - Step-by-Step Guide](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)
- [Copy Data in Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}