---
category: general
date: 2026-03-18
description: C# का उपयोग करके वर्कशीट में वैकल्पिक पंक्तियों के रंग कैसे लागू करें,
  सीखें। इसमें पंक्ति की पृष्ठभूमि रंग सेट करना, हल्का पीला पृष्ठभूमि जोड़ना, और पंक्तियों
  को वैकल्पिक रूप से रंगना शामिल है।
draft: false
keywords:
- apply alternating row colors
- set row background color
- add light yellow background
- set alternating row shading
- color rows alternately
language: hi
og_description: C# में वैकल्पिक पंक्तियों के रंग लागू करके पठनीयता बढ़ाएँ। यह गाइड
  दिखाता है कि पंक्ति की पृष्ठभूमि का रंग कैसे सेट करें, हल्का पीला पृष्ठभूमि जोड़ें,
  और पंक्तियों को वैकल्पिक रूप से रंगें।
og_title: C# में वैकल्पिक पंक्तियों के रंग लागू करें – पूर्ण ट्यूटोरियल
tags:
- C#
- DataTable
- Spreadsheet styling
- UI design
title: C# में वैकल्पिक पंक्तियों के रंग लागू करें – चरण‑दर‑चरण मार्गदर्शिका
url: /hi/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में वैकल्पिक पंक्ति रंग लागू करें – पूर्ण ट्यूटोरियल

क्या आपको कभी **वैकल्पिक पंक्ति रंग** डेटा‑ड्रिवन वर्कशीट पर लागू करने की ज़रूरत पड़ी, लेकिन शुरुआत कहाँ से करें, यह नहीं पता चला? आप अकेले नहीं हैं — ज्यादातर डेवलपर्स को पहली बार टेबल को थोड़ा अधिक दोस्ताना बनाने की कोशिश में यही समस्या आती है। अच्छी खबर? सिर्फ कुछ ही C# लाइनों में आप **पंक्ति पृष्ठभूमि रंग सेट** कर सकते हैं, **हल्का पीला पृष्ठभूमि जोड़** सकते हैं, और एक ऐसा पॉलिश्ड ग्रिड बना सकते हैं जो तुरंत पठनीयता को बेहतर बनाता है।

इस ट्यूटोरियल में हम पूरे प्रोसेस को चरण‑दर‑चरण देखेंगे, `DataTable` को मेमोरी में लोड करने से लेकर प्रत्येक पंक्ति को हल्के पीले‑सफ़ेद स्ट्राइप से स्टाइल करने तक। अंत तक आप **पंक्तियों को वैकल्पिक रूप से रंग** सकेंगे, और कुछ उपयोगी वैरिएशन भी देखेंगे जब आपको अलग‑अलग शेड्स या डायनामिक थीमिंग चाहिए।

## आपको क्या चाहिए

- एक .NET प्रोजेक्ट जो .NET 6 या बाद के संस्करण को टार्गेट करता हो (कोड .NET Framework 4.7+ पर भी काम करता है)।  
- एक स्प्रेडशीट लाइब्रेरी जो स्टाइल ऑब्जेक्ट्स को सपोर्ट करती हो – उदाहरण में एक generic `Workbook`/`Worksheet` API का उपयोग किया गया है जो **Aspose.Cells**, **GemBox.Spreadsheet**, या **ClosedXML** जैसी लाइब्रेरीज़ को दर्शाता है।  
- एक `DataTable` स्रोत – यह डेटाबेस क्वेरी, CSV इम्पोर्ट, या किसी भी इन‑मेमोरी कलेक्शन से हो सकता है।  

स्प्रेडशीट लाइब्रेरी के अलावा कोई अतिरिक्त NuGet पैकेज नहीं चाहिए। यदि आप Aspose.Cells उपयोग कर रहे हैं, तो नेमस्पेस `Aspose.Cells` है; ClosedXML के लिए `ClosedXML.Excel`। `CreateStyle` और `ImportDataTable` कॉल्स को उसी अनुसार बदलें।

