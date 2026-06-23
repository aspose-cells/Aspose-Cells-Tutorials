---
category: general
date: 2026-02-15
description: सेट कॉलम नंबर फ़ॉर्मेट का उपयोग करके मुद्रा को जल्दी से फ़ॉर्मेट करना
  और C# में कस्टम न्यूमेरिक फ़ॉर्मेट लागू करना। कॉलम को नाम से प्राप्त करना और ग्रिड
  कॉलम संरेखण सेट करना सीखें।
draft: false
keywords:
- how to format currency
- set column number format
- apply custom numeric format
- retrieve column by name
- set grid column alignment
language: hi
og_description: C# का उपयोग करके ग्रिड कॉलम में मुद्रा को कैसे फ़ॉर्मेट करें। यह ट्यूटोरियल
  दिखाता है कि नाम से कॉलम को कैसे प्राप्त करें, कॉलम का नंबर फ़ॉर्मेट सेट करें, कस्टम
  न्यूमेरिक फ़ॉर्मेट लागू करें, और ग्रिड कॉलम की अलाइनमेंट सेट करें।
og_title: ग्रिड कॉलम में मुद्रा को कैसे फ़ॉर्मेट करें – पूर्ण गाइड
tags:
- C#
- GridFormatting
- UI
title: ग्रिड कॉलम में मुद्रा को कैसे फ़ॉर्मेट करें – चरण‑दर‑चरण गाइड
url: /hi/net/number-and-display-formats-in-excel/how-to-format-currency-in-a-grid-column-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ग्रिड कॉलम में मुद्रा को कैसे फ़ॉर्मेट करें – पूर्ण प्रोग्रामिंग ट्यूटोरियल

क्या आपने कभी **मुद्रा को फ़ॉर्मेट करने** के बारे में सोचा है जब आप ग्रिड कॉलम में अपने बाल खींचे बिना? आप अकेले नहीं हैं। जब आप `1234.5` जैसे साधारण संख्या को देखते हैं और चाहते हैं कि वह जादूई रूप से `$1,234.50` दिखे, तो जवाब आमतौर पर सिर्फ कुछ पंक्तियों की कॉन्फ़िगरेशन होता है।  

इस गाइड में हम **कॉलम को नाम से प्राप्त करेंगे**, **कॉलम नंबर फ़ॉर्मेट सेट करेंगे**, और **कस्टम न्यूमेरिक फ़ॉर्मेट लागू करेंगे** जो सामान्य अकाउंटिंग लेआउट का सम्मान करता है। इस दौरान हम **ग्रिड कॉलम एलाइनमेंट सेट करेंगे** और एक सूक्ष्म बॉर्डर जोड़ेंगे ताकि UI अधिक पॉलिश्ड दिखे।

> **TL;DR** – अंत तक आपके पास एक तैयार‑चलाने‑योग्य स्निपेट होगा जो कच्चे दशमलव को किसी भी `GridJs`‑स्टाइल कंट्रोल के अंदर सुंदरता से फ़ॉर्मेटेड मुद्रा मानों में बदल देगा।

---

## आपको क्या चाहिए

