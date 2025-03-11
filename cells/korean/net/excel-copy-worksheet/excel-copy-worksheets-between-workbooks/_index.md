---
title: Excel에서 워크북 간 워크시트 복사
linktitle: Excel에서 워크북 간 워크시트 복사
second_title: .NET API 참조를 위한 Aspose.Cells
description: Aspose.Cells for .NET을 사용하여 Excel 워크북 간에 워크시트를 복사하는 방법을 알아보세요. 스프레드시트 관리를 간소화하기 위한 코드 예제가 포함된 단계별 가이드입니다.
weight: 30
url: /ko/net/excel-copy-worksheet/excel-copy-worksheets-between-workbooks/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 워크북 간 워크시트 복사

## 소개

Excel 통합 문서 간에 워크시트를 수동으로 복사하는 자신을 발견한 적이 있습니까? 단륜차를 타면서 저글링을 시도하는 것과 비슷합니다! 하지만 Aspose.Cells for .NET을 사용하면 이 작업을 간소화하고 버터를 자르는 것처럼 매끄럽게 만들 수 있습니다. 대규모 데이터 세트를 관리하든 정보를 통합해야 하든 통합 문서 간에 워크시트를 복사하면 많은 시간을 절약할 수 있습니다. 이 자습서에서는 Aspose.Cells for .NET을 사용하여 이 작업을 수행하는 방법을 정확히 보여드리겠습니다. 이 가이드를 마치면 Excel 작업을 쉽게 처리할 수 있을 것입니다.

## 필수 조건

코드를 살펴보기 전에 시작하는 데 필요한 올바른 도구가 있는지 확인해 보겠습니다.