## चरण 1: स्रोत डेटा को DataTable के रूप में प्राप्त करें

सबसे पहले वह डेटा प्राप्त करें जिसे आप दिखाना चाहते हैं। वास्तविक‑दुनिया के ऐप्स में आमतौर पर इसका मतलब डेटाबेस से कनेक्ट होना होता है, लेकिन स्पष्टता के लिए हम एक हेल्पर मेथड `GetData()` बनाते हैं जो एक भरपूर `DataTable` रिटर्न करता है।

```csharp
// Step 1: Retrieve the source data as a DataTable
DataTable dataTable = GetData();   // Replace with your actual data retrieval logic
```

> **Why this matters:** `DataTable` उन पंक्तियों और कॉलमों को परिभाषित करता है जिन पर बाद में वैकल्पिक शेडिंग लागू होगी। यदि टेबल खाली है, तो स्टाइल करने के लिए कुछ नहीं रहेगा, इसलिए आगे बढ़ने से पहले हमेशा `Rows.Count` > 0 है यह जांचें।

### प्रो टिप
यदि आप Entity Framework से डेटा ला रहे हैं, तो `SqlCommand` चलाने के बाद `DataTable.Load(reader)` का उपयोग कर सकते हैं। इससे कोड साफ़ रहता है और मैन्युअल कॉलम परिभाषा से बचा जा सकता है।

## चरण 2: प्रत्येक पंक्ति के लिए स्टाइल रखने हेतु एक एरे अलोकेट करें

अब हमें एक कंटेनर चाहिए जो पंक्तियों की संख्या के बराबर हो। अधिकांश स्प्रेडशीट APIs आपको इम्पोर्ट मेथड में एक स्टाइल एरे पास करने की अनुमति देती हैं, इसलिए हम `Style[]` बनाते हैं जिसका आकार ठीक पंक्ति गिनती के बराबर होगा।

```csharp
// Step 2: Allocate an array to hold a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];
```

> **Explanation:** एरे को पहले से अलोकेट करके हम हर इटरेशन में नया स्टाइल ऑब्जेक्ट बनाने से बचते हैं, जो हजारों पंक्तियों के साथ काम करते समय प्रदर्शन में सुधार कर सकता है।

## चरण 3: वैकल्पिक पंक्ति रंग लागू करें (हल्का पीला / सफ़ेद)

अब मुख्य काम: **वैकल्पिक पंक्ति रंग लागू करें**। हम प्रत्येक पंक्ति पर लूप करेंगे, वर्कबुक से एक नया स्टाइल इंस्टेंस बनाएँगे, और पंक्ति इंडेक्स के आधार पर उसका बैकग्राउंड सेट करेंगे। सम पंक्तियों को हल्का पीला फ़िल मिलेगा, विषम पंक्तियों को सफ़ेद रहेगा।

```csharp
// Step 3: Create alternating background colors (light yellow / white) for the rows
for (int rowIndex = 0; rowIndex < dataTable.Rows.Count; rowIndex++)
{
    // Create a new style instance from the workbook
    rowStyles[rowIndex] = wb.CreateStyle();

    // Apply a light yellow background to even rows, white to odd rows
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow   // add light yellow background
        : Color.White;        // set row background color to white

    rowStyles[rowIndex].Pattern = BackgroundType.Solid; // set alternating row shading
}
```

### क्यों यह काम करता है
- **`rowIndex % 2 == 0`** जांचता है कि पंक्ति सम है या नहीं।  
- **`Color.LightYellow`** एक कोमल, गैर‑आक्रामक ह्यू देता है जो डेटा टेबल के लिए एकदम उपयुक्त है।  
- **`BackgroundType.Solid`** सुनिश्चित करता है कि फ़िल पूरे सेल को कवर करे, जिससे **set row background color** प्रभाव प्राप्त होता है।  

आप `Color.LightYellow` को किसी भी अन्य शेड (जैसे `Color.LightCyan`) से बदल सकते हैं यदि आप अलग लुक चाहते हैं। वही लॉजिक आपको **पंक्तियों को वैकल्पिक रूप से रंग** अन्य मानदंडों (जैसे स्टेटस फ्लैग) के आधार पर भी अनुमति देता है।

