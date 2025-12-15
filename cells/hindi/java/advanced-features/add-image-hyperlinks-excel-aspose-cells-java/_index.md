---
date: '2025-12-10'
description: Aspose.Cells for Java के साथ Excel में छवियों में हाइपरलिंक जोड़ना सीखें,
  स्थिर चित्रों को इंटरैक्टिव लिंक में बदलकर अधिक समृद्ध स्प्रेडशीट बनाएं।
keywords:
- image hyperlinks in Excel
- Aspose.Cells for Java
- interactive Excel spreadsheets
title: Aspose.Cells for Java का उपयोग करके Excel में छवियों में हाइपरलिंक कैसे जोड़ें
url: /hi/java/advanced-features/add-image-hyperlinks-excel-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel में चित्रों में हाइपरलिंक कैसे जोड़ें Aspose.Cells for Java का उपयोग करके

## Introduction

यदि आप अपने Excel रिपोर्ट को अधिक इंटरैक्टिव बनाना चाहते हैं, तो चित्रों में हाइपरलिंक जोड़ना सीखना एक अच्छा प्रारंभ बिंदु है। इस ट्यूटोरियल में आप देखेंगे कि Aspose.Cells for Java कैसे क्लिक करने योग्य चित्र एम्बेड करता है, जिससे स्थैतिक विज़ुअल को फ़ंक्शनल लिंक में बदला जा सकता है जो वेब पेज, दस्तावेज़ या अन्य संसाधनों को सीधे स्प्रेडशीट से खोलता है।

### What You'll Learn
- Java में Aspose.Cells वर्कबुक को इनिशियलाइज़ करना।  
- एक चित्र सम्मिलित करना और उसे हाइपरलिंक में बदलना।  
- मुख्य मेथड्स जैसे `addHyperlink`, `setPlacement`, और `setScreenTip`।  
- परफ़ॉर्मेंस और लाइसेंसिंग के लिए सर्वोत्तम प्रथाएँ।  

## Quick Answers
- **आवश्यक लाइब्रेरी कौन सी है?** Aspose.Cells for Java।  
- **क्या मैं .xlsx फ़ाइलें उपयोग कर सकता हूँ?** हाँ – API .xls और .xlsx दोनों के साथ काम करता है।  
- **क्या मुझे लाइसेंस चाहिए?** मूल्यांकन के लिए ट्रायल काम करता है; उत्पादन के लिए स्थायी लाइसेंस आवश्यक है।  
- **कोड की कितनी पंक्तियाँ?** क्लिक करने योग्य चित्र जोड़ने के लिए लगभग 20 पंक्तियाँ।  
- **क्या यह थ्रेड‑सेफ़ है?** Workbook ऑब्जेक्ट थ्रेड‑सेफ़ नहीं हैं; प्रत्येक थ्रेड के लिए अलग इंस्टेंस बनाएं।

## How to Add Hyperlink to an Image in Excel

### Prerequisites
Before you begin, make sure you have:

- **Aspose.Cells for Java** (v25.3 या बाद का)।  
- **JDK 8+** स्थापित हो।  
- एक IDE (IntelliJ IDEA, Eclipse, या NetBeans) और निर्भरता प्रबंधन के लिए Maven या Gradle।  

### Required Libraries
Add Aspose.Cells to your project:

**Maven**
```xml
<dependency>
  <groupId>com.aspose</groupId>
  <artifactId>aspose-cells</artifactId>
  <version>25.3</version>
</dependency>
```

**Gradle**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### License Acquisition
Aspose.Cells व्यावसायिक है, लेकिन आप मुफ्त ट्रायल से शुरू कर सकते हैं या अस्थायी लाइसेंस का अनुरोध कर सकते हैं:

