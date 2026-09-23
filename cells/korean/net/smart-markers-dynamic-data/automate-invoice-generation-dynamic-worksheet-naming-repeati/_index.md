---
category: general
date: 2026-02-14
description: 'SmartMarker로 청구서 생성을 자동화하세요: 워크시트를 복제하고 동적으로 이름을 지정하는 방법을 배우며, 몇 분 안에
  동적 워크시트 명명 기술을 마스터하세요.'
draft: false
keywords:
- automate invoice generation
- how to name worksheets
- how to repeat worksheet
- dynamic worksheet naming
language: ko
og_description: SmartMarker로 청구서 생성을 자동화하세요. 이 가이드는 워크시트를 반복하고, 동적으로 이름을 지정하며, 동적
  워크시트 명명법을 마스터하는 방법을 보여줍니다.
og_title: 청구서 자동 생성 – 동적 워크시트 명명 및 반복
tags:
- C#
- SmartMarker
- Excel Automation
title: 인보이스 자동 생성 – C#에서 동적 워크시트 명명 및 반복
url: /ko/net/smart-markers-dynamic-data/automate-invoice-generation-dynamic-worksheet-naming-repeati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 자동 인보이스 생성 – 동적 워크시트 명명 및 반복 in C#

각 주문마다 시트를 수동으로 복사하지 않고 **자동 인보이스 생성**을 할 수 있는 방법이 궁금하셨나요? 당신만 그런 것이 아닙니다. 많은 개발자들이 인보이스당 별도의 워크시트가 필요하면서 동시에 시트 이름에 주문 번호를 반영하고 싶을 때 난관에 부딪힙니다. 이 튜토리얼에서는 SmartMarker의 `SmartMarkerProcessor`를 사용해 이 문제를 해결하고 **워크시트 명명**을 동적으로 수행하는 방법과 **워크시트를 반복**하는 방법을 다룹니다. 최종적으로 각 인보이스가 자체적으로 깔끔하게 이름이 지정된 탭에 배치되는 실행 가능한 C# 샘플을 얻을 수 있습니다.

우리는 데이터 소스에서 주문을 가져오는 단계부터 `SmartMarkerOptions`를 설정해 동적 워크시트 명명을 구현하는 단계까지 모든 과정을 차근차근 살펴볼 것입니다. 외부 문서는 필요 없으며, 여기서 바로 필요한 모든 정보를 제공합니다. C#에 대한 기본 지식과 Aspose.Cells 라이브러리(또는 SmartMarker와 호환되는 엔진)만 있으면 충분합니다.

---

## 만들게 될 것

- 주문 객체 컬렉션을 가져옵니다.
- SmartMarker를 구성하여 각 주문에 대해 **워크시트를 반복**합니다.
- `{OrderId}` 자리표시자를 사용하여 **동적 워크시트 명명**을 적용합니다.
- 각 탭이 `Invoice_12345`, `Invoice_67890` 등으로 이름이 지정된 Excel 파일을 생성합니다.
- 워크북을 열어 출력물을 확인합니다.

---

## 사전 요구 사항

- .NET 6.0 이상 (코드는 .NET 5+에서도 컴파일됩니다).
- Aspose.Cells for .NET (또는 SmartMarker를 구현하는 라이브러리). NuGet을 통해 설치합니다:

```bash
dotnet add package Aspose.Cells
```

- 기본 `Order` 클래스 (자신의 DTO로 교체 가능).

---

## 단계 1: 프로젝트 및 모델 설정

