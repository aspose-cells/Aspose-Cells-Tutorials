---
title: 원하는 페이지 크기로 차트 PDF 만들기
linktitle: 원하는 페이지 크기로 차트 PDF 만들기
second_title: Aspose.Cells .NET Excel 처리 API
description: Aspose.Cells for .NET을 사용하여 Excel 차트로 PDF를 만드세요. 이 단계별 가이드로 방법을 알아보세요.
weight: 12
url: /ko/net/chart-rendering-and-conversion/create-chart-pdf-with-desired-page-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 원하는 페이지 크기로 차트 PDF 만들기

## 소개

시각적으로 매력적이고 유익한 차트를 만드는 것은 다양한 분야에서 데이터를 표현하는 데 필수적입니다. 판매 데이터, 성과 지표 또는 기타 유형의 정보를 다루는 경우 고품질 차트를 생성할 수 있는 기능은 결과에 깊이와 명확성을 제공합니다. .NET 애플리케이션을 사용하는 경우 Aspose.Cells는 Excel 문서를 처리하고 차트를 생성하는 것을 쉽게 만드는 강력한 라이브러리입니다. 이 튜토리얼에서는 원하는 페이지 크기의 Excel 파일에서 차트의 PDF를 만드는 과정을 안내합니다.

## 필수 조건

코드를 살펴보기 전에 원활한 경험을 위해 반드시 충족해야 할 몇 가지 전제 조건이 있습니다.

### C# 및 .NET에 대한 기본 지식

C# 프로그래밍과 .NET 프레임워크에 대한 기본적인 이해가 필요합니다. 그러면 이 가이드에서 접하게 될 코드의 구조를 파악하는 데 도움이 될 것입니다.

### .NET용 Aspose.Cells

