---
category: general
date: 2026-10-10
description: C# के साथ Excel वर्कबुक में पूरी पंक्ति को कैसे हटाया जाए, सीखें। यह
  चरण‑दर‑चरण गाइड यह भी बताता है कि इंडेक्स द्वारा पंक्ति को कैसे हटाया जाए और Aspose.Cells
  का उपयोग करके इंडेक्स द्वारा पंक्ति को कैसे हटाया जाए।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete entire row
- how to delete row
- remove row by index
- delete row excel
- delete row c#
language: hi
lastmod: 2026-10-10
og_description: C# का उपयोग करके Excel वर्कबुक में पूरी पंक्ति हटाएँ। इस गाइड का पालन
  करके सीखें कि इंडेक्स द्वारा पंक्ति कैसे हटाएँ, इंडेक्स द्वारा पंक्ति कैसे निकालें,
  और फ़ाइल को सुरक्षित रूप से कैसे सहेजें।
og_image_alt: Screenshot of an Excel worksheet before and after deleting an entire
  row with C# code
og_title: C# के साथ Excel में पूरी पंक्ति हटाएँ – पूर्ण प्रोग्रामिंग गाइड
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to delete entire row in an Excel workbook with C#. This step‑by‑step
    guide also covers how to delete row by index and remove row by index using Aspose.Cells.
  headline: How to delete entire row in an Excel file using C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: C# का उपयोग करके Excel फ़ाइल में पूरी पंक्ति कैसे हटाएँ
url: /hi/net/row-and-column-management/how-to-delete-entire-row-in-an-excel-file-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# का उपयोग करके Excel फ़ाइल में पूरी पंक्ति हटाएँ

यदि आपको Excel वर्कबुक में **पूरी पंक्ति हटानी** है, तो यह गाइड आपको C# के साथ इसे कैसे करें, बिल्कुल दिखाता है। चाहे आप आयातित डेटा को साफ़ कर रहे हों या रिपोर्टिंग टूल बना रहे हों, नीचे दिए गए चरण आपको पंक्ति को उसके इंडेक्स से हटाने और परिणाम को अन्य डेटा खोए बिना सहेजने की अनुमति देते हैं।

आप यह भी देखेंगे कि वही तरीका कैसे **इंडेक्स द्वारा पंक्ति कैसे हटाएँ** प्रश्न का उत्तर देता है, **इंडेक्स द्वारा पंक्ति हटाएँ** और क्यों यह **delete row excel** परिदृश्यों में C# में काम करता है।

## पूर्वापेक्षाएँ

* .NET 6.0 या बाद का संस्करण (कोड .NET Framework 4.6+ के साथ भी काम करता है)  
* **Aspose.Cells for .NET** लाइब्रेरी (NuGet के माध्यम से उपलब्ध: `Install-Package Aspose.Cells`)  
* C# कंसोल या डेस्कटॉप प्रोजेक्ट्स की बुनियादी परिचितता  

कोई अतिरिक्त Excel इंटरऑप या COM घटक आवश्यक नहीं हैं, जिससे समाधान हल्का और सर्वर‑साइड निष्पादन के लिए सुरक्षित रहता है।

## चरण 1: प्रोजेक्ट सेट अप करें और नेमस्पेस आयात करें

