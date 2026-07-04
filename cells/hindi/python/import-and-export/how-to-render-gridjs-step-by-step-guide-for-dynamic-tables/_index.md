---
category: general
date: 2026-07-03
description: पूरा HTML/JS उदाहरण के साथ मिनटों में Gridjs को रेंडर करना सीखें। इसमें
  Gridjs लाइब्रेरी CDN, लेज़ी लोडिंग, और कॉन्फ़िगरेशन JSON टिप्स शामिल हैं।
draft: false
keywords:
- how to render gridjs
- gridjs configuration JSON
- gridjs lazy loading
- gridjs library CDN
- gridjs render method
language: hi
og_description: 'Gridjs को जल्दी रेंडर करने का तरीका: CDN का उपयोग करें, कॉन्फ़िगरेशन
  JSON प्राप्त करें, और रेंडर मेथड को कॉल करें। डायनेमिक डेटा टेबल्स के लिए एकदम उपयुक्त।'
og_title: Gridjs को कैसे रेंडर करें – पूर्ण कार्यान्वयन गाइड
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to render Gridjs in minutes with a full HTML/JS example.
    Includes Gridjs library CDN, lazy loading, and configuration JSON tips.
  headline: How to Render Gridjs – Step‑by‑Step Guide for Dynamic Tables
  type: TechArticle
