---
category: general
date: 2026-06-21
description: Grid.js का उपयोग करके इंटरैक्टिव डेटा ग्रिड बनाएं और सीखें कि सॉर्टिंग,
  पेजिनेशन और सर्च के साथ JSON डेटा टेबल कैसे प्रदर्शित करें। वेब डैशबोर्ड्स के लिए
  एकदम उपयुक्त।
draft: false
keywords:
- create interactive data grid
- display json data table
- how to use gridjs
language: hi
og_description: मिनटों में इंटरैक्टिव डेटा ग्रिड बनाएं। पेजिनेशन, सॉर्टिंग और सर्च
  के साथ JSON डेटा टेबल दिखाने के लिए Grid.js का उपयोग कैसे करें, सीखें।
og_title: Grid.js के साथ इंटरैक्टिव डेटा ग्रिड बनाएं – पूर्ण ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create interactive data grid using Grid.js and learn how to display
    JSON data table with sorting, pagination, and search. Perfect for web dashboards.
  headline: Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create interactive data grid using Grid.js and learn how to display
    JSON data table with sorting, pagination, and search. Perfect for web dashboards.
  name: Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide
  steps:
  - name: A modern browser (Chrome, Edge, or Firefox) – Grid.js relies on ES6 features.
    text: A modern browser (Chrome, Edge, or Firefox) – Grid.js relies on ES6 features.
  - name: A local or remote folder containing a `grid_data.json` file (we’ll show
      the format).
    text: A local or remote folder containing a `grid_data.json` file (we’ll show
      the format).
  - name: Basic familiarity with HTML and JavaScript – nothing fancy, just the ability
      to open a `.html` file in a browser.
    text: Basic familiarity with HTML and JavaScript – nothing fancy, just the ability
      to open a `.html` file in a browser.
  type: HowTo
tags:
- JavaScript
- Grid.js
- Data Visualization
title: Grid.js के साथ इंटरैक्टिव डेटा ग्रिड बनाएं – पूर्ण चरण‑दर‑चरण गाइड
url: /hi/python/import-and-export/create-interactive-data-grid-with-grid-js-full-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Grid.js के साथ इंटरैक्टिव डेटा ग्रिड बनाएं – पूर्ण चरण‑दर‑चरण गाइड

क्या आपने कभी सोचा है कि कैसे **इंटरैक्टिव डेटा ग्रिड** बनाया जाए जो उपयोगकर्ताओं को बिना बैकएंड लिखे सॉर्ट, सर्च और पेजिंग करने देता है? आप अकेले नहीं हैं। कई डैशबोर्ड्स में सबसे बड़ी समस्या स्थैतिक JSON डंप को एक सुगम, सर्चेबल टेबल में बदलना है—ऐसा कुछ जो स्प्रेडशीट जैसा सहज लगे लेकिन पूरी तरह ब्राउज़र में चले।

इस ट्यूटोरियल में हम **how to use Grid.js** को **display JSON data table** पर एक साधारण HTML पेज पर दिखाने की प्रक्रिया को समझेंगे। अंत तक आपके पास एक कार्यशील उदाहरण होगा जिसे आप किसी भी प्रोजेक्ट में डाल सकते हैं, साथ ही टूलबार को कस्टमाइज़ करने, बड़े डेटा सेट को संभालने और सामान्य समस्याओं से बचने के टिप्स भी मिलेंगे।

## आप क्या सीखेंगे

- कैसे एक JSON फ़ाइल प्राप्त करें जो कॉलम और पंक्तियों को परिभाषित करती है।
- कैसे **Grid.js** को पेजिनेशन, सॉर्टिंग, सर्चिंग और कस्टम टूलबार के साथ इनिशियलाइज़ करें।
- कैसे ग्रिड को लक्ष्य कंटेनर में रेंडर करें।
- वैकल्पिक समायोजन: कस्टम सेल फ़ॉर्मेटिंग, थीम स्विचिंग, और एरर हैंडलिंग।
- एक पूर्ण, कॉपी‑एंड‑पेस्ट‑तैयार कोड नमूना।

### पूर्वापेक्षाएँ

1. एक आधुनिक ब्राउज़र (Chrome, Edge, या Firefox) – Grid.js ES6 फीचर्स पर निर्भर करता है।  
2. एक स्थानीय या रिमोट फ़ोल्डर जिसमें `grid_data.json` फ़ाइल हो (हम फ़ॉर्मेट दिखाएंगे)।  
3. HTML और JavaScript की बुनियादी समझ – कुछ भी जटिल नहीं, बस एक `.html` फ़ाइल को ब्राउज़र में खोलने की क्षमता।

कोई बिल्ड टूल्स नहीं, कोई npm इंस्टॉल नहीं, कोई सर्वर‑साइड कोड नहीं। यही है **create interactive data grid** के साथ Grid.js की खूबी: यह सीधे CDN से काम करता है।

---