एक नया कंसोल एप्लिकेशन बनाएँ (या कोड को मौजूदा प्रोजेक्ट में जोड़ें) और आवश्यक `using` निर्देश जोड़ें:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // The rest of the tutorial code lives here.
        }
    }
}
```

*यह क्यों महत्वपूर्ण है*: `Aspose.Cells` को आयात करने से आपको `Workbook`, `Worksheet`, और `DeleteRows` मेथड तक पहुँच मिलती है जो वास्तविक पंक्ति हटाने को निष्पादित करता है।

## चरण 2: वर्कबुक लोड करें और वर्कशीट चुनें

आपको स्रोत फ़ाइल (`input.xlsx`) लोड करनी होगी और वह वर्कशीट प्राप्त करनी होगी जिसे आप संशोधित करना चाहते हैं। पहली वर्कशीट को इंडेक्स `0` से एक्सेस किया जाता है।

```csharp
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Get the first worksheet (you can also use workbook.Worksheets["SheetName"])
Worksheet ws = workbook.Worksheets[0];
```

> **टिप**: यदि आपको किसी विशिष्ट शीट के साथ काम करना है, तो इंडेक्स को शीट नाम से बदलें: `workbook.Worksheets["Data"]`।

## चरण 3: शून्य‑आधारित इंडेक्स द्वारा पूरी पंक्ति हटाएँ

Aspose.Cells शून्य‑आधारित इंडेक्सिंग का उपयोग करता है, इसलिए पहली पंक्ति `0` है। पंक्ति 5 (छठी दृश्य पंक्ति) को हटाने के लिए, `DeleteRows` को `DeleteOptions.DeleteEntireRow` के साथ कॉल करें।

```csharp
// Delete one row starting at index 5 (zero‑based) and remove the whole row
ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
```

*व्याख्या*:

* `ws.Cells[5, 0]` उस पंक्ति की पहली सेल की ओर इशारा करता है जिसे आप हटाना चाहते हैं।  
* `DeleteRows(1, DeleteOptions.DeleteEntireRow)` Aspose.Cells को **1** पंक्ति हटाने के लिए बताता है, और `DeleteEntireRow` फ़्लैग सुनिश्चित करता है कि **पूरी पंक्ति** गायब हो जाए, नीचे की पंक्तियाँ ऊपर की ओर शिफ्ट हो जाएँ।

### अन्य परिदृश्यों में इंडेक्स द्वारा पंक्ति कैसे हटाएँ

* **एकाधिक क्रमिक पंक्तियों को हटाएँ** – पहले तर्क को उन पंक्तियों की संख्या में बदलें जिन्हें आप मिटाना चाहते हैं:

  ```csharp
  // Remove rows 5, 6 and 7 (three rows total)
  ws.Cells[5, 0].DeleteRows(3, DeleteOptions.DeleteEntireRow);
  ```

* **अंतिम पंक्ति हटाएँ** – नीचे सबसे अधिक पॉप्युलेटेड पंक्ति का इंडेक्स प्राप्त करने के लिए `ws.Cells.MaxDataRow` का उपयोग करें:

  ```csharp
  int lastRow = ws.Cells.MaxDataRow;
  ws.Cells[lastRow, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
  ```

ये स्निपेट्स **इंडेक्स द्वारा पंक्ति हटाएँ** की आवश्यकता को पूरा करते हैं जबकि कोड को पढ़ने में आसान रखते हैं।

## चरण 4: पंक्ति हटाने के बाद वर्कबुक सहेजें

हटाने के बाद, संशोधित वर्कबुक को डिस्क पर वापस लिखें। आप मूल फ़ाइल को ओवरराइट कर सकते हैं या नई फ़ाइल बना सकते हैं।

```csharp
// Save the workbook to a new file (or overwrite the original)
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

यदि आपको मूल फ़ाइल को अपरिवर्तित रखना है, तो बस आउटपुट पाथ बदलें। `Save` मेथड कई फ़ॉर्मैट्स (`.xls`, `.csv`, `.pdf`, आदि) को सपोर्ट करता है – बस फ़ाइल एक्सटेंशन बदल दें।

## पूर्ण कार्यशील उदाहरण

सब कुछ मिलाकर, यहाँ एक पूर्ण, चलाने के लिए तैयार प्रोग्राम है:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // 2️⃣ Select the first worksheet
            Worksheet ws = workbook.Worksheets[0];

            // 3️⃣ Delete the entire row at index 5 (sixth visual row)
            ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);

            // 4️⃣ Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");

            Console.WriteLine("Row deleted successfully. Output saved to output.xlsx");
        }
    }
}
```

**अपेक्षित आउटपुट**: प्रोग्राम चलाने के बाद, `output.xlsx` में सभी मूल पंक्तियाँ होंगी सिवाय उस पंक्ति के जो दृश्य पंक्ति 6 से शुरू हुई थी। हटाई गई पंक्ति के नीचे का सभी डेटा स्वतः ऊपर शिफ्ट हो जाएगा, फ़ॉर्मूले और फ़ॉर्मेटिंग को संरक्षित रखते हुए।

## सामान्य कठिनाइयाँ और उन्हें कैसे टालें

| समस्या | क्यों होता है | समाधान |
|-------|----------------|-----|
| **Index out of range** | ऐसी पंक्ति इंडेक्स को हटाने की कोशिश करना जो मौजूद नहीं है (जैसे, 200‑पंक्तियों वाली शीट में `ws.Cells[1000,0]`) | `DeleteRows` कॉल करने से पहले वैध अधिकतम इंडेक्स की जाँच करने के लिए `ws.Cells.MaxDataRow` का उपयोग करें। |
| **Partial row deletion** | `DeleteOptions.DeleteEntireRow` को छोड़ने से केवल सेल की सामग्री साफ़ होती है | जब आपको पूरी पंक्ति हटानी हो, तो हमेशा `DeleteOptions.DeleteEntireRow` पास करें। |
| **Unexpected formula changes** | फ़ॉर्मूला रेंज का हिस्सा होने वाली पंक्तियों को हटाने से रेफ़रेंसेज़ टूट सकती हैं | यदि आपका वर्कबुक डायनामिक रेंज पर निर्भर है, तो हटाने के बाद फ़ॉर्मूले पुनः‑मूल्यांकन करें (`workbook.CalculateFormula()`)। |
| **Saving to a read‑only location** | `Save` कॉल फ़ोल्डर संरक्षित होने पर अपवाद फेंकता है | सुनिश्चित करें कि लक्ष्य डायरेक्टरी लिखने योग्य है या प्रोग्राम को उचित अनुमतियों के साथ चलाएँ। |

इन मुद्दों को संबोधित करने से समाधान उत्पादन उपयोग के लिए मजबूत बनता है और **delete row excel** और **delete row c#** प्रश्नों को संतुष्ट करता है।

## उन्नत: शर्त के आधार पर पंक्तियों को हटाना

कभी‑कभी आपको उन पंक्तियों को हटाना पड़ता है जो किसी मानदंड को पूरा करती हैं (जैसे, कॉलम A खाली होने वाली पंक्तियाँ)। निम्नलिखित लूप नीचे से ऊपर की ओर स्कैन करके मिलती‑जुलती पंक्तियों को हटाने का सुरक्षित तरीका दर्शाता है:

```csharp
int lastRow = ws.Cells.MaxDataRow;
for (int row = lastRow; row >= 0; row--)
{
    // Check if column A (index 0) is empty
    if (ws.Cells[row, 0].StringValue == string.Empty)
    {
        ws.Cells[row, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
    }
}
workbook.Save("YOUR_DIRECTORY/cleaned.xlsx");
```

ऊपर की ओर स्कैन करने से इंडेक्स शिफ्ट समस्या से बचा जाता है जो आगे की ओर इटरिटेट करते हुए पंक्तियों को हटाने पर उत्पन्न होती है।

## निष्कर्ष

अब आप जानते हैं कि C# का उपयोग करके Excel वर्कबुक में **पूरी पंक्ति कैसे हटाएँ**। गाइड ने निम्नलिखित को कवर किया:

* वर्कबुक लोड करना और वर्कशीट चुनना  
* `DeleteRows` को `DeleteOptions.DeleteEntireRow` के साथ उपयोग करके इंडेक्स द्वारा **पंक्ति कैसे हटाएँ**  
* संशोधित फ़ाइल को सुरक्षित रूप से सहेजना  
* एज‑केस हैंडलिंग, प्रदर्शन टिप्स, और शर्त‑आधारित डिलीशन उदाहरण  

इस ज्ञान के साथ आप आत्मविश्वास से **इंडेक्स द्वारा पंक्ति हटाएँ** कार्यक्षमता लागू कर सकते हैं, डेटा सफ़ाई को स्वचालित कर सकते हैं, और किसी भी C# एप्लिकेशन में Excel मैनिपुलेशन को एकीकृत कर सकते हैं।  

**अगले कदम**: Aspose.Cells की अन्य सुविधाओं जैसे पंक्तियों को इन्सर्ट करना, रेंज कॉपी करना, या वर्कबुक को PDF में बदलना—इनमें से प्रत्येक वही `Workbook` और `Worksheet` ऑब्जेक्ट्स पर आधारित है जिन्हें आपने अभी सीखा है। कोडिंग का आनंद लें!

## आप आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API सुविधाओं में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करती हैं।

- [Aspose.Cells .NET का उपयोग करके Excel पंक्ति कैसे हटाएँ: एक व्यापक गाइड](/cells/english/net/worksheet-management/delete-excel-row-aspose-cells-net-tutorial/)
- [Aspose Cells पंक्तियों को हटाएँ – Excel में हेडर पंक्ति की सुरक्षा](/cells/english/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/)
- [Aspose.Cells for Java का उपयोग करके Excel में कुशल पंक्ति प्रबंधन: इन्सर्ट और डिलीट पंक्तियाँ](/cells/english/java/worksheet-management/aspose-cells-java-row-operations-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}