먼저 새 콘솔 앱을 만들고 주문을 나타내는 데이터 모델을 정의합니다.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    // Simple POCO representing an order – replace fields as needed
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }
    }

    class Program
    {
        static void Main()
        {
            // Retrieve orders (in real life this could be a DB call)
            var orders = GetOrders();

            // The rest of the tutorial continues here...
        }

        // Mock method – in production pull from EF Core, Dapper, etc.
        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

> **팁:** 데모용 모델은 가볍게 유지하세요; 나중에 라인 아이템, 세금 상세 정보 등으로 언제든지 확장할 수 있습니다.

---

## 단계 2: Excel 템플릿 준비

SmartMarker는 템플릿 워크북을 기반으로 동작합니다. `InvoiceTemplate.xlsx`라는 파일을 만들고, 워크시트 이름을 `InvoiceTemplate`으로 지정합니다. 셀 **A1**에 다음과 같은 SmartMarker 자리표시자를 넣습니다:

```
{{OrderId}} – {{Customer}} – {{Date}} – ${{Total}}
```

셀 서식은 원하는 대로 지정할 수 있습니다—굵은 헤더, 통화 서식 등. 파일을 프로젝트 루트 폴더에 저장하세요.

> **왜 템플릿인가?** 레이아웃을 코드와 분리함으로써 디자이너가 로직을 건드리지 않고도 외관을 조정할 수 있습니다.

---

## 단계 3: SmartMarker 옵션 구성 – 워크시트 반복 및 명명

이제 SmartMarker에게 템플릿 워크시트를 각 주문마다 *반복*하고, 복사본마다 주문 ID를 포함한 이름을 부여하도록 지시합니다. 이것이 **동적 워크시트 명명**의 핵심입니다.

```csharp
// Inside Main() after retrieving orders
// Load the template workbook
Workbook wb = new Workbook("InvoiceTemplate.xlsx");

// Set up SmartMarker options
var smartMarkerOptions = new SmartMarkerOptions
{
    // Instructs SmartMarker to create a new worksheet per data item
    RepeatWorksheet = true,

    // Naming pattern – {OrderId} will be replaced with the actual value
    RepeatWorksheetName = "Invoice_{OrderId}"
};

// Run the processor
wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

// Save the result
string outputPath = "GeneratedInvoices.xlsx";
wb.Save(outputPath);

Console.WriteLine($"✅ Invoices generated: {outputPath}");
```

### 작동 방식

- **`RepeatWorksheet = true`** 은 엔진에게 `orders` 컬렉션의 각 요소에 대해 원본 시트를 복제하도록 지시합니다. 이는 **워크시트를 반복**하는 요구 사항을 충족합니다.
- **`RepeatWorksheetName = "Invoice_{OrderId}"`** 은 템플릿 문자열로, `{OrderId}` 자리표시자를 SmartMarker가 현재 주문의 ID로 교체합니다. 이는 **워크시트 명명 방법**과 **동적 워크시트 명명**에 대한 답변입니다.
- 프로세서는 각 주문의 필드(`{{OrderId}}`, `{{Customer}}` 등)를 복제된 시트에 병합하여 완전한 인보이스를 생성합니다.

---

## 단계 4: 애플리케이션 실행 및 출력 확인

콘솔 앱을 컴파일하고 실행합니다:

```bash
dotnet run
```

콘솔에 성공 메시지가 표시될 것입니다. `GeneratedInvoices.xlsx`를 열면 세 개의 탭을 확인할 수 있습니다:

- **Invoice_1001**
- **Invoice_1002**
- **Invoice_1003**

각 시트에는 자리표시자가 주문 데이터로 교체된 내용이 들어 있습니다. 템플릿에서 설계한 레이아웃이 그대로 유지되어 **자동 인보이스 생성**이 엔드‑투‑엔드로 작동함을 입증합니다.

### 예상 스크린샷 (SEO용 alt 텍스트)

![자동 인보이스 생성 예시 – 동적으로 이름이 지정된 세 개의 워크시트 표시](/images/invoice-automation.png)

> *이미지 alt 텍스트에는 주요 키워드가 포함되어 SEO를 만족합니다.*

---

## 단계 5: 엣지 케이스 및 일반 변형

### OrderId에 불법 문자(Illegal characters)가 포함된 경우는?

Excel 시트 이름에는 `\ / ? * [ ] :` 문자를 사용할 수 없습니다. ID에 이러한 문자가 포함될 가능성이 있다면 정제하세요:

```csharp
RepeatWorksheetName = "Invoice_{SanitizedOrderId}"
```

`Order`에 계산된 속성을 추가합니다:

```csharp
public string SanitizedOrderId => OrderId.ToString().Replace("/", "-").Replace("\\", "-");
```

### 원본 템플릿 시트를 유지해야 하는 경우

`smartMarkerOptions.RemoveTemplate = false;` (기본값은 `true`) 로 설정합니다. 이렇게 하면 원본 `InvoiceTemplate`이 참조용으로 남아 있습니다.

### 고객별로 인보이스를 그룹화하고 싶나요?

**반복 그룹**을 중첩할 수 있습니다. 먼저 고객별로 반복하고, 각 고객 워크시트 안에서 주문별로 반복합니다. 구문이 약간 복잡해지지만 원리는 동일합니다—`RepeatWorksheet`와 계층 구조를 반영하는 명명 패턴을 사용합니다.

---

## 전체 작업 예제 (모든 코드를 한 곳에)

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }

        // Helper for safe sheet names
        public string SanitizedOrderId => OrderId.ToString();
    }

    class Program
    {
        static void Main()
        {
            var orders = GetOrders();

            // Load template
            Workbook wb = new Workbook("InvoiceTemplate.xlsx");

            // Configure SmartMarker for repeating and naming worksheets
            var smartMarkerOptions = new SmartMarkerOptions
            {
                RepeatWorksheet = true,
                RepeatWorksheetName = "Invoice_{OrderId}" // dynamic worksheet naming
                // RemoveTemplate = true; // default behavior
            };

            // Process the data
            wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

            // Save the final workbook
            string outputPath = "GeneratedInvoices.xlsx";
            wb.Save(outputPath);

            Console.WriteLine($"✅ Invoices generated: {outputPath}");
        }

        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

이 코드를 `Program.cs`에 복사·붙여넣고, `InvoiceTemplate.xlsx`를 같은 폴더에 두면 바로 실행할 수 있습니다.

---

## 자주 묻는 질문

**Q: 이 접근 방식이 대규모 데이터 세트(수천 개의 인보이스)에도 적용되나요?**  
A: 네. SmartMarker는 데이터를 효율적으로 스트리밍하지만 메모리 사용량을 주시하세요. 한계에 도달하면 배치 처리로 나누어 각각 별도 워크북에 기록하는 방식을 고려하십시오.

**Q: 모든 인보이스에 로고를 자동으로 추가할 수 있나요?**  
A: 물론 가능합니다. 템플릿 시트에 로고 이미지를 배치하면 시트가 복제될 때마다 로고가 자동으로 각 인보이스에 나타납니다.

**Q: 워크시트를 보호해야 하면 어떻게 하나요?**  
A: 처리 후 `wb.Worksheets`를 순회하면서 `ws.Protect(Password, ProtectionType.All)`을 호출하면 됩니다.

---

## 결론

우리는 SmartMarker의 워크시트 반복 기능과 스마트한 명명 패턴을 활용해 **자동 인보이스 생성**을 구현했습니다. 이번 튜토리얼에서는 **워크시트 명명 방법**을 다루고, 각 주문에 대해 **워크시트를 반복**하는 방법을 시연했으며, 워크북을 깔끔하고 검색 가능하게 유지하는 **동적 워크시트 명명**을 소개했습니다.

데이터 추출, 템플릿 설정, `SmartMarkerOptions` 구성, 엣지 케이스 처리까지 전체 과정을 통해 완전한 실행 가능한 솔루션을 얻었습니다. 이제 라인 아이템 테이블을 추가하거나 조건부 서식을 적용하고, 동일 데이터를 PDF로 내보내는 등 완전 자동 청구 파이프라인을 구축해 보세요.

다음 단계로는 “Aspose.Cells를 활용한 대량 Excel 내보내기”, “워크시트 PDF 변환”, “C#에서 직접 생성된 인보이스 이메일 전송” 등 관련 주제를 탐색해 보세요. 가능성은 무한합니다—행복한 코딩 되세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}