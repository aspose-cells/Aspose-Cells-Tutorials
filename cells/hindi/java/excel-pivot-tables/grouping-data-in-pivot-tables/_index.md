---
"description": "जावा के लिए Aspose.Cells का उपयोग करके Excel में पिवट टेबल बनाना सीखें। स्रोत कोड उदाहरणों के साथ डेटा समूहीकरण और विश्लेषण को स्वचालित करें।"
"linktitle": "पिवट तालिकाओं में डेटा समूहीकरण"
"second_title": "Aspose.Cells जावा एक्सेल प्रोसेसिंग एपीआई"
"title": "पिवट तालिकाओं में डेटा समूहीकरण"
"url": "/hi/java/excel-pivot-tables/grouping-data-in-pivot-tables/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# पिवट तालिकाओं में डेटा समूहीकरण


पिवट टेबल स्प्रेडशीट में डेटा का विश्लेषण और सारांश बनाने के लिए एक शक्तिशाली उपकरण है। वे आपको मूल्यवान जानकारी प्राप्त करने के लिए डेटा को समूहीकृत और वर्गीकृत करने की अनुमति देते हैं। इस लेख में, हम स्रोत कोड उदाहरणों के साथ-साथ जावा के लिए Aspose.Cells का उपयोग करके पिवट टेबल में डेटा को प्रभावी ढंग से समूहीकृत करने का तरीका जानेंगे।

## परिचय

पिवट टेबल बड़े डेटासेट से डेटा को व्यवस्थित और सारांशित करने का एक लचीला तरीका प्रदान करते हैं। वे आपको अपने डेटा को श्रेणियों या पदानुक्रमों में समूहीकृत करके उसके कस्टम दृश्य बनाने की अनुमति देते हैं। इससे आपको अपने डेटा में रुझानों, पैटर्न और आउटलेयर को अधिक आसानी से पहचानने में मदद मिल सकती है।

## चरण 1: पिवट तालिका बनाएं

आइए जावा के लिए Aspose.Cells का उपयोग करके पिवट टेबल बनाना शुरू करें। नीचे एक नमूना एक्सेल फ़ाइल से पिवट टेबल बनाने का एक उदाहरण दिया गया है।

```java
// एक्सेल फ़ाइल लोड करें
Workbook workbook = new Workbook("sample.xlsx");

// डेटा युक्त वर्कशीट तक पहुंचें
Worksheet worksheet = workbook.getWorksheets().get(0);

// डेटा रेंज निर्दिष्ट करें
CellArea sourceData = new CellArea();
sourceData.startRow = 0;
sourceData.endRow = 19; // मान लें कि डेटा की 20 पंक्तियाँ हैं
sourceData.startColumn = 0;
sourceData.endColumn = 3; // डेटा के 4 कॉलम मानते हुए

// डेटा रेंज के आधार पर पिवट टेबल बनाएं
int index = worksheet.getPivotTables().add(sourceData, "A1", "PivotTable1");

// इंडेक्स द्वारा पिवट तालिका प्राप्त करें
PivotTable pivotTable = worksheet.getPivotTables().get(index);

// पंक्तियों और स्तंभों में फ़ील्ड जोड़ें
pivotTable.addFieldToArea("Product", PivotFieldType.ROW);
pivotTable.addFieldToArea("Region", PivotFieldType.COLUMN);

// मान जोड़ें और एकत्रीकरण लागू करें
pivotTable.addFieldToArea("Sales", PivotFieldType.DATA);
pivotTable.getDataFields().get(0).setFunction(PivotFieldFunction.SUM);

// संशोधित एक्सेल फ़ाइल को सहेजें
workbook.save("output.xlsx");
```

## चरण 2: डेटा समूहित करें

Java के लिए Aspose.Cells में, आप पिवट तालिका के भीतर डेटा को समूहीकृत कर सकते हैं `PivotField` वर्ग। पिवट तालिका में फ़ील्ड को समूहीकृत करने का एक उदाहरण यहां दिया गया है:

```java
// पिवट तालिका में "उत्पाद" फ़ील्ड तक पहुँचें
PivotField productField = pivotTable.getPivotFields().get("Product");

// "उत्पाद" फ़ील्ड को किसी विशिष्ट मानदंड के अनुसार समूहीकृत करें, जैसे, आरंभिक अक्षर के अनुसार
productField.setIsAutoSubtotals(false);
productField.setBaseField("Product");
productField.setAutoSort(true);
productField.setAutoShow(true);

// संशोधित Excel फ़ाइल को समूहीकृत डेटा के साथ सहेजें
workbook.save("output_grouped.xlsx");
```

## चरण 3: समूहीकरण को अनुकूलित करें

आप समूहीकरण सेटिंग को और भी अनुकूलित कर सकते हैं, जैसे कि दिनांक-आधारित समूहीकरण अंतराल या कस्टम समूहीकरण नियम निर्दिष्ट करना। यहाँ दिनांक-आधारित समूहीकरण को अनुकूलित करने का एक उदाहरण दिया गया है:

```java
// पिवट तालिका में "दिनांक" फ़ील्ड तक पहुँचें (मान लें कि यह एक दिनांक फ़ील्ड है)
PivotField dateField = pivotTable.getPivotFields().get("Date");

// महीनों के अनुसार तिथियों को समूहीकृत करें
dateField.setIsAutoSubtotals(false);
dateField.setIsDateGroup(true);
dateField.setDateGroupingType(PivotFieldDateGroupingType.MONTHS);

// संशोधित Excel फ़ाइल को कस्टम दिनांक समूहीकरण के साथ सहेजें
workbook.save("output_custom_grouping.xlsx");
```

## निष्कर्ष

एक्सेल में डेटा का विश्लेषण और सारांश बनाने के लिए पिवट टेबल में डेटा को समूहीकृत करना एक मूल्यवान तकनीक है, और जावा के लिए Aspose.Cells इस प्रक्रिया को स्वचालित करना आसान बनाता है। प्रदान किए गए स्रोत कोड उदाहरणों के साथ, आप पिवट टेबल बना सकते हैं, समूहीकरण को अनुकूलित कर सकते हैं, और अपने डेटा से कुशलतापूर्वक जानकारी प्राप्त कर सकते हैं।

## पूछे जाने वाले प्रश्न

### 1. एक्सेल में पिवट टेबल का उद्देश्य क्या है?

एक्सेल में पिवट टेबल का उपयोग बड़े डेटासेट को सारांशित करने और उनका विश्लेषण करने के लिए किया जाता है। वे आपको अपने डेटा के कस्टम दृश्य बनाने की अनुमति देते हैं, जिससे पैटर्न और रुझानों की पहचान करना आसान हो जाता है।

### 2. मैं पिवट टेबल में डेटा के समूहीकरण को कैसे अनुकूलित कर सकता हूं?

आप पिवट तालिका में डेटा के समूहीकरण को अनुकूलित कर सकते हैं `PivotField` जावा के लिए Aspose.Cells में क्लास। यह आपको समूहीकरण मानदंड निर्दिष्ट करने की अनुमति देता है, जैसे दिनांक-आधारित अंतराल या कस्टम नियम।

### 3. क्या मैं Java के लिए Aspose.Cells का उपयोग करके पिवट टेबल के निर्माण को स्वचालित कर सकता हूँ?

हां, आप जावा के लिए Aspose.Cells का उपयोग करके एक्सेल में पिवट टेबल के निर्माण को स्वचालित कर सकते हैं, जैसा कि प्रदान किए गए स्रोत कोड उदाहरणों में प्रदर्शित किया गया है।
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}