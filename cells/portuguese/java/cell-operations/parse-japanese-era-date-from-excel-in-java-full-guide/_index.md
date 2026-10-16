---
category: general
date: 2026-10-07
description: Ler data do Excel em Java com Aspose.Cells. Este guia mostra como analisar
  datas de eras japonesas, ler data de células do Excel e extrair datetime de células
  do Excel rapidamente.
draft: false
keywords:
- read date from excel
- extract datetime from excel
- java excel date conversion
- japanese era date parsing
- aspose.cells java
lastmod: 2026-10-07
og_description: Ler data do Excel em Java com Aspose.Cells. Este guia mostra como
  analisar datas de eras japonesas, ler data de células do Excel e extrair datetime
  de células do Excel em apenas alguns passos.
og_image_alt: 'Developer guide: Read date from Excel in Java using Aspose.Cells'
og_title: Ler data do Excel em Java com Aspose.Cells – guia completo
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Read date from Excel in Java with Aspose.Cells. This guide shows you
    how to parse Japanese era dates, read date from Excel cells, and extract datetime
    from Excel cells quickly.
  headline: Read date from Excel in Java with Aspose.Cells – full guide
  type: TechArticle
- description: Read date from Excel in Java with Aspose.Cells. This guide shows you
    how to parse Japanese era dates, read date from Excel cells, and extract datetime
    from Excel cells quickly.
  name: Read date from Excel in Java with Aspose.Cells – full guide
  steps:
  - name: Multiple Eras
    text: Japan has had several eras (Meiji, Taishō, Shōwa, Heisei, Reiwa). The `setParseDateUsingJapaneseEra(true)`
      flag covers all of them automatically, but be aware that older dates may fall
      outside the library’s supported range (typically 1868‑present). If you encounter
      a date like “昭和45年12月31日”, the sam
  - name: Blank or Invalid Cells
    text: 'If a cell is empty or contains a malformed string, `cell.getDateTime()`
      throws a `CellsException`. Guard against this with a simple check:'
  - name: Time Component
    text: The example only includes a date, but if your Excel file also stores time
      (e.g., “令和3年5月10日 14:30”), Aspose.Cells will preserve the time portion. The
      `LocalDateTime` you receive will include hours, minutes, and seconds.
  type: HowTo
tags:
- Java
- Excel
- DateTime
- read date from excel
- java excel date conversion
title: Ler data do Excel em Java com Aspose.Cells – guia completo
url: /pt/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ler data do Excel em Java com Aspose.Cells – guia completo

Se você precisa **ler data do Excel** em planilhas que contêm strings de era japonesa, está no lugar certo. Em muitas planilhas legadas de contabilidade ou governamentais a data é armazenada como “令和3年5月10日”, e convertê‑la para um `LocalDateTime` gregoriano padrão pode ser propenso a erros. Este tutorial mostra, passo a passo, como habilitar a análise sensível a eras, ler o valor da célula e **extrair datetime do Excel** usando Aspose.Cells para Java.

## Respostas rápidas
- **Qual biblioteca lida com datas de era japonesa?** Aspose.Cells para Java.  
- **Qual versão do Java é necessária?** Java 17 ou mais recente (Java 8 também funciona).  
- **Preciso de licença para testes?** Uma avaliação gratuita é suficiente para desenvolvimento.  
- **O mesmo código lê datas gregorianas?** Sim, a API detecta o formato automaticamente.  
- **A informação de horário é preservada?** Absolutamente – horas, minutos e segundos são mantidos na conversão.

## O que significa ler data do Excel?
A expressão “ler data do Excel” refere‑se a obter o valor de data de uma célula e convertê‑lo em um objeto de data‑hora Java, como `java.time.LocalDateTime`. Aspose.Cells abstrai o formato binário de baixo nível do Excel, permitindo trabalhar com datas sem precisar analisar strings manualmente.

## Por que usar Aspose.Cells para análise de eras japonesas?
Aspose.Cells suporta **mais de 50 formatos de entrada e saída** e pode processar pastas de trabalho com centenas de páginas sem carregar todo o arquivo na memória. Seu analisador interno sensível a eras converte todas as eras japonesas (Meiji, Taishō, Shōwa, Heisei, Reiwa) para datas gregorianas em uma única chamada de API, eliminando código frágil baseado em expressões regulares.

