---
category: general
date: 2026-11-22
description: Aprenda como definir o locale em uma planilha Java, alterar o idioma
  da planilha e configurar o calendário para japonês com exemplos de código claros.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set locale
- change workbook language
- set locale to japanese
- how to set calendar
language: pt
lastmod: 2026-11-22
og_description: Como definir o locale em uma planilha Java rapidamente. Siga este
  tutorial para mudar o idioma da planilha, definir o locale para japonês e configurar
  o calendário japonês.
og_image_alt: Screenshot showing how to set locale in a Java workbook
og_title: Como definir o locale em um workbook Java – guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  headline: How to set locale in a Java workbook using Aspose.Cells
  type: TechArticle
- description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  name: How to set locale in a Java workbook using Aspose.Cells
  steps:
  - name: Run the **FullLocaleExample** class.
    text: Run the **FullLocaleExample** class.
  - name: Open the generated `FullJapaneseLocale.xlsx` in Excel.
    text: Open the generated `FullJapaneseLocale.xlsx` in Excel.
  - name: 'Verify that:'
    text: 'Verify that:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Internationalization
- Workbook
title: Como definir a localidade em uma planilha Java usando Aspose.Cells
url: /pt/java/workbook-operations/how-to-set-locale-in-a-java-workbook-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como definir o locale em uma pasta de trabalho Java usando Aspose.Cells

Definir o locale em uma pasta de trabalho Java é um requisito comum quando você precisa adaptar sua planilha a diferentes regiões. Neste guia, você aprenderá como definir o locale, alterar o idioma da pasta de trabalho e definir o calendário para japonês usando a API Aspose.Cells.

Internacionalizar uma pasta de trabalho vai além de traduzir texto; também influencia formatos numéricos, análise de datas e o sistema de calendário padrão. Ao final deste tutorial, você será capaz de:

* Configurar o locale da pasta de trabalho para Japonês (Japão) – **set locale to japanese**.  
* Alterar o idioma da pasta de trabalho para que fórmulas e strings da UI respeitem a cultura alvo – **change workbook language**.  
* Trocar o calendário para o calendário imperial japonês – **how to set calendar**.  

As etapas funcionam com qualquer versão recente do Aspose.Cells para Java (v23.9 ou posterior) e requerem apenas um ambiente de desenvolvimento Java padrão.

## Pré-requisitos

| Requisito | Motivo |
|-------------|--------|
| Java 8 ou superior | A biblioteca tem como alvo Java 8+. |
| Aspose.Cells for Java (v23.9+) | Fornece `Workbook`, `WorkbookSettings` e utilitários de locale. |
| IDE (IntelliJ IDEA, Eclipse, ou VS Code) | Para compilar e executar o exemplo. |
| Conhecimento básico de Java | Necessário para entender os trechos de código. |

Adicione a dependência Maven do Aspose.Cells ao seu `pom.xml` (ou faça o download do JAR manualmente):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust for your JDK version -->
</dependency>
```

## Como definir locale e calendário em uma pasta de trabalho

O primeiro passo é criar uma instância de workbook e obter seu objeto de configurações. O objeto de configurações expõe as APIs de locale e calendário.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorkbookSettings;
import java.util.Locale;
import java.util.Calendar;

public class WorkbookLocaleDemo {
    public static void main(String[] args) {
        // Step 1: Create a new workbook (empty by default)
        Workbook workbook = new Workbook();

        // Step 2: Access the workbook's settings
        WorkbookSettings settings = workbook.getSettings();

        // Step 3: Set the calendar to the Japanese calendar
        // Aspose.Cells uses java.util.Calendar; the Japanese calendar is available via Calendar.JAPANESE
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // Step 4: Set the locale to Japanese (Japan)
        // This influences number formats, date formats, and built‑in function behaviour.
        settings.setLocale(new Locale("ja", "JP"));

        // Optional: Save the workbook to verify the settings
        workbook.save("LocaleDemo.xlsx");
    }
}
```

### Por que cada linha importa

* **`new Workbook()`** – Instancia um workbook vazio que você pode manipular antes de salvar.  
* **`getSettings()`** – Retorna um objeto `WorkbookSettings`; todas as opções regionais vivem aqui.  
* **`setCalendar(...)`** – Substitui o calendário gregoriano padrão pelo calendário imperial japonês, afetando como as datas são renderizadas e analisadas.  
* **`setLocale(new Locale("ja","JP"))`** – Altera o idioma e as convenções regionais (por exemplo, meses, separadores decimais). Este é o núcleo de **how to set locale** para o workbook.  

Executar o programa cria `LocaleDemo.xlsx`. Abra-o no Excel ou LibreOffice e você verá nomes de meses em japonês, símbolos de moeda Yen japonês e datas formatadas de acordo com o calendário japonês.

## Alterar o idioma da pasta de trabalho (definir locale para Japonês)

Se seu objetivo principal é **alterar o idioma da pasta de trabalho**, você pode focar apenas na chamada `setLocale`. O trecho a seguir isola essa etapa:

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Change only the language to Japanese (Japan)
settings.setLocale(new Locale("ja", "JP"));
workbook.save("JapaneseLanguage.xlsx");
```

**O que muda?**  
* As strings de formatação de célula mudam para japonês (por exemplo, `#,##0.00` torna‑se `#,##0.00` com o símbolo de yen).  
* Nomes de funções internas (como `SUM`) permanecem em inglês porque o locale das funções do Excel é independente, mas strings de datas e mensagens de erro seguem convenções japonesas.  

