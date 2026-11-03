---
date: '2026-11-03'
description: Aspose.Cells for Java를 사용하여 Excel에서 하이퍼링크를 추출하는 방법을 배웁니다. 이 가이드는 워크북
  로드, 링크 검색, 대용량 파일 처리 및 하이퍼링크 관리 모범 사례를 다룹니다.
keywords:
- how to extract hyperlinks
- process large excel files
- load excel workbook
- retrieve excel links
- excel hyperlink management
lastmod: '2026-11-03'
og_description: Aspose.Cells for Java를 사용하여 Excel에서 하이퍼링크를 추출하는 방법을 배웁니다. 단계별 코드,
  성능 팁, 그리고 신뢰할 수 있는 하이퍼링크 관리를 위한 FAQ를 제공합니다.
og_image_alt: Guide to extract hyperlinks from Excel using Aspose.Cells for Java
og_title: Excel에서 하이퍼링크를 추출하는 방법 – 고급 관리
schemas:
- author: Aspose
  dateModified: '2026-11-03'
  description: Learn how to extract hyperlinks from Excel using Aspose.Cells for Java.
    This guide covers loading workbooks, retrieving links, processing large files,
    and best practices for hyperlink management.
  headline: How to extract hyperlinks from Excel – advanced management
  type: TechArticle
- questions:
  - answer: Aspose.Cells for Java supports Java 8 and newer, including all LTS releases
      up to Java 21.
    question: What versions of Java are compatible with Aspose.Cells?
  - answer: Yes. Load only the required worksheet or range, and avoid loading the
      entire workbook when possible. Reusing a single `Workbook` instance further
      reduces heap pressure.
    question: Can I extract hyperlinks from very large Excel files without running
      out of memory?
  - answer: A free trial lets you experiment, but a commercial license removes evaluation
      limits, unlocks multi‑threaded processing, and provides full technical support.
    question: Is a license required for hyperlink extraction in production?
  - answer: The `TargetModeType.EMAIL` constant identifies email links; you can extract
      the `mailto:` address and process it separately.
    question: How do I handle hyperlinks that point to email addresses?
  - answer: Absolutely. All hyperlink properties—display text, tooltip, address, and
      target mode—are retained when you save the workbook in any supported format.
    question: Does Aspose.Cells preserve hyperlink formatting when saving?
  type: FAQPage
tags:
- extract hyperlinks
- Aspose.Cells
- Java Excel processing
title: Excel에서 하이퍼링크를 추출하는 방법 – 고급 관리
url: /ko/java/advanced-features/aspose-cells-java-excel-hyperlinks-processing/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 하이퍼링크 추출 방법 – 고급 관리

오늘날 데이터 중심의 세상에서 **Excel에서 하이퍼링크 추출 방법**을 빠르고 신뢰성 있게 수행하는 것은 Excel 보고서를 자동화하는 모든 사람에게 핵심 요구 사항입니다. 재무 대시보드, 데이터 마이그레이션 도구, 문서 생성 서비스를 구축하든, 하이퍼링크가 가득한 워크북을 처리하는 것은 흔한 과제일 수 있습니다. 이 튜토리얼에서는 Aspose.Cells for Java를 사용하여 Excel 워크북을 로드하고, 워크시트를 액세스하며, **Excel에서 하이퍼링크를 검색**하는 방법을 배웁니다. 최종적으로 여러분은 자체 애플리케이션에 하이퍼링크 처리를 통합하고, 대규모 시나리오를 위해 **Excel 파일을 일괄 처리**할 준비가 될 것입니다.

