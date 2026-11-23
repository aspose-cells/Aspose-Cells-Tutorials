---
category: general
date: 2026-11-22
description: Flask का उपयोग करके वेब ऐप में Excel को सर्व करने का तरीका सीखें। यह
  गाइड दिखाता है कि Excel वर्कबुक को कैसे लोड करें और GridJs के साथ वेब पर Excel को
  कैसे प्रदर्शित करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to serve excel
- load excel workbook
- display excel web
language: hi
lastmod: 2026-11-22
og_description: Flask और GridJs का उपयोग करके Excel फ़ाइलें कैसे सर्व करें। इस पूर्ण
  ट्यूटोरियल का पालन करके Excel वर्कबुक लोड करें और इसे वेब पर प्रदर्शित करें।
og_image_alt: Screenshot of a Flask‑powered GridJs table showing Excel data
og_title: Flask के साथ Excel को सर्व करने का तरीका – चरण‑दर‑चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to serve Excel in a web app using Flask. This guide shows
    how to load Excel workbook and display Excel on the web with GridJs.
  headline: How to serve Excel files with Flask and GridJs
  type: TechArticle
- description: Learn how to serve Excel in a web app using Flask. This guide shows
    how to load Excel workbook and display Excel on the web with GridJs.
  name: How to serve Excel files with Flask and GridJs
  steps:
  - name: Load the Excel workbook
    text: '```python # Step 1: Load the workbook you want to expose via GridJs import
      cells'
  - name: Create a GridJs server‑side handler
    text: '```python # Step 2: Create a GridJs server‑side handler for the workbook
      grid_handler = cells.GridJsHandler(workbook) ```'
  - name: Enable optional features (lazy loading)
    text: '```python # Step 3: Enable optional features (e.g., lazy loading for large
      sheets) grid_handler.settings.lazy_load = True ```'
  - name: Set up a minimal Flask application
    text: '```python # Step 4: Set up a minimal Flask application to serve the GridJs
      UI from flask import Flask, request, jsonify'
  - name: Define the GridJs endpoint
    text: '```python # Step 5: Define an endpoint that returns the current view state
      # and applies any client‑side edits sent as JSON @app.route("/gridjs", methods=["GET",
      "POST"]) def gridjs(): if request.method == "POST": # Apply edits sent from
      the GridJs UI grid_handler.apply_changes(request.json) # Retur'
  - name: Run the Flask server
    text: '```python # Step 6: Run the Flask server (default port 5000) if __name__
      == "__main__": # Debug mode is off for production; enable it only during development.
      app.run(port=5000, debug=False) ```'
  type: HowTo
tags:
- Flask
- Python
- Excel
title: Flask और GridJs के साथ Excel फ़ाइलों को कैसे सर्व करें
url: /hi/python/integration-and-interoperability/how-to-serve-excel-files-with-flask-and-gridjs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Flask और GridJs के साथ Excel फ़ाइलें सर्व करने का तरीका

यदि आपको Python वेब एप्लिकेशन में **how to serve excel** की आवश्यकता है, तो यह ट्यूटोरियल एक पूर्ण समाधान दिखाता है। आप सीखेंगे कि कैसे `cells` लाइब्रेरी के साथ **load excel workbook** किया जाता है, इसे Flask एंडपॉइंट के माध्यम से एक्सपोज़ किया जाता है, और उपयोगकर्ताओं को GridJs का उपयोग करके **display excel web** करने दिया जाता है।

हम कोड की हर पंक्ति को विस्तार से देखेंगे, समझाएंगे कि प्रत्येक भाग क्यों महत्वपूर्ण है, और आपको एक तैयार‑से‑चलाने वाला उदाहरण देंगे। गाइड के अंत तक आप किसी भी `.xlsx` फ़ाइल को एक रिस्पॉन्सिव, क्लाइंट‑साइड ग्रिड में एम्बेड कर सकते हैं, बिना कस्टम JavaScript डेटा पार्सर लिखे।

## पूर्वापेक्षाएँ

- Python 3.9+ स्थापित हो  
- `flask` और `cells` पैकेज (`pip install flask cells`)  
- एक नमूना Excel फ़ाइल (जैसे, `sample.xlsx`) ज्ञात डायरेक्टरी में  

कोई अतिरिक्त फ्रंट‑एंड फ्रेमवर्क आवश्यक नहीं है; GridJs स्वचालित रूप से UI संभालता है।

## समाधान का अवलोकन

मुख्य विचार सरल है:

1. **Load** सर्वर पर Excel वर्कबुक लोड करें।  
2. **Create** एक `GridJsHandler` बनाएं जो वर्कशीट डेटा को GridJs द्वारा अपेक्षित JSON फ़ॉर्मेट में बदलता है।  
3. **Expose** एक Flask रूट जो JSON व्यू लौटाता है और क्लाइंट से एडिट्स स्वीकार करता है।  
4. **Run** Flask सर्वर ताकि ब्राउज़र डेटा फ़ेच कर सके और ग्रिड रेंडर कर सके।  

अब चलिए प्रत्येक चरण को लागू करते हैं।

## Flask और GridJs के साथ Excel सर्व करने का तरीका

### चरण 1: Excel वर्कबुक लोड करें

```python
# Step 1: Load the workbook you want to expose via GridJs
import cells

