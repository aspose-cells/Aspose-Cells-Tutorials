---
category: general
date: 2026-04-07
description: 피벗 테이블을 새로 고치고, Excel에 이미지를 삽입하며, 그림 자리표시자를 사용해 Excel 워크북을 몇 단계만에 저장하는
  방법을 배워보세요.
draft: false
keywords:
- how to refresh pivot
- insert image into excel
- save excel workbook
- add picture placeholder
- refresh pivot table
language: ko
og_description: Excel에서 피벗 테이블을 새로 고치고, 이미지를 삽입하며, 그림 자리표시자를 사용해 C#로 Excel 워크북을 저장하는
  방법. 단계별 코드 예제.
og_title: 피벗 새로 고침 및 엑셀에 이미지 삽입 방법 – 완전 가이드
tags:
- Aspose.Cells
- C#
- Excel automation
title: 피벗 새로 고침 및 엑셀에 이미지 삽입하는 방법 – 완전 가이드
url: /ko/net/pivot-tables/how-to-refresh-pivot-and-insert-image-into-excel-complete-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 피벗 새로 고침 및 Excel에 이미지 삽입 방법 – 완전 가이드

소스 데이터가 변경될 때 **피벗을 새로 고치는 방법**과, 최신 차트나 테이블 이미지를 같은 시트에 바로 삽입하는 방법이 궁금하신가요? 여러분만 그런 것이 아닙니다. 많은 보고 파이프라인에서 데이터는 데이터베이스에 저장되고, 피벗 테이블이 이를 가져오며, 최종 Excel 파일은 최신 숫자를 그림으로 표시해야 합니다—그래야 하위 사용자가 실수로 원본을 편집하지 못하게 할 수 있기 때문이죠.

이 튜토리얼에서는 정확히 다음을 단계별로 살펴봅니다: **피벗 새로 고침**, **Excel에 이미지 삽입**, 그리고 **그림 자리표시자(picture placeholder)**를 사용해 **Excel 워크북 저장**까지. 끝까지 따라오시면 모든 작업을 수행하는 단일 C# 프로그램을 얻을 수 있으며, 각 코드 라인이 왜 필요한지도 이해하게 됩니다.

> **Pro tip:** 이 방법은 Aspose.Cells 2024 이상에서 동작하므로 서버에 Excel을 설치할 필요가 없습니다.

---

## 준비물

- **Aspose.Cells for .NET** (NuGet 패키지 `Aspose.Cells`).  
- .NET 6.0 SDK 이상 (코드는 .NET 8에서도 컴파일됩니다).  
- 피벗 테이블과 그림 자리표시자(시트의 첫 번째 그림 객체)가 이미 포함된 기본 Excel 파일(`input.xlsx`).  
- Excel 객체 모델에 대한 약간의 호기심.

추가 COM 인터옵, Office 설치 없이 순수 C#만으로 가능합니다.

---

## 피벗 새로 고침 및 최신 데이터 캡처

먼저 해야 할 일은 Excel(정확히는 Aspose.Cells)에게 피벗 테이블이 최신 소스 범위를 기준으로 다시 계산하도록 알려주는 것입니다. 이 단계를 건너뛰면 오래된 데이터가 남아 자동화의 의미가 사라집니다.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// 1️⃣ Load the workbook and grab the first worksheet
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelDemo\input.xlsx");
Worksheet worksheet = workbook.Worksheets[0];

// 2️⃣ Refresh the first pivot table so it reflects the latest data
worksheet.PivotTables[0].Refresh();
```

**왜 중요한가:**  
`Refresh()`를 호출하면 피벗 엔진이 집계 로직을 다시 실행합니다. 이후 피벗을 이미지로 내보내면 그림에 *현재* 합계가 표시되며, 파일이 마지막으로 저장됐을 때의 값이 아니라 최신 값이 표시됩니다.

---

## 그림 자리표시자를 이용한 Excel 이미지 삽입

피벗이 최신 상태가 되었으니 이제 이를 정적인 이미지로 변환해야 합니다. 배포용으로 시각을 고정하거나 나중에 PowerPoint 슬라이드에 삽입하고 싶을 때 유용합니다.

```csharp
// 3️⃣ Set up image options – we want a PNG image
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png
};

// 4️⃣ Render the refreshed pivot table to an image using the options
Image pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);
```

`ImageOrPrintOptions` 객체를 사용하면 해상도, 배경, 포맷 등을 제어할 수 있습니다. PNG는 무손실이며 대부분의 비즈니스 보고서에 적합합니다.

---

## 워크시트에 그림 자리표시자 추가

대부분의 Excel 템플릿에는 동적 그래픽을 위한 “슬롯” 역할을 하는 도형이나 그림이 이미 포함되어 있습니다. 아직 없다면 Excel에서 빈 그림을 삽입하고 템플릿을 저장하면—Aspose.Cells가 이를 `Pictures[0]`으로 노출합니다.

```csharp
// 5️⃣ Place the rendered image into the first picture placeholder on the sheet
worksheet.Pictures[0].Image = pivotImage;
```

**여러 개의 자리표시자가 있는 경우:**  
인덱스(`Pictures[1]`, `Pictures[2]`, …)를 바꾸거나 `worksheet.Pictures`를 순회하면서 이름으로 찾으면 됩니다.

---

## 수정 후 Excel 워크북 저장

마지막으로 변경 사항을 영구히 저장합니다. 이제 워크북에는 새로 고친 피벗, 방금 생성한 PNG, 그리고 해당 이미지로 업데이트된 그림 자리표시자가 들어 있습니다.

```csharp
// 6️⃣ Save the workbook to see the result
workbook.Save(@"C:\MyProjects\ExcelDemo\output.xlsx");
```

`output.xlsx`를 열면 그림 슬롯에 최신 피벗 스냅샷이 채워진 것을 확인할 수 있습니다. 수동 작업이 전혀 필요 없습니다.

---

## 전체 작업 예제 (전체 단계 통합)

아래는 복사‑붙여넣기만 하면 바로 실행 가능한 완전한 프로그램입니다. 필요한 `using` 문, 오류 처리, 그리고 각 비직관적인 라인을 설명하는 주석이 포함되어 있습니다.

```csharp
using Aspose.Cells;
using System;
using System.Drawing.Imaging;