- description: Learn how to render Gridjs in minutes with a full HTML/JS example.
    Includes Gridjs library CDN, lazy loading, and configuration JSON tips.
  name: How to Render Gridjs – Step‑by‑Step Guide for Dynamic Tables
  steps:
  - name: Why Use the CDN?
    text: '- **Performance:** Browsers cache the file across sites, so returning visitors
      may already have it. - **Simplicity:** No bundler configuration, just a single
      `<script>` tag. - **Lazy loading:** You can defer the script with `defer` or
      load it only when needed, which ties into our next step.'
  - name: Breaking Down the Code
    text: '| Line | What It Does | Why It Matters | |------|--------------|----------------|
      | `fetch(''YOUR_DIRECTORY/lazygrid.json'')` | Retrieves the configuration JSON
      via HTTP GET. | Keeps the HTML clean and allows you to change the grid layout
      without touching the page code. | | `.then(response => response'
  - name: Sample `lazygrid.json`
    text: Below is a minimal yet functional configuration file. Save it as `lazygrid.json`
      in the same directory as your HTML (or adjust the fetch path accordingly).
  - name: 1. Using Custom Render Functions
    text: 'Sometimes you need to format a cell—say, add a badge for ages over 28.
      Extend the column definition:'
  - name: 2. Server‑Side Pagination
    text: If your dataset is huge, fetching the entire JSON can be slow. Gridjs supports
      server‑side pagination—just set `pagination.server` to `true` and implement
      an API endpoint that returns slices of data based on `page` and `limit` query
      parameters.
  - name: 3. Styling with CSS Variables
    text: 'The Mermaid theme uses CSS variables for colors. Override them in a `<style>`
      block:'
  - name: 4. Accessibility Considerations
    text: Gridjs adds ARIA attributes automatically, but you can enhance keyboard
      navigation by ensuring your placeholder `<div>` is focusable (`tabindex="0"`).
      This helps screen‑reader users interact with the table.
  type: HowTo
tags:
- JavaScript
- Front‑end
- Data Tables
title: Gridjs को कैसे रेंडर करें – डायनामिक टेबल्स के लिए स्टेप‑बाय‑स्टेप गाइड
url: /hi/python/import-and-export/how-to-render-gridjs-step-by-step-guide-for-dynamic-tables/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ग्रिडजएस को रेंडर करने की स्टेप‑बाय‑स्टेप गाइड फॉर डायनामिक टेबल्स

क्या आप कभी सोचे हैं **कैसे ग्रिडजएस को** एक साधारण HTML पेज पर बिना भारी फ्रेमवर्क के रेंडर किया जाए? आप अकेले नहीं हैं। कई डेवलपर्स को एक हल्की, सॉर्टेबल टेबल चाहिए होती है जिसे JSON फ़ाइल से डेटा मिल सके, और ग्रिडजएस इसे आसान बनाता है। इस ट्यूटोरियल में हम हर लाइन को समझेंगे, ग्रिडजएस लाइब्रेरी CDN लोड करने से लेकर कॉन्फ़िगरेशन JSON को लेज़ी फ़ेच करने और अंत में रेंडर मेथड कॉल करने तक।

हम कुछ बेस्ट‑प्रैक्टिस टिप्स भी देंगे—जैसे लेज़ी लोडिंग से पेज स्पीड कैसे बढ़ती है, और आपका JSON कैसे स्ट्रक्चर करना चाहिए ताकि ग्रिडजएस रेंडर मेथड बिना दिक्कत काम करे। अंत तक आपके पास एक पूरी तरह से फंक्शनल ग्रिड होगा जिसे आप किसी भी प्रोजेक्ट में डाल सकते हैं।

## आप क्या बनाएँगे

- एक मिनिमल HTML पेज जो CDN से ग्रिडजएस को खींचेगा  
- एक `lazygrid.json` फ़ाइल जो कॉलम, डेटा और वैकल्पिक प्लगइन्स को परिभाषित करेगी  
- जावास्क्रिप्ट जो JSON को फ़ेच करेगा, एक Gridjs इंस्टेंस बनाएगा, और उसे प्लेसहोल्डर में रेंडर करेगा  

कोई बिल्ड टूल नहीं, कोई npm नहीं, सिर्फ साधारण HTML और थोड़ा वैनिला JS। स्टैटिक साइट्स, डॉक्यूमेंटेशन पोर्टल्स, या तेज़ प्रोटोटाइप्स के लिए परफेक्ट।

## प्री‑रिक्विज़िट्स

- HTML और जावास्क्रिप्ट की बेसिक समझ (कोई फ्रेमवर्क नहीं चाहिए)  
- एक वेब सर्वर या लोकल डेवलपमेंट एनवायरनमेंट जो स्टैटिक फ़ाइलें सर्व कर सके (जैसे VS Code Live Server)  
- `lazygrid.json` फ़ाइल को ब्राउज़र से एक्सेसिबल जगह पर रखें  

अगर आप इनसे सहज हैं, तो चलिए शुरू करते हैं।

## स्टेप 1: ग्रिडजएस लाइब्रेरी CDN शामिल करें

पेज पर ग्रिडजएस लाने का सबसे तेज़ तरीका है उसका UMD बंडल CDN से रेफ़र करना। इससे npm इंस्टॉल की जरूरत नहीं रहती और ट्यूटोरियल हल्का रहता है।

```html
<!-- Step 1: Include the Gridjs library -->
<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
```

> **प्रो टिप:** `theme/mermaid.min.css` स्टाइलशीट एक साफ़, मॉडर्न लुक देती है। अगर आप अलग स्टाइल पसंद करते हैं तो इसे किसी और थीम से बदल सकते हैं।

### CDN क्यों इस्तेमाल करें?

- **परफ़ॉर्मेंस:** ब्राउज़र साइट्स के बीच फ़ाइल को कैश कर लेता है, इसलिए रिटर्निंग विज़िटर्स के पास पहले से ही यह फ़ाइल हो सकती है।  
- **सिम्प्लिसिटी:** कोई बंडलर कॉन्फ़िगरेशन नहीं, सिर्फ एक `<script>` टैग।  
- **लेज़ी लोडिंग:** आप स्क्रिप्ट को `defer` के साथ डिफर कर सकते हैं या जब ज़रूरत हो तभी लोड कर सकते हैं, जो हमारे अगले स्टेप से जुड़ा है।

## स्टेप 2: ग्रिड के लिए एक प्लेसहोल्डर एलिमेंट जोड़ें

ग्रिडजएस को टेबल माउंट करने के लिए एक DOM नोड चाहिए। एक यूनिक ID वाला `<div>` बनाएं—यही वह जगह होगी जहाँ ग्रिडजएस रेंडर मेथड टेबल मार्कअप इन्जेक्ट करेगा।

```html
<!-- Step 2: Placeholder where Gridjs will appear -->
<div id="grid"></div>
```

अगर आपको कस्टम चौड़ाई या मार्जिन चाहिए तो आप इस कंटेनर को CSS से स्टाइल कर सकते हैं। अभी के लिए, थीम की डिफ़ॉल्ट स्टाइलिंग चीज़ों को व्यवस्थित रखेगी।

## स्टेप 3: ग्रिडजएस कॉन्फ़िगरेशन JSON लोड करें और ग्रिड रेंडर करें

यहीं पर जादू होता है। हम एक JSON फ़ाइल (`lazygrid.json`) फ़ेच करेंगे जो कॉलम, डेटा रो और किसी भी प्लगइन को बताती है। फिर हम उस कॉन्फ़िगरेशन के साथ Gridjs को इंस्टैंशिएट करेंगे और उसका रेंडर मेथड कॉल करेंगे।

```html
<!-- Step 3: Fetch config and render Gridjs -->
<script>
  // Step 3.1: Pull the JSON config (replace the path as needed)
  fetch('YOUR_DIRECTORY/lazygrid.json')
    .then(response => {
      if (!response.ok) {
        throw new Error('Network response was not ok');
      }
      return response.json();
    })
    .then(config => {
      // Step 3.2: Create a Gridjs instance using the fetched configuration
      const grid = new GridJs(config);
      // Step 3.3: Render the grid inside the placeholder element
      grid.render(document.getElementById('grid'));
    })
    .catch(error => console.error('Error loading Gridjs config:', error));