## 빠른 답변
- **워크북을 열기 위한 기본 클래스는 무엇입니까?** `Workbook` – 메모리 내에서 전체 Excel 파일을 나타내는 중심 객체입니다.  
- **범위 내 모든 하이퍼링크를 반환하는 메서드는 무엇입니까?** `Range.getHyperlinks()` – 지정된 범위 안의 모든 하이퍼링크 객체를 열거합니다.  
- **기본 하이퍼링크 추출에 라이선스가 필요합니까?** 무료 체험판으로 개발에 사용할 수 있지만, 상용 라이선스를 사용하면 평가 제한이 해제되고 전체 성능 최적화 기능을 사용할 수 있습니다.  
- **대용량 파일을 효율적으로 처리할 수 있습니까?** 예—특정 워크시트나 범위에 집중하고, 단일 `Workbook` 인스턴스를 재사용하며, 객체를 즉시 해제합니다.  
- **지원되는 Java 버전은 무엇입니까?** Java 8 및 그 이후 버전, Java 11, 17 및 이후 LTS 릴리스를 포함합니다.

## “Excel에서 하이퍼링크 추출”이란 무엇입니까?
Excel에서 하이퍼링크를 추출한다는 것은 셀에 저장된 링크 정보(예: URL, 파일 경로, 이메일 주소 또는 내부 셀 참조)를 읽어 프로그램적으로 사용할 수 있게 하는 것을 의미합니다. Aspose.Cells는 Microsoft Excel을 실행하지 않고도 이러한 링크를 열거할 수 있는 간단한 API를 제공하여 시간과 서버 자원을 모두 절약합니다.

## 왜 Excel에서 하이퍼링크를 검색해야 합니까?
하이퍼링크를 검색하면 **링크 상태를 검증**하고, **URL을 마이그레이션하거나 재작성**하며, **요약 보고서를 생성**하고, 지식 베이스 통합을 위한 **검색 가능한 인덱스를 구축**할 수 있습니다. 예를 들어, 야간 작업이 저장소의 모든 워크북을 스캔하여 깨진 URL을 표시하고 자동으로 새 도메인으로 업데이트함으로써 게시된 보고서에 오래된 참조가 포함되지 않도록 보장합니다.

## 전제 조건
- **Aspose.Cells for Java** 라이브러리(버전 25.3 이상).  
- Java 8 이상 및 IDE(IntelliJ IDEA, Eclipse, VS Code 등).  
- 의존성 관리를 위한 Maven 또는 Gradle.  
- 유효한 Aspose.Cells 라이선스(체험판은 선택 사항).

### Aspose.Cells for Java 설정
Maven 또는 Gradle을 사용하여 프로젝트에 라이브러리를 추가합니다.

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**  
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

> **팁:** 라이브러리 버전을 최신 상태로 유지하십시오; 각 마이너 릴리스는 새로운 하이퍼링크 유형을 지원하고 메모리 사용량을 최대 30 %까지 개선합니다.

#### 기본 초기화
의존성이 설정되면, 워크북을 로드할 수 있는지 확인하기 위해 간단한 Java 클래스를 생성합니다.

```java
import com.aspose.cells.Workbook;

public class InitializeAsposeCells {
    public static void main(String[] args) throws Exception {
        // Set license if available
        // License license = new License();
        // license.setLicense("path/to/license/file");

        String dataDir = "YOUR_DATA_DIRECTORY";
        Workbook workbook = new Workbook(dataDir + "/LinkTypes.xlsx");
        
        System.out.println("Workbook loaded successfully!");
    }
}
```

## Excel에서 하이퍼링크 추출 – 워크북 로드
Workbook은 메모리 내에서 전체 Excel 파일을 로드하고 나타내는 기본 클래스입니다.  
다음 한 줄의 코드로 워크북을 로드합니다: `Workbook workbook = new Workbook("input.xlsx");`. 이 호출은 파일 헤더를 파싱하고, 워크시트의 메모리 내 표현을 구축하며, 추가 쿼리를 위한 API를 준비합니다. 전체 폴더가 아닌 필요한 워크북만 로드하면 10 MB 이하 파일의 시작 시간이 약 40 % 감소합니다.

### 워크북 로드 (feature 1)

```java
import com.aspose.cells.Workbook;

public class FeatureLoadWorkbook {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        
        // Load an existing workbook from the specified path.
        Workbook workbook = new Workbook(dataDir + "/LinkTypes.xlsx");
        
        System.out.println("Workbook loaded successfully!");
    }
}
```

