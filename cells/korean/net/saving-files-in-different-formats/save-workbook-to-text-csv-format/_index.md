---
title: 통합 문서를 텍스트 CSV 형식으로 저장
linktitle: 통합 문서를 텍스트 CSV 형식으로 저장
second_title: Aspose.Cells .NET Excel 처리 API
description: 이 포괄적이고 단계별 튜토리얼은 .NET 개발자를 대상으로 설계되었으며, Aspose.Cells를 사용하여 Excel 통합 문서를 CSV 형식으로 손쉽게 변환하는 방법을 알아봅니다.
weight: 17
url: /ko/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 통합 문서를 텍스트 CSV 형식으로 저장

## 소개
데이터를 다룰 때, 선택하는 형식은 실제로 얼마나 쉽게 작업할 수 있는지를 결정할 수 있습니다. 표 형식 데이터를 처리하는 가장 일반적인 형식 중 하나는 CSV(쉼표로 구분된 값)입니다. Excel 파일을 사용하여 작업하는 개발자이고 통합 문서를 CSV 형식으로 변환해야 하는 경우 Aspose.Cells for .NET은 이 작업을 단순화하는 환상적인 라이브러리입니다. 이 자습서에서는 Excel 통합 문서를 텍스트 CSV 형식으로 원활하게 변환하는 단계를 분석합니다.
## 필수 조건
본격적으로 시작하기에 앞서, 시작하는 데 필요한 모든 것이 준비되었는지 확인해 보겠습니다.
1. C#과 .NET에 대한 기본 지식: C#로 코드를 작성하므로 해당 언어와 .NET 프레임워크에 대한 지식이 필수적입니다.
2. Aspose.Cells 라이브러리: 개발 환경에 Aspose.Cells for .NET 라이브러리가 설치되어 있는지 확인하세요. 다운로드할 수 있습니다.[여기](https://releases.aspose.com/cells/net/).
3. Visual Studio 또는 모든 C# IDE: 코드를 작성하고 실행하려면 통합 개발 환경(IDE)이 필요합니다. Visual Studio가 인기 있는 선택입니다.
4. Excel 통합 문서: 변환을 테스트하기 위해 일부 데이터가 포함된 샘플 Excel 통합 문서(예: "book1.xls")를 준비합니다.
## 패키지 가져오기
이제 전제 조건을 충족했으므로 프로세스의 첫 번째 단계는 필요한 패키지를 가져오는 것입니다. C# 프로젝트에서 코드 파일 맨 위에 다음 네임스페이스를 포함해야 합니다.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
이러한 네임스페이스를 사용하면 Excel 파일을 다루고 메모리 스트림을 관리하는 데 필요한 클래스와 메서드에 액세스할 수 있습니다.
## 1단계: 문서 디렉토리 경로 정의
프로세스의 첫 번째 단계는 문서(Excel 워크북)가 저장되는 위치를 정의하는 것입니다. 이는 프로그램이 처리해야 하는 파일을 어디에서 찾을 수 있는지 알 수 있게 해주기 때문에 필수적입니다. 
```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "Your Document Directory";
```
 교체를 꼭 해주세요`"Your Document Directory"` "book1.xls" 파일이 있는 실제 경로와 함께. 이는 컴퓨터의 디렉토리 또는 서버 경로일 수 있습니다.
## 2단계: 소스 워크북 로드
다음으로, CSV 형식으로 변환할 Excel 통합 문서를 로드해야 합니다.
```csharp
// 소스 통합 문서 로드
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
 그만큼`Workbook` Aspose.Cells 라이브러리의 클래스는 Excel 통합 문서의 조작 및 액세스를 허용합니다. 파일 경로를 전달하면 지정된 통합 문서를 처리하기 위해 로드합니다.
## 3단계: 통합 문서 데이터에 대한 바이트 배열 초기화
통합 문서를 CSV로 변환하기 전에 먼저 모든 워크시트 데이터를 보관할 빈 바이트 배열을 초기화해야 합니다.
```csharp
// 0바이트 배열
byte[] workbookData = new byte[0];
```
이 바이트 배열은 각 워크시트의 데이터를 단일 구조로 결합하여 나중에 파일에 쓸 수 있습니다.
## 4단계: 텍스트 저장 옵션 설정
이제 텍스트 형식을 저장하는 방법에 대한 옵션을 설정해 보겠습니다. 사용자 지정 구분 기호를 선택하거나 탭을 고수할 수 있습니다.
```csharp
// 텍스트 저장 옵션. 모든 유형의 구분 기호를 사용할 수 있습니다.
TxtSaveOptions opts = new TxtSaveOptions();
opts.Separator = '\t'; // 탭을 구분 기호로 설정
```
 이 예에서 우리는 구분 기호로 탭 문자를 사용하고 있습니다. 다음을 바꿀 수 있습니다.`'\t'` 쉼표(,)와 같이 원하는 문자로 입력할 수 있습니다.`,`), CSV 형식을 어떻게 지정하고 싶은지에 따라 달라집니다.
## 5단계: 각 워크시트 반복
 다음으로, 통합 문서 내의 모든 워크시트를 반복하여 각각을 저장합니다.`workbookData` 배열을 사용하려면 먼저 어떤 워크시트에서 작업할지 선택해야 합니다.
```csharp
// 통합 문서 데이터 배열 내부의 텍스트 형식으로 각 워크시트 데이터를 복사합니다.
for (int idx = 0; idx < workbook.Worksheets.Count; idx++)
{
    // 활성 워크시트를 텍스트 형식으로 저장
    MemoryStream ms = new MemoryStream();
    workbook.Worksheets.ActiveSheetIndex = idx;
    workbook.Save(ms, opts);
```
 루프는 통합 문서의 각 워크시트를 통과합니다.`ActiveSheetIndex` 루프를 통과할 때마다 현재 워크시트를 저장하도록 설정됩니다. 결과는 다음을 사용하여 메모리에 저장됩니다.`MemoryStream`.
## 6단계: 워크시트 데이터 검색
 워크시트를 메모리 스트림에 저장한 후 다음 단계는 이 데이터를 검색하여 우리의`workbookData` 정렬.
```csharp
    // 워크시트 데이터를 시트 데이터 배열에 저장합니다.
    ms.Position = 0; // 메모리 스트림 위치 재설정
    byte[] sheetData = ms.ToArray(); // 바이트 배열을 가져옵니다
```
`ms.Position = 0;` 쓰기 후 읽기 위치를 재설정합니다. 그런 다음 사용합니다.`ToArray()` 메모리 스트림을 워크시트 데이터를 보관하는 바이트 배열로 변환합니다.
## 7단계: 워크시트 데이터 결합
 이제 각 워크시트의 데이터를 하나로 결합합니다.`workbookData` 배열은 이전에 초기화되었습니다.
```csharp
    // 이 워크시트 데이터를 통합 문서 데이터 배열로 결합합니다.
    byte[] combinedArray = new byte[workbookData.Length + sheetData.Length];
    Array.Copy(workbookData, 0, combinedArray, 0, workbookData.Length);
    Array.Copy(sheetData, 0, combinedArray, workbookData.Length, sheetData.Length);
    workbookData = combinedArray;
}
```
기존 통합 문서 데이터와 새 워크시트 데이터를 모두 보관할 수 있을 만큼 큰 새 배열을 만듭니다. 그런 다음 기존 데이터와 새 데이터를 나중에 사용하기 위해 이 결합된 배열에 복사합니다.
## 8단계: 전체 통합 문서 데이터를 파일에 저장
 마지막으로, 우리의 모든 데이터를 결합하면`workbookData` 배열을 지정된 파일 경로에 저장할 수 있습니다.
```csharp
//전체 통합 문서 데이터를 파일에 저장
File.WriteAllBytes(dataDir + "out.txt", workbookData);
```
`WriteAllBytes` 결합된 바이트 배열을 가져와서 지정된 디렉토리의 "out.txt"라는 텍스트 파일에 씁니다.
## 결론
이제 Aspose.Cells for .NET을 사용하여 Excel 통합 문서를 CSV 형식으로 성공적으로 변환했습니다. 이 프로세스는 효율적일 뿐만 아니라 추가 분석이나 보고를 위해 Excel 데이터를 쉽게 조작할 수 있습니다. 이제 데이터 처리 작업을 자동화하거나 이 기능을 더 큰 애플리케이션에 통합할 수도 있습니다.
## 자주 묻는 질문
### CSV 파일에 다른 구분 기호를 사용할 수 있나요?
 네, 변경할 수 있습니다.`opts.Separator` 쉼표나 파이프 등 원하는 문자로 바꿀 수 있습니다.
### Aspose.Cells는 무료로 사용할 수 있나요?
 Aspose.Cells는 무료가 아니지만 무료 체험판을 받을 수 있습니다.[여기](https://releases.aspose.com/).
### CSV 외에 어떤 형식으로 저장할 수 있나요?
Aspose.Cells를 사용하면 XLSX, PDF 등 다양한 형식으로 저장할 수 있습니다.
### Aspose.Cells를 사용하여 대용량 Excel 파일을 처리할 수 있나요?
네, Aspose.Cells는 대용량 파일을 효율적으로 처리하도록 설계되었지만 성능은 시스템 리소스에 따라 달라질 수 있습니다.
### 더 자세한 문서는 어디에서 볼 수 있나요?
포괄적인 문서와 예제는 다음에서 찾을 수 있습니다.[참조 사이트](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
