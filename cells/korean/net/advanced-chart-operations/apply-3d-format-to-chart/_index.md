---
title: 차트에 3D 형식 적용
linktitle: 차트에 3D 형식 적용
second_title: Aspose.Cells .NET Excel 처리 API
description: Aspose.Cells for .NET을 사용하여 Excel에서 멋진 3D 차트를 만드는 방법을 알아보세요. 간단한 단계별 가이드를 따르세요.
weight: 10
url: /ko/net/advanced-chart-operations/apply-3d-format-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 차트에 3D 형식 적용

## 소개

데이터 시각화가 가장 중요한 시대에, 우리가 데이터를 표현하는 방식은 기본적인 그래프와 차트를 넘어섭니다. Aspose.Cells for .NET과 같은 도구를 사용하면 주의를 끌 뿐만 아니라 정보를 효과적으로 전달하는 놀라운 3D 차트로 데이터 프레젠테이션을 향상시킬 수 있습니다. 이 가이드에서는 Aspose.Cells를 사용하여 차트에 3D 형식을 적용하는 단계를 안내하여 원시 데이터를 매력적인 디스플레이로 변환합니다.

## 필수 조건

차트에 3D 형식을 적용하는 세부적인 내용을 알아보기 전에 필요한 모든 것이 있는지 확인해 보겠습니다.

### 소프트웨어 요구 사항

