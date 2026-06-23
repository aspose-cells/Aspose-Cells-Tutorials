---
category: general
date: 2026-03-25
description: 스마트 마커를 사용해 템플릿을 작성하고, 행을 반복하고, 데이터를 바인딩하며, 보고서를 생성하고 템플릿을 손쉽게 만드는 방법.
draft: false
keywords:
- how to write template
- how to repeat rows
- how to bind data
- how to generate report
- how to create template
language: ko
og_description: Smart Markers를 사용하여 템플릿을 작성하는 방법. 행을 반복하고, 데이터를 바인딩하며, 보고서를 생성하고 C#에서
  템플릿을 만드는 방법을 알아보세요.
og_title: 스마트 마커를 사용한 템플릿 작성 방법 – 전체 가이드
tags:
- Aspose.Cells
- C#
- SmartMarkers
title: 스마트 마커를 사용한 템플릿 작성 방법 – 단계별 가이드
url: /ko/net/smart-markers-dynamic-data/how-to-write-template-with-smart-markers-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Smart Markers 로 템플릿 작성 방법 – 전체 튜토리얼  

데이터에 따라 자동으로 확장되는 **템플릿 작성 방법**을 궁금해 본 적 있나요? 당신만 그런 것이 아닙니다—동적 Excel 보고서가 필요하지만 어떤 API 기능을 사용해야 할지 모르는 개발자들이 많습니다. 좋은 소식은? Aspose.Cells Smart Markers를 사용하면 단일 셀 템플릿을 만들고, 계층형 데이터를 바인딩하며, 라이브러리가 행을 자동으로 반복하도록 할 수 있습니다. 이 가이드에서는 **행 반복 방법**, **데이터 바인딩 방법**, 그리고 워크시트를 수동으로 반복하지 않고 **보고서 생성 방법**까지 다룹니다.

이 튜토리얼을 마치면 마스터‑디테일 시나리오를 위한 **템플릿 생성 방법**을 보여주는 완전하고 실행 가능한 예제를 얻게 되며, 엣지 케이스와 성능 팁도 포함됩니다. 외부 문서는 필요 없습니다—필요한 모든 것이 여기 있습니다.

---

## 만들게 될 것

주문(마스터)과 해당 라인 아이템(디테일)을 나열하는 Excel 워크북을 생성합니다. 템플릿은 **A1** 셀에 위치하며, Smart Markers가 이를 깔끔하게 포맷된 테이블로 확장합니다. 최종 시트는 다음과 같습니다:

```
Order1
   A
   B
Order2
   C
```

이는 전형적인 “보고서 생성 방법” 시나리오이며, 코드는 .NET 6+ 및 Aspose.Cells 23.x(이후 버전)에서 동작합니다.

---

## 사전 요구 사항

- .NET 6 SDK (또는 최신 .NET 버전)  
- Visual Studio 2022 또는 VS Code  
- Aspose.Cells for .NET (NuGet 통해 설치: `Install-Package Aspose.Cells`)  

위 항목들을 갖추었다면 바로 시작할 수 있습니다.

---

## Step 1: 프로젝트 설정 및 Aspose.Cells 추가  

```csharp
// Create a new console app (run this in a terminal)
// dotnet new console -n SmartMarkerDemo
// cd SmartMarkerDemo
// dotnet add package Aspose.Cells
```

```csharp
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new workbook with a single worksheet
            var workbook = new Workbook();
            var worksheet = workbook.Worksheets[0];
```

*왜 중요한가*: 새 `Workbook`을 시작하면 깨끗한 캔버스를 보장합니다. `Worksheet` 객체는 템플릿을 배치할 위치입니다.

---

## Step 2: Smart Marker 템플릿 작성  

템플릿은 주문 제목에 `${Master.Name}`을, 각 라인 아이템을 반복하기 위해 `${Detail:Repeat}`을 사용합니다.

```csharp
            // Step 2: Define a Smart Marker template that repeats detail rows for each master record
            string smartMarkerTemplate = @"${Master.Name}
${Detail:Repeat}
   ${Detail.Item}
${/Detail}";
            
            // Write the template into cell A1
            worksheet.Cells["A1"].PutValue(smartMarkerTemplate);
```

