---
category: general
date: 2026-03-18
description: Excel से तिथि निकालें और yyyy‑mm‑dd प्रारूप में ISO तिथि आउटपुट करें।
  जापानी युग तिथियों को पढ़ना, उन्हें परिवर्तित करना, और C# में ISO तिथियों को प्रदर्शित
  करना सीखें।
draft: false
keywords:
- extract date from excel
- output date yyyy-mm-dd
- display date iso format
language: hi
og_description: Excel से तिथि निकालें और ISO फ़ॉर्मेट में yyyy‑mm‑dd के रूप में तिथि
  आउटपुट करें। पूर्ण कोड और व्याख्याओं के साथ चरण‑दर‑चरण C# ट्यूटोरियल।
og_title: Excel से तिथि निकालें – C# में तिथि को yyyy‑mm‑dd रूप में आउटपुट करें
tags:
- C#
- Excel
- DateTime
- Aspose.Cells
title: Excel से तारीख निकालें और yyyy‑mm‑dd प्रारूप में आउटपुट करें – पूर्ण C# गाइड
url: /hi/net/data-loading-and-parsing/extract-date-from-excel-and-output-date-yyyy-mm-dd-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel से तिथि निकालें – ISO फ़ॉर्मेट में yyyy‑mm‑dd तिथि कैसे आउटपुट करें

क्या आपको कभी **Excel से तिथि निकालनी** पड़ी है लेकिन जापानी युग तिथियों को संभालने या साफ़ `yyyy‑mm‑dd` स्ट्रिंग प्राप्त करने में संदेह रहा है? आप अकेले नहीं हैं। कई डेटा‑माइग्रेशन प्रोजेक्ट्स में स्रोत वर्कबुक जापानी सम्राट कैलेंडर का उपयोग करके तिथियों को संग्रहीत करता है, और डाउनस्ट्रीम सिस्टम एक ISO‑अनुपालन तिथि जैसे `2024-04-01` की अपेक्षा करता है।

इस गाइड में हम एक पूर्ण, चलाने योग्य समाधान के माध्यम से चलेंगे जो एक सेल पढ़ता है, जापानी युग को समझता है, और **तिथि को yyyy‑mm‑dd में आउटपुट करता है**। अंत तक आप बिल्कुल जान पाएँगे कि किसी भी .NET एप्लिकेशन में **ISO फ़ॉर्मेट में तिथि कैसे प्रदर्शित करें** और आपके पास एक पुन: उपयोग योग्य कोड स्निपेट होगा जिसे आप अपने प्रोजेक्ट में डाल सकते हैं।

## आपको क्या चाहिए

- **.NET 6+** (या .NET Framework 4.7.2+).  
- **Aspose.Cells for .NET** – वह लाइब्रेरी जो वर्कबुक लोड करते समय कस्टम कैलेंडर सेट करने की अनुमति देती है।  
- एक Excel फ़ाइल (`japan-date.xlsx`) जिसमें जापानी युग सेल में तिथि संग्रहीत है (उदाहरण के लिए `令和3年4月1日`)।  
- आपका पसंदीदा IDE – Visual Studio, Rider, या यहाँ तक कि VS Code भी चलेगा।

Aspose.Cells के अलावा कोई अतिरिक्त NuGet पैकेज आवश्यक नहीं है, और कोड Windows, Linux, या macOS पर काम करता है।

## चरण 1: प्रोजेक्ट सेट अप करें और Aspose.Cells स्थापित करें

```bash
dotnet new console -n ExcelDateDemo
cd ExcelDateDemo
dotnet add package Aspose.Cells
```

> **Pro tip:** यदि आप CI सर्वर पर हैं, तो पैकेज संस्करण (`Aspose.Cells 23.12`) को पिन करें ताकि पुनरुत्पादनीय बिल्ड सुनिश्चित हो सके।

## चरण 2: जापानी सम्राट कैलेंडर के साथ वर्कबुक लोड करें

जब स्रोत गैर‑ग्रेगोरियन कैलेंडर का उपयोग करता है, तो **Excel से तिथि निकालने** की कुंजी यह है कि लोड करते समय Aspose.Cells को बताएं कि कौन सा कैलेंडर लागू करना है। हम यह `LoadOptions.Calendar` के साथ करते हैं।

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create load options and set the Japanese Emperor calendar
        LoadOptions loadOptions = new LoadOptions
        {
            // This tells Aspose.Cells to interpret era dates correctly
            Calendar = new JapaneseEmperorCalendar()
        };

        // Step 3: Open the workbook that contains Japanese era dates
        // Replace the path with the actual location of your Excel file
        string filePath = @"YOUR_DIRECTORY\japan-date.xlsx";
        Workbook workbook = new Workbook(filePath, loadOptions);
