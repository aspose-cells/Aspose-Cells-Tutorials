---
title: Excel에서 런타임에 조건부 서식 적용
linktitle: Excel에서 런타임에 조건부 서식 적용
second_title: Aspose.Cells .NET Excel 처리 API
description: 이 포괄적인 단계별 가이드를 통해 Aspose.Cells for .NET을 사용하여 Excel에서 런타임에 조건부 서식을 적용하는 방법을 알아보세요.
weight: 11
url: /ko/net/excel-conditional-formatting/applying-conditional-formatting-at-runtime/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 런타임에 조건부 서식 적용

## 소개

데이터 분석 및 시각화를 위한 강력한 도구입니다. Excel의 두드러진 기능 중 하나는 조건부 서식으로, 사용자가 값에 따라 셀에 특정 서식 스타일을 적용할 수 있습니다. 이를 통해 추세를 파악하고, 중요한 데이터 포인트를 강조하거나, 단순히 데이터를 더 읽기 쉽게 만드는 것이 더 쉬워질 수 있습니다. Excel 파일에서 조건부 서식을 프로그래밍 방식으로 구현하려는 경우 올바른 위치에 있습니다! 이 가이드에서는 Aspose.Cells for .NET을 사용하여 런타임에 조건부 서식을 적용하는 방법을 살펴보겠습니다.

## 필수 조건
코드를 살펴보기 전에 시작하는 데 필요한 모든 것이 있는지 확인해 보겠습니다.

1. Visual Studio: 컴퓨터에 Visual Studio가 설치되어 있는지 확인하세요. .NET 개발을 지원하는 모든 버전을 사용할 수 있습니다.
2.  Aspose.Cells for .NET: Aspose.Cells for .NET이 설치되어 있어야 합니다. 다음에서 다운로드할 수 있습니다.[Aspose 웹사이트](https://releases.aspose.com/cells/net/).
3. C#에 대한 기본 지식: C# 프로그래밍에 익숙하면 코드 조각을 더 잘 이해하는 데 도움이 됩니다.
4. .NET Framework: 프로젝트가 호환되는 .NET Framework 버전을 대상으로 하는지 확인하세요.

이제 전제 조건을 충족했으니, 재미있는 부분으로 넘어가보죠!

## 패키지 가져오기
Aspose.Cells를 시작하려면 C# 프로젝트에서 필요한 네임스페이스를 가져와야 합니다. 방법은 다음과 같습니다.

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

이러한 네임스페이스를 사용하면 Excel 파일을 조작하고 조건부 서식을 적용하는 데 필요한 클래스와 메서드에 액세스할 수 있습니다.

이제 조건부 서식을 적용하는 과정을 관리하기 쉬운 단계로 나누어 보겠습니다.

## 1단계: 프로젝트 설정
우선, Visual Studio에서 새 C# 프로젝트를 만들어야 합니다. 방법은 다음과 같습니다.

1. Visual Studio를 열고 파일 > 새로 만들기 > 프로젝트를 선택합니다.
2. 콘솔 앱(.NET Framework)을 선택하고 프로젝트 이름을 지정합니다.
3. 만들기를 클릭합니다.

## 2단계: Aspose.Cells 참조 추가
프로젝트가 설정되면 Aspose.Cells 라이브러리에 대한 참조를 추가해야 합니다.

1. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 버튼으로 클릭합니다.
2. NuGet 패키지 관리를 선택합니다.
3. Aspose.Cells를 검색하여 설치하세요.

이렇게 하면 Aspose.Cells 라이브러리가 제공하는 모든 기능을 사용할 수 있습니다.

## 3단계: 통합 문서 개체 만들기
다음으로, 새로운 워크북과 워크시트를 만들어 보겠습니다. 여기서 모든 마법이 일어납니다.

```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "Your Document Directory";
string filePath = dataDir + "Book1.xlsx";

// Workbook 개체 인스턴스화
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

이 단계에서는 Excel 파일이 저장될 디렉토리를 정의하고, 새 통합 문서를 만들고, 첫 번째 워크시트에 액세스합니다.

## 4단계: 조건부 서식 추가
이제 조건부 서식을 추가해 보겠습니다. 빈 조건부 서식 객체를 만드는 것으로 시작하겠습니다.

```csharp
// 빈 조건부 서식을 추가합니다
int index = sheet.ConditionalFormattings.Add();
FormatConditionCollection fcs = sheet.ConditionalFormattings[index];
```

여기서는 서식 규칙을 보관할 새로운 조건부 서식 컬렉션을 워크시트에 추가합니다.

## 5단계: 형식 범위 정의
다음으로, 조건부 서식을 적용할 셀 범위를 지정해야 합니다. 첫 번째 행과 두 번째 열을 서식 지정하고 싶다고 가정해 보겠습니다.

```csharp
// 조건부 서식 범위를 설정합니다.
CellArea ca = new CellArea();
ca.StartRow =0;
ca.EndRow =0;
ca.StartColumn =0;
ca.EndColumn =0;
fcs.AddArea(ca);

ca = new CellArea();
ca.StartRow =1;
ca.EndRow =1;
ca.StartColumn =1;
ca.EndColumn =1;
fcs.AddArea(ca);
```

이 코드에서 우리는 조건부 서식을 위한 두 영역을 정의합니다. 첫 번째 영역은 (0,0)에 있는 셀을 위한 것이고 두 번째 영역은 (1,1)을 위한 것입니다. 여러분의 특정 요구 사항에 따라 이 범위를 자유롭게 조정하세요!

## 6단계: 조건부 서식 조건 추가
이제 서식에 대한 조건을 정의할 시간입니다. 값에 따라 셀을 강조 표시하고 싶다고 가정해 보겠습니다.

```csharp
// 조건을 추가합니다.
int conditionIndex = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "=A2", "100");

