---
title: 차트에 그림 추가
linktitle: 차트에 그림 추가
second_title: Aspose.Cells .NET Excel 처리 API
description: Aspose.Cells for .NET을 사용하여 Excel 차트에 그림을 쉽게 추가하는 방법을 알아보세요. 몇 가지 간단한 단계만으로 차트와 프레젠테이션을 강화하세요.
weight: 11
url: /ko/net/inserting-controls-in-charts/add-picture-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 차트에 그림 추가

## 소개

개인적인 터치가 없는 지루한 차트에 지치셨나요? 그림을 추가하여 Excel 비주얼을 더 매력적으로 만드는 방법을 배우고 싶으신가요? 글쎄요, 운이 좋으시네요! 이 튜토리얼에서는 Aspose.Cells for .NET의 세계로 뛰어들어 Excel에서 차트에 그림을 추가하는 방법을 알아봅니다. 좋아하는 커피 한 잔을 들고 시작해 볼까요!

## 필수 조건

코딩의 핵심에 들어가기 전에 순조롭게 따라가기 위해 꼭 필요한 몇 가지 전제 조건이 있습니다.

- Visual Studio: 여기서 .NET 코드를 작성하고 실행합니다. 설치했는지 확인하세요.
-  .NET용 Aspose.Cells: Excel 파일을 사용하려면 이 라이브러리가 필요합니다.[여기서 다운로드하세요](https://releases.aspose.com/cells/net/).
- C#에 대한 기본적인 이해: 코드를 안내해드리겠지만, C#의 기본을 알고 있으면 더 명확하게 이해할 수 있습니다.

### 설치 단계

1. Aspose.Cells 설치: NuGet 패키지 관리자를 통해 Visual Studio 프로젝트에 Aspose.Cells를 추가할 수 있습니다. 도구 > NuGet 패키지 관리자 > 솔루션용 NuGet 패키지 관리로 이동하여 "Aspose.Cells"를 검색합니다. 설치를 클릭합니다.
2. 프로젝트 설정: Visual Studio에서 새 C# 콘솔 애플리케이션 프로젝트를 만듭니다.

## 패키지 가져오기

모든 것을 설정했으면 다음 단계는 필요한 패키지를 프로젝트에 가져오는 것입니다. 방법은 다음과 같습니다.

### 필요한 네임스페이스 가져오기

C# 코드 파일의 맨 위에서 다음 네임스페이스를 가져와야 합니다.

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using Aspose.Cells.Drawing;
using System.IO;
```

이것은 당신의 프로그램에 "이봐! Aspose.Cells의 멋진 기능들을 사용할 거야."라고 말합니다.

이제 전제 조건이 마련되었으니, 과정을 작은 단계로 나누어 보겠습니다. 

## 1단계: 디렉토리 정의

가장 먼저, 입력 및 출력 파일의 경로를 설정해야 합니다. 이 단계는 기존 Excel 파일을 어디에서 찾을 수 있고 수정된 파일을 어디에 저장할지 알아야 하기 때문에 중요합니다.

```csharp
//소스 디렉토리
string sourceDir = "Your Document Directory/";

//출력 디렉토리
string outputDir = "Your Output Directory/";
```

 바꾸다`Your Document Directory` 그리고`Your Output Directory` 컴퓨터의 실제 경로를 사용합니다. 

## 2단계: 기존 통합 문서 로드

이제 차트에 그림을 추가하려는 기존 Excel 파일을 로드해 보겠습니다.

```csharp
// 기존 파일을 엽니다.
Workbook workbook = new Workbook(sourceDir + "sampleAddingPictureInChart.xls");
```

이 코드는 통합 문서를 열어 편집할 수 있도록 준비합니다.

## 3단계: 이미지 스트림 준비

그림을 추가하기 전에 차트에 삽입하려는 이미지를 읽어야 합니다. 

```csharp
// 스트림으로 이미지 파일을 가져옵니다.
FileStream stream = new FileStream(sourceDir + "sampleAddingPictureInChart.png", FileMode.Open, FileAccess.Read);
```

지정된 디렉토리에 사진이 저장되어 있는지 확인하세요.

## 4단계: 차트 타겟팅

이제, 어떤 차트에 그림을 추가할지 지정해 보겠습니다. 이 예에서는 첫 번째 워크시트의 첫 번째 차트를 타겟으로 삼겠습니다.

```csharp
// 두 번째 시트에서 디자이너 차트를 받으세요.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

색인을 적절히 변경하면 모든 워크시트에 접근할 수 있습니다.

## 5단계: 차트에 그림 추가

차트를 선택했으면 이제 그림을 추가할 차례입니다! 

```csharp
// 차트에 새로운 그림을 추가합니다.
Aspose.Cells.Drawing.Picture pic0 = chart.Shapes.AddPictureInChart(50, 50, stream, 200, 200);
```

 여기,`50` 그리고`50` 이미지가 배치될 X 및 Y 좌표입니다.`200` 이미지의 너비와 높이입니다.

## 6단계: 그림의 선 형식 사용자 지정

사진에 약간의 멋을 더하고 싶으신가요? 테두리를 사용자 지정할 수 있습니다! 방법은 다음과 같습니다.

```csharp
// 그림의 lineformat 유형을 가져옵니다.
Aspose.Cells.Drawing.LineFormat lineformat = pic0.Line; 

// 대시 스타일을 설정합니다.
lineformat.DashStyle = MsoLineDashStyle.Solid;

// 선의 굵기를 설정합니다.
lineformat.Weight = 4;    
```

이 스니펫을 사용하면 테두리 모양과 두께를 선택할 수 있습니다. 프레젠테이션과 어울리는 스타일을 선택하세요!

## 7단계: 수정된 통합 문서 저장

모든 힘든 작업을 마친 후 다음 코드 줄을 실행하여 수정 사항을 저장해 보겠습니다.

```csharp
// Excel 파일을 저장합니다.
workbook.Save(outputDir + "outputAddingPictureInChart.xls");
```

이제 그림이 차트에 성공적으로 통합되었고 출력 파일을 볼 준비가 되었습니다!

## 8단계: 성공을 나타냅니다

마지막으로 작업이 성공적이었음을 확인하는 간단한 메시지를 추가할 수 있습니다.

```csharp
Console.WriteLine("AddingPictureInChart executed successfully.");
```

## 결론

이 튜토리얼에서는 Aspose.Cells for .NET을 사용하여 그림을 추가하여 Excel 차트에 약간의 개성을 불어넣는 방법을 살펴보았습니다. 몇 가지 간단한 단계만 거치면 프레젠테이션을 평범한 것에서 기억에 남는 것으로 격상시킬 수 있습니다. 그럼, 무엇을 기다리고 계신가요? 시도해 보고 차트를 빛나게 하세요!

## 자주 묻는 질문

### 하나의 차트에 여러 개의 그림을 추가할 수 있나요?
 네! 전화할 수 있어요`AddPictureInChart` 원하는 만큼 많은 사진을 추가하려면 이 방법을 여러 번 반복하세요.

### Aspose.Cells는 어떤 이미지 형식을 지원하나요?
Aspose.Cells는 PNG, JPEG, BMP, GIF 등 다양한 이미지 형식을 지원합니다.

### 그림의 위치를 사용자 지정할 수 있나요?
 물론입니다! X 및 Y 좌표는`AddPictureInChart` 이 방법을 사용하면 정확한 위치 지정이 가능합니다.

### Aspose.Cells는 무료로 사용할 수 있나요?
Aspose.Cells는 무료 체험판을 제공하지만, 모든 기능을 사용하려면 라이선스가 필요합니다. 가격은 다음과 같습니다.[여기](https://purchase.aspose.com/buy).

### 더 많은 예를 어디서 볼 수 있나요?
 확인해보세요[Aspose.Cells 설명서](https://reference.aspose.com/cells/net/) 더 자세한 예와 기능은 다음과 같습니다.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
