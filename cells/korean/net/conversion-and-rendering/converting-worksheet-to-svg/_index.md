---
title: .NET에서 워크시트를 SVG로 변환
linktitle: .NET에서 워크시트를 SVG로 변환
second_title: Aspose.Cells .NET Excel 처리 API
description: 이 단계별 가이드를 통해 Aspose.Cells for .NET을 사용하여 Excel 워크시트를 SVG로 변환하는 방법을 알아보세요. Excel을 SVG로 렌더링하려는 .NET 개발자에게 완벽합니다.
weight: 11
url: /ko/net/conversion-and-rendering/converting-worksheet-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET에서 워크시트를 SVG로 변환

## 소개

Excel 워크시트를 SVG 형식으로 변환하고 싶다면, 당신은 올바른 곳에 왔습니다! Aspose.Cells for .NET은 개발자가 Excel 파일을 조작하고 이를 널리 지원되는 SVG(Scalable Vector Graphics)를 포함한 다양한 형식으로 변환할 수 있는 강력한 도구입니다. 이 튜토리얼은 .NET에서 워크시트를 SVG로 변환하는 과정을 단계별로 나누어 안내하므로 초보자도 쉽게 따라할 수 있습니다.

## 필수 조건

코드를 살펴보기 전에 먼저 필요한 모든 것이 있는지 확인해 보겠습니다.

