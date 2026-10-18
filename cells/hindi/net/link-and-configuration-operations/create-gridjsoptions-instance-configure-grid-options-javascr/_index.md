---
category: general
date: 2026-05-30
description: जानिए कैसे GridJsOptions इंस्टेंस बनाएं और डायनेमिक टेबल्स के लिए ग्रिड
  विकल्प जावास्क्रिप्ट को कॉन्फ़िगर करें। पूर्ण कोड के साथ चरण‑दर‑चरण गाइड।
draft: false
keywords:
- create gridjsoptions instance
- configure grid options javascript
- gridjs initialization
- javascript data grid settings
- dynamic table configuration
language: hi
og_description: मिनटों में GridJsOptions इंस्टेंस बनाएं और जावास्क्रिप्ट में ग्रिड
  विकल्प कॉन्फ़िगर करें। पूर्ण उदाहरण, व्याख्याएँ और सर्वोत्तम अभ्यास टिप्स।
og_title: GridJsOptions इंस्टेंस बनाएं – ग्रिड विकल्प जावास्क्रिप्ट कॉन्फ़िगर करें
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to create GridJsOptions instance and configure grid options
    JavaScript for dynamic tables. Step‑by‑step guide with full code.
  headline: Create GridJsOptions Instance – Configure Grid Options JavaScript
  type: TechArticle
- description: Learn how to create GridJsOptions instance and configure grid options
    JavaScript for dynamic tables. Step‑by‑step guide with full code.
  name: Create GridJsOptions Instance – Configure Grid Options JavaScript
  steps:
  - name: Prerequisites
    text: '- A modern browser (Chrome, Edge, Firefox) – no build tools required. -
      Basic familiarity with JavaScript (variables, objects, DOM). - The Grid.js library
      (we’ll pull it from a CDN).'
  - name: Why this matters
    text: Loading the library from a CDN ensures you always get the latest stable
      version without a local install. The `<div id="grid-wrapper">` is the placeholder
      that the Grid.js constructor will target once we **configure grid options JavaScript**.
  - name: What you’re configuring
    text: '- **NumberFormatAlignment** – aligns numeric strings automatically. - **Pagination**
      – controls page size and navigation. - **Sorting** – toggles column sorting.
      - **Columns** – defines headers, data types, and custom renderers.'
  - name: Edge‑case note
    text: If you later supply a custom data source that already returns paginated
      results, you’ll want to disable Grid.js’s built‑in pagination to avoid double‑paging.
      Simply set `gridOptions.Pagination.enabled = false;`.
  - name: Expected Output
    text: 'When you open the HTML file in a browser you should see:'
  type: HowTo
tags:
- gridjs
- javascript
- data‑grid
title: GridJsOptions इंस्टेंस बनाएं – ग्रिड विकल्प जावास्क्रिप्ट कॉन्फ़िगर करें
url: /hi/net/link-and-configuration-operations/create-gridjsoptions-instance-configure-grid-options-javascr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GridJsOptions इंस्टेंस बनाएं – ग्रिड विकल्प जावास्क्रिप्ट कॉन्फ़िगर करें

क्या आप कभी सोचते थे कि **create GridJsOptions instance** को बिखरे दस्तावेज़ों में खोजे बिना कैसे बनाया जाए? आप अकेले नहीं हैं। जब आपको वेब पेज पर एक चिकनी, सॉर्टेबल टेबल चाहिए, तो ग्रिड विकल्प जावास्क्रिप्ट को कॉन्फ़िगर करना एक पॉलिश्ड UI की ओर पहला कदम है।

इस ट्यूटोरियल में हम आपको बिल्कुल वही कोड दिखाएंगे जिसकी आपको जरूरत है, समझाएंगे कि प्रत्येक सेटिंग क्यों महत्वपूर्ण है, और एक पूर्ण, चलाने योग्य उदाहरण दिखाएंगे। अंत तक आप **create GridJsOptions instance** बनाने, एलाइनमेंट, पेजिनेशन, और कस्टम सेल रेंडरर्स को ट्यून करने में सहज हो जाएंगे—सभी साधारण जावास्क्रिप्ट के साथ।

## आप क्या सीखेंगे