## Pré‑requisitos
- Java 17 (ou Java 8+) instalado na sua máquina.  
- Sistema de build Maven ou Gradle.  
- Familiaridade básica com arquivos Excel.  
- Biblioteca Aspose.Cells para Java (versão de avaliação ou licenciada).

Se algum desses itens lhe for desconhecido, não se preocupe—você verá exatamente como adicionar a biblioteca no próximo passo.

## Como ler data do Excel em Java?

Carregue sua pasta de trabalho, habilite a análise sensível a eras e solicite ao célula seu valor `DateTime`. Todo o processo leva **duas linhas de código funcional** assim que a biblioteca está no classpath.

### Etapa 1: adicionar Aspose.Cells ao seu projeto

**Maven**:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- check for latest version -->
</dependency>
```

**Gradle**:

```groovy
implementation 'com.aspose:aspose-cells:24.9'
```

Depois que a dependência for resolvida, você pode começar a usar a API para **ler data do Excel** nas células.

### Etapa 2: criar uma pasta de trabalho e selecionar a primeira planilha

A classe `Workbook` representa um arquivo Excel completo na memória. Criar uma nova instância garante um ambiente limpo para as etapas subsequentes de análise.

```java
import com.aspose.cells.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize workbook and worksheet
        Workbook workbook = new Workbook();               // creates a blank workbook
        Worksheet sheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

### Etapa 3: inserir uma string de data de era japonesa na célula A1

Para demonstração, escrevemos a string de era nós mesmos; em produção você carregaria um `.xlsx` existente.

```java
        // Step 3: Insert a Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日"); // Reiwa 3rd year = 2021-05-10
```

O texto segue o padrão convencional japonês: *Era* + *Ano* + *Mês* + *Dia*.

### Etapa 4: habilitar a análise de datas sensível a eras

Diga ao Aspose.Cells para tratar strings de era como datas definindo a propriedade `ParseDateUsingJapaneseEra`.  
`ParseDateUsingJapaneseEra` é uma propriedade que, quando verdadeira, habilita a conversão automática de strings de era japonesa para datas gregorianas.

```java
        // Step 4: Turn on era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);
```

Sem essa propriedade, a biblioteca trataria “令和3年5月10日” como texto simples, e você perderia a conversão automática.

### Etapa 5: recuperar o valor DateTime analisado

Agora solicite à célula sua representação de data. `cell.getDateTime()` devolve o valor da célula como um objeto `java.util.Date`. O método retorna um `java.util.Date`, que convertemos imediatamente para o moderno `java.time.LocalDateTime`. `LocalDateTime` é uma classe Java que representa data e hora sem fuso horário.

```java
        // Step 5: Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime(); // returns java.util.Date
        // Convert to java.time.LocalDateTime for modern APIs
        java.time.Instant instant = javaDate.toInstant();
        java.time.ZoneId zone = java.time.ZoneId.systemDefault();
        java.time.LocalDateTime dateTime = java.time.LocalDateTime.ofInstant(instant, zone);
```

Isso satisfaz o requisito de **extrair datetime do Excel** de forma segura em termos de tipo.

### Etapa 6: verificar o resultado

Imprima a data gregoriana para confirmar que a conversão foi bem‑sucedida.

```java
        // Step 6: Output the Gregorian date
        System.out.println(dateTime); // Expected output: 2021-05-10T00:00
    }
}
```

Ao executar o programa, você deverá ver:

```
2021-05-10T00:00
```

A saída comprova que lemos **data do Excel**, analisamos a era japonesa e **extraímos datetime do Excel** em um fluxo único.

## Tratamento de casos reais

### Múltiplas eras

O Japão teve várias eras (Meiji, Taishō, Shōwa, Heisei, Reiwa). A flag `setParseDateUsingJapaneseEra(true)` cobre todas elas automaticamente, mas esteja ciente de que datas mais antigas podem estar fora do intervalo suportado pela biblioteca (geralmente 1868‑presente). Se você encontrar uma data como “昭和45年12月31日”, o mesmo código a converterá para 1970‑12‑31.

