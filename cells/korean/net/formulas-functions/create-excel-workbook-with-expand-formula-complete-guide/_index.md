---
category: general
date: 2026-07-13
description: EXPAND를 사용하여 Excel 워크북을 만들고 셀 수식을 설정합니다. 워크북을 다시 계산하는 방법과 C#에서 Excel
  수식을 동적으로 작성하는 방법을 배웁니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set cell formula
- recalculate workbook
- write excel formula
- how to use expand
language: ko
lastmod: 2026-07-13
og_description: Excel 워크북을 즉시 만들세요. 이 가이드는 셀 수식을 설정하고 워크북을 다시 계산하며, 동적 범위를 위해 EXPAND를
  사용하는 방법을 마스터하는 방법을 보여줍니다.
og_image_alt: Screenshot showing create excel workbook with EXPAND formula in C#
og_title: EXPAND 수식으로 Excel 워크북 만들기 – 단계별
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Create Excel workbook and set cell formula using EXPAND. Learn how
    to recalculate workbook and write Excel formulas dynamically in C#.
  headline: Create Excel Workbook with EXPAND Formula – Complete Guide
  type: TechArticle
tags:
- excel
- csharp
- aspnet
title: EXPAND 수식을 사용한 Excel 워크북 만들기 – 완전 가이드
url: /ko/net/formulas-functions/create-excel-workbook-with-expand-formula-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# EXPAND 함수로 Excel 워크북 만들기 – 완전 가이드

프로그래밍으로 **Excel 워크북을 생성**하고 단일 수식이 전체 테이블을 채우게 하고 싶으셨나요? 여러분만 그런 것이 아닙니다. 많은 보고서나 데이터‑내보내기 시나리오에서 워크북을 사용자의 Downloads 폴더에 넣고, 셀에 수식을 뿌린 뒤 자동으로 계산되게 해야 합니다.  

이 튜토리얼에서는 바로 그 과정을 단계별로 살펴보겠습니다: **Excel 워크북을 생성**하고, 새 `EXPAND` 함수를 사용해 **셀 수식 설정**, 그리고 **워크북을 재계산**하여 결과가 즉시 나타나게 합니다. 마지막으로 **expand**를 활용한 동적 범위 사용법을 익히고, 변화하는 데이터 크기에 맞게 **Excel 수식 작성** 코드를 작성하는 방법을 배웁니다.

---

## 만들게 될 것

- 템플릿이 필요 없는 새 `Workbook` 인스턴스.  
- `A1`에 배치된 배열 수식이 5 행 × 3 열 블록으로 확장되는 예시.  
- `Calculate()` 호출을 통해 엔진이 수식을 즉시 평가하도록 함.  
- 채워진 셀을 빠르게 읽어와 출력 확인.

핵심 Aspose.Cells(또는 유사한 .NET Excel 엔진) 외에 외부 라이브러리는 필요하지 않으며, 순수 C#만 사용합니다.

---

## 사전 준비

- .NET 6+ (또는 .NET Framework 4.7.2+).  
- 동적 배열 함수를 지원하는 Excel 조작 라이브러리 참조(예: **Aspose.Cells**, **GemBox.Spreadsheet**, 또는 최신 Excel 엔진을 갖춘 **ClosedXML**).  
- C# 기본 문법에 익숙함—“Hello World” 정도 작성해 본 경험이면 충분합니다.

---

## 1단계: Excel 워크북 생성 및 워크시트 추가

먼저 워크북 객체를 만들어야 합니다. 이는 나중에 내용을 채울 빈 노트북이라고 생각하면 됩니다.

```csharp
// Step 1: Instantiate a new workbook
var workbook = new Workbook();               // Primary object
var sheet = workbook.Worksheets[0];          // Grab the default sheet
```

> **왜 중요한가:** `Workbook` 클래스는 모든 Excel 작업의 진입점입니다. 이 없이는 수식을 설정하거나 재계산할 수 없습니다. 워크북을 미리 생성해 두면 상황이 확장될 때 여러 시트를 추가하기도 쉽습니다.

