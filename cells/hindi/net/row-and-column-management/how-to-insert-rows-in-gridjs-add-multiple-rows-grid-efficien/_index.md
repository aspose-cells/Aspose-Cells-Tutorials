---
category: general
date: 2026-03-29
description: GridJs में पंक्तियों को जल्दी से कैसे डालें, सीखें। यह गाइड पंक्तियों
  को जोड़ने और बैच ऑपरेशन के साथ ग्रिड में कई पंक्तियों को जोड़ने के बारे में भी बताता
  है।
draft: false
keywords:
- how to insert rows
- how to add rows
- add multiple rows grid
- batch row insertion
- large grid performance
language: hi
og_description: GridJs में पंक्तियों को जल्दी से कैसे डालें, सीखें। यह गाइड दिखाता
  है कि पंक्तियों को कैसे जोड़ें, ग्रिड में कई पंक्तियों को कैसे जोड़ें, और बड़े बैच
  इन्सर्ट को कैसे संभालें।
og_title: GridJs में पंक्तियों को कैसे डालें – ग्रिड में कई पंक्तियों को कुशलतापूर्वक
  जोड़ें
tags:
- GridJs
- C#
- data‑grid
title: GridJs में पंक्तियों को कैसे डालें – ग्रिड में कई पंक्तियों को कुशलता से जोड़ें
url: /hi/net/row-and-column-management/how-to-insert-rows-in-gridjs-add-multiple-rows-grid-efficien/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GridJs में पंक्तियों को कैसे डालें – ग्रिड में कई पंक्तियों को कुशलतापूर्वक जोड़ें

क्या आपने कभी सोचा है कि **how to insert rows** को एक बड़े GridJs टेबल में UI को फ्रीज़ किए बिना कैसे डालें? शायद आप **add rows** को एक‑एक करके जोड़ने की कोशिश में अटक गए हैं और प्रदर्शन बिगड़ जाता है। अच्छी खबर यह है कि GridJs एक बैच API प्रदान करता है जो आपको **add multiple rows grid** को एक ही कॉल में जोड़ने देता है, जिससे लाखों एंट्रीज़ के साथ भी सब कुछ तेज़ रहता है।

इस ट्यूटोरियल में हम एक पूर्ण, चलाने योग्य उदाहरण के माध्यम से दिखाएंगे कि `InsertRowsBatch` का उपयोग करके **how to insert rows** कैसे किया जाता है। आप देखेंगे कि बैचिंग क्यों महत्वपूर्ण है, परिणाम की पुष्टि कैसे करें, और जब आप जिस इंडेक्स को लक्षित कर रहे हैं वह बहुत बड़ा हो तो किन बातों का ध्यान रखें। अंत तक आप किसी भी GridJs इंस्टेंस में आत्मविश्वास के साथ हजारों नए रिकॉर्ड डाल सकेंगे।

## आवश्यकताएँ

- .NET 6.0 या बाद का (कोड किसी भी हालिया SDK के साथ कम्पाइल होता है)
- `GridJs` NuGet पैकेज का रेफ़रेंस (या यदि आप कस्टम बिल्ड उपयोग कर रहे हैं तो DLL)
- बेसिक C# ज्ञान – आपको गुरु बनने की ज़रूरत नहीं, बस क्लास और मेथड्स के साथ सहज होना चाहिए
- आपका पसंदीदा IDE या एडिटर (Visual Studio, Rider, VS Code… सभी काम करेंगे)

> **Pro tip:** यदि आप वास्तव में बड़े ग्रिड्स (दसियों मिलियन पंक्तियों) के साथ काम करने की योजना बना रहे हैं, तो UI रेंडरिंग को हल्का रखने के लिए `gridJs.EnableVirtualization = true;` सक्षम करें।

## चरण 1: GridJs इंस्टेंस बनाएं और कॉन्फ़िगर करें

सबसे पहले: आपको एक लाइव `GridJs` ऑब्जेक्ट चाहिए। इसे उस कैनवास की तरह सोचें जहाँ आप पंक्तियों को पेंट करेंगे।