</script>
```

### कोड का विवरण

| लाइन | क्या करता है | क्यों महत्वपूर्ण है |
|------|--------------|----------------|
| `fetch('YOUR_DIRECTORY/lazygrid.json')` | HTTP GET के ज़रिए कॉन्फ़िगरेशन JSON रिट्रीव करता है। | HTML को साफ़ रखता है और आपको ग्रिड लेआउट बदलने की अनुमति देता है बिना पेज कोड छुए। |
| `.then(response => response.json())` | रिस्पॉन्स को जावास्क्रिप्ट ऑब्जेक्ट में पार्स करता है। | सुनिश्चित करता है कि आप ग्रिडजएस को सही ऑब्जेक्ट पास कर रहे हैं। |
| `new GridJs(config)` | दी गई कॉन्फ़िग के साथ एक Gridjs इंस्टेंस बनाता है। | यह **gridjs render method** का एंट्री पॉइंट है; कॉन्फ़िग कॉलम, डेटा और प्लगइन्स को ड्राइव करता है। |
| `grid.render(document.getElementById('grid'))` | टेबल को `<div id="grid">` में इन्सर्ट करता है। | अंतिम स्टेप जो स्क्रीन पर **Gridjs को रेंडर** करता है। |
| `.catch(...)` | नेटवर्क या पार्सिंग एरर्स को ग्रेसफ़ुली हैंडल करता है। | पेज को साइलेंटली ब्रेक होने से बचाता है और डिबगिंग जानकारी देता है। |

### सैंपल `lazygrid.json`

नीचे एक मिनिमल लेकिन फंक्शनल कॉन्फ़िगरेशन फ़ाइल दी गई है। इसे `lazygrid.json` के रूप में उसी डायरेक्टरी में सेव करें जहाँ आपका HTML है (या फ़ेच पाथ को उसी अनुसार एडजस्ट करें)।

```json
{
  "columns": [
    "Name",
    "Email",
    { "id": "age", "name": "Age", "type": "number" }
  ],
  "data": [
    ["Alice", "alice@example.com", 30],
    ["Bob", "bob@example.com", 25],
    ["Carol", "carol@example.com", 27]
  ],
  "search": true,
  "pagination": {
    "enabled": true,
    "limit": 5
  }
}
```

- **gridjs configuration JSON**: `columns` एरे में साधारण स्ट्रिंग्स या ऑब्जेक्ट्स हो सकते हैं अधिक कंट्रोल के लिए (जैसे कस्टम रेंडरर्स)।  
- **gridjs lazy loading**: इस JSON को अलग रखकर आप इसे बिना HTML री‑डिप्लॉय किए बदल सकते हैं।  
- **gridjs render method**: `grid.render(...)` कॉल इस कॉन्फ़िग को पढ़ता है और टेबल डायनामिकली बनाता है।

## स्टेप 4: आउटपुट वेरिफ़ाई करें

HTML फ़ाइल को ब्राउज़र में खोलें। आपको एक सर्चेबल, पेजिनेटेड टेबल दिखना चाहिए जो `lazygrid.json` के डेटा से मेल खाता हो। डिफ़ॉल्ट Mermaid थीम हल्की शेडिंग और होवर इफ़ेक्ट्स जोड़ती है।

**अपेक्षित आउटपुट:**

| Name  | Email               | Age |
|-------|---------------------|-----|
| Alice | alice@example.com   | 30  |
| Bob   | bob@example.com     | 25  |
| Carol | carol@example.com   | 27  |

अगर टेबल नहीं दिख रहा:

1. ब्राउज़र कंसोल (F12) खोलें और एरर्स देखें।  
2. सुनिश्चित करें कि `fetch('YOUR_DIRECTORY/lazygrid.json')` में पाथ सही है।  
3. CDN स्क्रिप्ट लोड हुआ है या नहीं, नेटवर्क टैब में चेक करें।  

## एडवांस्ड टिप्स & एज केसेज

### 1. कस्टम रेंडर फ़ंक्शन्स का उपयोग

कभी‑कभी आपको सेल को फ़ॉर्मेट करना पड़ता है—जैसे 28 से ऊपर की उम्र के लिए बैज जोड़ना। कॉलम डिफ़िनिशन को इस तरह एक्सटेंड करें:

```json
{
  "id": "age",
  "name": "Age",
  "formatter": (cell) => {
    return cell > 28 ? `<span style="color:red;">${cell}</span>` : cell;
  }
}
```

> **नोट:** फ़ॉर्मैटर एक जावास्क्रिप्ट फ़ंक्शन होना चाहिए, इसलिए आपको कॉन्फ़िग को सीधे स्क्रिप्ट में एम्बेड करना पड़ेगा या अगर आप इसे JSON में रखना चाहते हैं तो मॉड्यूल के रूप में लोड करना पड़ेगा।

### 2. सर्वर‑साइड पेजिनेशन

अगर आपका डेटा सेट बहुत बड़ा है, तो पूरी JSON फ़ेच करना स्लो हो सकता है। ग्रिडजएस सर्वर‑साइड पेजिनेशन को सपोर्ट करता है—सिर्फ `pagination.server` को `true` सेट करें और एक API एंडपॉइंट इम्प्लीमेंट करें जो `page` और `limit` क्वेरी पैरामीटर्स के आधार पर डेटा के स्लाइस रिटर्न करे।

### 3. CSS वेरिएबल्स के साथ स्टाइलिंग

Mermaid थीम रंगों के लिए CSS वेरिएबल्स का उपयोग करती है। आप इन्हें `<style>` ब्लॉक में ओवरराइड कर सकते हैं:

```html
<style>
  :root {
    --gridjs-header-bg: #2c3e50;
    --gridjs-header-color: #ecf0f1;
  }
