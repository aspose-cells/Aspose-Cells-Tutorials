---
category: general
date: 2026-03-18
description: C#로 주석이 포함된 Excel 워크북을 만들고 워크북을 XLSX 형식으로 저장합니다. 주석 추가 방법, Excel 주석 생성
  방법, 그리고 Excel 파일 자동화에 대해 배워보세요.
draft: false
keywords:
- create excel workbook c#
- add excel comment
- save workbook as xlsx
- how to add comment
- generate excel comment
language: ko
og_description: C#로 주석이 포함된 Excel 워크북을 만들고 워크북을 XLSX 형식으로 저장하세요. 이 단계별 가이드를 따라 Excel
  주석을 추가하고 프로그래밍으로 Excel 주석을 생성하세요.
og_title: C#로 Excel 워크북 만들기 – 주석 추가 및 XLSX로 저장
tags:
- C#
- Excel Automation
- Aspose.Cells
title: C#로 Excel 워크북 만들기 – 주석 추가 및 XLSX로 저장
url: /ko/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel 워크북 C# 만들기 – 주석 추가 및 XLSX로 저장

Ever needed to **create Excel workbook C#** and stick a note inside a cell, but weren’t sure where to start? You’re not the only one—developers constantly ask *how to add comment* without opening Excel manually.

이 튜토리얼에서는 **excel 주석 추가 방법**, Smart Marker를 사용한 **excel 주석 생성**, 그리고 **워크북을 xlsx로 저장**을 한 번에 보여주는 완전하고 바로 실행 가능한 솔루션을 제공합니다. 남는 참조 없이, Visual Studio에 복사해 붙여넣기만 하면 바로 동작하는 순수 코드입니다.

## 배울 내용

- C#를 사용하여 처음부터 Excel 워크북을 초기화합니다.
- Excel 주석이 되는 Smart Marker를 삽입합니다.
- JSON 데이터를 제공하여 마커를 실제 주석으로 변환합니다.
- 파일을 `.xlsx` 워크북으로 저장합니다.
- Smart Marker 없이 주석을 추가하는 선택적 방법.

### 전제 조건

- .NET 6 (또는 .NET Framework 4.7+).  
- **Aspose.Cells for .NET** NuGet 패키지 – Smart Marker 기능을 지원하는 라이브러리.  
- 기본 C# 개발 환경 (Visual Studio, VS Code, Rider…).

> **Pro tip:** 예산이 한정돼 있다면, Aspose는 개발 및 테스트에 완전히 기능하는 무료 체험판을 제공합니다.

---

## Step 1: Excel 워크북 C# 만들기 – 프로젝트 설정

먼저, 새로운 콘솔 앱을 만들고 Aspose.Cells 패키지를 가져옵니다.

```bash
dotnet new console -n ExcelCommentDemo
cd ExcelCommentDemo
dotnet add package Aspose.Cells
```

`Program.cs`를 엽니다. 가장 먼저 하는 일은 **새 워크북을 생성**하는 것입니다.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1️⃣: Create a fresh workbook and grab the first worksheet
        Workbook workbook = new Workbook();               // creates an empty Excel file in memory
        Worksheet ws = workbook.Worksheets[0];            // default sheet is named "Sheet1"
```

왜 새 워크북부터 시작할까요? 깨끗한 상태를 보장하고 숨겨진 서식을 제거하며 처음부터 모든 것을 제어할 수 있어 자동 보고서 생성에 최적입니다.

---

## Step 2: 주석 추가 방법 – Smart Marker 사용

Smart Marker는 Aspose가 런타임에 데이터를 대체하는 플레이스홀더입니다. **`${Comment:UserComment}`** 패턴을 따르는 마커를 삽입하면 엔진이 해당 플레이스홀더를 실제 주석으로 변환하도록 지시합니다.

```csharp
        // Step 2️⃣: Place a Smart Marker in B2 that will become a comment
        ws.Cells["B2"].PutValue("${Comment:UserComment}");
```

`Comment:` 접두사를 보셨나요? 이는 프로세서가 값을 일반 텍스트가 아니라 주석으로 처리하도록 하는 신호입니다. *“다른 셀 유형에서도 작동하나요?”* 라는 궁금증이 있다면—예, 병합된 영역을 포함한 모든 셀에 동일한 마커를 적용할 수 있습니다.

---

## Step 3: JSON 데이터 준비 – 주석 내용

다음은 데이터 소스입니다. 여기서는 간단한 JSON 문자열을 사용하지만 DataTable, List, 혹은 사용자 정의 객체를 제공할 수도 있습니다.

```csharp
        // Step 3️⃣: Define JSON that supplies the comment text
        string json = "{ \"UserComment\": \"Reviewed by QA\" }";
```

`"Reviewed by QA"`를 원하는 동적 값으로 교체해도 됩니다—예를 들어 타임스탬프, 사용자 이름, 혹은 이슈 트래커 링크 등. 키 이름(`UserComment`)은 마커 식별자와 일치해야 합니다.

---

## Step 4: Excel 주석 생성 – Smart Marker 처리

이제 JSON을 Smart Marker 프로세서에 전달합니다. 바로 이 순간에 **excel 주석 생성**이 실제로 이루어집니다.

```csharp
        // Step 4️⃣: Process the marker and turn it into a real comment
        ws.SmartMarkerProcessor.Process(json);