## चरण 4: तैयार स्टाइल एरे के साथ DataTable को Worksheet में इम्पोर्ट करें

अंत में, हम सब कुछ Worksheet में डालते हैं। अधिकांश लाइब्रेरीज़ `ImportDataTable` का एक ओवरलोड प्रदान करती हैं जो स्टाइल एरे को स्वीकार करता है। `true` फ़्लैग API को कॉलम हेडर लिखने के लिए बताता है, और `0, 0` कॉर्डिनेट्स टॉप‑लेफ़्ट सेल से शुरू होते हैं।

```csharp
// Step 4: Import the DataTable into the worksheet, applying the prepared row styles
ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

> **Result:** Worksheet अब आपके डेटा को एक साफ़ **वैकल्पिक पंक्ति शेडिंग** पैटर्न के साथ दिखाता है—सम पंक्तियों पर हल्का पीला, विषम पंक्तियों पर सफ़ेद। उपयोगकर्ता ग्रिड को बिना आँखें बार‑बार हिलाए स्कैन कर सकते हैं।

### अपेक्षित आउटपुट
यदि आप परिणामी स्प्रेडशीट खोलते हैं, तो आपको कुछ इस तरह दिखेगा:

| ID | Name      | Quantity |
|----|-----------|----------|
| **1** | Apple      | 50       |
| **2** | Banana     | 30       |
| **3** | Cherry     | 20       |
| **4** | Date       | 15       |

पंक्तियाँ 1, 3, 5… **हल्का पीला बैकग्राउंड** रखती हैं, जबकि पंक्तियाँ 2, 4, 6… **सफ़ेद** रहती हैं। हेडर पंक्ति (row 0) डिफ़ॉल्ट स्टाइल को इनहेरिट करती है जब तक आप इसे अलग से कस्टमाइज़ न करें।

## वैकल्पिक वैरिएशन और एज केस

### 1. अलग रंग पैलेट का उपयोग
यदि हल्का पीला आपके ब्रांडिंग के साथ टकराता है, तो बस `Color.LightYellow` को किसी अन्य `System.Drawing.Color` से बदल दें। ब्लू‑ग्रे थीम के लिए आप उपयोग कर सकते हैं:

```csharp
rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
    ? Color.FromArgb(220, 235, 247) // soft blue
    : Color.White;
```

### 2. डेटा के आधार पर डायनामिक शेडिंग
कभी‑कभी आप उन पंक्तियों को हाईलाइट करना चाहते हैं जो किसी शर्त को पूरा करती हैं (जैसे कम इन्वेंटरी)। मॉड्यूलो चेक को एक कस्टम टेस्ट के साथ मिलाएँ:

```csharp
int quantity = Convert.ToInt32(dataTable.Rows[rowIndex]["Quantity"]);
if (quantity < 20)
{
    rowStyles[rowIndex].ForegroundColor = Color.Salmon; // urgent low‑stock color
}
else
{
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow
        : Color.White;
}
```

### 3. केवल विशिष्ट कॉलम पर स्टाइल लागू करना
यदि आपको कुछ कॉलम पर ही **set row background color** चाहिए, तो प्रत्येक कॉलम के लिए एक अलग स्टाइल बनाएं और इम्पोर्ट के बाद Worksheet के सेल रेंज API का उपयोग करके उसे असाइन करें।

```csharp
// Example for column B only
var colBStyle = wb.CreateStyle();
colBStyle.ForegroundColor = Color.LightYellow;
colBStyle.Pattern = BackgroundType.Solid;

