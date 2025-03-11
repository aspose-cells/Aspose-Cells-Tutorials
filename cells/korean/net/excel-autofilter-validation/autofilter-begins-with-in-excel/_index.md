---
title: Excel에서 자동 필터 시작
linktitle: Excel에서 자동 필터 시작
second_title: Aspose.Cells .NET Excel 처리 API
description: 이 포괄적인 단계별 가이드를 통해 .NET에서 Aspose.Cells를 사용하여 Excel 행을 자동으로 필터링하는 방법을 손쉽게 알아보세요.
weight: 10
url: /ko/net/excel-autofilter-validation/autofilter-begins-with-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 자동 필터 시작

## 소개

데이터 작업에 있어서 Excel은 수많은 산업과 목적에 적합한 필수 애플리케이션으로 자리매김했습니다. 가장 강력한 기능 중 하나는 AutoFilter로, 방대한 데이터 세트를 손쉽게 걸러낼 수 있습니다. Aspose.Cells for .NET을 사용하는 경우 이 기능을 프로그래밍 방식으로 활용하여 데이터 관리 작업을 크게 향상시킬 수 있습니다. 이 가이드에서는 특정 문자열로 시작하는지 여부에 따라 Excel 행을 필터링하는 기능을 구현하는 과정을 안내합니다.

## 필수 조건

시작하기 전에 다음과 같은 전제 조건이 충족되었는지 확인하세요.