**Quando usar isso?**  
* Quando você precisa de uma planilha que exiba números e datas para um público japonês, mas o calendário subjacente pode permanecer gregoriano.  
* Para relatórios que são exportados para PDF ou impressos, garantindo que o idioma visual corresponda ao mercado alvo.

## Como definir o calendário para o calendário japonês

Às vezes, o requisito de **how to set calendar** é separado do locale. Para sistemas legados que armazenam datas na era imperial japonesa, você deve definir explicitamente o calendário, opcionalmente mantendo o locale padrão.

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Set only the calendar; keep the default (US) locale
settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

// Verify the calendar by creating a date cell
int row = 0, column = 0;
workbook.getWorksheets().get(0).getCells().putValue(row, column, new java.util.Date());

// Save to see the Japanese era (e.g., "R3/04/01" for Reiwa 3)
workbook.save("JapaneseCalendar.xlsx");
```

**Pontos‑chave:**

* `Calendar.getInstance(Locale.JAPAN)` retorna um `java.util.Calendar` configurado para a era japonesa.  
* O workbook agora renderizará datas usando símbolos de era (R para Reiwa, H para Heisei, etc.).  
* Essa configuração **não** afeta a formatação numérica ou o idioma da UI; combine‑a com `setLocale` se precisar de ambos.

## Exemplo completo de ponta a ponta

Abaixo está um programa completo e executável que demonstra **how to set locale**, **change workbook language** e **set the calendar** em um fluxo coeso. Ele também adiciona uma célula de exemplo para ilustrar o efeito.

```java
import com.aspose.cells.*;
import java.util.*;

public class FullLocaleExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Access settings
        WorkbookSettings settings = workbook.getSettings();

        // 1️⃣ Set the locale to Japanese (Japan) – changes language & number formats
        settings.setLocale(new Locale("ja", "JP"));

        // 2️⃣ Set the calendar to the Japanese imperial calendar
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // 3️⃣ Add a sample date and number to visualize the changes
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Date cell – will show Japanese era after applying the calendar
        cells.putValue(0, 0, new Date());

        // Number cell – will use Japanese Yen symbol and comma separator
        cells.putValue(1, 0, 1234567.89);

        // Apply a style to the number cell for currency formatting
        Style style = cells.getRows().get(1).getStyle();
        style.setNumber(3); // Built‑in currency format
        cells.getRows().get(1).setStyle(style);

        // Save the workbook
        workbook.save("FullJapaneseLocale.xlsx");
        System.out.println("Workbook created with Japanese locale and calendar.");
    }
}
```

**Saída esperada:**  
Abrindo `FullJapaneseLocale.xlsx` mostra a primeira célula com uma data como `R3/04/01` (Reiwa 3) e a segunda célula formatada como `¥1,234,567.89`. Isso confirma que **how to set locale**, **change workbook language** e **how to set calendar** funcionam juntos.

## Armadilhas comuns e como evitá‑las

| Armadilha | Por que acontece | Correção |
|-----------|------------------|----------|
| Usar `Locale.CHINA` em vez de `new Locale("ja","JP")` | `Locale.CHINA` define o idioma chinês, não japonês. | Sempre instancie `Locale` com `"ja", "JP"` para japonês. |
| Esquecer de chamar `settings.setCalendar(...)` após `setLocale` | O calendário padrão é o gregoriano, então as datas aparecem na era errada. | Chame `setCalendar` **depois** de definir o locale, ou defina ambos juntos conforme mostrado. |
| Salvar o workbook antes de aplicar as configurações | As configurações são aplicadas ao objeto em memória; salvar cedo grava o locale padrão. | Aplique todas as alterações de locale/calendário **antes** de chamar `workbook.save()`. |
| Usar uma versão desatualizada do Aspose.Cells | Versões antigas não possuem sobrecargas `setCalendar`. | Atualize para v23.9+ ou verifique as notas de versão para suporte a locale. |

## Testando sua configuração

1. Execute a classe **FullLocaleExample**.  
2. Abra o `FullJapaneseLocale.xlsx` gerado no Excel.  
3. Verifique que:  
   * A coluna de datas mostra símbolos de era japoneses (`R`, `H`, etc.).  
   * A coluna de números usa o símbolo Yen e separadores de vírgula.  
   * Qualquer mensagem de erro interna (por exemplo, `#DIV/0!`) aparece em japonês se o workbook contiver erros.  

Se alguma dessas verificações falhar, verifique novamente se o objeto `WorkbookSettings` que você modificou é a mesma instância usada ao salvar.

## Próximos passos

* **Localize formulas** – Enquanto o locale controla a formatação, você também pode traduzir nomes de funções personalizadas usando `FormulaParser`.  
* **Apply locale to existing workbooks** – Carregue um workbook com `new Workbook

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Formato de Data Aspose Cells: Como Definir Formato de Data Personalizado em Java](/cells/english/java/formatting/aspose-cells-date-format-how-to-set-custom-date-format-in-ja/)
- [Como Definir Idioma em Arquivos Excel Usando Aspose.Cells .NET para Suporte Multilíngue](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)
- [Como definir formato numérico de célula e converter datas japonesas em C# usando Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}