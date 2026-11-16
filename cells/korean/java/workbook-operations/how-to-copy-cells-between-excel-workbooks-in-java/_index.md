---
category: general
date: 2026-11-16
description: Java에서 Excel 워크북 간에 셀을 복사하는 방법 – 워크북을 로드하고, 워크북 간에 범위를 복사(피벗 테이블 포함)한
  뒤, 워크북 파일을 저장합니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy cells
- copy range between workbooks
- copy pivot table workbook
- save workbook file
- load excel workbook java
language: ko
lastmod: 2026-11-16
og_description: Java에서 Excel 워크북 간에 셀을 복사하는 방법. Excel 워크북을 로드하고, 워크북 간에 범위(피벗 테이블
  포함)를 복사한 뒤 워크북 파일을 저장하는 방법을 배웁니다.
og_image_alt: Screenshot of Java code copying a cell range from one Excel workbook
  to another
og_title: Java에서 Excel 워크북 간 셀 복사 방법 – 완벽 가이드
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  headline: How to copy cells between Excel workbooks in Java
  type: TechArticle
- description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  name: How to copy cells between Excel workbooks in Java
  steps:
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Define the range that includes the pivot table
    text: '```java // Define the cell range that you want to copy. // Adjust "A1:G20"
      to match the area that contains your data/pivot table. Range srcRange = srcWs.getCells().createRange("A1:G20");
      ```'
  - name: Create the destination workbook
    text: '```java // Create a new, empty workbook that will receive the copied range.
      Workbook destWb = new Workbook(); // defaults to a single empty sheet Worksheet
      destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range to the destination workbook
    text: '```java // Copy the source range to cell A1 of the destination worksheet.
      destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1")); ```'
  - name: Save the destination workbook
    text: '```java // Save the new workbook to disk. destWb.save("YOUR_DIRECTORY/dest.xlsx");
      } } ```'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Workbook manipulation
title: Java를 사용하여 Excel 워크북 간에 셀 복사하는 방법
url: /ko/java/workbook-operations/how-to-copy-cells-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 Excel 워크북 간 셀 복사 방법

Java를 사용해 한 Excel 워크북에서 다른 워크북으로 **셀을 복사**해야 할 때, 이 가이드는 신뢰할 수 있는 방법을 보여줍니다. **Excel 워크북 Java 로드**, 피벗 테이블이 포함될 수 있는 범위 복사, 그리고 복사된 데이터를 **워크북 파일 저장**하는 방법을 배울 수 있습니다.

이 튜토리얼에서 다루는 내용:

* 소스 워크북을 로드하고 워크시트를 선택하기.  
* 이동하려는 정확한 범위 정의(피벗 테이블 포함).  
* 대상 워크북을 생성하고 범위를 복사하기.  
* 대상 파일 저장하기.  

예제는 Microsoft Office 없이 Excel 파일을 다룰 수 있는 Aspose.Cells for Java 라이브러리를 사용합니다. 코드는 Java 8+ 및 최신 IDE(IntelliJ IDEA, Eclipse, VS Code 등)에서 실행됩니다.

---

## 사전 요구 사항

시작하기 전에 다음을 준비하세요:

| Requirement | Reason |
|-------------|--------|
| Java Development Kit (JDK) 8 이상 | 코드를 컴파일하고 실행하는 데 필요합니다. |
| Maven 또는 Gradle 빌드 도구 | Aspose.Cells 의존성을 쉽게 추가할 수 있습니다. |
| Aspose.Cells for Java 라이브러리(최신 버전) | 예제에서 사용하는 `Workbook`, `Worksheet`, `Range` 클래스를 제공합니다. |
| 두 개의 Excel 파일(`source.xlsx`와 `dest.xlsx`를 저장할 빈 폴더) | 소스 파일에는 복사하려는 데이터와 선택적으로 피벗 테이블이 포함되어 있어야 합니다. |

`pom.xml`(Maven) 또는 `build.gradle`(Gradle)에 Aspose.Cells 의존성을 추가합니다. Maven 예시:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

---

## Aspose.Cells 로 셀 복사하기

다음 단계는 전체 프로세스를 단계별로 안내합니다. 각 단계에는 Java 코드, **왜** 이 단계가 중요한지에 대한 설명, 그리고 흔히 발생하는 실수를 피하기 위한 팁이 포함됩니다.

### Step 1: 소스 워크북 로드

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source Excel file (replace with your actual path)
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Get the first worksheet (index 0)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**Why?**  
`Workbook`은 전체 Excel 파일을 나타냅니다. 이를 로드하면 모든 워크시트, 셀 및 피벗 테이블과 같은 객체에 접근할 수 있습니다. 첫 번째 워크시트를 사용하는 것이 일반적이지만, 이름으로(`srcWb.getWorksheets().get("Sheet2")`) 원하는 시트를 선택할 수도 있습니다.

**Pro tip:**  
소스 파일이 큰 경우 *메모리 효율* 모드로 로드하는 것을 고려하세요: `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setMemorySetting(MemorySetting.MEMORY_PREFERENCE); }});`

### Step 2: 피벗 테이블을 포함하는 범위 정의

```java
        // Define the cell range that you want to copy.
        // Adjust "A1:G20" to match the area that contains your data/pivot table.
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**Why?**  
`Range` 객체는 사각형 셀 블록을 추상화합니다. `"A1:G20"`을 지정하면 Aspose.Cells에 해당 셀들—내장된 피벗 테이블 포함—을 정확히 복사하도록 지시합니다. 라이브러리는 데이터, 스타일, 피벗 정의를 자동으로 복사합니다.