1. 개발 환경: .NET 개발 환경에 익숙해지세요. 이는 Visual Studio 또는 원하는 다른 IDE일 수 있습니다.
2.  Aspose.Cells for .NET: Aspose.Cells for .NET을 설치해야 합니다. 아직 설치하지 않았다면 편리하게 다운로드할 수 있습니다.[여기](https://releases.aspose.com/cells/net/).
3. C#에 대한 기본 지식: C#에 대한 기본적인 이해와 .NET 라이브러리를 사용하는 방법을 이해하면 원활하게 따라갈 수 있습니다.
4.  샘플 데이터: Excel 파일이 있어야 하며, 다음과 같은 이름이 지정되어야 합니다.`sourseSampleCountryNames.xlsx`, 지정된 소스 디렉토리에 있습니다. 이 파일에는 필터링할 데이터가 포함됩니다.
5.  라이센스: 전체 기능을 사용하려면 이 라이센스를 취득하는 것을 고려하세요.[링크](https://purchase.aspose.com/buy) . 기능을 테스트하려면 요청할 수 있습니다.[임시 면허](https://purchase.aspose.com/temporary-license/).

다 준비됐어? 가자!

## 패키지 가져오기

시작하려면 C# 파일 맨 위에 필요한 네임스페이스를 가져옵니다.

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

이는 콘솔 상호작용에 필요한 기본 시스템 기능과 함께 핵심 Aspose.Cells 기능을 가져옵니다.

이제 환경이 설정되고 필요한 패키지가 임포트되었으니, 자동 필터 기능을 관리 가능한 단계로 나누어 보겠습니다. "Ba"로 시작하는 행을 추출하는 필터를 구현할 것입니다.

## 1단계: 소스 및 출력 디렉토리 정의

먼저, 입력 Excel 파일의 위치와 필터링된 출력을 저장할 위치를 정의해 보겠습니다.

```csharp
// 소스 디렉토리
string sourceDir = "Your Document Directory\\";

// 출력 디렉토리
string outputDir = "Your Document Directory\\";
```

 설명: 여기서 교체하세요`"Your Document Directory\\"` 디렉토리의 실제 경로로. 디렉토리 경로를 이중 백슬래시(`\\`) 경로 문제를 방지합니다.

## 2단계: 통합 문서 개체 인스턴스화

다음으로, Excel 파일을 가리키는 Workbook 객체를 생성해 보겠습니다.

```csharp
// 샘플 데이터를 포함하는 Workbook 개체 인스턴스화
Workbook workbook = new Workbook(sourceDir + "sourseSampleCountryNames.xlsx");
```

 설명: 이 줄은 지정된 파일 경로를 사용하여 새 Workbook 인스턴스를 초기화합니다.`Workbook` 클래스는 전체 Excel 파일을 나타내므로 기본입니다.

## 3단계: 첫 번째 워크시트 액세스

이제 작업하려는 특정 워크시트에 액세스해야 합니다.

```csharp
// Excel 파일의 첫 번째 워크시트에 액세스하기
Worksheet worksheet = workbook.Worksheets[0];
```

 설명:`Worksheets` 컬렉션을 사용하면 개별 시트에 액세스할 수 있습니다. 사용`[0]` 일반적으로 단일 시트 파일로 작업할 때 사용되는 일반적인 관행인 Excel 파일의 첫 번째 워크시트를 참조합니다.

## 4단계: 자동 필터 설정

마법이 시작되는 곳이 여기입니다! 데이터에 대한 자동 필터 범위를 만듭니다.

```csharp
// 셀 범위를 지정하여 자동 필터 만들기
worksheet.AutoFilter.Range = "A1:A18";
```

 설명:`AutoFilter.Range` 속성을 사용하면 필터링할 행을 지정할 수 있습니다. 이 경우, 데이터를 보관하는 것으로 가정되는 A1~A18 범위 내의 행을 필터링합니다.

## 5단계: 필터 조건 적용

다음 단계는 필터 조건을 정의하는 것입니다. 첫 번째 열 값이 "Ba"로 시작하는 행만 표시하려고 합니다.

```csharp
// 문자열 "Ba"로 시작하는 행에 대한 필터를 초기화합니다.
worksheet.AutoFilter.Custom(0, FilterOperatorType.BeginsWith, "Ba");
```

 설명:`Custom` 메서드는 필터링 로직을 정의합니다. 첫 번째 인수(`0` )는 첫 번째 열(A)을 기준으로 필터링하고 있음을 나타냅니다.`FilterOperatorType.BeginsWith` "Ba"로 시작하는 행을 찾기 위한 조건을 지정합니다.

## 6단계: 필터 새로 고침

필터 조건을 적용한 후에는 변경 사항을 반영하기 위해 Excel이 새로 고쳐지는지 확인해야 합니다.

```csharp
// 필터링된 행을 표시하거나 숨기려면 필터를 새로 고칩니다.
worksheet.AutoFilter.Refresh();
```

설명: 이 줄은 자동 필터에 새로 고침을 호출하여 표시된 행이 적용된 필터 기준과 일치하는지 확인합니다. Excel에서 새로 고침 버튼을 누르는 것과 비슷합니다.

## 7단계: 수정된 Excel 파일 저장

이제 변경한 내용을 저장할 시간입니다.

```csharp
// 수정된 Excel 파일 저장하기
workbook.Save(outputDir + "outSourseSampleCountryNames.xlsx");
```

 설명:`Save` 방법은 수정된 Workbook을 지정된 출력 경로에 다시 씁니다. 이는 정의된 필터를 새 파일에 쓰는 것에 속하므로 원래 데이터는 그대로 유지됩니다.

## 8단계: 출력 확인

마지막으로, 작업이 성공적으로 완료되었는지 확인해 보겠습니다.

```csharp
Console.WriteLine("AutofilterBeginsWith executed successfully.\r\n");
```

설명: 이 간단한 줄은 필터링 프로세스가 오류 없이 완료되었음을 알려주는 확인 메시지를 콘솔에 출력합니다.

## 결론

데이터 관리가 압도적으로 느껴질 수 있는 세상에서 Aspose.Cells for .NET을 통해 Excel의 AutoFilter와 같은 기능을 마스터하면 효율적이고 효과적으로 데이터를 조작할 수 있습니다. "Ba"로 시작하는 Excel 행을 필터링하는 방법을 배웠고, 단계별로 방법을 구현했습니다. 연습을 통해 진행 중인 프로젝트에서 다양한 데이터 필터링 요구 사항에 맞게 이 방법을 적용할 수 있습니다.

## 자주 묻는 질문

### Excel에서 자동 필터의 목적은 무엇입니까?  
자동 필터를 사용하면 사용자가 스프레드시트에서 데이터를 빠르게 정렬하고 필터링하여 특정 데이터 세트에 쉽게 집중할 수 있습니다.

### Aspose.Cells를 사용하여 여러 기준에 따라 필터링할 수 있나요?  
네, Aspose.Cells는 여러 기준을 설정할 수 있는 고급 필터링 옵션을 지원합니다.

### Aspose.Cells를 사용하려면 라이선스가 필요합니까?  
무료 체험판으로 시작할 수 있지만, 모든 기능을 사용하고 체험판 제한을 제거하려면 라이선스가 필요합니다.

### Aspose.Cells를 사용하여 어떤 유형의 필터링을 수행할 수 있나요?  
값, 조건(시작 문자 또는 종료 문자 등) 및 사용자 정의 필터링을 기준으로 데이터를 필터링하여 특정 요구 사항을 충족할 수 있습니다.

### .NET용 Aspose.Cells에 대한 자세한 정보는 어디에서 찾을 수 있나요?  
 문서를 확인할 수 있습니다[여기](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
