---
title: Excel에서 위치 그림(절대)
linktitle: Excel에서 위치 그림(절대)
second_title: Aspose.Cells .NET Excel 처리 API
description: 이 포괄적인 단계별 튜토리얼을 통해 Aspose.Cells for .NET을 사용하여 Excel에서 이미지를 절대 위치에 배치하는 방법을 알아보세요.
weight: 13
url: /ko/net/excel-ole-picture-objects/position-picture-absolute-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 위치 그림(절대)

## 소개
Excel 스프레드시트에서 이미지를 올바르게 배치하는 데 어려움을 겪은 적이 있습니까? 당신만 그런 것은 아닙니다! 많은 사용자가 이런 문제에 직면합니다. 특히 데이터 시각화에 더 나은 미학이나 명확성을 위해 절대적인 위치가 필요할 때 더욱 그렇습니다. 더 이상 찾지 마세요. 이 가이드에서는 Aspose.Cells for .NET을 사용하여 Excel 워크시트에서 그림을 절대적인 위치에 배치하는 간단한 프로세스를 안내합니다. Excel 조작을 담당하는 개발자이든 보고서를 개선하려는 데이터 분석가이든, 단계별 자습서를 통해 이미지를 사용한 Excel 경험을 간소화할 수 있습니다!
## 필수 조건
코드와 세부 사항을 살펴보기 전에 준비해야 할 몇 가지 사항이 있습니다.
1.  Aspose.Cells 라이브러리: .NET용 Aspose.Cells 라이브러리의 최신 버전이 있는지 확인하세요. 다음에서 다운로드할 수 있습니다.[릴리스 페이지](https://releases.aspose.com/cells/net/).
2. 개발 환경: 작동하는 .NET 개발 환경이 설정되어 있는지 확인하세요. Visual Studio나 원하는 다른 IDE를 사용할 수 있습니다.
3. C#에 대한 기본 지식: C# 프로그래밍 언어에 대한 지식은 코드 조각을 이해하는 데 도움이 됩니다.
4. 이미지 파일: Excel 시트에 삽입할 이미지 파일(예: "logo.jpg")을 지정된 문서 디렉토리에 저장해 둡니다.

## 패키지 가져오기
시작하려면 프로젝트에 필요한 패키지를 가져오도록 합시다. 프로젝트 파일에는 다음 네임스페이스가 포함되어야 합니다.
```csharp
using System.IO;
using Aspose.Cells;
```
이러한 네임스페이스를 가져오면 프로그램에서 Aspose.Cells가 제공하는 기능을 활용할 수 있습니다.
명확성을 위해 이를 관리 가능한 단계로 나누어 보겠습니다.
## 1단계: 문서 디렉토리 설정
이 초기 단계에서는 문서가 있는 디렉토리를 정의해야 합니다. 이는 프로그램이 파일을 저장하거나 가져올 위치를 아는 데 필수적입니다. 설정 방법은 다음과 같습니다.
```csharp
string dataDir = "Your Document Directory";
```
 간단히 교체하세요`"Your Document Directory"` 이미지 파일이 있는 실제 경로와 함께. 이것은 다음과 같을 수 있습니다.`"C:\\Users\\YourUsername\\Documents\\"`.
## 2단계: 통합 문서 개체 인스턴스화
 다음으로, 새 인스턴스를 생성해야 합니다.`Workbook` 클래스. 이 객체는 Excel 파일을 나타냅니다.
```csharp
Workbook workbook = new Workbook();
```
이제 데이터와 이미지를 채울 수 있는 통합 문서가 준비되었습니다.
## 3단계: 새 워크시트 추가
이제 워크북이 있으니 워크시트를 추가해야 합니다. 여기서 이미지를 추가하고 배치하는 마법이 일어납니다.
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
 이 줄은 통합 문서 내에 새 워크시트를 만들고 해당 인덱스를 반환합니다. 이 인덱스는 변수에 저장됩니다.`sheetIndex`.
## 4단계: 새 워크시트 얻기
새로 만든 워크시트를 참조해 보겠습니다. 방금 얻은 인덱스를 사용하여 워크시트에 액세스하고 조작할 수 있습니다.
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
 이제 다음과 같이 작업할 수 있습니다.`worksheet` 이미지를 포함한 콘텐츠를 추가할 개체입니다.
## 5단계: 사진 추가
이제 흥미로운 부분입니다! 여기서 그림을 워크시트에 추가합니다. 그림을 고정할 행 및 열 인덱스를 지정합니다(이 경우, 행 5, 열 5인 셀 "F6"에 지정):
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
이 줄은 전체 워크시트에 대해 지정된 위치에 이미지를 효과적으로 잠급니다. 그러나 지금은 셀과 함께 크기 조정이 가능합니다.
## 6단계: 새로 추가된 사진에 액세스하기
그림을 더욱 조작하려면 해당 속성에 접근해야 합니다.
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
이렇게 하면 방금 추가한 이미지의 속성에 접근할 수 있습니다!
## 7단계: 그림의 절대 위치 설정
 그림을 절대적으로(픽셀 단위로) 배치하려면 다음을 사용하여 그림의 위치를 정의해야 합니다.`Left` 그리고`Top` 속성. 여기서 이미지가 나타나는 위치를 제어할 수 있습니다.
```csharp
picture.Left = 60;
picture.Top = 10;
```
필요에 따라 두 값을 조정할 수 있으며, 각각 이미지의 수평 및 수직 위치를 나타냅니다.
## 8단계: Excel 파일 저장
마지막으로 모든 수정을 마친 후에는 통합 문서를 저장할 차례입니다.
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
 이렇게 하면 이름이 지정된 Excel 파일이 생성됩니다.`book1.out.xls` 이전에 정의한 문서 디렉토리에 그림이 있는 워크시트를 절대적으로 넣으세요.

## 결론
이제 Aspose.Cells for .NET을 사용하여 절대 위치 지정으로 Excel 시트에 그림을 성공적으로 배치했습니다. 이 간단한 프로세스는 Excel 문서의 시각적 표현을 향상시킬 뿐만 아니라 셀 크기와 행 높이를 변경하더라도 이미지가 원하는 위치에 정확히 유지되도록 보장합니다. 이제 보고서를 준비하든 대시보드를 만들든 항상 그림이 완벽하게 배치되도록 할 수 있습니다.
## 자주 묻는 질문
### .NET용 Aspose.Cells란 무엇인가요?
.NET용 Aspose.Cells는 개발자가 Microsoft Excel이 없어도 Excel 스프레드시트를 프로그래밍 방식으로 만들고, 조작하고, 변환할 수 있는 .NET 라이브러리입니다.
### Aspose.Cells를 사용하여 다른 이미지 조작을 수행할 수 있나요?
네, 위치 지정 외에도 Aspose.Cells 라이브러리를 사용하면 Excel 스프레드시트 내에서 이미지의 크기를 조정하고 회전하고 수정할 수도 있습니다.
### Aspose.Cells는 무료로 사용할 수 있나요?
 Aspose.Cells는 상업용 제품이지만, 해당 사이트에서 무료 평가판을 사용할 수 있습니다.[무료 체험 페이지](https://releases.aspose.com/).
### Aspose.Cells에 대한 임시 라이선스를 얻으려면 어떻게 해야 하나요?
 임시 면허 신청은 다음을 통해 신청할 수 있습니다.[임시 라이센스 페이지](https://purchase.aspose.com/temporary-license/) Aspose에서 제공.
### 더 많은 예와 문서는 어디에서 볼 수 있나요?
 그만큼[Aspose.Cells 설명서](https://reference.aspose.com/cells/net/) 코드 예제와 더 자세한 기능을 포함한 광범위한 리소스가 포함되어 있습니다.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
