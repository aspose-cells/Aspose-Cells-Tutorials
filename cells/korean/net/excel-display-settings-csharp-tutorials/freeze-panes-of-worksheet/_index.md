---
title: 워크시트의 창 고정
linktitle: 워크시트의 창 고정
second_title: .NET API 참조를 위한 Aspose.Cells
description: 이 포괄적인 튜토리얼에서는 .NET용 Aspose.Cells를 사용하여 Excel에서 창을 고정하는 방법을 알아봅니다. 단계별 지침과 필수 팁이 포함되어 있습니다.
weight: 70
url: /ko/net/excel-display-settings-csharp-tutorials/freeze-panes-of-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 워크시트의 창 고정

## 소개

큰 Excel 워크시트에서 작업할 때 스크롤하는 동안 특정 행이나 열을 보이도록 유지할 수 있으면 생산성을 크게 향상시킬 수 있습니다. 고정 창이라고 하는 이 기능을 사용하면 워크시트의 특정 섹션을 잠그어 스프레드시트를 탐색하는 동안 중요한 데이터를 추적할 수 있습니다. 이 튜토리얼에서는 Aspose.Cells for .NET을 사용하여 Excel 워크시트에서 창을 고정하는 방법을 살펴보겠습니다. 그러니 노트북을 들고 Aspose.Cells의 세계로 뛰어드세요!

## 필수 조건

실제 코딩 부분으로 넘어가기 전에 시작하는 데 필요한 모든 것이 있는지 확인해 보겠습니다.

### C#의 기본 지식
- C# 프로그래밍에 익숙해야 합니다. 이를 사용하여 코드를 작성해야 하기 때문입니다.