namespace ExcelPivotImageDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths – adjust to your environment
            string inputPath = @"C:\MyProjects\ExcelDemo\input.xlsx";
            string outputPath = @"C:\MyProjects\ExcelDemo\output.xlsx";

            try
            {
                // Load workbook
                Workbook workbook = new Workbook(inputPath);
                Worksheet sheet = workbook.Worksheets[0];

                // -------------------------------------------------
                // Refresh pivot table – this is the core of "how to refresh pivot"
                // -------------------------------------------------
                if (sheet.PivotTables.Count == 0)
                {
                    Console.WriteLine("No pivot tables found on the first worksheet.");
                    return;
                }
                sheet.PivotTables[0].Refresh();

                // -------------------------------------------------
                // Convert refreshed pivot to PNG image
                // -------------------------------------------------
                ImageOrPrintOptions imgOpts = new ImageOrPrintOptions
                {
                    ImageFormat = ImageFormat.Png,
                    // Optional: higher DPI for sharper images
                    HorizontalResolution = 150,
                    VerticalResolution = 150
                };
                Image pivotImg = sheet.PivotTables[0].ToImage(imgOpts);

                // -------------------------------------------------
                // Insert the image into the first picture placeholder
                // -------------------------------------------------
                if (sheet.Pictures.Count == 0)
                {
                    // If the template lacks a placeholder, we create one on the fly
                    int picIdx = sheet.Pictures.Add(0, 0, pivotImg);
                    sheet.Pictures[picIdx].Name = "PivotSnapshot";
                }
                else
                {
                    sheet.Pictures[0].Image = pivotImg;
                }

                // -------------------------------------------------
                // Save the updated workbook – this fulfills "save excel workbook"
                // -------------------------------------------------
                workbook.Save(outputPath);
                Console.WriteLine($"Workbook saved successfully to {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
                // In production you might log the stack trace or rethrow
            }
        }
    }
}
```

**예상 결과:**  
`output.xlsx`를 열면 첫 번째 그림 객체에 새로 고친 피벗 테이블의 PNG가 표시됩니다. `input.xlsx`의 소스 데이터를 바꾸고 프로그램을 다시 실행하면 그림이 자동으로 업데이트됩니다—수동 복사‑붙여넣기가 전혀 필요 없습니다.

---

## 일반적인 변형 및 예외 상황

| 상황 | 변경 방법 |
|-----------|----------------|
| **여러 개의 피벗 테이블** | `sheet.PivotTables`를 순회하며 각각 `Refresh()`하고, 이미지에 사용할 피벗을 선택합니다. |
| **다른 이미지 포맷** | `ImageOrPrintOptions`에서 `ImageFormat = ImageFormat.Jpeg`(또는 `Bmp`)로 설정합니다. |
| **동적 자리표시자 선택** | 인덱스 대신 `sheet.Pictures["MyPlaceholderName"]`을 사용합니다. |
| **대용량 워크북** | `Workbook.Settings.CalculateFormulaEngine`을 `EngineType.Fast`로 설정해 계산 속도를 높입니다. |
| **헤드리스 서버에서 실행** | Aspose.Cells는 UI 없이 완전 동작하므로 추가 설정이 필요 없습니다. |

---

## 자주 묻는 질문

**Q: 매크로가 포함된 워크북(`.xlsm`)에서도 작동하나요?**  
A: 네. Aspose.Cells는 다른 워크북과 동일하게 취급합니다; 매크로는 보존되지만 새로 고침 중에는 실행되지 않습니다.

**Q: 피벗이 외부 데이터 소스를 사용하고 있다면?**  
A: 코드를 실행하는 머신에서 연결 문자열이 유효해야 합니다. `pivotTable.CacheDefinition.ConnectionInfo`를 사용해 프로그래밍적으로 조정할 수 있습니다.

**Q: 그림 자리표시자 대신 특정 셀 범위에 이미지를 넣을 수 있나요?**  
A: 가능합니다. `sheet.Pictures.Add(row, column, pivotImg)`를 사용하면 `row`와 `column`은 0부터 시작하는 인덱스입니다.

---

## 마무리

우리는 **피벗 새로 고침**, **Excel에 이미지 삽입**, **그림 자리표시자 추가**, 그리고 **Excel 워크북 저장**까지 모두 깔끔한 C# 스니펫으로 다뤘습니다. 먼저 피벗을 새로 고침함으로써 그림이 최신 데이터를 반영하도록 보장하고, 자리표시자를 활용해 템플릿을 깔끔하고 재사용 가능하게 유지합니다.

다음 단계로 시도해 볼 수 있는 내용:

- 동일한 이미지를 PDF 보고서(`PdfSaveOptions`)로 내보내기.  
- 서로 다른 소스 데이터를 가진 파일들을 일괄 처리 자동화.  
- Aspose.Slides를 사용해 PNG를 바로 PowerPoint 슬라이드에 붙여넣기.

PNG를 JPEG로 바꾸거나 DPI를 조정하고, 여러 그림을 추가해 보세요. 핵심 아이디어는 변함없습니다: 데이터를 최신 상태로 유지하고, 이미지를 캡처한 뒤, 필요한 위치에 삽입하는 것.

코딩 즐겁게! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}