---

## 2단계: `EXPAND`로 셀 수식 설정

이제 `A1`에 **셀 수식**을 설정합니다. `EXPAND` 함수는 “spill” 참조(`A1#`)를 받아 지정된 크기로 확장합니다—이번 예에서는 5행 × 3열입니다.

```csharp
// Step 2: Insert an expanding array formula into cell A1
// The source range A1# will be stretched to 5 rows × 3 columns
sheet.Cells[0, 0].Formula = "=EXPAND(A1#,5,3)";
```

> **프로 팁:** Excel 계산 엔진을 그대로 구현한 라이브러리를 사용한다면 `#` spill 연산자는 바로 동작합니다. 그렇지 않은 경우 라이브러리 설정에서 동적 배열 지원을 활성화해야 할 수 있습니다.  
> **소스 셀이 비어 있으면?** `EXPAND`는 `#SPILL!`을 반환합니다. 이를 방지하려면 `IFERROR`로 감싸거나 기본값을 제공하세요. 예: `=IFERROR(EXPAND(A1#,5,3),0)`.

---

## 3단계: 소스 셀 채우기 (선택 사항)

`EXPAND`가 확장할 무언가가 필요합니다. 간단한 배열 상수를 `A1`에 넣어 spill 동작을 확인해 보겠습니다.

```csharp
// Optional: Fill A1 with a 2‑by‑2 array constant
sheet.Cells[0, 0].ArrayFormula = "{1,2;3,4}";
```

이제 `A1#`은 2 × 2 블록을 나타내며, `EXPAND`는 요청된 5 × 3 행렬로 늘려 남은 셀을 0(또는 엔진이 선택한 값)으로 채웁니다.

---

## 4단계: 워크북 재계산하여 수식 평가

수식을 설정했지만 **워크북을 재계산**하지 않으면 엔진이 실제 값을 계산하지 않습니다.

```csharp
// Step 4: Force calculation of all formulas
workbook.Calculate();
```

> **재계산이 필요한 이유:** 일부 라이브러리는 저장하거나 명시적으로 값을 요청할 때만 수식을 지연 평가합니다. `Calculate()`를 호출하면 spill 영역이 즉시 채워져 이후 처리나 UI 반환에 필수적입니다.

---

## 5단계: 결과 확인 – 확장된 범위 읽어오기

확장된 영역에서 몇 개의 셀을 읽어와 정상 동작을 확인해 보겠습니다.

```csharp
// Step 5: Read back a few cells from the expanded block
for (int row = 0; row < 5; row++)
{
    for (int col = 0; col < 3; col++)
    {
        var value = sheet.Cells[row, col].Value;
        Console.Write($"{value}\t");
    }
    Console.WriteLine();
}
```

**예상 콘솔 출력**

```
1	2	0	
3	4	0	
0	0	0	
0	0	0	
0	0	0	
```

원본 2 × 2 배열이 좌상단에 배치되고, 나머지 셀은 `EXPAND`가 대상 크기가 소스보다 클 때 기본값(0)으로 채우는 모습을 확인할 수 있습니다.

---

## 일반적인 변형 및 엣지 케이스

| 상황 | 처리 방법 |
|-----------|------------------|
| **소스 범위가 대상보다 클 때** | `EXPAND`는 초과된 행/열을 잘라냅니다. 전체 소스를 유지하려면 크기 인수를 생략하세요. |
| **동적 소스 크기** | `ROWS(A1#)`와 `COLUMNS(A1#)`를 `EXPAND` 안에 사용해 자동 조정되는 spill을 만들 수 있습니다. |
| **거대한 범위에서 성능** | 대용량 워크북 재계산은 느릴 수 있습니다. 영향을 받는 시트에만 `Calculate()`를 호출하세요: `sheet.Calculate();`. |
| **워크북 저장** | 검증이 끝나면 `workbook.Save("Report.xlsx");`를 호출해 파일을 영구 저장합니다. |
| **다른 동적 함수와 결합** | `SEQUENCE`, `FILTER`, `SORT`와 `EXPAND`를 함께 쓰면 강력합니다. 예: `=EXPAND(FILTER(A2:A20, B2:B20>0),10,2)`. |