```csharp
using System;
using GridJsLibrary;   // Assume this is the namespace for GridJs

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Initialize the grid
            GridJs gridJs = new GridJs();

            // Optional: turn on virtualization for huge data sets
            gridJs.EnableVirtualization = true;

            // Populate the grid with some dummy data so we can see the effect
            SeedInitialData(gridJs);

            // Now we’re ready to insert rows in bulk
            InsertRowsInBatch(gridJs);
        }

        // Helper: add 2 000 000 rows so our batch lands at index 2 000 001
        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }
```

> **Why this step matters:** ग्रिड को इनिशियलाइज़ करना और वैकल्पिक रूप से डेटा सीड करना एक वास्तविक परिदृश्य को दर्शाता है जहाँ ग्रिड में पहले से ही बड़ी मात्रा में जानकारी होती है। बाद में हम जो बैच इन्सर्ट करेंगे उसे ज़ीरो‑बेस्ड इंडेक्स का सम्मान करना होगा, इसलिए हम सटीक इन्सर्शन पॉइंट दिखाने के लिए पहले से डेटा डालते हैं।

## चरण 2: `InsertRowsBatch` का उपयोग करके **Add Multiple Rows Grid**

अब ट्यूटोरियल का मुख्य भाग – वह कॉल जो वास्तव में **add rows** को बल्क में जोड़ता है। मेथड सिग्नेचर है `InsertRowsBatch(int startIndex, int count)`। हमारे उदाहरण में हम इंडेक्स 2 000 000 (जो 2 000 001वीं पंक्ति के बराबर है) से शुरू करेंगे और दस पंक्तियाँ जोड़ेंगे।

```csharp
        // Step 2 – Insert a batch of rows
        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based, so this is row 2 000 001
            int rowsToAdd = 10;

            // The batch call creates placeholder rows; you can later populate them
            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Verify by reading back a few rows
            VerifyInsertion(grid, startIndex, rowsToAdd);
        }
```

> **How it works:** `InsertRowsBatch` आंतरिक रूप से अनुरोधित संख्या में पंक्तियों को आवंटित करता है और मौजूदा पंक्तियों को नीचे शिफ्ट करता है। क्योंकि यह ऑपरेशन एक ही ट्रांज़ैक्शन में किया जाता है, UI केवल एक बार रिफ्रेश होता है, इसलिए यह मेथड **how to add rows** को कुशलतापूर्वक करने का सुझाया गया तरीका है।

## चरण 3: इन्सर्शन की पुष्टि करें – क्या पंक्तियाँ अपेक्षित स्थान पर आईं?

बैच ऑपरेशन के बाद आपको यह सुनिश्चित करना होगा कि पंक्तियाँ वहीँ हैं जहाँ आप सोचते हैं। नीचे दिया गया हेल्पर नए जोड़े गए ब्लॉक की पहली और आखिरी पंक्तियों को पढ़ता है और उन्हें कंसोल में प्रिंट करता है।

```csharp
        // Step 3 – Simple verification
        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

**अपेक्षित आउटपुट**

```
Initial seed completed – 2 000 000 rows present.
Inserted 10 rows starting at index 2000001.
Verifying inserted rows:
Row 2000001: , 
Row 2000002: , 
...
Row 2000010: , 
```

खाली सेल्स यह दर्शाते हैं कि पंक्तियाँ प्लेसहोल्डर हैं और डेटा की प्रतीक्षा कर रही हैं। अब आप उन्हें व्यक्तिगत रूप से भर सकते हैं या कोई और बैच अपडेट चला सकते हैं।

> **Edge case note:** यदि `startIndex` वर्तमान पंक्ति संख्या से अधिक है, तो GridJs स्वचालित रूप से नई पंक्तियों को अंत में जोड़ देगा। इसके विपरीत, नकारात्मक इंडेक्स `ArgumentOutOfRangeException` फेंकेगा, इसलिए हमेशा उपयोगकर्ता‑द्वारा प्रदान किए गए इंडेक्स की वैधता जांचें।

## चरण 4: नई पंक्तियों को भरें (वैकल्पिक लेकिन सामान्य)

अक्सर आप सिर्फ खाली पंक्तियाँ नहीं चाहते; आपको उन्हें अर्थपूर्ण मानों से भरना पड़ता है। आप नई बनाई गई रेंज पर लूप करके `SetCell` या समान API को कॉल कर सकते हैं।

```csharp
        // Optional: fill the newly added rows with sample data
        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }
