---
"description": "Aspose.Cells for .NET을 사용하여 Excel에서 원형 차트를 만드는 방법을 단계별 가이드를 통해 알아보세요. 데이터를 손쉽게 시각화해 보세요."
"linktitle": "파이 차트 만들기"
"second_title": "Aspose.Cells .NET Excel 처리 API"
"title": "파이 차트 만들기"
"url": "/ko/net/manipulating-chart-types/create-pie-chart/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 파이 차트 만들기

## 소개

차트 만들기는 데이터를 시각적으로 표현하는 데 필수적이며, 원형 차트는 부분이 어떻게 전체를 구성하는지 보여주는 가장 널리 사용되는 방법 중 하나입니다. Aspose.Cells for .NET을 사용하면 Excel 파일에서 원형 차트 생성을 쉽게 자동화할 수 있습니다. 이 튜토리얼에서는 Aspose.Cells for .NET을 사용하여 원형 차트를 처음부터 만드는 방법을 단계별 가이드를 통해 쉽고 간편하게 만들어 보겠습니다. 이 도구를 처음 사용하는 분이든 Excel 자동화 기술을 향상시키고 싶은 분이든, 이 가이드가 도움이 될 것입니다!

## 필수 조건

코드를 살펴보기 전에 다음 사항이 설정되어 있는지 확인하세요.