-  .NET용 Aspose.Cells: 다운로드할 수 있습니다.[여기](https://releases.aspose.com/cells/net/).
- Visual Studio나 .NET 프레임워크를 지원하는 IDE.
-  유효한 면허증 또는[임시 면허](https://purchase.aspose.com/temporary-license/)Aspose.Cells의 전체 기능을 테스트하고 싶다면
- C# 및 .NET 프레임워크에 대한 기본적인 이해.

 또한 다음을 확인할 수도 있습니다.[Aspose.Cells 설명서](https://reference.aspose.com/cells/net/) 자세한 내용은.

## 패키지 가져오기

코딩을 시작하기 전에 필요한 패키지를 가져와야 합니다. 이는 여행을 떠나기 전에 가방을 챙기는 것과 같습니다. 원활하게 만들기 위해서는 적절한 도구가 필요합니다.

```csharp
using Aspose.Cells;
```

이 간단한 코드 줄은 Aspose.Cells 라이브러리를 가져옵니다. 이 라이브러리는 우리가 곧 작업할 모든 Excel 마법의 도구로 들어가는 관문입니다.


이제 모든 것을 설정했으니 Excel 통합 문서 간에 워크시트를 복사하는 과정을 살펴보겠습니다. 각 단계는 이해하기 쉽도록 세분화되어 있습니다. 따라서 Aspose.Cells를 처음 사용하는 분이라도 따라할 수 있을 것입니다.

## 1단계: 문서 디렉토리 설정

먼저, 파일이 어디에 있는지 정의해야 합니다. 이 단계는 보물찾기 지도를 선택하는 것으로 생각하세요. 코드에 워크북을 찾고 저장할 위치를 알려줍니다.

```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

 이 줄에서 다음을 바꾸세요.`"YOUR DOCUMENT DIRECTORY"`Excel 파일에 대한 실제 경로입니다. 여기서 통합 문서가 로드되고 저장됩니다.

## 2단계: 첫 번째 통합 문서 열기

다음으로, 복사하려는 워크시트가 들어 있는 첫 번째 워크북을 엽니다. 이것은 종이 한 장을 잡기 위해 폴더를 여는 것으로 상상해 보세요.

```csharp
string InputPath = dataDir + "book1.xls";
// 워크북을 만드세요.
// 첫 번째 책에 있는 파일을 엽니다.
Workbook excelWorkbook0 = new Workbook(InputPath);
```

 여기, 로딩 중입니다`book1.xls` (파일이 디렉토리에 있는지 확인하세요) 새로 만들기`Workbook` 객체라고 불림`excelWorkbook0`. 이것은 복사할 워크시트가 들어 있는 소스 통합 문서입니다.

## 3단계: 두 번째 통합 문서 만들기

이제 첫 번째 통합 문서를 열었으니, 복사한 워크시트를 붙여넣을 또 다른 빈 통합 문서를 만들 차례입니다. 데이터를 전송할 새 빈 노트북을 여는 것으로 생각하세요.

```csharp
// 다른 통합 문서를 만듭니다.
Workbook excelWorkbook1 = new Workbook();
```

 이 줄은 이름이 지정된 빈 통합 문서를 만듭니다.`excelWorkbook1`. 첫 번째 통합 문서에서 복사한 워크시트를 옮긴 후 해당 워크시트가 저장되는 위치입니다.

## 4단계: 워크시트 복사

마법이 온다! 이 단계에서는 실제로 첫 번째 워크북의 워크시트를 두 번째 워크북으로 복사합니다. 이것은 한 노트북에서 다른 노트북으로 노트를 옮기는 것과 같습니다.

```csharp
// 첫 번째 책의 첫 번째 시트를 두 번째 책에 복사하세요.
excelWorkbook1.Worksheets[0].Copy(excelWorkbook0.Worksheets[0]);
```

 여기서 무슨 일이 일어나고 있습니까? 코드는 첫 번째 워크시트를 가져옵니다.`excelWorkbook0` 그리고 그것을 첫 번째 시트에 복사합니다.`excelWorkbook1`. 정말 쉽죠?

## 5단계: 새 통합 문서 저장

마지막으로, 복사된 워크시트와 함께 두 번째 워크북을 저장합니다. 이것은 컴퓨터의 새 폴더에 새로 쓴 노트를 저장하는 것과 같습니다.

```csharp
// 파일을 저장합니다.
excelWorkbook1.Save(dataDir + "CopyWorksheetsBetweenWorkbooks_out.xls");
```

 이렇게 하면 복사된 워크시트가 포함된 두 번째 통합 문서가 새 파일에 저장됩니다.`CopyWorksheetsBetweenWorkbooks_out.xls`원하는 이름으로 변경하세요!

## 결론

그리고 그게 전부입니다! Aspose.Cells for .NET을 사용하여 한 Excel 통합 문서에서 다른 통합 문서로 워크시트를 성공적으로 복사했습니다. 특히 복잡하거나 큰 스프레드시트로 작업할 때 수동 복사-붙여넣기에서 벗어나는 간단한 프로세스입니다. Aspose.Cells for .NET은 시트를 복사하든, 통합 문서를 병합하든, 더 고급 작업을 수행하든 Excel 파일을 쉽게 조작할 수 있는 강력한 도구입니다.

기억하세요, 코딩은 작은 단계로 나누면 더 쉬워집니다. 그러니 다음에 Excel 파일을 관리해야 할 때 프로처럼 처리할 준비가 되어 있을 겁니다.

## 자주 묻는 질문

### 한 번에 여러 개의 워크시트를 복사할 수 있나요?

 네, 소스 워크북의 워크시트를 반복하여 대상 워크북에 복사할 수 있습니다. 각 워크시트에는 고유한`Copy` 방법.

### 이미 데이터가 있는 통합 문서에 워크시트를 복사할 수 있습니까?

물론입니다! 이미 데이터가 들어 있더라도 워크시트를 기존 워크북에 복사할 수 있습니다. 올바른 워크시트 인덱스만 지정하면 됩니다.

### 이 기능을 사용하려면 유료 라이선스가 필요합니까?

 기본 기능을 사용하려면 Aspose.Cells의 무료 버전을 사용할 수 있지만[임시 면허](https://purchase.aspose.com/temporary-license/) 또는 워터마크와 같은 제한을 피하고 모든 기능을 사용하려면 유료 라이선스를 구입해야 합니다.

### 차트와 이미지가 있는 워크시트를 복사할 수 있나요?

네! Aspose.Cells는 차트, 이미지 및 기타 개체가 포함된 워크시트 복사를 완벽하게 지원합니다. 복사 프로세스 동안 모든 것이 보존됩니다.

### 새 통합 문서의 특정 위치에 워크시트를 복사하려면 어떻게 해야 합니까?

 복사된 워크시트를 배치할 인덱스를 지정하려면 다음을 사용하십시오.`Worksheets.AddCopy` 이 방법을 사용하면 시트의 위치를 더 잘 제어할 수 있습니다.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