- स्क्रैच से **create GridJsOptions instance** कैसे बनाएं।
- प्रमुख प्रॉपर्टीज़ जो आपको **configure grid options JavaScript** करने देती हैं (सॉर्टिंग, पेजिनेशन, नंबर फ़ॉर्मेटिंग, आदि)।
- सामान्य गलतियाँ (जैसे स्ट्रिंग और न्यूमेरिक टाइप्स को मिलाना) और उन्हें कैसे टालें।
- एक पूर्ण HTML पेज जिसे आप किसी भी प्रोजेक्ट में कॉपी‑पेस्ट कर तुरंत परिणाम देख सकते हैं।

### पूर्वापेक्षाएँ

- एक आधुनिक ब्राउज़र (Chrome, Edge, Firefox) – कोई बिल्ड टूल्स आवश्यक नहीं।
- जावास्क्रिप्ट की बुनियादी समझ (वेरिएबल्स, ऑब्जेक्ट्स, DOM)।
- Grid.js लाइब्रेरी (हम इसे CDN से लेंगे)।

यदि इनमें से कोई भी परिचित नहीं लग रहा है, तो घबराएँ नहीं—प्रत्येक चरण में एक त्वरित रिफ्रेशर शामिल है।

---

## Step 1: Load Grid.js and Prepare the HTML Skeleton

**create GridJsOptions instance** बनाने से पहले हमें लाइब्रेरी चाहिए। सबसे आसान तरीका आधिकारिक CDN का उपयोग करना है। नीचे एक न्यूनतम HTML स्केलेटन है जो एक `<div>` भी रिज़र्व करता है जहाँ ग्रिड रेंडर होगा।

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Grid.js Demo – Configuring Options</title>
  <!-- Grid.js CSS -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
</head>
<body>
  <h2>Simple Data Grid</h2>
  <div id="grid-wrapper"></div>

  <!-- Grid.js JS -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
  <!-- Our custom script will go here -->
  <script src="grid-config.js"></script>
</body>
</html>
```

> **Pro tip:** अपने स्टाइल्स से पहले CSS लिंक रखें ताकि ग्रिड का डिफ़ॉल्ट थीम सही से लोड हो सके।

### क्यों यह महत्वपूर्ण है

CDN से लाइब्रेरी लोड करने से आपको हमेशा नवीनतम स्थिर संस्करण मिलता है बिना लोकल इंस्टॉल के। `<div id="grid-wrapper">` वह प्लेसहोल्डर है जिसे Grid.js कंस्ट्रक्टर तब टार्गेट करेगा जब हम **configure grid options JavaScript** करेंगे।

---

## Step 2: Create a New GridJsOptions Instance

अब ट्यूटोरियल का मुख्य भाग: वह लाइन जो वास्तव में **creates GridJsOptions instance** करती है। एक अलग फ़ाइल `grid-config.js` (HTML में रेफ़रेंस किया गया) में हम लिखेंगे:

```javascript
// grid-config.js

// Step 2: Create a new GridJsOptions instance to configure grid behavior
const gridOptions = new GridJsOptions();
```

यह एकल लाइन आपको एक साफ़ ऑब्जेक्ट देती है जिसे आप सेटिंग्स से भरना शुरू कर सकते हैं। `gridOptions` को आप प्रत्येक फीचर के कंट्रोल पैनल के रूप में सोच सकते हैं जिसे आप बाद में सक्षम करेंगे।

### आप क्या कॉन्फ़िगर कर रहे हैं

- **NumberFormatAlignment** – संख्यात्मक स्ट्रिंग्स को स्वचालित रूप से एलाइन करता है।
- **Pagination** – पेज साइज और नेविगेशन को नियंत्रित करता है।
- **Sorting** – कॉलम सॉर्टिंग को टॉगल करता है।
- **Columns** – हेडर, डेटा टाइप्स, और कस्टम रेंडरर्स को परिभाषित करता है।

आप इन प्रॉपर्टीज़ में से कोई भी जोड़ सकते हैं इससे पहले कि आप अंत में ग्रिड को इंस्टैंसिएट करें।

---

## Step 3: Enable Number Alignment (A Common Requirement)

अधिकांश टेबल्स में टेक्स्ट और नंबरों का मिश्रण होता है। डिफ़ॉल्ट रूप से Grid.js सब कुछ बाएँ एलाइन करता है, जो मौद्रिक मानों के लिए अजीब दिखता है। उचित एलाइनमेंट के लिए **configure grid options JavaScript** करने हेतु `NumberFormatAlignment` फ़्लैग सेट करें:

```javascript
// Enable left/right alignment for numeric strings
gridOptions.NumberFormatAlignment = true;
```

यह क्यों सक्षम करें? जब फ़्लैग true होता है, तो Grid.js प्रत्येक सेल की जाँच करता है; यदि वह नंबर जैसा दिखता है (जैसे “1234”, “12.34%”), तो वह स्वचालित रूप से दाएँ‑एलाइन कर देता है। यह छोटा बदलाव रिपोर्ट को बहुत अधिक पढ़ने योग्य बनाता है।

---

## Step 4: Add Pagination and Sorting

एक वास्तविक‑दुनिया ग्रिड कभी भी एक ही स्क्रीन पर फिट नहीं होता। चलिए पेजिनेशन (प्रति पेज 10 पंक्तियाँ) चालू करते हैं और उपयोगकर्ताओं को किसी भी कॉलम को सॉर्ट करने की अनुमति देते हैं।

```javascript
gridOptions.Pagination = {
  limit: 10,          // rows per page
  enabled: true
};