**Edge case:**  
피벗 테이블이 정의된 범위를 넘어선다면 주소를 확장하세요(예: `"A1:Z100"`). `srcWs.getCells().getMaxDataColumn()` 및 `getMaxDataRow()`를 사용해 사용 영역을 동적으로 계산할 수도 있습니다.

### Step 3: 대상 워크북 생성

```java
        // Create a new, empty workbook that will receive the copied range.
        Workbook destWb = new Workbook();               // defaults to a single empty sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**Why?**  
새 워크북을 사용하면 원하지 않는 서식이나 숨겨진 시트가 복사된 내용에 영향을 주지 않습니다. 기본 워크북에는 이미 하나의 워크시트가 포함되어 있으며, 이를 목표 시트로 사용할 것입니다.

### Step 4: 범위를 대상 워크북에 복사

```java
        // Copy the source range to cell A1 of the destination worksheet.
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));
```

**Why?**  
`copyRange`는 값, 수식, 서식, 심지어 피벗 캐시까지 모든 셀 속성을 처리합니다. `"A1"`에 복사하면 대상 시트의 좌측 상단에 원본 레이아웃을 그대로 배치합니다.

**Common question:** *피벗 테이블은 계속 작동하나요?*  
네. Aspose.Cells는 피벗 테이블 정의와 캐시를 복사하므로, 피벗은 소스 워크북과 동일하게 작동합니다.

### Step 5: 대상 워크북 저장

```java
        // Save the new workbook to disk.
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Why?**  
`save`를 호출하면 메모리 상의 워크북이 실제 `.xlsx` 파일로 기록됩니다. 파일 확장자를 바꾸거나 `SaveOptions`를 사용하면 다른 형식(`.xls`, `.csv`, `.pdf`)으로도 저장할 수 있습니다.

**Tip:**  
파일을 웹 응답으로 스트리밍해야 한다면 `destWb.save(OutputStream, SaveFormat.XLSX);`와 같이 파일 경로 대신 스트림을 사용하세요.

---

## 워크북 간 범위 복사 – 전체 소스 코드

아래는 완전한 실행 가능한 Java 클래스입니다. `YOUR_DIRECTORY`를 실제 폴더 경로로 교체하세요.

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Define the range that includes the data and pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Create a new destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Copy the defined range to the destination workbook
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Expected result:**  
`dest.xlsx`는 `source.xlsx`의 `A1:G20` 범위를 정확히 복제합니다. 소스 범위에 피벗 테이블이 포함되어 있었다면, 대상 파일에서도 동일한 피벗이 복사된 셀을 데이터 소스로 사용합니다.

`dest.xlsx`를 Excel, LibreOffice 또는 `.xlsx`를 지원하는 뷰어에서 열어 값, 서식, 피벗 기능이 그대로 유지되는지 확인할 수 있습니다.

---

## 피벗 테이블 워크북 복사 – 알아두어야 할 점

* **피벗 캐시가 자동으로 복사됩니다.** 라이브러리가 기본 캐시를 전송하므로 피벗을 수동으로 새로 고칠 필요가 없습니다.
* **외부 데이터 소스는 전송되지 않습니다.** 피벗이 외부 데이터베이스에서 데이터를 가져오는 경우, 대상 워크북이 동일한 소스에 접근할 수 있도록 하거나 캐시를 로컬에서 재생성해야 합니다.
* **대형 피벗 테이블은 메모리 사용량을 증가시킬 수 있습니다.** 매우 큰 워크북의 경우 JVM 힙(`-Xmx2g`)을 늘려 `OutOfMemoryError`를 방지하세요.

---

## 다양한 형식으로 워크북 파일 저장

Aspose.Cells를 사용하면 별도 코드 변경 없이 여러 형식으로 결과를 저장할 수 있습니다:

```java
// Save as XLS (Excel 97-2003)
destWb.save("dest.xls");

// Save as CSV (first worksheet only)
destWb.save("dest.csv");

// Save as PDF (visual representation)
destWb.save("dest.pdf");
```

프로세스에 맞는 형식을 선택하세요. `copyRange` 로직은 최종 형식에 관계없이 동일하게 작동합니다.

---

## Excel 워크북 로드 Java – 추가 팁

* **암호화된 파일 로드:** `LoadOptions`에 비밀번호를 지정하세요:  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setPassword("myPassword");
  Workbook wb = new Workbook("encrypted.xlsx", opt);
  ```
* **특정 시트만 읽기:**  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setLoadDataOnly(true); // faster if you only need values
  Workbook wb = new Workbook("file.xlsx", opt);
  ```

이 옵션들은 특히 대용량 파일에서 **load excel workbook java** 단계를 가속화하는 데 도움이 됩니다.

---

## 결론

이제 Java에서 Excel 워크북 간 **셀 복사** 방법, **피벗 테이블이 포함된 범위 복사** 방법, 그리고 필요에 따라 **워크북 파일 저장** 방법을 알게 되었습니다. 위 단계들을 따르면 보고서 엔진, ETL 파이프라인, 간단한 파일 변환 유틸리티 등 어떤 Java 애플리케이션에서도 Excel 데이터 조작을 손쉽게 통합할 수 있습니다.

**다음 단계**로 탐색해 볼 내용:

* **copy range between workbooks**를 사용해 여러 보고서를 하나로 병합하기


## 다음에 배워야 할 내용은?


다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하며, 관련 주제를 깊이 있게 다룹니다. 각 리소스는 단계별 설명과 완전한 코드 예제를 제공하여 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용할 수 있도록 돕습니다.

- [Save New Workbook in Java – Copy Range Between Workbooks Tutorial](/cells/english/java/workbook-operations/save-new-workbook-in-java-copy-range-between-workbooks-tutor/)
- [How to copy pivot tables between Excel workbooks in Java](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/)
- [How to copy range in Java – Copy Pivot Table with Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}