// Apply after import
ws.Cells[$"B2:B{dataTable.Rows.Count + 1}"].SetStyle(colBStyle);
```

### 4. बड़े टेबल्स के लिए प्रदर्शन टिप
जब आप > 10,000 पंक्तियों के साथ काम कर रहे हों, तो प्रत्येक रंग के लिए एक ही स्टाइल ऑब्जेक्ट को पुनः उपयोग करने पर विचार करें, बजाय हर पंक्ति के लिए नया बनाते रहने के। एरे तब दो साझा स्टाइल्स के रेफ़रेंसेज़ रखेगा, जिससे मेमोरी उपयोग में काफी कमी आएगी।

```csharp
Style yellowStyle = wb.CreateStyle();
yellowStyle.ForegroundColor = Color.LightYellow;
yellowStyle.Pattern = BackgroundType.Solid;

Style whiteStyle = wb.CreateStyle();
whiteStyle.ForegroundColor = Color.White;
whiteStyle.Pattern = BackgroundType.Solid;

for (int i = 0; i < dataTable.Rows.Count; i++)
    rowStyles[i] = (i % 2 == 0) ? yellowStyle : whiteStyle;
```

## पूर्ण कार्यशील उदाहरण

नीचे एक सेल्फ‑कंटेन्ड प्रोग्राम दिया गया है जिसे आप कॉन्सोल ऐप में पेस्ट कर सकते हैं। यह एक काल्पनिक `Workbook`/`Worksheet` API का उपयोग करता है; अपने चुने हुए लाइब्रेरी के टाइप्स से इन्हें बदलें।

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using YourSpreadsheetLib;     // Replace with actual namespace

class Program
{
    static void Main()
    {
        // Initialize workbook & worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Step 1: Retrieve data
        DataTable dataTable = GetData();

        // Step 2: Allocate style array
        Style[] rowStyles = new Style[dataTable.Rows.Count];

        // Step 3: Apply alternating row colors
        for (int i = 0; i < dataTable.Rows.Count; i++)
        {
            rowStyles[i] = wb.CreateStyle();
            rowStyles[i].ForegroundColor = (i % 2 == 0)
                ? Color.LightYellow   // add light yellow background
                : Color.White;        // set row background color
            rowStyles[i].Pattern = BackgroundType.Solid; // set alternating row shading
        }

        // Step 4: Import with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // Save to file
        wb.Save("AlternatingRows.xlsx");
        Console.WriteLine("Workbook saved with alternating row colors.");
    }

    // Sample data generator
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Quantity", typeof(int));

        dt.Rows.Add(1, "Apple", 50);
        dt.Rows.Add(2, "Banana", 30);
        dt.Rows.Add(3, "Cherry", 20);
        dt.Rows.Add(4, "Date", 15);
        dt.Rows.Add(5, "Elderberry", 5);
        return dt;
    }
}
```

**Output:** एक फ़ाइल जिसका नाम `AlternatingRows.xlsx` है, जहाँ प्रत्येक पंक्ति हल्के पीले फ़िल और सफ़ेद के बीच वैकल्पिक रूप से बदलती है, जिससे टेबल आँखों के लिए आसान बन जाती है।

## अक्सर पूछे जाने वाले प्रश्न

**Q: क्या यह तरीका Excel‑स्टाइल कंडीशनल फॉर्मेटिंग के साथ काम करता है?**  
A: हाँ। यदि आपकी लाइब्रेरी कंडीशनल रूल्स को सपोर्ट करती है, तो आप वही लॉजिक एक रूल में ट्रांसलेट कर सकते हैं जो `MOD(ROW(),2)=0` चेक करता है। यहाँ दिखाया गया कोड‑बेस्ड मेथड उन लाइब्रेरीज़ में अधिक पोर्टेबल है जिनमें बिल्ट‑इन कंडीशनल फॉर्मेटिंग नहीं होती।

**Q: यदि मुझे Excel शीट की बजाय PDF टेबल में **पंक्तियों को वैकल्पिक रूप से रंग**ना हो तो क्या करें?**  
A: अधिकांश PDF टेबल जेनरेटर (जैसे iTextSharp, PdfSharp) आपको प्रत्येक पंक्ति के लिए `BackgroundColor` सेट करने की अनुमति देते हैं। वही मॉड्यूलो कैलकुलेशन लागू होता है—

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}