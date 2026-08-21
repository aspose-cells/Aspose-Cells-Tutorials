---
category: general
date: 2026-08-20
description: Java를 사용하여 소수점 이하 자리수를 제한하고 유효 숫자를 유지하면서 Excel을 TXT 파일로 내보내고 워크북을 TXT로
  저장하는 방법을 배웁니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- limit decimal places
- keep significant digits
- save workbook as txt
language: ko
lastmod: 2026-08-20
og_description: Aspose.Cells를 사용하여 Excel을 TXT로 내보내기. 이 가이드는 소수점 자리수를 제한하고, 유효 숫자를
  유지하며, Java에서 워크북을 TXT로 저장하는 방법을 보여줍니다.
og_image_alt: Result of export excel to txt showing limited decimal places and kept
  significant digits
og_title: Java에서 Excel을 TXT로 내보내기 – 소수점 자리수와 유효숫자 제어
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn to export Excel to TXT while limiting decimal places, keeping
    significant digits, and saving workbook as TXT using Java.
  headline: How to export Excel to TXT with Aspose.Cells and control decimal precision
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Text export
title: Aspose.Cells를 사용하여 Excel을 TXT로 내보내고 소수점 자릿수를 제어하는 방법
url: /ko/java/excel-import-export/how-to-export-excel-to-txt-with-aspose-cells-and-control-dec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel을 TXT로 내보내고 소수점 자리수를 제어하는 방법 (Aspose.Cells 사용)

Excel을 **TXT로 내보내**고 출력이 특정 소수점 자리수를 유지하도록 해야 한다면, 이 가이드는 완전한 솔루션을 제공합니다. 소수점 자리수를 제한하고, 유효 숫자를 유지하며, Aspose.Cells for Java 라이브러리를 사용해 **워크북을 TXT로 저장**하는 방법을 확인할 수 있습니다.

이 튜토리얼은 워크북 생성, 고정밀 값 삽입, TXT 저장 옵션 구성, 파일 디스크에 쓰기 과정을 단계별로 안내합니다. 최종적으로 수동 후처리 없이도 요구하는 정확한 정밀도를 가진 텍스트 파일을 생성할 수 있습니다.

## 필요 사항

- Java 17 (또는 지원되는 JDK)
- Aspose.Cells for Java 23.10 이상
- 의존성 관리를 위한 IDE 또는 빌드 도구 (Maven/Gradle)
- 출력 디렉터리에 대한 쓰기 권한

## 단계 1: 워크북 생성 및 첫 번째 워크시트 접근

워크북을 생성하는 것은 **Excel을 TXT로 내보내**고자 할 때 첫 번째 단계입니다. `Workbook` 클래스는 전체 Excel 파일을 나타내며, `Worksheet`는 셀에 접근할 수 있게 해줍니다.

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
```

*왜 중요한가*: 워크북 객체는 모든 데이터, 스타일, 메타데이터를 보유합니다. 새 워크북으로 시작하면 숨겨진 서식이 텍스트 내보내기에 방해되지 않음을 보장합니다.

## 단계 2: 숫자 값을 추가하고 소수점 자리수 제한

소수점이 많이 포함된 숫자를 삽입하여 내보내기 시 **소수점 자리수 제한**을 어떻게 적용하는지 보여줄 수 있습니다.

```java
        // Put a high‑precision number into cell A1
        sheet.getCells().putValue("A1", 0.000123456789);
```

*왜 중요한가*: Excel은 전체 정밀도를 저장하지만, 이후 내보낼 때 값을 잘라내거나 반올림하고 싶을 수 있습니다. `limit decimal places` 설정이 이를 자동으로 처리합니다.

## 단계 3: TXT 저장 옵션을 구성하여 유효 숫자 유지

Aspose.Cells는 `TxtSaveOptions`를 제공합니다. `significantDigits`를 설정하면 내보내기가 필요한 의미 있는 자리수만 유지하고 앞의 0은 무시하도록 지정합니다.

```java
        // Configure TXT export options
        TxtSaveOptions txtOptions = new TxtSaveOptions();

        // Keep exactly 5 significant digits (e.g., 0.00012346)
        txtOptions.setSignificantDigits(5);