// 조건을 추가합니다.
int conditionIndex2 = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "50", "100");
```

 이 단계에서는 두 가지 조건을 추가합니다. 하나는 다음 사이의 값에 대한 조건입니다.`A2` 그리고`100` , 그리고 또 다른 것은 사이의 값입니다.`50` 그리고`100`이를 통해 값에 따라 셀을 동적으로 강조 표시할 수 있습니다.

## 7단계: 서식 스타일 설정
조건이 정해졌으므로 이제 서식 스타일을 설정할 수 있습니다. 조건의 배경색을 변경해 보겠습니다.

```csharp
// 배경색을 설정합니다.
FormatCondition fc = fcs[conditionIndex];
fc.Style.BackgroundColor = Color.Red;
```

여기서는 첫 번째 조건의 배경색을 빨간색으로 설정합니다. 필요에 따라 글꼴 색상, 테두리 및 기타 스타일을 변경하여 이를 추가로 사용자 지정할 수 있습니다!

## 8단계: Excel 파일 저장
마지막으로, 작업을 저장할 시간입니다! 지정된 디렉토리에 통합 문서를 저장합니다.

```csharp
// Excel 파일 저장하기
workbook.Save(dataDir + "output.xls");
```

이 코드 줄은 조건부 서식이 적용된 Excel 파일을 저장합니다. 출력 파일에 지정된 디렉토리를 확인하세요!

## 결론
이제 Aspose.Cells for .NET을 사용하여 Excel에서 런타임에 조건부 서식을 성공적으로 적용했습니다. 이 강력한 라이브러리를 사용하면 Excel 파일을 프로그래밍 방식으로 쉽게 조작하여 지루한 작업을 자동화하고 데이터 프레젠테이션을 향상시킬 수 있습니다. 소규모 프로젝트에서든 대규모 애플리케이션에서든 Aspose.Cells는 워크플로를 간소화하고 생산성을 개선하는 데 도움이 될 수 있습니다.

## 자주 묻는 질문

### Aspose.Cells란 무엇인가요?
Aspose.Cells는 개발자가 Excel 파일을 프로그래밍 방식으로 만들고, 조작하고, 변환할 수 있는 .NET 라이브러리입니다.

### Aspose.Cells를 다른 프로그래밍 언어와 함께 사용할 수 있나요?
네, Aspose.Cells는 Java, Python 등 여러 프로그래밍 언어로 사용할 수 있습니다.

### Aspose.Cells의 무료 평가판이 있나요?
 네, 무료 평가판을 다운로드할 수 있습니다.[Aspose 웹사이트](https://releases.aspose.com/).

### Aspose.Cells에 대한 지원은 어떻게 받을 수 있나요?
 방문하면 지원을 받을 수 있습니다.[Aspose 지원 포럼](https://forum.aspose.com/c/cells/9).

### Aspose.Cells를 사용하려면 라이선스가 필요한가요?
 예, 상업적 사용에는 라이센스가 필요하지만 임시 라이센스를 요청할 수 있습니다.[여기](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