> **Pro tip**: 템플릿을 단일 셀에 유지하세요; Smart Markers가 자동으로 행을 확장합니다.  

*이 문제 해결 방법*: 반복 블록을 셀에 직접 삽입하면 수동으로 행을 삽입할 필요가 없습니다—Aspose가 이를 처리합니다.

---

## Step 3: 템플릿에 맞는 계층형 데이터 구축  

데이터는 템플릿 구조와 일치해야 합니다: `Master` 컬렉션이며, 각 `Master`는 `Detail` 배열을 포함합니다.

```csharp
            // Step 3: Create hierarchical data matching the template structure
            var orderData = new
            {
                Master = new[]
                {
                    new
                    {
                        Name = "Order1",
                        Detail = new[]
                        {
                            new { Item = "A" },
                            new { Item = "B" }
                        }
                    },
                    new
                    {
                        Name = "Order2",
                        Detail = new[]
                        {
                            new { Item = "C" }
                        }
                    }
                }
            };
```

*왜 이렇게 데이터를 바인딩하는가*: Smart Markers는 리플렉션 방식 바인딩을 사용하므로 속성 이름이 플레이스홀더와 정확히 일치해야 합니다. 이것이 동적 보고서를 위한 **데이터 바인딩 방법**의 핵심입니다.

---

## Step 4: 템플릿 처리 – Smart Markers에게 작업을 맡기기  

```csharp
            // Step 4: Process the Smart Markers – the template will be expanded using the data above
            worksheet.SmartMarkerProcessor.Process(orderData);
```

처리 후 워크시트에는 확장된 행이 포함됩니다. 루프도, 수동 셀 쓰기도 없습니다.

---

## Step 5: 워크북 저장  

```csharp
            // Save the result to an XLSX file
            workbook.Save("SmartMarkerReport.xlsx", SaveFormat.Xlsx);
            System.Console.WriteLine("Report generated: SmartMarkerReport.xlsx");
        }
    }
}
```

생성된 파일을 열면 앞서 설명한 대로 마스터‑디테일 레이아웃이 정확히 표시됩니다. 이것이 **보고서 생성 방법**이며, 단 한 줄의 처리 코드로 가능합니다.

---

## 시각적 개요  

![Smart Markers 로 생성된 Excel 보고서 – 템플릿 작성 방법](/images/smart-marker-report.png "템플릿 작성 방법")

*Alt text*: "템플릿 작성 방법" – 각 주문에 대해 반복된 행을 보여주는 최종 Excel 파일의 스크린샷.

---

## 깊이 파보기: Smart Markers 가 왜 게임 체인저인가  

### 루프 없이 행을 반복하는 방법  

전통적인 Excel 자동화는 마지막 행을 계산하고, 새 행을 삽입하며, 스타일을 복사해야 하며—모두 오류가 발생하기 쉬운 작업입니다. Smart Markers는 선언형 `${Detail:Repeat}` 블록으로 이를 대체합니다. 엔진은 블록을 파싱하고, 컬렉션의 각 요소마다 행을 복제하고 값을 삽입합니다. 이 접근 방식이 **행을 효율적으로 반복하는 방법**입니다.

### 복잡한 객체 바인딩  

중첩 객체, 컬렉션, 혹은 DataTable도 바인딩할 수 있습니다. 속성 이름이 일치하기만 하면 프로세서는 객체 그래프를 탐색합니다. 이것이 **데이터 바인딩 방법**의 핵심입니다: 프로세서에 일반 CLR 객체(또는 익명 타입)를 제공하면 자동으로 매핑됩니다.

### 다양한 포맷 생성  

예제는 XLSX로 저장하지만, `SaveFormat.Pdf` 또는 `SaveFormat.Csv` 로 한 줄만 바꾸면 됩니다. 이는 템플릿을 수정하지 않고도 여러 포맷으로 **보고서 생성 방법**을 빠르게 구현하는 방법입니다.

### 템플릿 재사용  

다른 워크시트에 대한 **템플릿 생성 방법**이 필요하면 셀 내용을 다른 시트에 복사하거나 문자열 리소스로 저장하면 됩니다. 동일한 프로세서 호출이 어디서든 작동하므로 코드가 DRY하고 유지보수가 용이합니다.