workbook_path = "YOUR_DIRECTORY/sample.xlsx"
workbook = cells.Workbook(workbook_path)
```

**यह क्यों महत्वपूर्ण है:**  
`cells.Workbook` `.xlsx` फ़ाइल को मेमोरी में प्रतिनिधित्व में पार्स करता है। स्टार्टअप पर वर्कबुक को एक बार लोड करने से सर्वर तेज़ रहता है क्योंकि बाद के अनुरोध उसी ऑब्जेक्ट को पुनः उपयोग करते हैं, फ़ाइल सिस्टम को बार‑बार एक्सेस करने की बजाय।

### चरण 2: GridJs सर्वर‑साइड हैंडलर बनाएं

```python
# Step 2: Create a GridJs server‑side handler for the workbook
grid_handler = cells.GridJsHandler(workbook)
```

**यह क्यों महत्वपूर्ण है:**  
`GridJsHandler` Excel पंक्तियों/कॉलमों को GridJs द्वारा उपयोग किए जाने वाले JSON स्कीमा में बदलने का सारांश प्रदान करता है। यह क्लाइंट‑साइड एडिट्स को ट्रैक भी करता है, जिससे आवश्यकता पड़ने पर आप बाद में बदलावों को वर्कबुक में सहेज सकते हैं।

### चरण 3: वैकल्पिक सुविधाएँ सक्षम करें (lazy loading)

```python
# Step 3: Enable optional features (e.g., lazy loading for large sheets)
grid_handler.settings.lazy_load = True
```

**यह क्यों महत्वपूर्ण है:**  
जब एक वर्कशीट में हजारों पंक्तियाँ होती हैं, तो पूरी डेटा सेट को एक साथ भेजना ब्राउज़र को ओवरलोड कर सकता है। Lazy loading डेटा को पेज दर पेज स्ट्रीम करता है, जिससे **display excel web** परिदृश्य में प्रदर्शन सुधरता है।

### चरण 4: न्यूनतम Flask एप्लिकेशन सेट अप करें

```python
# Step 4: Set up a minimal Flask application to serve the GridJs UI
from flask import Flask, request, jsonify

