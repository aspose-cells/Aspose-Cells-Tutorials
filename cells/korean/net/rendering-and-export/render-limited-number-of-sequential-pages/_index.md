---
title: Aspose.Cells에서 순차적 페이지 렌더링
linktitle: Aspose.Cells에서 순차적 페이지 렌더링
second_title: Aspose.Cells .NET Excel 처리 API
description: Aspose.Cells for .NET을 사용하여 Excel에서 순차적 페이지를 렌더링하는 방법을 알아보세요. 이 단계별 튜토리얼은 선택한 페이지를 이미지로 변환하는 자세한 가이드를 제공합니다.
weight: 18
url: /ko/net/rendering-and-export/render-limited-number-of-sequential-pages/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells에서 순차적 페이지 렌더링

## 소개
Excel 통합 문서에서 특정 페이지를 렌더링하는 것은 특히 전체 파일 없이 특정 데이터 비주얼만 필요할 때 매우 유용할 수 있습니다. Aspose.Cells for .NET은 .NET 애플리케이션에서 Excel 문서를 정밀하게 제어하여 선택한 페이지를 렌더링하고 형식을 변경하는 등의 작업을 할 수 있는 강력한 라이브러리입니다. 이 튜토리얼은 특정 Excel 워크시트 페이지를 이미지 형식으로 변환하는 방법을 안내합니다. 이는 사용자 지정 데이터 스냅샷을 만드는 데 이상적입니다.
## 필수 조건
코드를 시작하기 전에 다음 항목이 설정되어 있는지 확인하세요.
-  .NET 라이브러리용 Aspose.Cells: 다음을 수행할 수 있습니다.[여기서 다운로드하세요](https://releases.aspose.com/cells/net/).
- 개발 환경: Visual Studio와 같은 .NET 지원 환경.
- Excel 파일: 여러 페이지가 있는 샘플 Excel 파일로, 로컬 디렉토리에 저장됩니다.
 또한 무료 평가판을 받거나 라이선스가 없는 경우 라이선스를 구매하세요.[임시 면허](https://purchase.aspose.com/temporary-license/) 구매하기 전에 모든 기능을 확인해보세요.
## 패키지 가져오기
시작하려면 Aspose.Cells와 필요한 네임스페이스를 .NET 환경으로 가져와야 합니다.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
```
이러한 패키지는 Excel 파일을 조작하고 렌더링하는 데 필요한 모든 클래스와 메서드를 제공합니다. 이제 렌더링 프로세스의 각 부분을 자세히 분석해 보겠습니다.
## 1단계: 소스 및 출력 디렉토리 설정
먼저, 입력 및 출력 파일에 대한 디렉토리를 정의하여 프로그램에서 파일을 검색하고 저장할 위치를 알 수 있도록 합니다.
```csharp
// 소스 디렉토리
string sourceDir = "Your Document Directory";
// 출력 디렉토리
string outputDir = "Your Document Directory";
```
소스 및 출력 디렉토리를 지정하면 읽기 및 쓰기 작업 모두에 대한 파일 액세스를 간소화할 수 있습니다. 런타임 오류를 피하기 위해 이러한 디렉토리가 있는지 확인하세요.
## 2단계: 샘플 Excel 파일 로드
 다음으로 Aspose.Cells를 사용하여 Excel 파일을 로드합니다.`Workbook` 클래스. 이 파일에는 렌더링하려는 데이터와 페이지가 포함됩니다.
```csharp
// 샘플 Excel 파일을 로드합니다
Workbook wb = new Workbook(sourceDir + "sampleImageOrPrintOptions_PageIndexPageCount.xlsx");
```
 그만큼`Workbook`클래스는 Aspose.Cells의 기본 Excel 핸들러와 같으며 시트, 스타일 등에 직접 액세스할 수 있도록 해줍니다.
## 3단계: 타겟 워크시트에 접근
이제 작업할 특정 워크시트를 선택해 보겠습니다. 이 튜토리얼에서는 첫 번째 시트를 사용하지만 필요한 시트로 수정할 수 있습니다.
```csharp
// 첫 번째 워크시트에 접근하세요
Worksheet ws = wb.Worksheets[0];
```
각 워크북에는 여러 워크시트가 있을 수 있으며, 올바른 워크시트를 선택하는 것이 중요합니다. 이 줄은 렌더링이 수행될 지정된 워크시트에 대한 액세스 권한을 부여합니다.
## 4단계: 이미지 또는 인쇄 옵션 설정
페이지가 렌더링되는 방식을 제어하기 위해 몇 가지 인쇄 옵션을 정의합니다. 여기서 렌더링할 페이지, 이미지 형식 및 기타 설정을 지정합니다.
```csharp
// 이미지 또는 인쇄 옵션 지정
ImageOrPrintOptions opts = new ImageOrPrintOptions();
opts.PageIndex = 3; // 4페이지부터 시작하세요
opts.PageCount = 4; // 4페이지 렌더링
opts.ImageType = Drawing.ImageType.Png;
```
 와 함께`ImageOrPrintOptions` , 설정할 수 있습니다`PageIndex` (시작 페이지),`PageCount` (렌더링할 페이지 수) 및`ImageType` (출력 형식). 이 설정은 렌더링 프로세스를 정확하게 제어할 수 있게 해줍니다.
## 5단계: 시트 렌더 객체 생성
이제 우리는 다음을 생성합니다.`SheetRender` 워크시트와 이미지 옵션을 가져와 지정된 각 페이지를 이미지로 렌더링하는 객체입니다.
```csharp
// 시트 렌더 객체 생성
SheetRender sr = new SheetRender(ws, opts);
```
 그만큼`SheetRender` 클래스는 워크시트를 이미지, PDF 또는 다른 형식으로 렌더링하는 데 필수적입니다. 워크시트와 구성한 옵션을 사용하여 출력을 생성합니다.
## 6단계: 각 페이지를 이미지로 렌더링하고 저장
마지막으로 지정된 각 페이지를 반복하여 이미지로 저장해 보겠습니다. 이 루프는 각 페이지를 렌더링하고 고유한 이름으로 저장하는 것을 처리합니다.
```csharp
// 모든 페이지를 이미지로 인쇄
for (int i = opts.PageIndex; i < sr.PageCount; i++)
{
    sr.ToImage(i, outputDir + "outputImage-" + (i + 1) + ".png");
}
```
다음은 진행 중인 작업에 대한 세부 내용입니다.
-  그만큼`for` 루프는 지정된 범위의 각 페이지를 살펴봅니다.
- `ToImage` 각 페이지를 이미지로 렌더링하고, 각 페이지를 구분하기 위한 사용자 정의 파일 이름 형식을 사용하는 데 사용됩니다.
## 7단계: 완료 확인
렌더링이 완료되면 간단한 확인 메시지를 추가합니다. 이 단계는 선택 사항이지만 성공적인 실행을 확인하는 데 유용할 수 있습니다.
```csharp
Console.WriteLine("RenderLimitedNoOfSequentialPages executed successfully.\r\n");
```
이 마지막 줄은 모든 것이 의도한 대로 작동했음을 확인합니다. 모든 페이지가 렌더링되고 저장된 후 콘솔에 이 메시지가 표시됩니다.
## 결론
그리고 이제 알게 되었습니다! Aspose.Cells for .NET을 사용하여 Excel 통합 문서의 특정 페이지를 렌더링하는 것은 데이터 출력을 사용자 지정하는 간단하면서도 강력한 방법입니다. 주요 지표의 스냅샷이나 특정 데이터 비주얼이 필요하든 이 튜토리얼이 해결해 드립니다. 이러한 단계를 따르면 이제 Excel 파일에서 모든 페이지 또는 페이지 범위를 아름다운 이미지 형식으로 렌더링할 수 있습니다.
 다른 옵션을 자유롭게 탐색하세요`ImageOrPrintOptions` 그리고`SheetRender` 더욱 더 많은 제어를 위해. 즐거운 코딩하세요!
## 자주 묻는 질문
### 여러 워크시트를 동시에 렌더링할 수 있나요?  
 네, 루프를 통해 수행할 수 있습니다.`Worksheets` 수집하여 각 시트에 개별적으로 렌더링 프로세스를 적용합니다.
### PNG 외에 어떤 다른 형식으로 페이지를 렌더링할 수 있나요?  
 Aspose.Cells는 JPEG, BMP, TIFF, GIF를 포함한 여러 형식을 지원합니다. 변경하기만 하면 됩니다.`ImageType` ~에`ImageOrPrintOptions`.
### 여러 페이지가 있는 큰 Excel 파일을 어떻게 처리합니까?  
대용량 파일의 경우 렌더링을 작은 섹션으로 나누어 메모리 사용량을 효과적으로 관리하는 것이 좋습니다.
### 이미지 해상도를 사용자 정의할 수 있나요?  
 예,`ImageOrPrintOptions` 사용자 정의 해상도에 대한 DPI 설정을 허용합니다.`HorizontalResolution` 그리고`VerticalResolution`.
### 페이지의 일부만 렌더링해야 하는 경우는 어떻게 되나요?  
당신은 사용할 수 있습니다`PrintArea` 속성에`PageSetup` 워크시트에서 렌더링할 특정 영역을 정의합니다.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
