---
title: 워크시트의 분할 창
linktitle: 워크시트의 분할 창
second_title: .NET API 참조를 위한 Aspose.Cells
description: Aspose.Cells for .NET에서 워크시트 창을 분할하는 방법을 단계별 가이드로 알아보세요. 이 간단한 튜토리얼로 Excel 파일 탐색을 개선하세요.
weight: 130
url: /ko/net/excel-display-settings-csharp-tutorials/split-panes-of-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 워크시트의 분할 창

## 소개

Aspose.Cells for .NET을 사용하여 Excel 워크시트의 창을 분할할 준비가 되셨나요? 상상해보세요. 거대한 Excel 시트가 있고, 어떤 열에서 작업하고 있는지 기억하기 위해 헤더로 계속 스크롤하는 데 지쳐 있습니다. "Split Panes"를 입력하세요. 이 편리한 기능을 사용하면 워크시트의 일부를 고정하여 탐색하기가 훨씬 쉬워집니다. 재무 데이터, 재고 관리 또는 방대한 데이터 세트로 작업하든 창을 분할하면 생산성이 10배 향상될 수 있습니다. 

## 필수 조건

스프레드시트 마법사처럼 창을 나누기 전에, 설정을 제대로 해봅시다. 필요한 것은 다음과 같습니다.