1.  .NET용 Aspose.Cells: .NET용 Aspose.Cells의 최신 버전을 다운로드하여 설치하세요.[.NET용 Aspose.Cells](https://releases.aspose.com/cells/net/).
2. .NET 개발 환경: Visual Studio나 다른 .NET IDE가 설치되어 있어야 합니다.
3. C#에 대한 기본 지식: C#에 대한 지식이 필요하지만 걱정하지 마세요. 모든 것을 명확하게 설명해 드리겠습니다.
4. Excel 파일: SVG 형식으로 변환하려는 Excel 파일을 준비하세요.

## 필요한 패키지 가져오기

코딩 단계로 넘어가기 전에 C# 파일의 맨 위에 필요한 네임스페이스를 포함시켰는지 확인하세요.

```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Rendering;
```

이러한 패키지는 Aspose.Cells를 사용하고 SVG 내보내기와 같은 렌더링 옵션을 처리하는 데 필요합니다.

이제 기본 사항은 다루어졌으므로 Excel 워크시트를 SVG 이미지로 변환하는 실제 단계를 알아보겠습니다.

## 1단계: 문서 디렉토리 경로 설정

가장 먼저 필요한 것은 Excel 파일이 있는 폴더의 경로를 정의하는 것입니다. 이는 코드가 파일을 로드하고 저장할 디렉토리를 참조하기 때문에 중요합니다.

```csharp
// 문서 디렉토리 경로
string dataDir = "Your Document Directory";
```

 교체를 꼭 해주세요`"Your Document Directory"`Excel 파일이 있는 실제 경로를 사용합니다.

##  2단계: 다음을 사용하여 Excel 파일 로드`Workbook`

 다음으로, 우리는 Excel 파일을 인스턴스에 로드해야 합니다.`Workbook` 클래스.`Workbook` 클래스는 모든 워크시트를 포함한 전체 Excel 파일을 나타냅니다.

```csharp
string filePath = dataDir + "Template.xlsx";
Workbook book = new Workbook(filePath);
```

 여기,`"Template.xlsx"` 는 작업 중인 Excel 파일의 이름입니다. 이 파일이 지정된 디렉토리에 있는지 확인하세요. 그렇지 않으면 오류가 발생합니다.

## 3단계: SVG 변환을 위한 이미지 또는 인쇄 옵션 설정

 워크시트를 SVG 형식으로 변환하기 전에 이미지 옵션을 지정해야 합니다.`ImageOrPrintOptions` 클래스를 사용하면 워크시트가 어떻게 변환될지 제어할 수 있습니다. 구체적으로, 우리는 다음을 설정해야 합니다.`SaveFormat` 에게`SVG` 각 워크시트가 한 페이지로 변환되었는지 확인하세요.

```csharp
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.SaveFormat = SaveFormat.Svg;
imgOptions.OnePagePerSheet = true;
```

 그만큼`SaveFormat.Svg` 이 옵션을 사용하면 출력 형식이 SVG가 됩니다.`OnePagePerSheet` 각 워크시트가 한 페이지에 렌더링되도록 보장합니다.

## 4단계: 워크북의 각 워크시트 반복

이제 Excel 파일의 모든 워크시트를 반복해야 합니다. 각 워크시트는 개별적으로 변환됩니다.

```csharp
foreach (Worksheet sheet in book.Worksheets)
{
    // 우리는 각 워크시트를 하나씩 처리할 것입니다
}
```

이 루프는 통합 문서에 워크시트가 아무리 많아도 각 워크시트가 처리되도록 보장합니다.

##  5단계: 생성`SheetRender` Object for Rendering

 각 워크시트에 대해 다음을 생성합니다.`SheetRender` 객체. 이 객체는 워크시트를 원하는 이미지 형식, 이 경우 SVG로 변환하는 역할을 합니다.

```csharp
SheetRender sr = new SheetRender(sheet, imgOptions);
```

 그만큼`SheetRender` 객체는 두 개의 인수를 취합니다. 변환하려는 워크시트와 이전에 정의한 이미지 옵션입니다.

## 6단계: 워크시트를 SVG로 변환

 마지막으로 루프 내에서 각 워크시트를 SVG 형식으로 변환합니다. 중첩 루프를 사용하여 페이지를 반복합니다(이 경우 워크시트당 페이지가 하나뿐이므로`OnePagePerSheet` 옵션).

```csharp
for (int i = 0; i < sr.PageCount; i++)
{
    // 워크시트를 Svg 이미지 형식으로 출력합니다.
    sr.ToImage(i, filePath + sheet.Name + i + ".out.svg");
}
```

이 코드는 워크시트를 Excel 파일과 같은 디렉토리에 SVG 파일로 저장합니다. 각 SVG 파일은 워크시트 이름과 인덱스 번호에 따라 명명되어 이름 충돌을 방지합니다.

## 결론

그리고 그게 전부입니다! Aspose.Cells for .NET을 사용하여 Excel 워크시트를 SVG 형식으로 성공적으로 변환했습니다. 이 프로세스를 통해 워크시트의 레이아웃과 디자인을 유지하면서 SVG를 지원하는 모든 브라우저나 기기에서 볼 수 있게 만들 수 있습니다. 이는 거의 모든 브라우저나 기기에서 가능합니다. 복잡한 Excel 파일이나 간단한 표로 작업하든 이 방법을 사용하면 데이터가 웹 친화적인 형식으로 아름답게 렌더링됩니다.

## 자주 묻는 질문

### SVG란 무엇이고, 왜 사용해야 하나요?
SVG(Scalable Vector Graphics)는 품질을 잃지 않고 무한히 확장할 수 있는 웹 친화적 포맷입니다. 다양한 크기로 표시해야 하는 차트, 다이어그램 및 이미지에 적합합니다.

### Aspose.Cells는 대용량 Excel 파일을 처리하여 변환할 수 있나요?
네, Aspose.Cells는 대용량 Excel 파일을 효율적으로 처리하고 이를 성능 문제 없이 SVG로 변환할 수 있습니다.

### SVG로 변환할 수 있는 워크시트 수에 제한이 있나요?
아니요, Aspose.Cells에는 여러 워크시트를 변환하는 데 고유한 제한이 없습니다. 유일한 제약은 시스템의 메모리와 성능입니다.

### Aspose.Cells를 사용하려면 라이선스가 필요한가요?
 네, Aspose.Cells는 프로덕션 사용을 위해 라이선스가 필요합니다. 임시 라이선스를 얻을 수 있습니다.[여기](https://purchase.aspose.com/temporary-license/) 또는 탐색하세요[무료 체험](https://releases.aspose.com/).

### SVG 출력을 사용자 정의할 수 있나요?
 네, 조정할 수 있습니다.`ImageOrPrintOptions` SVG 출력의 해상도와 크기 조절 등 다양한 측면을 사용자 정의합니다.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