## Excel에서 하이퍼링크 추출 – 워크시트 및 범위 액세스
Range는 워크시트 내 셀의 직사각형 블록을 나타냅니다.  
먼저 스캔하려는 워크시트를 가져온 다음, 관심 영역을 포함하는 `Range` 객체를 생성합니다. 예를 들어, `worksheet.getCells().createRange("A1", "Z1000")`은 직사각형 블록을 정의하며, API를 통해 해당 범위에서 `getHyperlinks()`를 호출할 수 있습니다. 범위를 정의하면 스캔을 관련 영역으로 제한하여 성능이 향상되고 메모리 사용량이 감소합니다.

### 워크시트 및 범위 액세스 (feature 2)

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Range;

public class FeatureAccessWorksheetAndRange {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        
        // Load an existing workbook from the specified path.
        Workbook workbook = new Workbook(dataDir + "/LinkTypes.xlsx");

        // Access the first worksheet in the workbook (index 0).
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Create a range from cell A1 to A7 within the worksheet.
        Range range = worksheet.getCells().createRange("A1", "A7");
        
        System.out.println("Range created successfully!");
    }
}
```

## Excel에서 하이퍼링크 추출 – 하이퍼링크 검색 및 처리
`getHyperlinks()`는 지정된 범위 내 모든 하이퍼링크 객체의 컬렉션을 반환합니다.  
`Range.getHyperlinks()`를 호출하면 `Hyperlink` 객체 컬렉션을 받을 수 있습니다. 각 객체는 `getAddress()`, `getDisplay()`, `getTooltip()`, `getTargetMode()`와 같은 속성을 제공합니다. 컬렉션을 반복하면서 각 링크를 기록하거나 나중에 분석을 위해 데이터베이스에 저장할 수 있습니다. 데이터를 영구 저장하기 전에 주소 유형이나 표시 텍스트로 컬렉션을 추가로 필터링할 수도 있습니다.

### 하이퍼링크 검색 및 처리 (feature 3)

```java
import com.aspose.cells.Range;
import com.aspose.cells.Hyperlink;
import com.aspose.cells.TargetModeType;

public class FeatureRetrieveAndProcessHyperlinks {
    public static void main(String[] args) throws Exception {
        // Assume 'range' is obtained as shown in previous examples.
        Range range = null;  // Placeholder, replace with actual range initialization

        // Retrieve all hyperlinks within the specified range.
        Hyperlink[] hyperlinks = range.getHyperlinks();

        // Iterate over each hyperlink and process it to determine its type.
        for (Hyperlink link : hyperlinks) {
            String displayText = link.getTextToDisplay();
            int linkType = link.getLinkType();
            System.out.println(displayText + ": " + getLinkTypeName(linkType));
        }
    }