-  Aspose.Cells for .NET: 다운로드하고 설치했는지 확인하세요. 아직 설치하지 않았다면 받으세요[여기](https://releases.aspose.com/cells/net/).
- .NET Framework: 이 가이드에서는 .NET 환경에서 작업하고 있다고 가정합니다.
- Excel 통합 문서: 이 기능의 작동 방식을 보여주기 위해 샘플 Excel 파일을 사용해 보겠습니다.
-  임시 또는 전체 라이센스: Aspose.Cells에는 라이센스가 필요합니다. 방금 시도해 보는 경우 다음을 얻으십시오.[무료 임시 라이센스](https://purchase.aspose.com/temporary-license/) 평가 제한을 피하기 위해.

## 패키지 가져오기

코드로 들어가기 전에 먼저 필요한 네임스페이스를 임포트해 보겠습니다. Aspose.Cells에서 이것을 포함하지 않고는 아무것도 할 수 없습니다.

```csharp
using System.IO;
using Aspose.Cells;
```

이제 기본적인 사항은 다루었으니, 흥미로운 부분인 유리창 나누기로 넘어가겠습니다!

## 1단계: 통합 문서 인스턴스화

 이 프로세스의 첫 번째 단계는 다음을 만드는 것입니다.`Workbook` 개체는 수정하려는 Excel 파일을 나타냅니다. 이 경우 디렉토리에서 파일을 로드합니다. 이것은 캔버스이며, 마법을 부릴 Excel 시트입니다.

창을 나누기 전에 작업할 워크북이 필요합니다! 이 단계는 책을 읽기 전에 책을 여는 것만큼 필수적입니다.

```csharp
// 문서 디렉토리 경로
string dataDir = "YOUR DOCUMENT DIRECTORY";

// 새 통합 문서를 인스턴스화하고 템플릿 파일을 엽니다.
Workbook book = new Workbook(dataDir + "Book1.xls");
```

 위의 코드에서 다음을 바꾸세요.`"YOUR DOCUMENT DIRECTORY"` Excel 파일이 있는 실제 경로와 함께.`Workbook`클래스는 Excel 파일을 메모리에 로드합니다.

## 2단계: 활성 셀 설정

 통합 문서를 로드한 후 활성 셀을 설정할 차례입니다. Excel 용어로 활성 셀은 현재 선택되어 있거나 포커스가 있는 셀입니다. 이 자습서에서는 셀을 선택합니다.`A20` 첫 번째 워크시트에서.

활성 셀을 설정하는 것은 중요합니다. 왜냐하면 패널 분할이 이 활성 셀에서 시작되기 때문입니다. 피자를 처음 자를 곳을 선택하는 것과 같습니다. 조각을 선택하세요!

```csharp
// 활성 셀 설정
book.Worksheets[0].ActiveCell = "A20";
```

 이 코드 조각은 다음을 만듭니다.`A20` 활성 셀입니다. 이 지점을 중심으로 분할이 발생하기 때문에 중요합니다. Excel에서 탐색이 종종 특정 셀을 중심으로 이루어지는 방식과 마찬가지입니다.

## 3단계: 워크시트 분할

이제 활성 셀이 설정되었으니, 재밌는 부분인 워크시트 분할로 넘어가겠습니다! 이 단계에서 마법이 일어납니다. 워크시트를 여러 창으로 나누어 더 쉽게 보고 탐색할 수 있습니다.

이것은 전체 튜토리얼의 핵심입니다. 워크시트를 분할하면 헤더나 다른 중요한 영역을 놓치지 않고 Excel 시트의 여러 섹션을 스크롤할 수 있는 별도의 창을 만들 수 있습니다.

```csharp
// 워크시트 창 분할
book.Worksheets[0].Split();
```

 와 함께`Split()` 이 방법을 사용하면 Aspose.Cells에 활성 셀에서 워크시트를 분할하도록 지시합니다.`A20` 이 경우). 이 지점에서 Excel은 사용자가 독립적으로 탐색할 수 있도록 창을 구분하는 구분선을 시트에 만듭니다.

## 4단계: 통합 문서 저장

창을 분할한 후에는 작업을 저장하는 것만 남았습니다. 이 마지막 단계에서는 변경 사항이 지정된 출력 파일에 저장되도록 합니다.

당신이 그것을 저장하지 않는다면 당신의 모든 노고가 무슨 소용이 있습니까? 저장은 당신의 아름답게 갈라진 유리창이 미래에 사용할 수 있도록 그대로 유지되도록 보장합니다.

```csharp
// Excel 파일을 저장하세요
book.Save(dataDir + "output.xls");
```

 여기서,`Save()` 이 방법은 새로 분할된 창이 있는 통합 문서를 출력 Excel 파일에 저장합니다. 변경한 내용은 이제 귀하 또는 다른 사람이 사용할 수 있습니다.

## 결론

이제 다 알게 되었습니다! 방금 Aspose.Cells for .NET을 사용하여 Excel 워크시트에서 창을 분할하는 방법을 배웠습니다. 더 이상 끝없이 스크롤하거나 데이터를 추적하지 못할 필요가 없습니다. 이 방법을 사용하면 대용량 Excel 파일을 훨씬 덜 힘들고 훨씬 더 효율적으로 처리할 수 있습니다. 창을 분할할 수 있으므로 복잡한 스프레드시트에서 작업하는 동안 중요한 데이터 포인트를 추적할 수 있습니다.

## 자주 묻는 질문

### 두 개 이상의 창을 나눌 수 있나요?  
 예, 다른 활성 셀을 지정하고 다음을 호출하여 워크시트를 여러 창으로 분할할 수 있습니다.`Split()` 방법.

### 유리창을 나누는 것과 유리창을 얼리는 것의 차이점은 무엇인가요?  
창을 분할하면 두 창에서 독립적으로 스크롤할 수 있습니다. 창을 고정하면 헤더나 특정 행/열이 잠기므로 스크롤할 때 계속 표시됩니다.

### 적용 후 갈라진 부분을 제거할 수 있나요?  
네, 통합 문서를 닫았다가 다시 열거나 프로그래밍 방식으로 다시 설정하면 분할을 제거할 수 있습니다.

### 다른 Excel 파일 형식(XLS, XLSX)에서도 창 분할이 동일하게 작동합니까?  
 네,`Split()` 이 방법은 XLS와 XLSX 형식 모두에 적용됩니다.

### 라이선스 없이 Aspose.Cells를 사용할 수 있나요?  
 네, 하지만 제한이 있습니다. 전체 경험을 위해서는 다음을 사용하는 것이 가장 좋습니다.[일시적인](https://purchase.aspose.com/temporary-license/) 또는[유료 라이센스](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