---

## 전체 작업 예제 (모든 단계 결합)

```csharp
using System;
using Aspose.Cells;   // Replace with your chosen library

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];

        // 2️⃣ Set an expanding formula in A1
        sheet.Cells[0, 0].Formula = "=EXPAND(A1#,5,3)";

        // 3️⃣ Optional: give A1 a 2x2 array constant
        sheet.Cells[0, 0].ArrayFormula = "{1,2;3,4}";

        // 4️⃣ Recalculate so the formula evaluates
        workbook.Calculate();

        // 5️⃣ Print the first 5 rows × 3 columns
        for (int r = 0; r < 5; r++)
        {
            for (int c = 0; c < 3; c++)
            {
                Console.Write($"{sheet.Cells[r, c].Value}\t");
            }
            Console.WriteLine();
        }

        // Save if you want to inspect the file
        workbook.Save("ExpandDemo.xlsx");
    }
}
```

프로그램을 실행하면 앞서 보여준 콘솔 출력과 동일한 결과를 확인할 수 있으며, 동일한 spill 배열을 담은 `ExpandDemo.xlsx` 파일이 디스크에 생성됩니다.

---

## 현장에서 얻은 팁 & 트릭

- **프로 팁:** 확장된 값이 추가 계산에만 필요하고 사용자에게 보여줄 스프레드시트가 필요 없을 경우, `Calculate()` 직후 바로 값을 읽어오세요—디스크에 쓸 필요가 없습니다.  
- **주의점:** 일부 구버전 Excel 엔진은 동적 배열을 지원하지 않아 `#NAME?` 오류가 발생합니다. 사용 중인 라이브러리 버전을 항상 확인하세요.  
- **흔한 실수:** `Calculate()` 호출을 빼먹으면 셀이 비어 있어 사용자가 혼란스러워합니다. 전체 파이프라인을 반드시 테스트하세요.  
- **성능 힌트:** 수천 개 셀을 다룰 때는 개별 할당보다 `sheet.Cells[range].Formula = ...`와 같이 범위 단위로 수식을 한 번에 설정하는 것이 더 빠릅니다.

---

## 결론

이제 **Excel 워크북을 생성**, **강력한 `EXPAND` 함수로 셀 수식 설정**, 그리고 **워크북을 재계산**해 데이터가 정확히 원하는 위치에 spill되는 방법을 알게 되었습니다. 이 접근법을 통해 **Excel 수식 작성** 코드를 동적 데이터 크기에 맞게 조정할 수 있어 대시보드, 자동 보고서, 혹은 소스 데이터가 지속적으로 성장하는 모든 시나리오에 최적입니다.

다음 단계가 궁금하신가요? `EXPAND` 대신 `SEQUENCE`를 사용해 번호 매긴 그리드를 만들거나, `FILTER`와 결합해 조건에 맞는 행만 추출해 보세요. 또한 차트, 피벗 테이블, 조건부 서식에 **셀 수식 설정**을 적용해 보면서 방금 만든 워크북을 기반으로 더욱 풍부한 기능을 구현해 보시기 바랍니다.

엣지 케이스나 라이브러리별 특이사항에 대한 질문이 있으면 아래 댓글에 남겨 주세요. 즐거운 코딩 되세요!

## 다음에 배울 내용은?

다음 튜토리얼들은 이 가이드에서 다룬 기술을 확장하는 주제들을 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 제공해 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용할 수 있도록 돕습니다.

- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
- [Excel Automation with Aspose.Cells .NET&#58; Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [How to Load an Excel Workbook & Set Printer Sizes Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/load-workbook-set-printer-sizes-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}