Aspose.Cells for .NET이 설치되어 있는지 확인하세요. 자세한 내용은 다음에서 확인할 수 있습니다.[Aspose.Cells 설명서](https://reference.aspose.com/cells/net/). 

### 개발 환경

 개발 환경을 설정합니다. 이는 Visual Studio 또는 C#을 지원하는 다른 IDE일 수 있습니다. Aspose.Cells 라이브러리를 다운로드하여 설치합니다.[다운로드 페이지](https://releases.aspose.com/cells/net/).

### 샘플 Excel 파일

최소한 하나의 차트가 포함된 샘플 Excel 파일이 필요합니다. 이 튜토리얼 전체에서 사용할 샘플 파일을 만들거나 다운로드할 수 있습니다.

## 패키지 가져오기

Aspose.Cells 작업을 시작하려면 C# 애플리케이션에서 필요한 네임스페이스를 가져와야 합니다. 방법은 다음과 같습니다.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Aspose.Cells.Charts;
```

이러한 네임스페이스를 사용하면 Excel 통합 문서와 해당 내용을 조작하는 데 필요한 클래스와 메서드에 액세스할 수 있습니다.

이제 모든 전제 조건을 정리했으니, 과정을 자세한 단계로 나누어 보겠습니다.

## 1단계: 출력 및 소스 디렉토리 설정

시작하려면 출력 PDF를 저장할 위치와 원본 Excel 문서의 위치를 정의해야 합니다.

```csharp
//출력 디렉토리
string outputDir = "Your Output Directory";

//소스 디렉토리
string sourceDir = "Your Document Directory";
```

"Your Output Directory"와 "Your Document Directory"를 시스템의 실제 경로로 바꿔야 합니다. 이는 Aspose가 생성된 PDF를 저장할 위치와 Excel 파일을 찾을 위치를 지시합니다.

## 2단계: 샘플 Excel 파일 로드

다음으로, 차트가 포함된 Excel 파일을 로드해야 합니다. 방법은 다음과 같습니다.

```csharp
//차트가 포함된 샘플 Excel 파일을 로드합니다.
Workbook wb = new Workbook(sourceDir + "sampleCreateChartPDFWithDesiredPageSize.xlsx");
```

 그만큼`Workbook` 클래스는 Excel 문서와 상호 작용하는 데 핵심입니다. 경로가 Excel 파일을 올바르게 가리키는지 확인하세요. 여기에 오류가 있으면 나머지 코드가 실행되지 않습니다.

## 3단계: 첫 번째 워크시트에 액세스

통합 문서가 로드되면 다음 단계는 원하는 차트가 포함된 워크시트에 액세스하는 것입니다.

```csharp
//첫 번째 워크시트에 접근합니다.
Worksheet ws = wb.Worksheets[0];
```

 Aspose.Cells에서는 워크시트가 0부터 색인화되므로`Worksheets[0]` 첫 번째 시트를 가리킨다.

## 4단계: 첫 번째 차트에 액세스

이제 PDF로 내보내고 싶은 차트에 접근해 보겠습니다. 이 단계에서는 워크시트에 최소한 하나의 차트가 포함되어 있다고 가정합니다.

```csharp
//워크시트 내에서 첫 번째 차트에 접근합니다.
Chart ch = ws.Charts[0];
```

이렇게 하면 워크시트의 첫 번째 차트에 접근할 수 있습니다. 워크시트 구조가 이 접근 방식에 적합한지 확인하세요.

## 5단계: 원하는 페이지 크기로 PDF 만들기

마지막으로, 지정된 페이지 크기로 차트에서 PDF를 만들 시간입니다. 모든 것을 수행하는 마법의 코드 줄은 다음과 같습니다.

```csharp
//원하는 페이지 크기로 차트 PDF를 만듭니다.
ch.ToPdf(outputDir + "outputCreateChartPDFWithDesiredPageSize.pdf", 7, 7, PageLayoutAlignmentType.Center, PageLayoutAlignmentType.Center);
```

이 코드에서는:
- PDF는 이전에 지정한 출력 디렉토리에 저장됩니다.
-  숫자`7, 7` 각각 원하는 페이지 크기의 너비와 높이를 나타냅니다.
- PageLayoutAlignmentType.Center는 차트가 페이지의 가운데에 정렬되도록 합니다.

## 6단계: 확인 메시지

모든 것이 순조롭게 진행되었음을 자신(및 다른 사람)에게 알리려면 코드 끝에 확인 메시지를 포함하세요.

```csharp
Console.WriteLine("CreateChartPDFWithDesiredPageSize executed successfully.");
```

이 메시지는 프로세스가 완료되면 콘솔 창에 나타나며, PDF가 문제 없이 생성되었음을 알려줍니다.

## 결론

축하합니다! 방금 Aspose.Cells for .NET을 활용하여 Excel 파일에 포함된 차트에서 PDF를 만드는 방법을 배웠습니다. 이 강력한 라이브러리는 Excel 문서를 조작하고 데이터의 시각적 표현을 생성하는 프로세스를 간소화하여 수 시간의 수동 서식 지정을 절약합니다. PDF 생성을 넘어 Aspose.Cells가 제공하는 다양한 다른 기능을 탐색해 보세요. 무엇이 프로젝트를 더욱 향상시킬지 알 수 없습니다!

## 자주 묻는 질문

### Aspose.Cells for .NET은 무엇에 사용되나요?  
.NET용 Aspose.Cells는 .NET 애플리케이션에서 프로그래밍 방식으로 Excel 문서를 만들고, 편집하고, 변환하는 데 사용됩니다.

### Aspose.Cells를 무료로 사용할 수 있나요?  
 예, Aspose.Cells는 다음을 제공합니다.[무료 체험](https://releases.aspose.com/) 평가 목적으로.

### 체험 기간을 처음 기간보다 더 연장할 수 있는 방법이 있나요?  
 당신은 신청할 수 있습니다[임시 면허](https://purchase.aspose.com/temporary-license/) 확장된 테스트를 위해.

### 문제가 발생하거나 궁금한 점이 있으면 어떻게 해야 하나요?  
 Aspose 커뮤니티에서 도움을 요청할 수 있습니다.[지원 포럼](https://forum.aspose.com/c/cells/9).

### Aspose.Cells를 어떻게 구매할 수 있나요?  
 Aspose.Cells를 다음에서 구매할 수 있습니다.[구매 페이지](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