```

백그라운드에서 Aspose는 JSON을 파싱하고 `UserComment` 필드를 찾아 **B2** 셀에 주석으로 삽입합니다. 셀에 표시되는 값은 원래 플레이스홀더 텍스트 그대로이지만, 마우스를 올리면 Excel에서 주석을 표시합니다.

---

## Step 5: 워크북을 XLSX로 저장 – 결과 영구 저장

마지막으로 워크북을 디스크에 저장합니다. 이는 **워크북을 xlsx로 저장** 요구사항을 충족합니다.

```csharp
        // Step 5️⃣: Save the file – you’ll see the comment in B2 when you open it
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

`output.xlsx`를 Excel에서 열고 **B2** 셀에 마우스를 올리면 *“Reviewed by QA”* 주석이 나타납니다. 이제 끝—수동 단계도 없고, COM 인터롭도 없으며, 순수 C#만 사용합니다.

---

## 대안: Smart Marker 없이 주석 추가 방법

보다 직접적인 방법을 원한다면, 직접 주석 객체를 생성할 수 있습니다:

```csharp
// Direct comment creation (no Smart Marker)
Comment comment = ws.Comments[ws.Comments.Add("B2")];
comment.Note = "Directly added comment";
```

이 방법은 주석 텍스트가 컴파일 시점에 이미 알려져 있거나, 작성자, 너비, 높이와 같은 추가 속성을 설정해야 할 때 유용합니다. 하지만 Smart Marker를 통한 **excel 주석 생성**은 많은 행과 열을 가진 데이터 기반 시나리오에서 빛을 발합니다.

---

## 전문가 팁 및 흔히 겪는 문제

| 상황 | 주의할 점 | 권장 해결책 |
|-----------|-------------------|-----------------|
| 대규모 데이터셋 (10k+ 행) | Smart Marker 처리 시 메모리 사용량이 많을 수 있음 | 데이터를 스트리밍하는 `SmartMarkerProcessor.Process` 오버로드를 사용하거나 워크북을 여러 조각으로 나눕니다 |
| 사용자 지정 작성자 이름 필요 | 기본 작성자가 비어 있음 | 주석을 만든 후 `comment.Author = "MyApp";` |
| 기본적으로 주석을 보이게 하려면 | Excel은 주석을 마우스를 올릴 때까지 숨김 | `comment.Visible = true;` 설정 |
| 오래된 Excel 버전과 작업 | `.xlsx`가 지원되지 않을 수 있음 | 대신 `SaveFormat.Xls`로 저장하지만, 일부 주석 기능은 다를 수 있습니다 |

---

## 예상 출력

- **워크북 파일:** 프로젝트의 bin 폴더에 위치한 `output.xlsx`.  
- **셀 B2:** 플레이스홀더 텍스트 `${Comment:UserComment}`가 표시됩니다 (셀의 글꼴 색을 흰색으로 설정하면 숨길 수 있습니다).  
- **B2에 연결된 주석:** 마우스를 올리면 “Reviewed by QA”가 표시됩니다.

![셀 B2에 주석이 표시된 Excel 워크북 C# 예제](https://example.com/placeholder-image.png "셀 B2에 주석이 표시된 Excel 워크북 C# 예제")

*이미지 대체 텍스트:* **셀 B2에 주석이 표시된 Excel 워크북 C# 예제**

---

## 요약 – 달성한 내용

우리는 **Excel 워크북 C#**을 만들고, **Smart Marker**를 삽입해 **excel 주석**으로 변환했으며, JSON을 제공해 **excel 주석 생성**을 수행하고, 마지막으로 **워크북을 xlsx로 저장**했습니다. 전체 흐름은 몇십 줄의 깔끔하고 독립적인 C# 코드에 담겨 있습니다.

---

## 다음 단계? 솔루션 확장

- **배치 주석 생성:** DataTable을 순회하면서 각 행에 Smart Marker를 적용해 행별 메모를 추가합니다.  
- **주석 스타일링:** `Comment.RichText` 컬렉션을 사용해 글꼴 크기, 색상, 혹은 리치 텍스트를 조정합니다.  
- **PDF로 내보내기:** `workbook.Save("output.pdf", SaveFormat.Pdf);`를 사용해 주석이 포함된 보고서를 공유합니다.

다른 환경에서 **excel 주석 추가**를 프로그래밍적으로 구현하는 것이 궁금하다면—예를 들어 OpenXML SDK나 EPPlus를 사용하는 경우—이들 라이브러리 역시 주석 생성을 지원하지만 API가 다릅니다.

---

### 마무리 생각

C#에서 Excel 파일에 주석을 추가하는 것이 번거로운 작업일 필요는 없습니다. Aspose.Cells의 Smart Marker 엔진을 활용하면 최소한의 보일러플레이트로 **excel 주석 추가**, **excel 주석 생성**, 그리고 **워크북을 xlsx로 저장**을 간결하고 데이터 기반 방식으로 수행할 수 있습니다.

한 번 시도해 보고, JSON을 조정해 보세요. 원시 데이터를 깔끔하고 주석이 풍부한 스프레드시트로 빠르게 변환하는 모습을 확인할 수 있을 것입니다. 즐거운 코딩 되세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}