gridOptions.Sort = true;   // enables click‑to‑sort on all columns
```

### Edge‑case नोट

यदि आप बाद में एक कस्टम डेटा स्रोत प्रदान करते हैं जो पहले से पेजिनेटेड परिणाम देता है, तो दोहरी पेजिंग से बचने के लिए Grid.js की बिल्ट‑इन पेजिनेशन को डिसेबल करना चाहेंगे। बस `gridOptions.Pagination.enabled = false;` सेट करें।

---

## Step 5: Define Columns and Sample Data

अब हम ग्रिड को कुछ मॉक डेटा देंगे और बताएंगे कि प्रत्येक कॉलम क्या दर्शाता है। यही वह जगह है जहाँ **create gridjsoptions instance** पैटर्न वास्तव में चमकता है—सब कुछ एक ही टाइडी ऑब्जेक्ट में रहता है।

```javascript
// Sample data array of objects
const sampleData = [
  { id: 1, name: "Alice", salary: "54000", department: "Engineering" },
  { id: 2, name: "Bob",   salary: "47000", department: "Marketing" },
  { id: 3, name: "Cara",  salary: "62000", department: "Design" },
  // ...more rows as needed
];

// Column definitions
gridOptions.Columns = [
  { id: "id",   name: "ID",          width: "5%" },
  { id: "name", name: "Employee",    width: "35%" },
  { id: "salary", name: "Salary ($)", width: "20%" },
  { id: "department", name: "Dept.",  width: "40%" }
];

// Attach data source
gridOptions.Data = sampleData;
```

ध्यान दें कि हम कॉलम `id` वैल्यू को प्रत्येक डेटा ऑब्जेक्ट की कुंजियों के समान रखते हैं। यह कन्वेंशन Grid.js को वैल्यूज़ को स्वचालित रूप से मैप करने देता है, जिससे आपको हर कॉलम के लिए कस्टम फ़ॉर्मेटर लिखने की ज़रूरत नहीं पड़ती।

---

## Step 6: Instantiate the Grid with Our Options

हम अंत में `gridOptions` ऑब्जेक्ट को Grid कंस्ट्रक्टर में पास करके **configure grid options javascript** करते हैं। ग्रिड पहले तैयार किए गए `<div id="grid-wrapper">` के अंदर रेंडर होगा।

```javascript
// Create the Grid instance using the previously built options
const grid = new Grid(gridOptions);