```

**Why this matters:** कस्टम कैलेंडर के बिना, Aspose.Cells सेल को साधारण स्ट्रिंग मान लेगा, और आप युग की जानकारी खो देंगे। `JapaneseEmperorCalendar` असाइन करने से, लाइब्रेरी स्वचालित रूप से `令和3年4月1日` को बैकग्राउंड में `2021‑04‑01` में बदल देती है।

## चरण 3: किसी विशिष्ट सेल से तिथि प्राप्त करें

अब जब वर्कबुक को युग को समझने का तरीका पता है, हम सेल को `DateTime` के रूप में पढ़ सकते हैं। मान लेते हैं कि तिथि पहले वर्कशीट के सेल **A1** (पंक्ति 0, कॉलम 0) में है।

```csharp
        // Step 4: Retrieve the date value from the first worksheet, first cell
        Worksheet sheet = workbook.Worksheets[0];
        Cell dateCell = sheet.Cells[0, 0]; // A1

        // GetDateTime() returns a System.DateTime object
        DateTime extractedDate = dateCell.GetDateTime();
```

यदि सेल खाली है या गैर‑तिथि मान रखता है, तो `GetDateTime()` एक अपवाद फेंकेगा। एक रक्षाात्मक तरीका इस प्रकार दिखता है:

```csharp
        if (dateCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("The target cell does not contain a valid date.");
            return;
        }

        DateTime extractedDate = dateCell.GetDateTime();
```

**Edge case:** कुछ पुराने Excel फ़ाइलें तिथियों को संख्याओं (सीरियल डेट) के रूप में संग्रहीत करती हैं। Aspose.Cells इन्हें स्वचालित रूप से संभालता है, लेकिन यदि आप मिश्रित सामग्री की अपेक्षा करते हैं तो आपको अभी भी सेल प्रकार की जाँच करनी चाहिए।

## चरण 4: तिथि को yyyy‑mm‑dd (ISO) में आउटपुट करें और सत्यापित करें

`DateTime` हाथ में होने पर, इसे **output date yyyy‑mm‑dd** के रूप में फॉर्मेट करना एक लाइनर है:

```csharp
        // Step 5: Output the date in ISO format (yyyy‑mm‑dd)
        string isoDate = extractedDate.ToString("yyyy-MM-dd");
        Console.WriteLine($"Extracted date (ISO): {isoDate}");
    }
}
```

`令和3年4月1日` वाली फ़ाइल के खिलाफ प्रोग्राम चलाने पर यह प्रिंट करेगा:

```
Extracted date (ISO): 2021-04-01
```

यह वही **display date iso format** है जिसकी कई APIs को आवश्यकता होती है।

## पूर्ण कार्यशील उदाहरण

सभी भागों को मिलाकर, यहाँ पूरा, कॉपी‑एंड‑पेस्ट‑तैयार प्रोग्राम है:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook with Japanese era support
        LoadOptions loadOptions = new LoadOptions
        {
            Calendar = new JapaneseEmperorCalendar()
        };

        string filePath = @"YOUR_DIRECTORY\japan-date.xlsx";
        Workbook workbook = new Workbook(filePath, loadOptions);

        // Access the cell that holds the date (A1)
        Worksheet sheet = workbook.Worksheets[0];
        Cell dateCell = sheet.Cells[0, 0];

        // Validate the cell contains a date
        if (dateCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("The target cell does not contain a valid date.");
            return;
        }

        // Extract the DateTime value
        DateTime extractedDate = dateCell.GetDateTime();

        // Convert to ISO format (yyyy‑mm‑dd)
        string isoDate = extractedDate.ToString("yyyy-MM-dd");
        Console.WriteLine($"Extracted date (ISO): {isoDate}");
    }
}
```

> **Note:** `YOUR_DIRECTORY` को वास्तविक फ़ोल्डर से बदलें जिसमें `japan-date.xlsx` है। कोड किसी भी शीट और किसी भी सेल के साथ काम करता है – केवल इंडेक्स को समायोजित करें।

## अन्य कैलेंडरों को संभालना (वैकल्पिक)