---

## 일반 질문 및 엣지 케이스  

| Question | Answer |
|----------|--------|
| *마스터에 상세 행이 없으면 어떻게 되나요?* | `${Detail:Repeat}` 블록이 건너뛰어져 마스터 이름만 남습니다. 빈 행은 생성되지 않습니다. |
| *반복된 행에 스타일을 적용할 수 있나요?* | 예—처리 전에 템플릿 행에 서식(폰트, 테두리 등)을 적용하면 해당 스타일이 생성된 각 행에 복사됩니다. |
| *Workbook을 해제해야 하나요?* | `Workbook`은 `IDisposable`을 구현합니다. 프로덕션 코드에서는 `using` 블록으로 감싸야 하지만, 짧은 콘솔 데모에서는 선택 사항입니다. |
| *데이터 크기는 얼마나 될 수 있나요?* | Smart Markers는 메모리 효율적이지만, 수십만 건과 같은 매우 큰 컬렉션은 페이지 처리나 스트리밍이 필요할 수 있습니다. |
| *객체 대신 JSON 파일을 사용할 수 있나요?* | 물론입니다—JSON을 템플릿에 맞는 POCO로 역직렬화한 뒤 `Process`에 전달하면 됩니다. |

---

## 전체 작업 예제 (복사‑붙여넣기 준비)

```csharp
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize workbook
            var workbook = new Workbook();
            var worksheet = workbook.Worksheets[0];

            // Define template
            string smartMarkerTemplate = @"${Master.Name}
${Detail:Repeat}
   ${Detail.Item}
${/Detail}";

            worksheet.Cells["A1"].PutValue(smartMarkerTemplate);

            // Prepare data
            var orderData = new
            {
                Master = new[]
                {
                    new
                    {
                        Name = "Order1",
                        Detail = new[]
                        {
                            new { Item = "A" },
                            new { Item = "B" }
                        }
                    },
                    new
                    {
                        Name = "Order2",
                        Detail = new[]
                        {
                            new { Item = "C" }
                        }
                    }
                }
            };

            // Process template
            worksheet.SmartMarkerProcessor.Process(orderData);

            // Save file
            workbook.Save("SmartMarkerReport.xlsx", SaveFormat.Xlsx);
            System.Console.WriteLine("Report generated: SmartMarkerReport.xlsx");
        }
    }
}
```

프로그램을 실행(`dotnet run`)하고 *SmartMarkerReport.xlsx* 파일을 열면 마스터‑디테일 행이 깔끔하게 정렬된 것을 확인할 수 있습니다.

---

## 요약  

우리는 Aspose.Cells Smart Markers를 사용한 **템플릿 작성 방법**을 설명하고, **행 반복 방법**을 시연했으며, 계층형 객체를 이용한 **데이터 바인딩 방법**을 보여주고, XLSX(또는 다른 지원 포맷)로 **보고서 생성 방법**을 예시했습니다. 동일한 패턴을 사용하면 청구서, 재고 목록 또는 상상할 수 있는 모든 마스터‑디테일 레이아웃에 대한 **템플릿 생성 방법**을 적용할 수 있습니다.

---

## 다음 단계  

- **출력 스타일링**: 처리 전에 템플릿 행에 셀 스타일을 적용합니다.  
- **PDF로 내보내기**: 인쇄 가능한 보고서를 위해 `SaveFormat.Xlsx`를 `SaveFormat.Pdf`로 변경합니다.  
- **동적 헤더**: `${Headers}` 플레이스홀더를 추가하여 컬럼 제목을 실시간으로 생성합니다.  
- **다중 시트**: 다중 섹션 보고서를 위해 추가 워크시트에서 프로세스를 반복합니다.  

자유롭게 실험해 보세요—데이터 소스를 교체하고, 더 많은 중첩 레벨을 추가하거나, 수식과 결합할 수 있습니다. Smart Markers의 유연성 덕분에 루프 코딩에 드는 시간을 줄이고 가치 제공에 더 많은 시간을 할애할 수 있습니다.

*코딩 즐겁게! 문제가 발생하면 아래에 댓글을 남기거나 `aspose-cells` 태그와 함께 Stack Overflow에 알려 주세요. 대화를 이어갑시다.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}