- Visual Studio: .NET 애플리케이션을 사용하려면 Visual Studio가 설치되어 있는지 확인하세요.
-  .NET용 Aspose.Cells: 아직 다운로드하지 않았다면 Aspose.Cells를 다운로드하여 설치하세요.[여기](https://releases.aspose.com/cells/net/).

### 코딩 환경 설정

1. 새 .NET 프로젝트 만들기: Visual Studio를 열고 "새 프로젝트 만들기"를 선택한 다음 콘솔 응용 프로그램을 선택합니다.
2. Aspose.Cells 참조 추가: NuGet 패키지 관리자를 통해 Aspose.Cells를 검색하거나 패키지 관리자 콘솔을 통해 추가합니다.

```bash
Install-Package Aspose.Cells
```

3. 출력 디렉토리 설정: 생성된 파일이 저장될 출력 디렉토리를 지정합니다. 바탕 화면에 폴더를 만드는 것만큼 간단할 수도 있습니다.

이제 모든 준비가 끝났으니, 코드를 입력해서 눈부신 3D 차트를 만들어 볼 시간입니다!

## 패키지 가져오기

시작하려면 필요한 네임스페이스를 가져와야 합니다. 이렇게 하면 Aspose.Cells에서 제공하는 클래스와 메서드에 액세스할 수 있습니다. 방법은 다음과 같습니다.

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

이 섹션에서는 프로세스를 관리 가능한 단계로 나누어 각 단계를 명확하게 이해할 수 있도록 도와드립니다.

## 1단계: 통합 문서 초기화

 먼저 인스턴스를 생성해야 합니다.`Workbook` 클래스. 이 객체는 Excel 문서의 기초가 됩니다.

```csharp
//출력 디렉토리
string outputDir = "Your Document Directory";
Workbook book = new Workbook();
```
 이것을 생각해 보세요`Workbook` 빈 캔버스처럼—다채로운 데이터와 인상적인 시각화로 채울 수 있습니다.

## 2단계: 첫 번째 워크시트 이름 바꾸기

다음으로, 첫 번째 워크시트의 이름을 바꿔보겠습니다. 이렇게 하면 우리가 어떤 데이터로 작업하고 있는지 명확하게 알 수 있습니다.

```csharp
book.Worksheets[0].Name = "DataSheet";
```

이름은 직관적이어야 합니다. 이 경우, 데이터가 어디에 있는지 알 수 있도록 "DataSheet"라는 이름을 붙였습니다.

## 3단계: 차트에 대한 데이터 생성

이제 "DataSheet"에 데이터를 추가하겠습니다. 차트에서 사용할 값으로 채워 봅시다.

```csharp
Worksheet dataSheet = book.Worksheets["DataSheet"];
dataSheet.Cells["B1"].PutValue(1);
dataSheet.Cells["B2"].PutValue(2);
dataSheet.Cells["B3"].PutValue(3);
dataSheet.Cells["A1"].PutValue("A");
dataSheet.Cells["A2"].PutValue("B");
dataSheet.Cells["A3"].PutValue("C");
```

요리법이 재료에 따라 달라지는 것처럼, 차트의 효과도 입력 데이터의 질과 구성에 따라 달라집니다.

## 4단계: 새 차트 워크시트 설정

차트 자체에 대한 새 워크시트를 만들 시간입니다. 이렇게 하면 데이터 시각화를 체계적으로 유지하는 데 도움이 됩니다.

```csharp
Worksheet sheet = book.Worksheets.Add("MyChart");
```

이 워크시트를 귀하의 무대로 생각해보세요. 귀하의 데이터 성과가 펼쳐지는 곳입니다.

## 5단계: 차트 추가

여기서는 새로 만든 워크시트에 막대형 차트를 추가해 보겠습니다.  

```csharp
ChartCollection charts = sheet.Charts;
int chartSheetIdx = charts.Add(ChartType.Column, 5, 0, 25, 15);
```

우리는 차트에 대한 공간을 정의하고 그것이 어떤 유형인지 지정합니다. 아트워크에 대한 프레임 유형을 선택하는 것으로 생각하세요.

## 6단계: 차트 모양 사용자 지정

이제 배경색을 설정하여 차트의 모양을 사용자 지정해 보겠습니다. 

```csharp
Aspose.Cells.Charts.Chart chart = book.Worksheets["MyChart"].Charts[0];
chart.PlotArea.Area.BackgroundColor = Color.White;
chart.ChartArea.Area.BackgroundColor = Color.White;
chart.PlotArea.Area.ForegroundColor = Color.White;
chart.ChartArea.Area.ForegroundColor = Color.White;
chart.ShowLegend = false;
```

깔끔하고 흰색 배경은 데이터의 색상을 돋보이게 만들어 가시성을 높여줍니다.

## 7단계: 차트에 데이터 시리즈 추가

이제 차트에 데이터를 입력할 시간입니다. "DataSheet"에서 데이터 시리즈를 추가하여 차트가 필요한 데이터를 반영하도록 하겠습니다.

```csharp
chart.NSeries.Add("DataSheet!B1:B3", true);
chart.NSeries.CategoryData = "DataSheet!A1:A3";
```

이는 셰프가 특정 재료로 요리를 준비하는 것과 유사합니다. 각 데이터 포인트가 중요합니다!

## 8단계: 데이터 시리즈 액세스 및 포맷

이제 데이터를 연결했으니 데이터 시리즈를 가져와서 3D 효과를 적용해 보겠습니다.

```csharp
Aspose.Cells.Charts.Series ser = chart.NSeries[0];
ShapePropertyCollection spPr = ser.ShapeProperties;
Format3D fmt3d = spPr.Format3D;
```

우리는 요리에 약간의 풍미를 더할 준비를 하고 있습니다. 전반적인 풍미를 향상시키는 양념이라고 생각하시면 됩니다.

## 9단계: 3D 베벨 효과 적용

다음으로 차트에 차원감을 주기 위해 베벨 효과를 추가해 보겠습니다.

```csharp
Bevel bevel = fmt3d.TopBevel;
bevel.Type = BevelPresetType.Circle;
bevel.Height = 2;
bevel.Width = 5;
```

조각가가 돌을 조각하는 것처럼, 우리는 차트에 생명력을 불어넣는 깊이를 만들어내고 있습니다!

## 10단계: 표면 소재 및 조명 사용자 지정

차트를 밝게 빛나게 만들어 봅시다! 표면 소재와 조명 설정을 조정해 볼게요.

```csharp
fmt3d.SurfaceMaterialType = PresetMaterialType.WarmMatte;
fmt3d.SurfaceLightingType = LightRigType.ThreePoint;
fmt3d.LightingAngle = 20;
```

적절한 조명과 소재는 평평한 물체를 매혹적인 시각적 요소로 바꿀 수 있습니다. 모든 장면을 향상시키기 위해 전문적으로 조명된 영화 세트를 생각해보세요.

## 11단계: 시리즈 모습에 대한 마지막 손질

이제 색상을 조정하여 데이터 시리즈의 모양을 마무리합니다.

```csharp
ser.Area.BackgroundColor = Color.Maroon;
ser.Area.ForegroundColor = Color.Maroon;
ser.Border.Color = Color.Maroon;
```

적절한 색상은 특정한 감정과 반응을 불러일으킬 수 있습니다. 적갈색은 우아함과 세련미를 더해줍니다.

## 12단계: 통합 문서 저장

마지막으로, 걸작을 저장할 시간입니다! 저장하고 싶은 목적지를 지정하는 것을 잊지 마세요.

```csharp
book.Save(outputDir + "outputApplying3DFormat.xlsx");
Console.WriteLine("Applying3DFormat executed successfully.");
```

작품을 저장하는 것은 마치 예술 작품을 갤러리에 전시하는 것과 같습니다. 소중히 여기고 공유할 수 있는 순간입니다.

## 결론

축하합니다! Aspose.Cells for .NET을 사용하여 시각적으로 매력적인 3D 차트를 성공적으로 만들었습니다. 이러한 단계를 따르면 이제 데이터 프레젠테이션을 강화하여 정보적일 뿐만 아니라 시각적으로 매력적으로 만들 수 있는 강력한 도구가 생깁니다. 차트를 다듬을 때 각 시각화가 스토리라는 점을 기억하세요. 매력적이고 명확하며 영향력 있게 만들어 보세요!

## 자주 묻는 질문

### .NET용 Aspose.Cells란 무엇인가요?
.NET용 Aspose.Cells는 개발자가 차트와 다이어그램을 만드는 것을 포함하여 Excel 문서를 프로그래밍 방식으로 조작할 수 있는 강력한 라이브러리입니다.

### Aspose.Cells에서 차트 유형을 사용자 정의할 수 있나요?
네! Aspose.Cells는 열, 선, 원형 등 다양한 차트 유형을 지원하며, 쉽게 사용자 지정할 수 있습니다.

### Aspose.Cells의 무료 평가판이 있나요?
 물론입니다! 무료 체험판을 다운로드할 수 있습니다.[여기](https://releases.aspose.com/).

### 차트에 3D 형식 외에 다른 효과를 적용할 수 있나요?
네, 그림자, 그라데이션, 다양한 스타일 등 다양한 효과를 적용해 차트를 3D 이상으로 향상시킬 수 있습니다.

### Aspose.Cells에 대한 지원은 어디에서 찾을 수 있나요?
 지원을 받으려면 다음을 방문하세요.[Aspose 포럼](https://forum.aspose.com/c/cells/9) 지역사회에 대한 지원과 도움을 요청합니다.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