## चरण 1: अपनी टेबल को परिभाषित करने वाला JSON तैयार करें

पहली चीज़ जो आपको चाहिए वह एक JSON पेलोड है जो Grid.js को बताता है कि कौन‑से कॉलम मौजूद हैं और कौन‑सी पंक्तियाँ दिखानी हैं। इसे आपके **display JSON data table** का ब्लूप्रिंट समझें। नीचे एक न्यूनतम उदाहरण है जिसे आप अपने HTML फ़ाइल के समान डायरेक्टरी में `grid_data.json` के रूप में सहेज सकते हैं:

```json
{
  "columns": ["ID", "Name", "Email", "Country"],
  "rows": [
    [1, "Alice Johnson", "alice@example.com", "USA"],
    [2, "Bob Smith", "bob@example.com", "Canada"],
    [3, "Carlos Ruiz", "carlos@example.com", "Mexico"],
    [4, "Diana Lee", "diana@example.com", "UK"]
  ]
}
```

*यह फ़ॉर्मेट क्यों?* Grid.js अपेक्षा करता है कि `columns` स्ट्रिंग्स (या उन्नत कॉन्फ़िगरेशन के लिए ऑब्जेक्ट्स) की एरे हो और `rows` एरे ऑफ एरेज़ हो जहाँ प्रत्येक अंदरूनी एरे कॉलम क्रम से मेल खाता हो। आप ज़रूरत अनुसार अधिक कॉलम या नेस्टेड ऑब्जेक्ट्स जोड़ सकते हैं – Grid.js उन्हें रेंडर करेगा जब तक संरचना मेल खाती रहे।

> **Pro tip:** यदि आप API से डेटा ले रहे हैं, तो स्थैतिक `fetch('grid_data.json')` को अपने एंडपॉइंट URL से बदल दें। बाकी कोड वही रहेगा।

---

## चरण 2: Grid.js को इनिशियलाइज़ करें – **how to use gridjs** का हृदय

अब डेटा स्रोत तैयार है, हमें Grid.js को पेज पर लाना है और उसकी व्यवहार को बताना है। यही वह जगह है जहाँ हम वास्तव में **create interactive data grid** फ़ंक्शनैलिटी जैसे पेजिनेशन, सॉर्टिंग और एक उपयोगी टूलबार बटन बनाते हैं।

```html
<!-- Load Grid.js from the CDN -->
<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
```

CDN आपको नवीनतम स्थिर संस्करण देता है, और Meri­maid थीम बॉक्स से बाहर एक साफ़, आधुनिक लुक जोड़ती है। यदि आप डिफ़ॉल्ट स्टाइलिंग पसंद करते हैं तो `gridjs.min.css` से बदल सकते हैं।

अगला, एक `<script>` टैग के अंदर, JSON फ़ेच करें और ग्रिड को इनिशियलाइज़ करें:

```javascript
// Step 2: Initialise Grid.js with pagination, sorting, searching, and a toolbar
fetch('grid_data.json')
  .then(response => response.json())
  .then(data => {
    const grid = new gridjs.Grid({
      columns: data.columns,      // Pull column headers from JSON
      data: data.rows,            // Pull row data from JSON
      pagination: { enabled: true, limit: 10 }, // Show 10 rows per page
      sort: true,                 // Enable column sorting
      search: true,               // Add a search box above the grid
      toolbar: {
        enabled: true,
        items: [
          {
            type: 'button',
            text: 'Help',
            onClick: () => alert('Use the search box to filter rows or click column headers to sort.')
          }
        ]
      },
      // Optional: custom cell formatter for the Email column
      // This demonstrates a deeper dive into how to use Grid.js
      // and shows you can embed HTML inside cells.
      columns: data.columns.map(col => {
        if (col === 'Email') {
          return {
            name: col,
            formatter: cell => gridjs.html(`<a href="mailto:${cell}">${cell}</a>`)
          };
        }
        return col; // Simple string for other columns
      })
    });

    // Step 3: Render the grid into the target container
    grid.render(document.getElementById('grid-container'));
  })
  .catch(err => console.error('Failed to load grid data:', err));
```

### विकल्पों का विवरण

| विकल्प | क्या करता है | क्यों महत्वपूर्ण है |
|--------|--------------|--------------------|
| `pagination` | पंक्तियों को पेजों में विभाजित करता है (डिफ़ॉल्ट 10 प्रति पेज) | बड़े टेबल को उपयोगी रखता है बिना UI को भरने के। |
| `sort` | क्लिक करने योग्य कॉलम हेडर आरोही/अवरोही क्रम बदलते हैं | उपयोगकर्ता जल्दी से सबसे उच्च मान वाली पंक्तियों को खोज सकते हैं। |
| `search` | एक टेक्स्ट इनपुट जोड़ता है जो तुरंत पंक्तियों को फ़िल्टर करता है | डेटा को पुनः लोड किए बिना त्वरित खोज के लिए उत्कृष्ट। |
| `toolbar` | ग्रिड के ऊपर कस्टम बटन या ड्रॉपडाउन जोड़ता है | “Help”, “Export”, या “Refresh” कार्यों के लिए उपयुक्त। |
| `formatter` | सेल के लिए रॉ HTML रिटर्न करने देता है | यहाँ हम ईमेल स्ट्रिंग को क्लिक करने योग्य mailto लिंक में बदलते हैं। |