// Render the grid into the page
grid.render(document.getElementById("grid-wrapper"));
```

बस इतना ही। पूरी प्रक्रिया—**create gridjsoptions instance** से लेकर रेंडरिंग तक—कोडिंग में एक मिनट से भी कम समय लेती है।

### अपेक्षित आउटपुट

जब आप HTML फ़ाइल को ब्राउज़र में खोलेंगे तो आपको दिखना चाहिए:

- “ID”, “Employee”, “Salary ($)”, “Dept.” के साथ एक हेडर रो।
- `NumberFormatAlignment` के धन्यवाद से दाएँ‑एलाइन किए गए वेतन नंबर।
- नीचे पेजिनेशन कंट्रोल्स (यदि आपने दस से अधिक पंक्तियाँ जोड़ी हैं)।
- क्लिक करने योग्य कॉलम हेडर जो आरोही/अवरोही सॉर्ट करते हैं।

यदि कुछ गड़बड़ दिखे, तो ब्राउज़र कंसोल (F12) खोलें और एरर मैसेज देखें—अधिकतर बग्स कॉलम IDs के मिसमैच या लाइब्रेरी स्क्रिप्ट्स की कमी से होते हैं।

---

## Step 7: Advanced Tweaks (Optional)

नीचे कुछ त्वरित आइडियाज़ हैं जिन्हें आप बेसिक ग्रिड काम करने के बाद एक्सपेरिमेंट कर सकते हैं।

| फ़ीचर | कैसे सक्षम करें | यह क्यों मदद करता है |
|---------|---------------|--------------|
| **Custom cell renderer** | `gridOptions.Columns[2].formatter = (cell) => \`<b>$${cell}</b>\`;` | वेतन को बोल्ड में हाइलाइट करें। |
| **Search bar** | `gridOptions.Search = true;` | उपयोगकर्ताओं को तुरंत पंक्तियों को फ़िल्टर करने देता है। |
| **Server‑side data** | Set `gridOptions.Server = { url: "/api/employees", then: data => data.items };` | हजारों पंक्तियों तक स्केल करता है। |
| **Theme switching** | Add `gridOptions.ClassName = "gridjs-theme-dark";` | डार्क‑मोड डिज़ाइन से मेल खाता है। |

इन्हें मिलाकर‑जोड़कर प्रयोग करने में संकोच न करें—Grid.js जानबूझकर लचीला बनाया गया है। बस याद रखें कि मूल **create gridjsoptions instance** लाइन को शीर्ष पर रखें; सभी बाद के ट्यूनिंग उसी एक ऑब्जेक्ट पर निर्भर करते हैं।

---

## निष्कर्ष

हमने अभी-अभी एक पूर्ण वर्कफ़्लो को **create GridJsOptions instance** और **configure grid options JavaScript** के साथ एक फ़ंक्शनल, सॉर्टेबल, और पेजिनेटेड डेटा टेबल बनाने के लिए चलाया। एक साधारण HTML पेज से शुरू करके, हमने लाइब्रेरी लोड की, एक ऑप्शन ऑब्जेक्ट बनाया, नंबर एलाइनमेंट सक्षम किया, पेजिनेशन जोड़ा, कॉलम परिभाषित किए, और अंत में ग्रिड रेंडर किया।

अब आप कर सकते हैं:

- स्थिर `sampleData` को AJAX कॉल से बदलें।
- डेट्स, करंसीज़, या आइकन्स के लिए कस्टम फ़ॉर्मेटर्स जोड़ें।
- ग्रिड को React या Vue जैसे फ्रेमवर्क में इंटीग्रेट करें (वही `gridOptions` ऑब्जेक्ट वहाँ भी काम करता है)।

संभावनाएँ लगभग अनंत हैं, और हमने जो पैटर्न इस्तेमाल किया—सभी सेटिंग्स को एक ही `GridJsOptions` इंस्टेंस में केंद्रीकृत करना—आपके कोड को साफ़ और मेंटेनेबल रखता है।

कोई ऐसा यूज़‑केस है जिसमें आप अनिश्चित हैं? कमेंट छोड़ें, और हम साथ में उसे एक्सप्लोर करेंगे। हैप्पी कोडिंग, और Grid.js के साथ डायनामिक टेबल्स बनाते रहें!

## What Should You Learn Next?

- [Aspose.Cells .NET के साथ Excel वर्कबुक बनाना और कॉन्फ़िगर करना: चरण‑दर‑चरण गाइड](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Aspose.Cells for .NET का उपयोग करके Excel टेबल बनाना और स्टाइल करना | चरण‑दर‑चरण गाइड](/cells/english/net/tables-structured-references/aspose-cells-net-excel-tables-styling/)
- [Aspose.Cells for Java का उपयोग करके Excel सेल बनाना और फ़ॉर्मेट करना: चरण‑दर‑चरण गाइड](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}