```

*왜 중요한가*: **keep significant digits** 옵션은 출력 파일에 예측 가능한 정밀도를 포함하도록 보장하며, 고정 폭 숫자 형식을 기대하는 하위 시스템에 필수적입니다.

## 단계 4: 워크북을 TXT로 저장

마지막으로 워크북을 텍스트 파일로 기록합니다. `save` 메서드는 구성한 옵션을 반영하므로 결과 파일에 제한된 소수점 표현이 포함됩니다.

```java
        // Define the output path (replace with your own directory)
        String outputPath = "output/SignificantDigits.txt";

        // Export the workbook to TXT using the configured options
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

*왜 중요한가*: 준비된 `TxtSaveOptions`와 함께 **save workbook as txt**를 사용하면 이전 단계에서 설정한 정밀도 제약에 맞는 파일이 내보내집니다.

### `SignificantDigits.txt` 예상 내용

```
0.00012346
```

값은 반올림 후 다섯 개의 유효 숫자(`12346`)를 보여주며, 앞의 0은 TXT 형식에 따라 유지됩니다.

## 변형 및 엣지 케이스

| 시나리오 | 조정 |
|----------|------------|
| **다른 유효 숫자 개수** | Call `txtOptions.setSignificantDigits(n)` where `n` is 1‑15. |
| **전체 시트 대신 범위 내보내기** | Use `txtOptions.setExportRange("A1:B10")` before saving. |
| **열 구분자 유지** | Set `txtOptions.setSeparator('\t')` for tab‑delimited output. |
| **대용량 워크시트** | Increase `txtOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCES)` to avoid `OutOfMemoryError`. |

## 일반적인 함정 및 전문가 팁

- **유효 숫자와 소수점 자리수를 혼동하지 말 것**. 앞의 0은 유효 숫자로 계산되지 않으며, 의미 있는 정밀도를 위해 `setSignificantDigits`를 사용하고 소수점 뒤 고정 자리수가 필요하면 `setDecimalPlaces`를 사용하십시오.
- IDE에서 실행할 때 **항상 절대 출력 경로를 지정**하여 권한 오류를 방지하십시오.
- **생성된 파일을 검증**하기 위해 `java.nio.file.Files.readAllLines(Paths.get(outputPath))` 호출을 사용해 내용이 기대와 일치하는지 확인한 후 하위 프로세스에 전달하십시오.

## 참고용 전체 소스 코드

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Step 2: Insert a high‑precision number (will be limited later)
        sheet.getCells().putValue("A1", 0.000123456789);

        // Step 3: Set TXT options – keep 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(5);   // keep significant digits

        // Step 4: Save the workbook as TXT
        String outputPath = "output/SignificantDigits.txt";
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

프로그램을 실행하면 `SignificantDigits.txt` 파일이 생성되며, 단일 라인 `0.00012346`을 포함합니다. 이는 **export excel to txt** 과정이 **limit decimal places**와 **keep significant digits** 요구 사항을 모두 충족함을 보여줍니다.

## 결론

이제 Aspose.Cells for Java를 사용해 숫자 정밀도를 제어하면서 **Excel을 TXT로 내보내는** 방법을 알게 되었습니다. `TxtSaveOptions`를 구성하면 **소수점 자리수 제한**, **유효 숫자 유지**를 할 수 있으며, 추가 후처리 없이도 신뢰성 있게 **워크북을 txt로 저장**할 수 있습니다.

다음에 배울 내용은:

- 여러 시트를 별도의 TXT 파일로 내보내기 (`save workbook as txt`를 시트별로 사용)
- `setSeparator`를 사용해 CSV 호환 출력 만들기
- 대용량 데이터 세트를 위한 배치 변환 자동화

프로젝트의 정확한 요구에 맞게 다양한 자리수와 구분자를 실험해 보세요. 즐거운 코딩 되세요!

## 다음에 배울 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료는 단계별 설명과 함께 완전한 코드 예제를 제공하여 추가 API 기능을 숙달하고 프로젝트에서 대체 구현 방식을 탐색하도록 돕습니다.

- [Aspose.Cells Java를 사용해 Excel을 HTML로 생성 및 내보내는 방법 | 워크북 작업 가이드](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Excel을 텍스트로 저장 – Excel을 TXT로 내보내는 완전한 C# 가이드](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Aspose.Cells for Java를 사용해 Excel 워크북을 이미지로 내보내기: 단계별 가이드](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}