</style>
```

### 4. एक्सेसिबिलिटी कंसिडरेशन्स

ग्रिडजएस ऑटोमैटिकली ARIA एट्रिब्यूट्स जोड़ता है, लेकिन आप कीबोर्ड नेविगेशन को बेहतर बना सकते हैं अपने प्लेसहोल्डर `<div>` को फोकसेबल (`tabindex="0"`) बनाकर। इससे स्क्रीन‑रीडर यूज़र्स टेबल के साथ इंटरैक्ट कर पाएँगे।

## फुल वर्किंग एग्ज़ाम्पल

सब कुछ एक साथ लाते हुए, यहाँ एक सिंगल HTML फ़ाइल है जिसे आप कॉपी‑पेस्ट करके लोकली रन कर सकते हैं।

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>How to Render Gridjs Demo</title>
  <!-- Gridjs library CDN -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
  <style>
    /* Optional custom theme tweaks */
    :root {
      --gridjs-header-bg: #34495e;
      --gridjs-header-color: #ecf0f1;
    }
  </style>
</head>
<body>
  <!-- Placeholder for the grid -->
  <div id="grid"></div>

  <!-- Fetch config and render Gridjs -->
  <script>
    fetch('lazygrid.json')
      .then(r => r.ok ? r.json() : Promise.reject('Failed to load'))
      .then(cfg => {
        const grid = new GridJs(cfg);
        grid.render(document.getElementById('grid'));
      })
      .catch(err => console.error(err));
  </script>

  <!-- Optional screenshot for documentation -->
  <img src="gridjs-screenshot.png" alt="Screenshot demonstrating how to render Gridjs grid" style="display:none;">
</body>
</html>
```

इसे `index.html` के रूप में `lazygrid.json` के बगल में सेव करें, ब्राउज़र में खोलें, और ग्रिड तुरंत दिखाई देगा।

## निष्कर्ष

अब आपके पास **ग्रिडजएस को रेंडर करने** का स्पष्ट, एंड‑टू‑एंड उत्तर है: Gridjs लाइब्रेरी CDN लोड करें, एक `gridjs configuration JSON` प्रदान करें, उसे लेज़ी फ़ेच करें, Gridjs ऑब्जेक्ट इंस्टैंशिएट करें, और `gridjs render method` को कॉल करें। यह अप्रोच आपका HTML साफ़ रखता है, बेहतर परफ़ॉर्मेंस के लिए लेज़ी लोडिंग का फायदा देता है, और आपको कॉलम, डेटा और प्लगइन्स पर पूरी कंट्रोल देता है।

अब आगे क्या? कोशिश करें:

- **gridjs lazy loading** के साथ बड़े डेटा सेट्स को सर्वर‑साइड पेजिनेशन के ज़रिए लोड करना।  
- कस्टम सेल रेंडरर्स के साथ चार्ट्स या प्रोग्रेस बार जोड़ना।  
- एक्सपोर्ट प्लगइन्स का उपयोग करके यूज़र्स को CSV या Excel फ़ाइल डाउनलोड करने देना।  

इसे एक्सपेरिमेंट करें, और अगर कोई दिक्कत आए तो नीचे कमेंट करें। हैप्पी कोडिंग!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Render Excel Sheets as Images Using Aspose.Cells .NET for Seamless Data Visualization](/cells/english/net/import-export/render-excel-sheets-images-aspose-cells-dotnet/)
- [How to Render Excel Sheets as Images Using Aspose.Cells for Java (Workbook Operations)](/cells/english/java/workbook-operations/render-excel-sheets-images-aspose-cells-java/)
- [How to Efficiently Filter Data While Loading Excel Workbooks Using Aspose.Cells in Java](/cells/english/java/data-analysis/filter-data-excel-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}