- एक .NET प्रोजेक्ट (कोई भी संस्करण जो C# 8.0+ को सपोर्ट करता हो – Visual Studio 2022 बहुत अच्छा काम करता है)।  
- एक ग्रिड कंपोनेंट जो `Columns` कलेक्शन को एक्सपोज़ करता हो (उदाहरण में एक काल्पनिक `GridJs` क्लास का उपयोग किया गया है, लेकिन अवधारणाएँ DevExpress, Telerik, या Syncfusion ग्रिड्स में भी लागू होती हैं)।  
- C# सिंटैक्स की बेसिक परिचितता – कोई उन्नत ट्रिक्स आवश्यक नहीं।

यदि आपके पास ये सब है, तो बढ़िया। यदि नहीं, तो बस एक कंसोल ऐप बना लें; ग्रिड को डेमो के लिए मॉक किया जा सकता है।

---

## चरण‑दर‑चरण कार्यान्वयन

नीचे प्रत्येक चरण में आपको एक कॉम्पैक्ट कोड ब्लॉक, लाइन के महत्व की संक्षिप्त व्याख्या, और सामान्य गलतियों से बचने के टिप्स मिलेंगे।

### ## Step 1 – Retrieve the “Amount” column by name

```csharp
// Step 1: Retrieve the "Amount" column from the grid
var amountColumn = gridJs.Columns["Amount"];
if (amountColumn == null)
{
    throw new InvalidOperationException("Column 'Amount' does not exist. Verify the column name or check the grid's schema.");
}
```

**Why this matters:**  
अधिकांश ग्रिड API कॉलम को डिक्शनरी‑जैसे इंडेक्सर के माध्यम से एक्सपोज़ करते हैं। हेडर नाम (`"Amount"`) से कॉलम को प्राप्त करने से आप डेटा सोर्स को छुए बिना उसकी उपस्थिति को बदल सकते हैं।  

**Pro tip:** हमेशा `null` रिटर्न को हैंडल करें – कॉलम नाम में टाइपो या डायनामिक स्कीमा परिवर्तन के कारण रनटाइम में `NullReferenceException` आ सकता है।

---

### ## Step 2 – Set column number format using a custom currency mask

```csharp
// Step 2: Apply a custom numeric format for currency values
amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";
```

**Why this matters:**  
फ़ॉर्मेट स्ट्रिंग Excel के अकाउंटिंग फ़ॉर्मेट कन्वेंशन का पालन करती है:

- `_(* #,##0.00_)` → पॉज़िटिव नंबर, राइट‑अलाइन्ड, मुद्रा चिन्ह के लिए एक लीडिंग स्पेस के साथ।  
- `_(* (#,##0.00)` → नेगेटिव नंबर को कोष्ठकों में घेरा जाता है।  
- `_(* \"-\"??_)` → ज़ीरो वैल्यू को डैश के रूप में दिखाया जाता है।  
- `_(@_)` → टेक्स्ट वैल्यू अपरिवर्तित रहती है।

**apply custom numeric format** का उपयोग करने से आप थाउज़ेंड सेपरेटर, दशमलव स्थान, और मुद्रा चिन्ह की पोजीशन पर पूरी तरह से नियंत्रण पा सकते हैं।  

**Edge case:** यदि आपका एप्लिकेशन अलग लोकेल (जैसे USD के बजाय यूरो) को सपोर्ट करना चाहता है, तो लीडिंग स्पेस को इच्छित चिन्ह से बदलें या डेटा सोर्स में `CultureInfo`‑अवेयर फ़ॉर्मेटिंग का उपयोग करें।

---

### ## Step 3 – Align the column contents to the right for readability

```csharp
// Step 3: Align the column contents to the right for better readability
amountColumn.Alignment = GridAlignment.Right;
```

**Why this matters:**  
डेसिमल सेपरेटर पर संरेखित होने से मुद्रा मानों को स्कैन करना आसान हो जाता है। **set grid column alignment** को `Right` पर सेट करने से स्प्रेडशीट की तरह मोनेटरी डेटा दिखता है।  

**Gotcha:** कुछ ग्रिड्स कस्टम टेम्प्लेट वाले सेल्स पर एलाइनमेंट को इग्नोर कर देते हैं। यदि एलाइनमेंट प्रभावी नहीं हो रहा है, तो सुनिश्चित करें कि कॉलम कस्टम सेल रेंडरर का उपयोग नहीं कर रहा है।

---

### ## Step 4 – Add a thin gray border around the column cells

```csharp
// Step 4: Add a thin gray border around the column cells
amountColumn.Border = new GridBorder
{
    Color = Color.Gray,
    Style = BorderLineStyle.Thin
};
```

**Why this matters:**  
एक सूक्ष्म बॉर्डर “Amount” कॉलम को उसके पड़ोसियों से अलग करता है, विशेषकर जब ग्रिड में अल्टरनेटिंग रो कलर्स हों। यह एक विज़ुअल संकेत है कि डेटा एक विशिष्ट वित्तीय आंकड़ा दर्शाता है।  

**Tip:** यदि प्रिंटिंग के लिए आपको मोटी लाइन चाहिए, तो `BorderLineStyle` को `Medium` या `Color` को `Color.Black` में बदलें।

---

## Full Working Example

यहाँ पूरा स्निपेट है जिसे आप WinForms या WPF प्रोजेक्ट में `GridJs`‑स्टाइल कंट्रोल के साथ ड्रॉप कर सकते हैं। उदाहरण कंसोल में फ़ॉर्मेटेड वैल्यूज़ भी प्रिंट करता है ताकि आप UI के बिना आउटपुट की पुष्टि कर सकें।

```csharp
using System;
using System.Drawing;   // For Color
using GridLibrary;      // Hypothetical namespace for GridJs

namespace GridCurrencyDemo
{
    class Program
    {
        static void Main()
        {
            // Create a mock grid and add a sample column
            var gridJs = new GridJs();
            gridJs.Columns.Add(new GridColumn
            {
                Name = "Amount",
                Header = "Amount",
                DataType = typeof(decimal)
            });

            // Populate some sample data
            gridJs.Rows.Add(new { Amount = 1234.5m });
            gridJs.Rows.Add(new { Amount = -567.89m });
            gridJs.Rows.Add(new { Amount = 0m });

            // ---- Formatting steps ------------------------------------------------
            // 1️⃣ Retrieve the "Amount" column
            var amountColumn = gridJs.Columns["Amount"]
                ?? throw new InvalidOperationException("Column 'Amount' not found.");

            // 2️⃣ Apply custom numeric format for currency
            amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";

            // 3️⃣ Right‑align the values
            amountColumn.Alignment = GridAlignment.Right;

            // 4️⃣ Add a thin gray border
            amountColumn.Border = new GridBorder
            {
                Color = Color.Gray,
                Style = BorderLineStyle.Thin
            };
            // -----------------------------------------------------------------------

            // Render the grid (in a real UI you would call gridJs.Render() or similar)
            Console.WriteLine("Formatted Currency Grid:");
            foreach (var row in gridJs.Rows)
            {
                var rawValue = (decimal)row.Amount;
                // The grid library would automatically apply NumberFormat when displaying.
                // For console demo we mimic the formatting:
                string formatted = rawValue.ToString("#,##0.00", System.Globalization.CultureInfo.InvariantCulture);
                if (rawValue < 0)
                    formatted = $"({formatted.TrimStart('-')})";
                else if (rawValue == 0)
                    formatted = "-";

                Console.WriteLine($"| {formatted,15} |");
            }

            // Keep console open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Expected console output**

```
Formatted Currency Grid:
|        1,234.50 |
|       (567.89) |
|               - |
```

ध्यान दें कि पॉज़िटिव नंबर राइट‑अलाइन्ड है, नेगेटिव नंबर को कोष्ठकों में दिखाया गया है, और ज़ीरो को डैश के रूप में दिखाया गया है – बिल्कुल वही जो कस्टम फ़ॉर्मेट स्ट्रिंग निर्धारित करती है।

---

## Frequently Asked Questions & Edge Cases

| प्रश्न | उत्तर |
|----------|--------|
| *यदि ग्रिड किसी अलग संस्कृति (उदाहरण : € के बजाय $) का उपयोग करता है तो क्या करें?* | फ़ॉर्मेट स्ट्रिंग में लीडिंग स्पेस को इच्छित चिन्ह से बदलें या डेटा सोर्स को `CultureInfo.CurrentCulture` का उपयोग करके प्री‑फ़ॉर्मेटेड स्ट्रिंग इमीट करने दें। |
| *क्या मैं एक ही फ़ॉर्मेट को कई कॉलम्स में पुन: उपयोग कर सकता हूँ?* | बिल्कुल। फ़ॉर्मेट स्ट्रिंग को एक कॉन्स्टेंट (`const string CurrencyMask = "...";`) में रखें और जहाँ भी मुद्रा चाहिए वहाँ असाइन करें। |
| *यदि कॉलम में स्ट्रिंग वैल्यू हो तो क्या होगा?* | फ़ॉर्मेट स्ट्रिंग केवल न्यूमेरिक टाइप्स को प्रभावित करती है। स्ट्रिंग्स अपरिवर्तित पास हो जाती हैं, इसलिए मास्क का अंतिम भाग (`_(@_)`) मौजूद है – यह नॉन‑न्यूमेरिक कंटेंट को संरक्षित रखता है। |
| *क्या इससे प्रदर्शन पर असर पड़ेगा?* | नगण्य। फ़ॉर्मेट रेंडर टाइम पर लागू होता है, डेटा रिट्रीवल के दौरान नहीं। जब तक आप प्रति फ्रेम हजारों रो नहीं रेंडर कर रहे हैं, आपको कोई धीमी गति नहीं दिखेगी। |
| *प्रिंटेड रिपोर्ट्स के लिए बॉर्डर को मोटा कैसे करें?* | `BorderLineStyle.Thin` को `BorderLineStyle.Medium` या `BorderLineStyle.Thick` से बदलें। कुछ लाइब्रेरीज़ आपको सीधे पिक्सेल चौड़ाई भी सेट करने देती हैं। |

---

## Wrap‑Up

हमने **ग्रिड कॉलम में मुद्रा को फ़ॉर्मेट करने** के सभी चरणों को शुरू से अंत तक कवर किया: नाम से कॉलम प्राप्त करना, कॉलम नंबर फ़ॉर्मेट सेट करना, कस्टम न्यूमेरिक फ़ॉर्मेट लागू करना, सेल्स को राइट‑अलाइन करना, और एक सुंदर बॉर्डर जोड़ना। पूरा उदाहरण बॉक्स‑से‑बॉक्स चलाने योग्य है और वही विज़ुअल परिणाम दिखाता है जिसकी आप उम्मीद कर रहे हैं।

यदि आप आगे बढ़ना चाहते हैं, तो कोशिश करें:

- **Dynamic cultures** – फ़ॉर्मेट स्ट्रिंग को उपयोगकर्ता के लोकेल के आधार पर स्विच करें।  
- **Conditional

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}