### Aspose.Cells 설치됨
-  개발 환경에 Aspose.Cells for .NET이 설치되어 있는지 확인하세요. 아직 설치하지 않았다면 다음으로 이동하세요.[다운로드 링크](https://releases.aspose.com/cells/net/) 시작하려면 클릭하세요.

### 비주얼 스튜디오
- C# 애플리케이션을 만들고 실행하려면 Visual Studio와 같은 IDE가 필요합니다.

### 샘플 Excel 파일
- 데모 목적으로 Excel 파일이 필요합니다. 이를 Excel 파일이라고 합니다.`book1.xls`Microsoft Excel이나 호환되는 응용 프로그램을 사용하여 간단한 Excel 파일을 만들 수 있습니다.

이러한 전제 조건을 갖추면 코딩을 시작할 수 있습니다!

## 패키지 가져오기

이제 모든 것이 설정되었으니 필요한 Aspose.Cells 패키지를 가져오도록 합시다. 방법은 다음과 같습니다.

```csharp
using System.IO;
using Aspose.Cells;
```

이러한 패키지를 가져오면 Aspose.Cells가 제공하는 강력한 기능을 사용할 수 있습니다.

패널을 동결하는 과정을 관리 가능한 단계로 나누어 보겠습니다. 이 작업을 달성하기 위해 C#과 Aspose.Cells를 사용할 것입니다.

## 1단계: 환경 설정

Visual Studio에서 새 C# 프로젝트를 만들고 Aspose.Cells 라이브러리를 참조했는지 확인합니다.

귀하의 프로젝트는 코드를 실행하고 테스트할 수 있는 작업 공간 역할을 합니다. Aspose.Cells 참조를 추가하면 Excel 파일을 쉽게 조작하는 데 필요한 도구를 가져오게 됩니다.

## 2단계: 문서 경로 정의

Excel 파일이 있는 디렉토리를 지정하세요. 다음은 예입니다.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

 이 줄은 디렉토리 경로를 설정합니다. 바꾸기`"YOUR DOCUMENT DIRECTORY"` 실제 경로와 함께`book1.xls` 파일이 저장됩니다. 그것은 당신의 코드에 Excel 파일이 있는 집 주소를 제공하는 것과 같습니다. 그것은 그것을 어디에서 찾을 수 있는지 알아야 합니다!

## 3단계: 파일 스트림 만들기

FileStream을 사용하여 기존 Excel 파일을 엽니다. 방법은 다음과 같습니다.

```csharp
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```

 그만큼`FileStream` 바이트 스트림을 제공하여 파일을 읽고 쓸 수 있게 해줍니다. 간단히 말해서, Excel 파일에 대한 문을 열어 작업을 시작할 수 있게 해줍니다.

## 4단계: 통합 문서 개체 인스턴스화

 새로운 것을 만드세요`Workbook` 열려 있는 파일에 대해 작업할 개체:

```csharp
Workbook workbook = new Workbook(fstream);
```

 그만큼`Workbook` 객체는 메모리에 있는 전체 Excel 파일을 나타냅니다. 전체 파일을 작업 공간으로 가져와서 수정을 시작할 수 있다고 생각하세요.

## 5단계: 워크시트에 액세스

작업하려는 워크시트에 대한 참조를 얻으세요. 첫 번째 워크시트로 작업하는 경우:

```csharp
Worksheet worksheet = workbook.Worksheets[0];
```

여기서는 통합 문서의 첫 번째 시트에 액세스합니다. Excel 파일에 여러 개의 워크시트를 넣을 수 있지만 이 데모에서는 첫 번째 시트에 집중합니다. 마치 책의 특정 페이지를 열어서 읽는 것과 같습니다.

## 6단계: 동결 창 설정 적용

이제, 동결 창 기능을 적용합니다. 우리의 경우, 우리는 처음 세 행과 처음 두 열을 동결하고 싶습니다.

```csharp
worksheet.FreezePanes(3, 2, 3, 2);
```

이 줄에서 마법이 일어납니다! 지정된 행과 열을 잠그면 시트의 나머지 부분을 스크롤해도 계속 표시됩니다. 창문 유리처럼 생각하면 됩니다. 아무리 아래로 또는 가로로 스크롤해도 중요한 내용을 볼 수 있습니다.

## 7단계: 수정된 Excel 파일 저장

변경 사항을 적용한 후에는 통합 문서를 저장해야 합니다.

```csharp
workbook.Save(dataDir + "output.xls");
```

 파일을 저장하는 것이 중요합니다! 이 줄은 고정된 창을 포함하여 변경한 모든 내용이 새 Excel 파일에 다시 기록되도록 합니다.`output.xls`중요한 편지를 쓴 후 봉투를 봉인하는 것처럼 생각해 보세요.

## 8단계: 파일 스트림 닫기

마지막으로 리소스를 확보하기 위해 FileStream을 닫습니다.

```csharp
fstream.Close();
```

FileStream을 닫는 것은 리소스 관리에 필수적입니다. 작업을 마친 후 문을 닫는 것과 같습니다. 이 단계는 리소스가 낭비되지 않고 애플리케이션이 원활하게 실행되도록 보장합니다.

## 결론

축하합니다! Aspose.Cells for .NET을 사용하여 Excel 워크시트에서 창을 고정하는 프로세스를 마스터했습니다. 이러한 단계를 따르면 이제 필수 정보를 놓치지 않고도 대용량 데이터 세트를 쉽게 관리할 수 있습니다. 이 기능은 생산성을 향상시키고 데이터를 보다 효과적으로 분석하는 데 도움이 됩니다.

## 자주 묻는 질문

### Excel에서 창을 고정하는 목적은 무엇입니까?
창을 고정하면 대용량 데이터 세트를 스크롤하는 동안 특정 행이나 열을 표시된 상태로 유지할 수 있습니다.

### 한 번에 여러 행과 열을 고정할 수 있나요?
 예, 다음을 사용하여 위치를 지정하여 원하는 수의 행과 열을 고정할 수 있습니다.`FreezePanes` 방법.

### Aspose.Cells는 무료로 사용할 수 있나요?
Aspose.Cells는 무료 체험판을 제공하지만 장기 사용을 위해서는 라이선스를 구매해야 합니다.[구매 페이지](https://purchase.aspose.com/buy) 자세한 내용은.

### Aspose.Cells에 대한 지원은 어디에서 찾을 수 있나요?
 다음을 통해 지원을 받을 수 있습니다.[Aspose 포럼](https://forum.aspose.com/c/cells/9), 커뮤니티에서 질문을 하고 해결책을 찾을 수 있는 곳입니다.

### 다른 플랫폼에서도 Aspose.Cells를 사용할 수 있나요?
.NET용 Aspose.Cells는 .NET Framework, .NET Core 및 .NET Standard와 함께 작동하도록 설계되어 다양한 애플리케이션에 다양하게 활용할 수 있습니다.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