### Células vazias ou inválidas

Se uma célula estiver vazia ou contiver uma string malformada, `cell.getDateTime()` lança uma `CellsException`. Proteja‑se com uma verificação simples:

```java
if (cell.getType() == CellValueType.IS_DATE) {
    // safe to call getDateTime()
} else {
    System.out.println("Cell does not contain a parsable date.");
}
```

### Componente de horário

O exemplo inclui apenas data, mas se seu arquivo Excel também armazenar horário (por exemplo, “令和3年5月10日 14:30”), Aspose.Cells preservará a parte de tempo. O `LocalDateTime` que você receberá incluirá horas, minutos e segundos.

## Exemplo completo funcionando

Juntando tudo, aqui está o programa completo, pronto para copiar e colar:

```java
import com.aspose.cells.*;
import java.time.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Insert Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日");

        // Enable era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);

        // Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime();
        LocalDateTime dateTime = javaDate.toInstant()
                                         .atZone(ZoneId.systemDefault())
                                         .toLocalDateTime();

        // Output the Gregorian date
        System.out.println(dateTime); // 2021-05-10T00:00
    }
}
```

Salve como `JapaneseEraDateParser.java`, compile com `javac` e execute com `java`. Se tudo estiver configurado corretamente, a data gregoriana será impressa no console.

## Dicas profissionais & armadilhas comuns

- **Dica:** Habilite `setParseDateUsingJapaneseEra(true)` **antes** de ler quaisquer valores de célula. Alterar a flag depois não converterá retroativamente células já lidas.  
- **Observação de localidade:** O analisador trabalha diretamente com os caracteres Unicode, portanto não é necessário definir explicitamente uma localidade japonesa.  
- **Desempenho:** A análise de eras adiciona um overhead insignificante. Se precisar apenas para algumas células, ative a flag apenas para essas leituras.  
- **Testes:** Use a avaliação gratuita da Aspose para validar contra uma pasta de trabalho real que mistura datas gregorianas e de era. Isso garante que o código de produção se comporte como esperado.

## Perguntas frequentes

**P: Posso usar esta abordagem com um arquivo .xlsx existente?**  
R: Sim. Carregue o arquivo com `new Workbook("path/to/file.xlsx")` e a mesma flag analisará quaisquer strings de era encontradas.

**P: O que acontece se a célula contiver uma data gregoriana?**  
R: A biblioteca devolve o valor gregoriano inalterado; a análise de era afeta apenas strings que correspondam ao padrão de era.

**P: Aspose.Cells suporta datas anteriores a Meiji (1868)?**  
R: Não. Datas anteriores a 1868 estão fora do intervalo suportado e serão tratadas como texto simples.

**P: Como lidar com pastas de trabalho grandes sem esgotar a memória?**  
R: Use o construtor `Workbook` que aceita `LoadOptions` com `setMemorySetting(MemorySetting.MemoryPreference)` para transmitir dados em vez de carregar tudo de uma vez.

**P: É necessária licença comercial para uso em produção?**  
R: Sim, uma licença válida de Aspose.Cells remove as limitações de avaliação e habilita desempenho total.

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Master the 1904 Date System in Excel Using Aspose.Cells Java for Effective Cell Operations](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Efficiently Convert Excel to PDF with Custom Date Formats Using Aspose.Cells for Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [How to Select Cell Ranges in Excel Using Aspose.Cells for Java (2023 Guide)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

---

**Última atualização:** 2026-10-07  
**Testado com:** Aspose.Cells 24.12 para Java  
**Autor:** Aspose

## Tutoriais relacionados

- [Parse Japanese Era Date From Excel In Java Full Guide](/cells/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/)
- [Read Excel File Java with Aspose.Cells – Complete Guide](/cells/java/automation-batch-processing/aspose-cells-java-excel-manipulation/)
- [Save Excel Workbook with Aspose.Cells for Java – Complete Guide](/cells/java/automation-batch-processing/excel-workbook-automation-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}