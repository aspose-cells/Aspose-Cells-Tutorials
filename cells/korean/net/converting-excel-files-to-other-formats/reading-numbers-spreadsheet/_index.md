---
title: .NET에서 숫자 스프레드시트 프로그래밍 방식으로 읽기
linktitle: .NET에서 숫자 스프레드시트 프로그래밍 방식으로 읽기
second_title: Aspose.Cells .NET Excel 처리 API
description: 이 자세한 튜토리얼에서는 Aspose.Cells for .NET을 사용하여 Numbers 스프레드시트를 읽고 이를 PDF로 변환하는 방법을 알아봅니다.
weight: 18
url: /ko/net/converting-excel-files-to-other-formats/reading-numbers-spreadsheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET에서 숫자 스프레드시트 프로그래밍 방식으로 읽기

## 소개
오늘날의 디지털 세계에서 데이터 관리가 필수적인 기술이고, 스프레드시트는 데이터 구성의 최전선에 있습니다. 하지만 .NET을 사용하여 Apple의 Numbers 앱에서 만든 파일인 Numbers 스프레드시트로 작업해야 하는 경우는 어떨까요? 걱정하지 마세요. 여러분만 그런 것은 아닙니다! 이 튜토리얼에서는 Aspose.Cells for .NET을 사용하여 Numbers 스프레드시트를 프로그래밍 방식으로 읽는 과정을 살펴보겠습니다. Numbers 파일을 로드하고 PDF로 변환하는 방법을 알아봅니다.
## 필수 조건
시작하기 전에 꼭 준비해야 할 몇 가지 사항이 있습니다.
1. .NET용 Aspose.Cells: Aspose.Cells 라이브러리가 설치되어 있는지 확인하세요. 다운로드할 수 있습니다.[여기](https://releases.aspose.com/cells/net/).
2. Visual Studio: 컴퓨터에 Visual Studio(또는 다른 .NET 호환 IDE)를 설치하는 것이 좋습니다.
3. C#에 대한 기본 지식: C# 프로그래밍에 대한 약간의 지식이 있으면 원활하게 따라갈 수 있습니다.
4. 문서 디렉토리: Numbers 파일이 저장된 디렉토리와 변환된 PDF를 저장할 위치가 필요합니다.
이러한 전제 조건을 충족하면 시작할 준비가 된 것입니다!
## 패키지 가져오기
우선, 우리는 필요한 패키지를 C# 프로젝트로 가져와야 합니다. 이것은 Aspose.Cells 라이브러리가 제공하는 기능을 활용할 수 있게 해주기 때문에 중요한 단계입니다.
1. Visual Studio에서 C# 프로젝트를 엽니다.
2. Aspose.Cells 라이브러리에 참조를 추가합니다.
   - NuGet을 사용하는 경우 패키지 관리자 콘솔에서 다음 명령을 실행하기만 하면 됩니다.
```
 Install-Package Aspose.Cells
 ```
3. 코드에 필요한 네임스페이스를 가져옵니다.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
이제 필요한 패키지를 가져왔으니 Numbers 스프레드시트를 읽는 단계별 가이드로 넘어가겠습니다.
## 1단계: 소스 및 출력 디렉토리 지정
이 단계에서는 소스 Numbers 파일이 있는 디렉토리와 출력 PDF를 저장할 디렉토리를 설정합니다.
```csharp
// 소스 디렉토리
string sourceDir = "Your Document Directory"; // 이것을 실제 디렉토리로 업데이트하세요
// 출력 디렉토리
string outputDir = "Your Document Directory"; // 이것을 실제 디렉토리로 업데이트하세요
```
 여기서 우리는 두 개의 문자열 변수를 정의하고 있습니다.`sourceDir` 그리고`outputDir` , 입력 및 출력 파일의 위치를 지정하려면 다음을 수행해야 합니다.`"Your Document Directory"` 시스템의 실제 경로와 함께.
## 2단계: 숫자 형식에 대한 로드 옵션 설정
다음으로, Numbers 스프레드시트를 읽기 위한 로드 옵션을 지정합니다. 이 단계는 Aspose에 Numbers 파일을 해석하는 방법을 알려주기 때문에 필수적입니다.
```csharp
// 로드 옵션을 지정하세요. Numbers 스프레드시트를 로드하려고 합니다.
LoadOptions opts = new LoadOptions(LoadFormat.Numbers);
```
 우리는 만듭니다`LoadOptions` 객체를 지정하고 형식을 다음과 같이 지정합니다.`LoadFormat.Numbers`. 이렇게 하면 Aspose.Cells 라이브러리에 Numbers 파일로 작업하고 있다는 것을 알려줍니다. 
## 3단계: 숫자 스프레드시트를 통합 문서에 로드
이제 실제 Numbers 스프레드시트를 로드할 시간입니다.`Workbook` 물체.
```csharp
// 위의 로드 옵션을 사용하여 숫자 스프레드시트를 통합 문서에 로드합니다.
Workbook wb = new Workbook(sourceDir + "sampleNumbersByAppleInc.numbers", opts);
```
 우리는 인스턴스화합니다`Workbook` 객체를 만들고 로드 옵션과 함께 Numbers 파일의 파일 경로를 전달합니다. 파일 이름(`sampleNumbersByAppleInc.numbers`)는 Numbers 파일의 실제 이름과 일치합니다.
## 4단계: 통합 문서를 PDF로 저장
Numbers 파일이 성공적으로 로드되면 다음 단계는 해당 파일을 다른 형식, 구체적으로는 PDF로 저장하는 것입니다.
```csharp
// 통합 문서를 PDF 형식으로 저장
wb.Save(outputDir + "outputNumbersByAppleInc.pdf", SaveFormat.Pdf);
```
 여기서 우리는 다음을 호출합니다.`Save` 방법에 대한`Workbook` 객체, 출력 파일 경로와 저장하려는 형식을 지정합니다. 이 경우 PDF로 저장합니다. 출력 파일 이름(`outputNumbersByAppleInc.pdf`)은 고유하며 기존 파일을 덮어쓰지 않습니다.
## 5단계: 성공 확인
마지막으로, 작업이 성공적이었음을 확인하는 메시지를 추가해 보겠습니다.
```csharp
Console.WriteLine("ReadNumbersSpreadsheet executed successfully.\r\n");
```
이 코드 줄은 모든 것이 완료되면 콘솔에 성공 메시지를 출력합니다. 피드백을 받는 건 항상 좋은 일이죠, 맞죠?
## 결론
이제 다 됐습니다! 숫자 스프레드시트를 성공적으로 읽고 Aspose.Cells for .NET을 사용하여 PDF로 변환했습니다. 이 강력한 라이브러리를 사용하면 스프레드시트를 손쉽게 조작할 수 있어 데이터 관리 작업이 훨씬 수월해집니다. 애플리케이션을 개발하든 스프레드시트를 더 효율적으로 처리해야 하든 Aspose.Cells는 툴킷에 넣어두면 좋은 환상적인 도구입니다.
## 자주 묻는 질문
### Aspose.Cells는 어떤 유형의 파일을 읽을 수 있나요?  
Aspose.Cells는 XLS, XLSX, CSV, Numbers 파일을 포함한 다양한 파일 형식을 읽을 수 있습니다. 
### Aspose.Cells를 사용하여 Numbers 파일을 편집할 수 있나요?  
네, Aspose.Cells를 사용하여 Numbers 파일을 읽고, 조작하고, 저장할 수 있습니다.
### Aspose.Cells는 무료로 사용할 수 있나요?  
 Aspose.Cells는 무료 체험판을 제공하지만, 장기 사용을 위해서는 라이선스가 필요합니다. 가격 확인[여기](https://purchase.aspose.com/buy).
### Numbers 파일을 로드하는 동안 오류가 발생하면 어떻게 해야 하나요?  
 올바른 로드 옵션을 사용하고 파일 경로가 정확한지 확인하세요. 자세한 지원은 다음을 방문하세요.[Aspose 지원 포럼](https://forum.aspose.com/c/cells/9).
### Aspose.Cells에 대한 임시 라이센스를 어떻게 받을 수 있나요?  
 임시면허를 신청할 수 있습니다.[여기](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