1. Aspose.Cells for .NET 라이브러리: 프로젝트에 Aspose.Cells가 설치되어 있는지 확인하세요. 아직 설치하지 않으셨다면 다음에서 다운로드할 수 있습니다. [여기](https://releases.aspose.com/cells/net/).
2. .NET 개발 환경: 프로젝트가 .NET Framework 또는 .NET Core를 사용하도록 설정되어 있는지 확인하세요.
3. C#에 대한 기본 지식: C# 프로그래밍, 특히 객체 지향 프로그래밍(OOP)에 익숙해야 합니다.

고급 사용자의 경우 임시 라이선스를 적용하여 Aspose.Cells의 모든 기능을 사용할 수 있습니다. 다음에서 라이선스를 요청할 수 있습니다. [여기](https://purchase.aspose.com/temporary-license/).

## 패키지 가져오기

시작하려면 이 튜토리얼에 필요한 네임스페이스와 패키지를 가져오세요. 여기에는 기본 I/O 작업과 Aspose.Cells 패키지가 포함됩니다.

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

## 1단계: 새 통합 문서 만들기

먼저 인스턴스를 생성해야 합니다. `Workbook` Excel 파일을 나타내는 클래스입니다. 통합 문서에는 여러 개의 시트가 포함되어 있으며, 이 예제에서는 두 개의 시트를 사용합니다. 하나는 데이터용이고 다른 하나는 원형 차트용입니다.

```csharp
Workbook workbook = new Workbook();
```

이렇게 하면 새 Excel 통합 문서가 초기화됩니다. 그런데 데이터는 어디에 저장될까요? 다음 단계에서 이 부분을 처리해 보겠습니다.

## 2단계: 워크시트에 데이터 추가

통합 문서가 생성되면 첫 번째 워크시트에 접근하여 이름을 지정해야 합니다. 여기에 원형 차트에 필요한 데이터를 입력합니다.

```csharp
Worksheet sheet = workbook.Worksheets[0];
sheet.Name = "Data";
Cells cells = sheet.Cells;
```

이제 다양한 지역을 나타내는 더미 판매 데이터를 입력할 수 있습니다.

```csharp
cells["A1"].PutValue("Region");
cells["A2"].PutValue("France");
cells["A3"].PutValue("Germany");
cells["A4"].PutValue("England");
cells["A5"].PutValue("Sweden");
cells["A6"].PutValue("Italy");
cells["A7"].PutValue("Spain");
cells["A8"].PutValue("Portugal");

cells["B1"].PutValue("Sales");
cells["B2"].PutValue(70000);
cells["B3"].PutValue(55000);
cells["B4"].PutValue(30000);
cells["B5"].PutValue(40000);
cells["B6"].PutValue(35000);
cells["B7"].PutValue(32000);
cells["B8"].PutValue(10000);
```

여기서는 두 개의 열을 추가합니다. 하나는 지역별 열이고 다른 하나는 매출 실적 열입니다. 이 데이터는 원형 차트에 표시됩니다.

## 3단계: 차트 시트 추가

다음으로, 파이 차트를 보관할 별도의 워크시트를 추가해 보겠습니다.

```csharp
int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
Worksheet chartSheet = workbook.Worksheets[sheetIndex];
chartSheet.Name = "Chart";
```

이 새 시트에는 원형 차트가 호스팅됩니다. "차트"와 같은 이름을 지정하면 사용자가 파일을 열 때 어떤 내용이 표시되는지 쉽게 알 수 있습니다.

## 4단계: 원형 차트 만들기

이제 실제 차트를 만들 차례입니다. 원형 차트를 만들고 싶다는 내용과 시트에서의 위치를 정의하겠습니다.

```csharp
int chartIndex = chartSheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pie, 5, 0, 25, 10);
Aspose.Cells.Charts.Chart chart = chartSheet.Charts[chartIndex];
```

방법 `Add()` 차트 유형에 대한 매개변수를 허용합니다(이 경우, `ChartType.Pie`), 그리고 워크시트에서의 위치입니다. 숫자는 행과 열의 위치를 나타냅니다.

## 5단계: 차트 모양 사용자 지정

원형 차트는 약간의 맞춤 설정이 없이는 완성될 수 없습니다! 색상, 레이블, 제목을 조정하여 차트를 시각적으로 멋지게 만들어 보겠습니다.

### 차트 제목 설정
```csharp
chart.Title.Text = "Sales By Region";
chart.Title.Font.Color = Color.Blue;
chart.Title.Font.IsBold = true;
chart.Title.Font.Size = 12;
```

### 플롯 영역 사용자 정의
```csharp
chart.PlotArea.Area.ForegroundColor = Color.Coral;
chart.PlotArea.Area.FillFormat.SetTwoColorGradient(Color.Yellow, Color.White, GradientStyleType.Vertical, 2);
chart.PlotArea.Border.IsVisible = false;
```

플롯 영역에 그래디언트 채우기를 설정하고 테두리를 숨겨서 더 깔끔한 모양을 만듭니다.

## 6단계: 차트 데이터 정의

이제 차트를 데이터에 연결할 차례입니다. `NSeries` 차트의 속성은 판매 수치와 지역을 파이 차트에 연결합니다.

```csharp
chart.NSeries.Add("Data!B2:B8", true);
chart.NSeries.CategoryData = "Data!A2:A8";
chart.NSeries.IsColorVaried = true;
```

첫 번째 줄은 셀의 판매 데이터를 사용한다는 것을 지정합니다. `B2:B8`. 또한 차트에 지역 이름을 사용하도록 지시합니다. `A2:A8` 카테고리 라벨로.

## 7단계: 데이터 레이블 추가

차트 세그먼트에 직접 레이블을 추가하면 이해하기가 더 쉬워집니다. 원형 차트 슬라이스에 지역 이름과 매출 값을 포함시켜 보겠습니다.

```csharp
for (int i = 0; i < chart.NSeries.Count; i++)
{
    DataLabels labels = chart.NSeries[i].DataLabels;
    labels.ShowCategoryName = true;
    labels.ShowValue = true;
    labels.Position = LabelPositionType.InsideBase;
}
```

## 8단계: 차트 영역 및 범례 사용자 지정

마지막으로 차트 영역과 범례를 마무리해 보겠습니다. 이렇게 하면 차트의 전반적인 표현이 더욱 향상됩니다.

### 차트 영역
```csharp
ChartArea chartArea = chart.ChartArea;
chartArea.Area.Formatting = FormattingType.Custom;
chartArea.Area.FillFormat.Texture = TextureType.BlueTissuePaper;
```

### 전설
```csharp
Legend legend = chart.Legend;
legend.Position = LegendPositionType.Left;
legend.Font.IsBold = true;
legend.Border.Color = Color.Blue;
legend.Area.FillFormat.Texture = TextureType.Bouquet;
```

## 9단계: 통합 문서 저장

마지막으로 통합 문서를 Excel 파일로 저장합니다. 필요에 따라 출력 디렉터리와 파일 이름을 지정할 수 있습니다.

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## 결론

Aspose.Cells for .NET을 사용하면 원형 차트를 만드는 과정이 간단하고 사용자 정의가 가능합니다. 이 가이드를 따라 하면 몇 단계만으로 귀중한 통찰력을 전달하는 전문적인 차트를 만들 수 있습니다. 비즈니스 보고든 교육 목적이든, 차트 제작을 마스터하면 Excel 자동화 기술이 향상됩니다. Aspose.Cells는 멋지고 데이터 기반의 Excel 파일을 손쉽게 만드는 데 필요한 유연성을 제공합니다.

## 자주 묻는 질문

### Aspose.Cells for .NET을 사용하여 다른 유형의 차트를 만들 수 있나요?
네! Aspose.Cells는 막대형 차트, 선형 차트, 산점도 등 다양한 차트 유형을 지원합니다.

### Aspose.Cells for .NET을 사용하려면 유료 라이선스가 필요합니까?
일부 제한 사항이 있는 무료 버전을 사용할 수 있습니다. 모든 기능을 사용하려면 라이선스가 필요하며, 라이선스는 구매하실 수 있습니다. [여기](https://purchase.aspose.com/buy).

### 차트를 PDF나 이미지 등의 형식으로 내보낼 수 있나요?
물론입니다! Aspose.Cells를 사용하면 PDF, PNG 등 다양한 형식으로 차트를 내보낼 수 있습니다.

### 각 파이 조각에 다른 색상을 적용하는 것이 가능할까요?
예, 각 슬라이스에 다른 색상을 적용할 수 있습니다. `IsColorVaried` 재산에 `true`튜토리얼에서 보여준 대로.

### 하나의 통합 문서에서 여러 차트 생성을 자동화할 수 있나요?
네, 하나의 Excel 파일 내에서 필요한 만큼 많은 차트를 만들고 사용자 지정할 수 있습니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}