यदि आपको कभी **Excel से तिथि निकालनी** पड़े जो थाई बौद्ध कैलेंडर या हिब्रू कैलेंडर का उपयोग करता है, तो बस कैलेंडर इंस्टेंस को बदल दें:

```csharp
loadOptions.Calendar = new ThaiBuddhistCalendar();   // for Thai dates
// or
loadOptions.Calendar = new HebrewCalendar();         // for Hebrew dates
```

बाकी लॉजिक अपरिवर्तित रहता है, जो इस दृष्टिकोण की लचीलापन दर्शाता है।

## सामान्य समस्याएँ और उन्हें कैसे टालें

| समस्या | क्यों होता है | समाधान |
|-------|----------------|-----|
| `GetDateTime()` throws `InvalidCastException` | सेल तिथि नहीं है (शायद स्ट्रिंग) | `Cell.Type` को कॉल करने से पहले जांचें, या `Cell.StringValue` पर `DateTime.TryParse` उपयोग करें। |
| परिवर्तन के बाद गलत वर्ष | `Calendar` सेट किए बिना वर्कबुक लोड किया गया | फ़ाइल खोलने से **पहले** हमेशा उपयुक्त कैलेंडर के साथ `LoadOptions` बनाएं। |
| ISO आउटपुट में समय भाग दिखता है (`2021-04-01 00:00:00`) | `ToString()` को बिना फ़ॉर्मेट स्ट्रिंग के उपयोग किया | `"yyyy-MM-dd"` फ़ॉर्मेट स्पेसिफ़ायर का उपयोग करें ताकि **output date yyyy‑mm‑dd** बाध्य हो सके। |
| फ़ाइल नहीं मिली | रिलेटिव पाथ गलत फ़ोल्डर की ओर इशारा करता है | `Path.Combine(Environment.CurrentDirectory, "japan-date.xlsx")` का उपयोग करें या पूर्ण पाथ प्रदान करें। |

## प्रोडक्शन‑रेडी कोड के लिए प्रो टिप्स

1. **Cache the workbook** यदि आपको एक ही फ़ाइल से कई तिथियाँ पढ़नी हों – वर्कबुक खोलना तुलनात्मक रूप से महंगा होता है।  
2. **Wrap the extraction logic** को एक पुन: उपयोग योग्य मेथड में लपेटें:

   ```csharp
   static string ExtractIsoDate(string file, int sheetIdx, int row, int col)
   {
       var opts = new LoadOptions { Calendar = new JapaneseEmperorCalendar() };
       var wb = new Workbook(file, opts);
       var cell = wb.Worksheets[sheetIdx].Cells[row, col];
       if (cell.Type != CellValueType.IsDateTime) return null;
       return cell.GetDateTime().ToString("yyyy-MM-dd");
   }
   ```

3. **Log the original era string** (`cell.StringValue`) को ISO आउटपुट के साथ ऑडिट ट्रेल के लिए लॉग करें।  
4. **Unit test** मेथड को कुछ हार्ड‑कोडेड Excel फ़ाइलों के साथ विभिन्न युगों (Heisei, Reiwa) को कवर करके करें ताकि सहीपन सुनिश्चित हो सके।

## दृश्य अवलोकन

नीचे एक त्वरित आरेख है जो डेटा प्रवाह को दर्शाता है—Excel सेल से ISO स्ट्रिंग तक।

![Excel से तिथि निकालने का उदाहरण दिखाते हुए Excel → LoadOptions → DateTime → ISO स्ट्रिंग]

## निष्कर्ष

हमने वह सब कवर किया है जो आपको **Excel से तिथि निकालने**, जापानी युग मानों को संभालने, और **yyyy‑mm‑dd तिथि आउटपुट करने** के लिए चाहिए, ताकि यह आधुनिक APIs द्वारा पसंद किए जाने वाले **display date iso format** के अनुरूप हो। समाधान स्व-निहित है, किसी भी .NET संस्करण के साथ काम करता है जो Aspose.Cells का समर्थन करता है, और एक ही लाइन परिवर्तन से अन्य कैलेंडरों में विस्तारित किया जा सकता है।

क्या आपके मन में कोई अलग कैलेंडर है? या शायद आप कई कॉलम से तिथियाँ निकाल रहे हैं? `ExtractIsoDate` हेल्पर को संशोधित करने या नीचे टिप्पणी छोड़ने में संकोच न करें। कोडिंग का आनंद लें, और आपकी तिथियाँ हमेशा परिपूर्ण ISO सिंक में रहें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}