- फ़्री ट्रायल: [Aspose Downloads](https://releases.aspose.com/cells/java/) से डाउनलोड करें।  
- अस्थायी लाइसेंस: [Temporary License page](https://purchase.aspose.com/temporary-license/) के माध्यम से अनुरोध करें।  
- खरीद: दीर्घकालिक उपयोग के लिए, [Aspose Purchase](https://purchase.aspose.com/buy) पर जाएँ।

### Basic Initialization
Create a workbook and get the first worksheet:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

// Initialize workbook
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Step‑by‑Step Implementation

### Step 1: Prepare Your Workbook
We start by creating a new workbook and selecting the first sheet.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Step 2: Insert a Label and Adjust Cell Size
Add a descriptive label and give the cell enough space for the picture.

```java
worksheet.getCells().get("C2").setValue("Image Hyperlink");
worksheet.getCells().setRowHeight(3, 100); // Set row height for C4
worksheet.getCells().setColumnWidth(2, 21); // Adjust column width for C column
```

### Step 3: Add the Image
Load the picture file and place it on the sheet.

```java
int index = worksheet.getPictures().add(3, 2, "path/to/aspose-logo.jpg");
```
*Tip*: `"path/to/aspose-logo.jpg"` को अपने चित्र फ़ाइल के वास्तविक पथ से बदलें।

### Step 4: Configure Placement and Add the Hyperlink
Make the picture free‑floating and attach a hyperlink to it.

```java
import com.aspose.cells.Picture;
import com.aspose.cells.PlacementType;

Picture pic = worksheet.getPictures().get(index);
pic.setPlacement(PlacementType.FREE_FLOATING);

// Add hyperlink to the picture
pic.addHyperlink("http://www.aspose.com/");
```

### Step 5: Set a Screen Tip and Save the Workbook
Provide a helpful tooltip and write the workbook to disk.

```java
import com.aspose.cells.Hyperlink;

Hyperlink hlink = pic.getHyperlink();
hlink.setScreenTip("Click to go to Aspose site");

workbook.save("AIHyperlinks_out.xls");
```

## Troubleshooting Tips
- **Image path errors** – फ़ाइल स्थान को दोबारा जांचें और सुनिश्चित करें कि एप्लिकेशन के पास पढ़ने की अनुमति है।  
- **License not applied** – यदि ट्रायल समाप्त हो जाता है, तो हाइपरलिंक काम करना बंद कर सकते हैं; `License.setLicense` के साथ वैध लाइसेंस लागू करें।  
- **Hyperlink not clickable** – सुनिश्चित करें कि चित्र का `PlacementType` `FREE_FLOATING` पर सेट है।  

## Practical Applications
Embedding clickable images is useful in many scenarios:

1. **Marketing reports** – ब्रांड लोगो को प्रोडक्ट पेज से लिंक करें।  
2. **Technical documentation** – डायग्राम संलग्न करें जो विस्तृत स्कीमैटिक खोलते हैं।  
3. **Educational worksheets** – आइकन को अतिरिक्त वीडियो के शॉर्टकट में बदलें।  
4. **Project dashboards** – स्टेटस आइकन को संबंधित टास्क ट्रैकर खोलने के लिए बनाएं।  

## Performance Considerations
- छवि फ़ाइल आकार को उचित रखें; बड़ी तस्वीरें वर्कबुक मेमोरी उपयोग बढ़ाती हैं।  
- लूप में कई फ़ाइलें प्रोसेस करते समय अप्रयुक्त ऑब्जेक्ट्स (`workbook.dispose()`) को डिस्पोज़ करें।  
- परफ़ॉर्मेंस सुधार और बग फिक्स के लिए नवीनतम Aspose.Cells संस्करण में अपग्रेड करें।  

## Conclusion
आप अब जानते हैं **Excel में चित्रों में हाइपरलिंक कैसे जोड़ें** Aspose.Cells for Java का उपयोग करके, जिससे आप अधिक समृद्ध, इंटरैक्टिव स्प्रेडशीट बना सकते हैं। विभिन्न URLs, स्क्रीन टिप्स, और चित्र प्लेसमेंट के साथ प्रयोग करें ताकि आपकी रिपोर्टिंग आवश्यकताओं के अनुसार अनुकूल हो सके। अगला कदम आप शैप्स में हाइपरलिंक जोड़ने या कई वर्कशीट्स में बड़े पैमाने पर चित्र सम्मिलित करने को स्वचालित करने का अन्वेषण कर सकते हैं।

## Frequently Asked Questions

**Q:** Aspose.Cells for Java द्वारा समर्थित अधिकतम चित्र आकार क्या है?  
**A:** कोई सख्त सीमा नहीं है, लेकिन बहुत बड़ी छवियाँ परफ़ॉर्मेंस को प्रभावित कर सकती हैं और फ़ाइल आकार बढ़ा सकती हैं।

**Q:** क्या मैं इस फीचर को .xlsx फ़ाइलों के साथ उपयोग कर सकता हूँ?  
**A:** हाँ, API `.xls` और `.xlsx` दोनों फ़ॉर्मेट के साथ काम करता है।

**Q:** हाइपरलिंक जोड़ते समय अपवादों को कैसे संभालें?  
**A:** कोड को try‑catch ब्लॉक में रखें और `Exception` विवरण को लॉग करें ताकि पाथ या लाइसेंसिंग समस्याओं का निदान किया जा सके।

**Q:** क्या जोड़ने के बाद चित्र से हाइपरलिंक हटाना संभव है?  
**A:** हाँ – `Picture` ऑब्जेक्ट प्राप्त करें और `pic.getHyperlink().remove()` कॉल करें या कलेक्शन से चित्र को हटाएँ।

**Q:** मेरा हाइपरलिंक अपेक्षित रूप से क्यों काम नहीं कर रहा हो सकता है?  
**A:** सामान्य कारणों में गलत URL स्ट्रिंग, `http://`/`https://` प्रीफ़िक्स की कमी, या अनलाइसेंस्ड ट्रायल जो कुछ फीचर को डिसेबल कर देता है।

## Additional Resources
- **Documentation:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Download:** [Aspose Cells Release](https://releases.aspose.com/cells/java/)  
- **Purchase and Trial:** Visit [Aspose Purchase](https://purchase.aspose.com/buy) or [Temporary License Page](https://purchase.aspose.com/temporary-license/) for licensing options.  
- **Support Forum:** For assistance, check out the [Aspose Support Forum](https://forum.aspose.com/c/cells/9).

---

**अंतिम अपडेट:** 2025-12-10  
**परीक्षित संस्करण:** Aspose.Cells for Java 25.3  
**लेखक:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