> **Why this approach?** ग्रिड कॉन्फ़िगरेशन को डिक्लरेटिव रखकर, आप कोर रेंडरिंग लॉजिक को छुए बिना व्यवहार को आसानी से बदल सकते हैं। यह अधिकांश प्रोजेक्ट्स के लिए **how to use Grid.js** का अनुशंसित तरीका है।

---

## चरण 3: ग्रिड को अपने पेज में रेंडर करें

स्क्रिप्ट की अंतिम पंक्ति—`grid.render(document.getElementById('grid-container'))`—एक `<div>` में पूरी‑फ़ंक्शनल टेबल को इंजेक्ट करती है जिसे आपने अपने HTML बॉडी में कहीं रखा है:

```html
<div id="grid-container"></div>
```

बस इतना ही। जब पेज लोड होता है, ब्राउज़र JSON फ़ेच करता है, Grid.js इंस्टेंस बनाता है, और इंटरैक्टिव टेबल को स्क्रीन पर पेंट करता है। कोई रिफ्रेश नहीं, प्रारंभिक लोड के बाद कोई सर्वर कॉल नहीं।

---

## वैकल्पिक: स्टाइलिंग और थीम समायोजन

यदि डिफ़ॉल्ट Meri­maid थीम आपका पसंदीदा नहीं है, तो आप इसे किसी भी बिल्ट‑इन थीम (`gridjs.min.css`) से बदल सकते हैं या अपना खुद का CSS लिख सकते हैं। उदाहरण के लिए, हेडर बैकग्राउंड को हल्का ग्रे बनाने के लिए:

```css
.gridjs-th {
  background-color: #f5f5f5;
}
```

इस स्निपेट को `<style>` टैग के अंदर या बाहरी स्टाइलशीट में जोड़ें। Grid.js मानक CSS सिलेक्टर्स का सम्मान करता है, इसलिए फ़ॉन्ट, रंग और स्पेसिंग पर आपका पूरा नियंत्रण है।

---

## सामान्य समस्याएँ और उन्हें कैसे टालें

| समस्या | लक्षण | समाधान |
|---------|---------|-----|
| **CORS errors** जब किसी अन्य डोमेन से JSON फ़ेच किया जाता है | ब्राउज़र कंसोल में “Blocked by CORS policy” दिखता है | JSON को उसी ओरिजिन पर होस्ट करें या सर्वर पर CORS सक्षम करें। |
| **Large data sets cause lag** | स्क्रॉलिंग झटकेदार हो जाती है, पेजिनेशन धीमा | `server` पेजिनेशन (`pagination: { server: { url: (prev, page, limit) => … } }`) या लेज़ी‑लोड रोज़ का उपयोग करें। |
| **Toolbar button doesn’t appear** | `toolbar.enabled: true` होने के बावजूद कोई बटन नहीं दिख रहा है | सुनिश्चित करें कि आप Grid.js संस्करण 2.0+ का उपयोग कर रहे हैं; पुराने संस्करणों में टूलबार API अलग था। |
| **Email links not clickable** | फ़ॉर्मेटर साधारण टेक्स्ट रिटर्न करता है | उदाहरण में दिखाए अनुसार `gridjs.html(...)` रिटर्न करें, साधारण स्ट्रिंग के बजाय। |

इन समस्याओं को शुरुआती चरण में हल करने से बाद में कई घंटे की डिबगिंग बचती है।

---

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

नीचे पूरा HTML फ़ाइल है जिसे आप `index.html` के रूप में सहेज सकते हैं। इसे ब्राउज़र में खोलें, और आप एक पूरी तरह कार्यशील **create interactive data grid** डेमो देखेंगे जिसमें **display JSON data table** सॉर्टिंग, सर्चिंग और हेल्प बटन के साथ होगा।



## अब आपको आगे क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोचेज़ को एक्सप्लोर कर सकें।

- [Java के लिए Aspose.Cells के साथ Excel डेटा वैलिडेशन लिस्ट कैसे बनाएं: चरण‑दर‑चरण गाइड](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [.NET के लिए Aspose.Cells का उपयोग करके Excel में चेकबॉक्स कैसे बनाएं | डेटा वैलिडेशन ट्यूटोरियल](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)
- [Java के लिए Aspose.Cells का उपयोग करके Excel में XML डेटा बनाएं और इम्पोर्ट करें](/cells/english/java/import-export/create-import-xml-data-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}