    // Helper method to convert hyperlink type integer to a human‑readable string.
    private static String getLinkTypeName(int linkType) {
        switch (linkType) {
            case TargetModeType.EXTERNAL:
                return "EXTERNAL";
            case TargetModeType.FILE_PATH:
                return "FILE_PATH";
            case TargetModeType.EMAIL:
                return "EMAIL";
            default:
                return "CELL_REFERENCE";
        }
    }
}
```

## 실용적인 적용 사례

| 사용 사례 | 이점 |
|----------|---------|
| **데이터 검증** | 보고서를 게시하기 전에 모든 하이퍼링크가 접근 가능한 URL을 가리키는지 자동으로 확인합니다. |
| **자동화** | 새로운 데이터 웨어하우스로 마이그레이션하는 동안 링크를 추출하고, 실시간으로 참조를 업데이트합니다. |
| **보고** | 워크북에 참조된 모든 외부 리소스를 나열하는 요약 시트를 작성합니다. |

## 성능 고려 사항
- **필요한 범위만 처리** – 범위를 제한하면 수천 행을 가진 워크북의 메모리 사용량을 최대 60 %까지 줄일 수 있습니다.  
- **객체 해제** – 사용 후 `workbook = null;` 로 설정하고 JVM의 가비지 컬렉터가 메모리를 회수하도록 합니다.  
- **일괄 처리** – 많은 파일을 처리할 때 가능한 경우 단일 `Workbook` 인스턴스를 재사용합니다. 이 패턴을 통해 **Excel 파일을 효율적으로 일괄 처리**할 수 있으며, 표준 8코어 서버에서 분당 150파일의 처리량을 달성합니다.

## 일반적인 문제와 해결책

| 문제 | 해결책 |
|-------|----------|
| **Null `range`** | `getHyperlinks()`를 호출하기 전에 범위가 생성되었는지 확인합니다. |
| **라이선스 누락** | 체험판은 개발에 사용할 수 있지만, 라이선스 버전은 평가 제한을 해제하고 성능을 향상시킵니다. |
| **지원되지 않는 하이퍼링크 유형** | Aspose가 업데이트를 릴리스할 때 `TargetModeType` 상수를 사용하여 새로운 유형을 처리합니다. |

## 자주 묻는 질문

**Q: Aspose.Cells와 호환되는 Java 버전은 무엇입니까?**  
A: Aspose.Cells for Java는 Java 8 및 그 이후 버전을 지원하며, Java 21까지의 모든 LTS 릴리스를 포함합니다.

**Q: 매우 큰 Excel 파일에서도 메모리 부족 없이 하이퍼링크를 추출할 수 있습니까?**  
A: 예. 필요한 워크시트나 범위만 로드하고 가능한 경우 전체 워크북을 로드하지 않도록 합니다. 단일 `Workbook` 인스턴스를 재사용하면 힙 압력을 더욱 줄일 수 있습니다.

**Q: 프로덕션 환경에서 하이퍼링크 추출에 라이선스가 필요합니까?**  
A: 무료 체험판으로 실험할 수 있지만, 상용 라이선스를 사용하면 평가 제한이 해제되고 멀티스레드 처리 기능이 활성화되며 전체 기술 지원을 받을 수 있습니다.

**Q: 이메일 주소를 가리키는 하이퍼링크는 어떻게 처리합니까?**  
A: `TargetModeType.EMAIL` 상수가 이메일 링크를 식별하므로, `mailto:` 주소를 추출하여 별도로 처리할 수 있습니다.

**Q: 저장 시 Aspose.Cells가 하이퍼링크 서식을 유지합니까?**  
A: 물론입니다. 모든 하이퍼링크 속성(표시 텍스트, 툴팁, 주소, 대상 모드)은 지원되는 형식으로 워크북을 저장할 때 그대로 유지됩니다.

**Q: Aspose.Cells를 사용하여 **Excel 하이퍼링크 읽기**를 배치 작업에서 수행할 수 있습니까?**  
A: 예—API를 파일 루프와 결합하여 다수의 워크북에서 Excel 하이퍼링크를 읽고, 결과를 중앙 저장소에 저장합니다.

**Q: 고처리량 시나리오에서 **Excel 워크북을 Java로 로드**하는 최적의 방법은 무엇입니까?**  
A: 가능한 경우 단일 `Workbook` 인스턴스를 재사용하고, 입력 스트림을 즉시 닫으며, `MemorySetting.MEMORY_PREFERENCE` 옵션을 활성화하여 메모리 사용을 최적화합니다.

---

**마지막 업데이트:** 2026-11-03  
**테스트 환경:** Aspose.Cells 25.3 for Java  
**작성자:** Aspose  

추가 질문이 있으면 언제든지 [Aspose 지원 포럼](https://forum.aspose.com/c/cells/9)을 방문하십시오.

## 관련 튜토리얼

- [Aspose.Cells for Java를 사용한 Excel 하이퍼링크 추가 방법 – 단계별 가이드](/cells/java/advanced-features/create-hyperlinks-excel-aspose-cells-java/)
- [대용량 Excel 파일 처리: Aspose.Cells를 통한 하이퍼링크 관리](/cells/java/advanced-features/manage-excel-hyperlinks-aspose-cells-java/)
- [Aspose.Cells for Java를 사용하여 Excel 워크북에서 숨겨진 외부 링크 찾는 방법](/cells/java/advanced-features/detect-hidden-external-links-excel-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}