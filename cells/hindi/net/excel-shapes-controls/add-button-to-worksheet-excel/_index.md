---
"description": "इस चरण-दर-चरण ट्यूटोरियल के साथ .NET के लिए Aspose.Cells का उपयोग करके Excel वर्कशीट में बटन जोड़ना सीखें। इंटरैक्टिव बटन के साथ Excel स्प्रेडशीट को बेहतर बनाएँ।"
"linktitle": "एक्सेल में वर्कशीट में बटन जोड़ें"
"second_title": "Aspose.Cells .NET एक्सेल प्रोसेसिंग API"
"title": "एक्सेल में वर्कशीट में बटन जोड़ें"
"url": "/hi/net/excel-shapes-controls/add-button-to-worksheet-excel/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# एक्सेल में वर्कशीट में बटन जोड़ें

## परिचय
एक्सेल स्प्रेडशीट बहुमुखी हैं और आमतौर पर डेटा के प्रबंधन के लिए उपयोग की जाती हैं, लेकिन कभी-कभी उन्हें अतिरिक्त अन्तरक्रियाशीलता की आवश्यकता होती है। उपयोगकर्ता अनुभव को बढ़ाने के सर्वोत्तम तरीकों में से एक वर्कशीट में बटन जोड़ना है। ये बटन मैक्रोज़ को ट्रिगर कर सकते हैं या उपयोगकर्ताओं को सहायक लिंक पर नेविगेट कर सकते हैं। यदि आप एक्सेल फ़ाइलों के साथ काम करने वाले .NET डेवलपर हैं, तो Aspose.Cells for .NET बटन जोड़ने सहित एक्सेल वर्कबुक को प्रोग्रामेटिक रूप से हेरफेर करने का एक आसान तरीका प्रदान करता है।
इस ट्यूटोरियल में, हम आपको .NET के लिए Aspose.Cells का उपयोग करके Excel में वर्कशीट में बटन जोड़ने की प्रक्रिया के बारे में बताएँगे। हम हर विवरण को कवर करेंगे, जिसमें पूर्वापेक्षाएँ सेट करने से लेकर चरण-दर-चरण निर्देश शामिल हैं। चलिए शुरू करते हैं!
## आवश्यक शर्तें
इस ट्यूटोरियल का अनुसरण करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित उपकरण और पैकेज स्थापित हैं:
- Aspose.Cells for .NET लाइब्रेरी: आप इसे यहाँ से डाउनलोड कर सकते हैं [यहाँ](https://releases.aspose.com/cells/net/).
- .NET विकास वातावरण: सुनिश्चित करें कि आपके पास Visual Studio जैसा कार्यशील .NET वातावरण स्थापित है।
- C# की बुनियादी समझ: आपको C# प्रोग्रामिंग की मूल बातों से परिचित होना चाहिए।
- लाइसेंस: आपको वैध लाइसेंस की आवश्यकता होगी। यदि आपके पास लाइसेंस नहीं है, तो आप एक प्राप्त कर सकते हैं [मुफ्त परीक्षण](https://releases.aspose.com/) या आवेदन करें [अस्थायी लाइसेंस](https://purchase.aspose.com/temporary-license/).
आइये अब आवश्यक पैकेजों को आयात करने की ओर बढ़ें।
## पैकेज आयात करें
कोडिंग शुरू करने से पहले, आपको अपने .NET प्रोजेक्ट में आवश्यक पैकेज आयात करने होंगे। Aspose.Cells को अपने प्रोजेक्ट में आयात करने में आपकी मदद करने के लिए यहाँ एक सरल कोड स्निपेट दिया गया है:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
अब जबकि हमने आवश्यक पैकेज आयात कर लिए हैं, तो आइए उदाहरण को विस्तृत चरण-दर-चरण मार्गदर्शिका में विभाजित करें।
## चरण 1: कार्यपुस्तिका और कार्यपत्रक सेट करें
इस पहले चरण में, हम एक नई एक्सेल वर्कबुक बनाएंगे और पहली वर्कशीट का संदर्भ प्राप्त करेंगे।
```csharp
// अपने दस्तावेज़ निर्देशिका का पथ निर्धारित करें.
string dataDir = "Your Document Directory";
// यदि निर्देशिका पहले से मौजूद नहीं है तो उसे बनाएं।
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// एक नई कार्यपुस्तिका बनाएँ.
Workbook workbook = new Workbook();
// कार्यपुस्तिका में प्रथम कार्यपत्रक प्राप्त करें।
Worksheet sheet = workbook.Worksheets[0];
```

- कार्यपुस्तिका निर्माण: हम एक नई कार्यपुस्तिका बनाकर शुरू करते हैं `Workbook` ऑब्जेक्ट, जो एक एक्सेल फ़ाइल का प्रतिनिधित्व करता है.
- वर्कशीट संदर्भ: `Worksheets[0]` कमांड कार्यपुस्तिका में पहली वर्कशीट को पुनः प्राप्त करता है, जिसे हम संशोधित करेंगे।
यह चरण एकल वर्कशीट के साथ एक रिक्त एक्सेल फ़ाइल बनाकर आधार तैयार करता है।
## चरण 2: वर्कशीट में एक बटन जोड़ें
इसके बाद, हम वर्कशीट में एक बटन जोड़ेंगे। यहीं पर जादू होता है!
```csharp
// वर्कशीट में एक नया बटन जोड़ें.
Aspose.Cells.Drawing.Button button = sheet.Shapes.AddButton(2, 0, 2, 0, 28, 80);
```

- AddButton विधि: यह विधि वर्कशीट में निर्दिष्ट स्थान पर एक बटन जोड़ती है। पैरामीटर बटन की स्थिति (पंक्ति, स्तंभ, x-ऑफ़सेट, y-ऑफ़सेट) और आकार (ऊंचाई, चौड़ाई) को परिभाषित करते हैं।
- पंक्ति और स्तंभ: बटन को पंक्ति 2 और स्तंभ 0 पर रखा गया है, जिसमें कोई अतिरिक्त ऑफसेट नहीं है।
- आकार: बटन की ऊंचाई 28 और चौड़ाई 80 पर सेट की गई है।
यह चरण सफलतापूर्वक वर्कशीट में एक बटन जोड़ता है, लेकिन अभी हमारा काम पूरा नहीं हुआ है - चलिए इसे कस्टमाइज़ करते हैं।
## चरण 3: बटन गुण सेट करें
अब बटन के पाठ, फ़ॉन्ट और स्थान को निर्धारित करके उसके स्वरूप को अनुकूलित करने का समय है।
```csharp
// बटन का कैप्शन सेट करें.
button.Text = "Aspose";
// प्लेसमेंट प्रकार सेट करें, अर्थात बटन को कक्षों से जोड़ने का तरीका सेट करें।
button.Placement = PlacementType.FreeFloating;
```

- टेक्स्ट: हमने बटन का कैप्शन “Aspose” पर सेट किया है।
- स्थान: हम परिभाषित करते हैं कि बटन को वर्कशीट कक्षों के सापेक्ष किस प्रकार रखा जाए। `FreeFloating` बटन को कोशिकाओं से स्वतंत्र रूप से स्थानांतरित करने की अनुमति देता है।
यह चरण बटन के कैप्शन और स्थान को वैयक्तिकृत करता है।
## चरण 4: बटन का फ़ॉन्ट अनुकूलित करें
आइये फ़ॉन्ट गुणों को अनुकूलित करके बटन को कुछ आकर्षण प्रदान करें।
```csharp
// फ़ॉन्ट नाम सेट करें.
button.Font.Name = "Tahoma";
// कैप्शन स्ट्रिंग को बोल्ड सेट करें.
button.Font.IsBold = true;
// रंग नीला सेट करें.
button.Font.Color = Color.Blue;
```

- फ़ॉन्ट नाम: हमने फ़ॉन्ट को "ताहोमा" में बदल दिया है, जो एक साफ़ और आधुनिक फ़ॉन्ट है।
- बोल्ड: हम जोर देने के लिए बटन के टेक्स्ट को बोल्ड बनाते हैं।
- रंग: फ़ॉन्ट का रंग नीला सेट किया गया है, जिससे बटन का पाठ स्पष्ट दिखाई देता है।
यह कदम बटन के स्वरूप को निखारता है, तथा यह सुनिश्चित करता है कि यह कार्यात्मक और देखने में आकर्षक दोनों है।
## चरण 5: बटन में हाइपरलिंक जोड़ें
आप हाइपरलिंक जोड़कर बटन को और भी अधिक उपयोगी बना सकते हैं।
```csharp
// बटन के लिए हाइपरलिंक सेट करें.
button.AddHyperlink("https://www.aspose.com/");
```

- AddHyperlink: हम इस विधि का उपयोग बटन पर क्लिक करने योग्य हाइपरलिंक जोड़ने के लिए करते हैं। क्लिक करने पर, बटन Aspose वेबसाइट पर नेविगेट करेगा।
यह कदम बटन में अन्तरक्रियाशीलता जोड़ता है, जिससे यह केवल सौंदर्य से परे कार्यात्मक बन जाता है।
## चरण 6: एक्सेल फ़ाइल को सेव करें
एक बार सब कुछ सेट हो जाने पर, अपने परिवर्तनों को सहेजना न भूलें!
```csharp
// फ़ाइल को सहेजता है.
workbook.Save(dataDir + "book1.out.xls");
```

- बचाने की विधि: हम उपयोग करते हैं `Save` संशोधित कार्यपुस्तिका को नई फ़ाइल में लिखने की विधि। फ़ाइल निर्दिष्ट निर्देशिका में सहेजी जाएगी।
बधाई हो! अब आपने एक्सेल वर्कशीट में एक पूरी तरह से अनुकूलित बटन जोड़ लिया है।
## निष्कर्ष
एक्सेल वर्कशीट में बटन जोड़ने से आपकी स्प्रेडशीट की कार्यक्षमता में बहुत वृद्धि हो सकती है, जिससे वे अधिक इंटरैक्टिव और उपयोगकर्ता के अनुकूल बन सकते हैं। .NET के लिए Aspose.Cells के साथ, आप कोड की कुछ पंक्तियों के साथ इसे प्राप्त कर सकते हैं, जैसा कि हमने इस ट्यूटोरियल में दिखाया है।
Aspose.Cells for .NET एक शक्तिशाली लाइब्रेरी है जो एक्सेल हेरफेर के लिए अनंत संभावनाएँ प्रदान करती है। चाहे आप कार्यों को स्वचालित कर रहे हों या अपनी स्प्रेडशीट में नई सुविधाएँ जोड़ रहे हों, यह लाइब्रेरी आपके लिए सबसे अच्छा समाधान है।
यदि आपने अभी तक ऐसा नहीं किया है, [.NET लाइब्रेरी के लिए Aspose.Cells डाउनलोड करें](https://releases.aspose.com/cells/net/) और अपनी एक्सेल फाइलों को बेहतर बनाना शुरू करें।
## अक्सर पूछे जाने वाले प्रश्न
### क्या मैं .NET के लिए Aspose.Cells में बटन के अलावा अन्य आकृतियों का उपयोग कर सकता हूँ?
हां, Aspose.Cells आपको चेकबॉक्स, रेडियो बटन और अन्य सहित विभिन्न आकार जोड़ने की अनुमति देता है।
### क्या मैं Aspose.Cells के माध्यम से जोड़े गए बटन से मैक्रो को ट्रिगर कर सकता हूं?
हां, आप बटन को मैक्रो से लिंक कर सकते हैं, हालांकि आपको एक्सेल में मैक्रो कोड को अलग से संभालना होगा।
### मैं बटन का आकार कोशिकाओं के साथ स्वचालित रूप से कैसे बदल सकता हूँ?
उपयोग `PlacementType.Move` बटन को कोशिकाओं के साथ आकार बदलने की अनुमति देने के लिए गुण।
### क्या एक ही वर्कशीट पर एकाधिक बटन जोड़ना संभव है?
बिल्कुल! आप कॉल करके जितने चाहें उतने बटन जोड़ सकते हैं `AddButton` विधि का कई बार प्रयोग करें।
### क्या मैं बटन के स्वरूप को और अधिक अनुकूलित कर सकता हूँ?
हां, आप पृष्ठभूमि रंग, बॉर्डर शैली आदि सहित कई गुणों को संशोधित कर सकते हैं।

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}