app = Flask(__name__)
```

**यह क्यों महत्वपूर्ण है:**  
Flask एक हल्का HTTP सर्वर प्रदान करता है जो JSON एंडपॉइंट्स और स्थैतिक फ़ाइलें सर्व कर सकता है। Flask एप्लिकेशन को न्यूनतम रखने से अटैक सतह कम होती है और उदाहरण को अनुकूलित करना आसान बनता है।

### चरण 5: GridJs एंडपॉइंट परिभाषित करें

```python
# Step 5: Define an endpoint that returns the current view state
#         and applies any client‑side edits sent as JSON
@app.route("/gridjs", methods=["GET", "POST"])
def gridjs():
    if request.method == "POST":
        # Apply edits sent from the GridJs UI
        grid_handler.apply_changes(request.json)
    # Return the JSON view expected by GridJs
    return jsonify(grid_handler.get_view())
```

**यह क्यों महत्वपूर्ण है:**  

- **GET** – ब्राउज़र प्रारंभिक वर्कशीट व्यू फ़ेच करता है।  
- **POST** – जब उपयोगकर्ता किसी सेल को संपादित करता है, तो GridJs एक JSON पेलोड भेजता है; `apply_changes` उन एडिट्स को हैंडलर की आंतरिक स्थिति में मर्ज कर देता है।  

`grid_handler.get_view()` लौटाने से यह सुनिश्चित होता है कि क्लाइंट हमेशा नवीनतम डेटा प्राप्त करे, जो एक सुगम **display excel web** अनुभव के लिए आवश्यक है।

### चरण 6: Flask सर्वर चलाएँ

```python
# Step 6: Run the Flask server (default port 5000)
if __name__ == "__main__":
    # Debug mode is off for production; enable it only during development.
    app.run(port=5000, debug=False)
```

**यह क्यों महत्वपूर्ण है:**  
पोर्ट 5000 पर चलाना Flask का डिफ़ॉल्ट है, जिससे स्थानीय रूप से परीक्षण करना आसान हो जाता है (`http://localhost:5000/gridjs`)। प्रोडक्शन में आप Flask को एक WSGI सर्वर (जैसे, Gunicorn) के पीछे रखेंगे और संभवतः HTTPS सक्षम करेंगे।

## अपेक्षित JSON आउटपुट

जब आप GET अनुरोध के साथ `http://localhost:5000/gridjs` पर नेविगेट करते हैं, तो प्रतिक्रिया इस प्रकार दिखती है:

```json
{
  "columns": ["A", "B", "C"],
  "data": [
    ["Header1", "Header2", "Header3"],
    ["Row1Col1", "Row1Col2", "Row1Col3"],
    ["Row2Col1", "Row2Col2", "Row2Col3"]
  ],
  "settings": {
    "lazy_load": true
  }
}
```

GridJs इस पेलोड को स्वचालित रूप से उपभोग करता है, ब्राउज़र में एक खोज योग्य, सॉर्टेबल टेबल रेंडर करता है।

## पूर्ण चलाने योग्य उदाहरण

नीचे पूर्ण स्क्रिप्ट है जिसे आप `app.py` में कॉपी करके चलाएँ:

```python
import cells
from flask import Flask, request, jsonify

# -------------------------------------------------
# 1. Load the Excel workbook
# -------------------------------------------------
workbook_path = "YOUR_DIRECTORY/sample.xlsx"
workbook = cells.Workbook(workbook_path)

# -------------------------------------------------
# 2. Create the GridJs handler
# -------------------------------------------------
grid_handler = cells.GridJsHandler(workbook)

# -------------------------------------------------
# 3. Enable lazy loading (optional but recommended)
# -------------------------------------------------
grid_handler.settings.lazy_load = True

# -------------------------------------------------
# 4. Initialize Flask
# -------------------------------------------------
app = Flask(__name__)

# -------------------------------------------------
# 5. Define the GridJs endpoint
# -------------------------------------------------
@app.route("/gridjs", methods=["GET", "POST"])
def gridjs():
    if request.method == "POST":
        # Apply client‑side edits
        grid_handler.apply_changes(request.json)
    # Return current view as JSON
    return jsonify(grid_handler.get_view())

# -------------------------------------------------
# 6. Run the server
# -------------------------------------------------
if __name__ == "__main__":
    app.run(port=5000, debug=False)
```