```

यदि आपको पंक्तियों को तुरंत डिस्प्ले के लिए तैयार रखना है, तो बैच इन्सर्ट के बाद आप `PopulateNewRows(gridJs, startIndex, rowsToAdd);` कॉल कर सकते हैं।

## चरण 5: बहुत बड़े ग्रिड्स के लिए प्रदर्शन टिप्स

जब आप **add multiple rows grid** को मिलियनों में संभाल रहे हों, तो इन ट्रिक्स को याद रखें:

1. **Batch size matters** – एक बार में 10 000 पंक्तियों को डालना दस अलग‑अलग 1 000‑पंक्ति बैचों से तेज़ हो सकता है क्योंकि प्रत्येक बैच केवल एक UI रिफ्रेश उत्पन्न करता है।
2. **Turn off UI updates** – कुछ GridJs संस्करण `grid.SuspendLayout()` / `grid.ResumeLayout()` प्रदान करते हैं। यदि आपको लैग महसूस हो तो अपने बैच को इन कॉल्स के भीतर रैप करें।
3. **Use virtualization** – जैसा कि पहले दिखाया गया, `EnableVirtualization` मेमोरी उपयोग और रेंडरिंग समय को नाटकीय रूप से घटाता है।
4. **Avoid deep copies** – ग्रिड को सरल वैल्यू टाइप्स या हल्के ऑब्जेक्ट्स पास करें; भारी ऑब्जेक्ट्स ग्रिड को डेटा क्लोन करने के लिए मजबूर करते हैं, जिससे प्रदर्शन घटता है।

## पूरा कार्यशील उदाहरण

सब कुछ एक साथ रखते हुए, यहाँ पूरा प्रोग्राम है जिसे आप नई कंसोल प्रोजेक्ट में कॉपी‑पेस्ट कर सकते हैं:

```csharp
using System;
using GridJsLibrary;   // Replace with the actual namespace of your GridJs library

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            GridJs gridJs = new GridJs
            {
                EnableVirtualization = true
            };

            SeedInitialData(gridJs);
            InsertRowsInBatch(gridJs);
        }

        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }

        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based index for row 2 000 001
            int rowsToAdd = 10;

            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Optional: fill them with data
            PopulateNewRows(grid, startIndex, rowsToAdd);

            VerifyInsertion(grid, startIndex, rowsToAdd);
        }

        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }

        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

प्रोग्राम चलाएँ, और आप कंसोल आउटपुट देखेंगे जो पुष्टि करता है कि दस पंक्तियाँ सही स्थान पर डाली गईं और फिर भर दी गईं।

## निष्कर्ष

हमने **how to insert rows** को बैच API का उपयोग करके GridJs में कवर किया, **how to add rows** को कुशलतापूर्वक दिखाया, और **add multiple rows grid** को UI को बाधित किए बिना करने के तरीके खोजे। मुख्य बिंदु हैं:

- किसी भी बल्क ऑपरेशन के लिए `InsertRowsBatch(startIndex, count)` का उपयोग करें।
- इंडेक्स की वैधता जांचें और बड़े डेटासेट्स के लिए वर्चुअलाइज़ेशन पर विचार करें।
- यदि आपको तुरंत कंटेंट चाहिए तो बैच के बाद पंक्तियों को भरें।

अगला, आप **how to delete rows** को एक्सप्लोर कर सकते हैं, बैच एडिट्स के लिए **undo/redo** लागू कर सकते हैं, या GridJs को बैक‑एंड सर्विस के साथ इंटीग्रेट कर सकते हैं जो ऑन‑डिमांड डेटा स्ट्रीम करता है। ये सभी विषय सीधे उन अवधारणाओं पर आधारित हैं जो आपने अभी सीखी हैं।

बिना झिझक प्रयोग करें—बैच साइज बदलें, ग्रिड की शुरुआत में इन्सर्ट करने की कोशिश करें, या एक ही ट्रांज़ैक्शन में कई बैच को मिलाएँ। जितना अधिक आप खेलेंगे, उतना ही आप बड़े ग्रिड्स के साथ सहज हो जाएंगे।

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}