स्क्रिप्ट चलाएँ:

```bash
python app.py
```

एक ब्राउज़र खोलें और इसे एक साधारण HTML पेज की ओर इंगित करें जो GridJs लोड करता है ( `<script>` टैग के लिए GridJs दस्तावेज़ देखें)। ग्रिड तुरंत Excel सामग्री दिखाएगा।

## सामान्य विविधताएँ और किनारे के मामले

| स्थिति | अनुकूलन कैसे करें |
|-----------|--------------|
| **एकाधिक वर्कशीट्स** | प्रत्येक शीट के लिए एक अलग `GridJsHandler` बनाएं और अलग-अलग एंडपॉइंट (`/gridjs/sheet1`, `/gridjs/sheet2`) एक्सपोज़ करें। |
| **बड़ी फ़ाइलें (>10 MB)** | Flask की अनुरोध आकार सीमा (`app.config['MAX_CONTENT_LENGTH']`) बढ़ाएँ और `lazy_load` को सक्षम रखें। |
| **फ़ाइल में बदलाव सहेजना** | `apply_changes` के बाद, `workbook.save("output.xlsx")` कॉल करके बदलावों को डिस्क पर लिखें। |
| **प्रमाणीकरण** | डेटा लौटाने से पहले एंडपॉइंट को Flask‑Login या API टोकन जांच के साथ रैप करें। |
| **बाहरी फ्रंट‑एंड्स के लिए CORS** | क्रॉस‑ओरिजिन अनुरोधों की अनुमति देने के लिए `from flask_cors import CORS; CORS(app)` जोड़ें। |

ये बदलाव आपको **load excel workbook** प्रक्रिया को प्रोडक्शन वर्कलोड्स तक स्केल करने में मदद करते हैं।

## प्रो टिप्स

- **Cache the JSON view** यदि वर्कबुक शायद ही बदलती है; `grid_handler.get_view()` के आसपास `functools.lru_cache` का उपयोग करके सीरियलाइज़ेशन ओवरहेड कम करें।  
- **Validate incoming edits** (`request.json`) ताकि खराब डेटा वर्कबुक को भ्रष्ट न कर सके।  
- HTTPS पर सर्व करने के लिए, ट्रैफ़िक एन्क्रिप्ट करने हेतु `app.run(ssl_context=('cert.pem', 'key.pem'))` सेट करें।

## निष्कर्ष

अब आप जानते हैं कि Flask और GridJs का उपयोग करके **how to serve excel** फ़ाइलें कैसे सर्व करें, वर्कबुक लोड करने से लेकर JSON व्यू लौटाने तक जिसे ब्राउज़र रेंडर कर सकता है। उदाहरण पूरी लाइफ़साइकल को कवर करता है: **load excel workbook**, lazy loading सक्षम करना, REST एंडपॉइंट एक्सपोज़ करना, और प्रोडक्शन‑रेडी सर्वर चलाना।

अगला, संबंधित विषयों का अन्वेषण करें जैसे React फ्रंट‑एंड में **display excel web**, या हैंडलर को क्लाउड स्टोरेज (जैसे, AWS S3) से **load excel workbook** करने के लिए विस्तारित करें। GridJs कॉलम्स को स्टाइल करने, पेजिनेशन जोड़ने, या उपयोगकर्ता एडिट्स को मूल स्प्रेडशीट में सहेजने के साथ प्रयोग करें।

कोडिंग का आनंद लें, और स्थिर Excel फ़ाइलों को इंटरैक्टिव वेब टेबल्स में बदलने का मज़ा लें!

## अब आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स निकट-संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करती हैं।

- [How to Load and Modify Excel Files Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/workbook-operations/load-modify-excel-aspose-cells-net/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}