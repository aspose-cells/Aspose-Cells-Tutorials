---
category: general
date: 2026-06-21
description: Guia de formato de data do Aspose Cells – aprenda como definir um formato
  de data personalizado, alterar o idioma da pasta de trabalho e aplicar um formato
  de data global em Java.
draft: false
keywords:
- aspose cells date format
- set custom date format
- how to set date format
- change workbook locale
- set global date format
language: pt
og_description: 'Tutorial de formato de data do Aspose Cells: aprenda como definir
  um formato de data personalizado, alterar a localidade da pasta de trabalho e definir
  o formato de data global para projetos Java.'
og_title: Formato de Data do Aspose Cells – Definir Formato de Data Personalizado
  em Java
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Aspose Cells date format guide – learn how to set custom date format,
    change workbook locale, and apply a global date format in Java.
  headline: 'Aspose Cells Date Format: How to Set Custom Date Format in Java'
  type: TechArticle
- description: Aspose Cells date format guide – learn how to set custom date format,
    change workbook locale, and apply a global date format in Java.
  name: 'Aspose Cells Date Format: How to Set Custom Date Format in Java'
  steps:
  - name: 1. Overriding the Global Format at the Cell Level
    text: 'If a cell already has a style with a specific number format, the global
      setting is ignored for that cell. To force the global format, clear the cell’s
      style:'
  - name: 2. Changing Workbook Locale Without a Custom Pattern
    text: 'Sometimes you just want to **change workbook locale** so that built‑in
      date formats (like `14‑03‑2024`) follow regional conventions. You can do this
      without a `DateTimeFormatter`:'
  - name: 3. Using Multiple Custom Formats in One Workbook
    text: 'Aspose Cells allows you to define several custom formats and apply them
      selectively:'
  - name: 4. Resetting to the Default Format
    text: 'If you need to revert to Aspose’s default date handling, simply pass `null`:'
  type: HowTo
- questions:
  - answer: Yes—any worksheet loaded into the `Workbook` after you set the global
      format will inherit it, unless a cell already has an explicit style.
    question: Does this affect existing worksheets?
  - answer: Absolutely. The global format is applied at render time, so you can populate
      cells first and set the format later.
    question: Can I set the format after writing data?
  - answer: Use the appropriate `CultureInfo` code (`"th-TH"`), and the formatter
      will respect that calendar automatically.
    question: What if I need a locale‑specific calendar (e.g., Thai Buddhist)?
  - answer: Negligible. The formatter is cached inside `WorkbookSettings`, so the
      overhead is only incurred once per workbook.
    question: Is there a performance penalty?
  type: FAQPage
tags:
- aspose-cells
- java
- date-formatting
title: 'Formato de Data do Aspose Cells: Como Definir Formato de Data Personalizado
  em Java'
url: /pt/java/formatting/aspose-cells-date-format-how-to-set-custom-date-format-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Formato de Data do Aspose Cells – Guia Completo em Java

Já se perguntou como definir um formato de data personalizado no Aspose Cells para Java? Você não é o único. Seja gerando relatórios para um cliente japonês ou apenas precisando de um estilo de data consistente em toda a pasta de trabalho, dominar **aspose cells date format** é essencial.

Neste tutorial, percorreremos um exemplo prático, de ponta a ponta, que mostra **how to set date format** globalmente, altera o locale da pasta de trabalho e aplica um padrão personalizado como o ano da era japonesa. Ao final, você terá um trecho reutilizável que pode inserir em qualquer projeto—sem necessidade de adivinhações.

## O que este Guia Cobre

- Criando uma nova instância de `Workbook`.
- Alterando o locale da pasta de trabalho para que os formatos internos respeitem as regras regionais.
- Definindo um **set custom date format** usando `DateTimeFormatter`.
- Aplicando esse formato globalmente com `WorkbookSettings`.
- Armadilhas comuns (por exemplo, sobrescrever formatos a nível de célula) e como evitá‑las.
- Variações rápidas para outros locales ou strings de formato.

Você só precisa de um ambiente de desenvolvimento Java, Maven ou Gradle para incluir o Aspose Cells, e um entendimento básico da sintaxe Java. Pronto? Vamos mergulhar.

## Etapa 1: Configurar seu Projeto e Importar Aspose Cells

Primeiro de tudo—certifique-se de que o Aspose Cells para Java está no seu classpath. Se você estiver usando Maven, adicione a dependência a seguir ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

Usuários do Gradle podem adicionar:

```gradle
implementation 'com.aspose:aspose-cells:24.9'
```

> **Dica profissional:** Aspose oferece uma licença de avaliação gratuita de 30 dias. Coloque o arquivo `Aspose.Cells.lic` na raiz do seu projeto e chame `License license = new License(); license.setLicense("Aspose.Cells.lic");` antes de criar qualquer pasta de trabalho.

Agora importe as classes que precisaremos:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorkbookSettings;
import com.aspose.cells.DateTimeFormatter;
import com.aspose.cells.CultureInfo;
```

Essas importações nos dão acesso ao contêiner da pasta de trabalho, suas configurações e ao formatador sensível ao locale.

## Etapa 2: Criar uma Nova Pasta de Trabalho e Acessar suas Configurações

Um novo `Workbook` começa com o locale padrão (geralmente US). Para controlar o tratamento de datas globalmente, devemos obter seu objeto `WorkbookSettings`:

```java
// Step 2: Initialize a new workbook
Workbook workbook = new Workbook();

// Grab the settings object – this is where we’ll apply the date format
WorkbookSettings settings = workbook.getSettings();
```

O objeto `settings` é um hub central. Qualquer coisa que você mudar aqui—como o formato de data—afeta todas as células que **não** já possuem um estilo explícito que o sobrescreva.

## Etapa 3: Definir um Formato Personalizado de Data/Hora (Exemplo da Era Japonesa)

Vamos supor que você precise de datas no formato da era japonesa, por exemplo, “令和04.10.01”. O padrão `"ggyy.MM.dd"` funciona quando combinado com a cultura japonesa:

```java
// Step 3: Build a formatter for the Japanese era year
DateTimeFormatter formatter = new DateTimeFormatter(
        "ggyy.MM.dd",                // Pattern: era (gg), year (yy), month, day
        new CultureInfo("ja-JP")    // Locale: Japanese (Japan)
);
```

Se preferir um estilo ISO mais simples (`"yyyy-MM-dd"`), basta substituir a string do padrão—nenhuma outra alteração é necessária.

## Etapa 4: Aplicar o Formato Personalizado como Formato de Data Global

Agora vinculamos o formatador às configurações globais da pasta de trabalho. Esta é a etapa de **set global date format** que garante que qualquer célula exibindo uma data use automaticamente nosso padrão:

```java
// Step 4: Apply the custom formatter globally
settings.setDateTimeFormat(formatter);
```

Neste ponto, qualquer data que você escrever na planilha—seja via `Cell.putValue(new Date())` ou lendo de uma fonte de dados—será renderizada usando o padrão da era japonesa.

## Etapa 5: Preencher a Pasta de Trabalho com Datas de Exemplo (Opcional)

Vamos adicionar algumas linhas para que você veja o formato em ação. Esta parte não é estritamente necessária para a lógica de formatação de data, mas ajuda a verificar se tudo funciona:

```java
// Step 5: Insert sample dates into the first sheet
var sheet = workbook.getWorksheets().get(0);
var cells = sheet.getCells();

cells.get("A1").putValue(new java.util.Date()); // Today’s date
cells.get("A2").putValue(java.sql.Date.valueOf("2024-12-31")); // Specific date
cells.get("A3").putValue(java.time.LocalDateTime.now()); // Date‑time now
```

Ao salvar a pasta de trabalho, essas células exibirão algo como:

```
A1: 令和05.04.21
A2: 令和06.12.31
A3: 令和05.04.21 14:37:12
```

(O ano exato da era depende do calendário japonês atual.)

## Etapa 6: Salvar a Pasta de Trabalho e Verificar a Saída

Finalmente, escreva a pasta de trabalho em um arquivo para que você possa abri‑la no Excel, LibreOffice ou qualquer visualizador que respeite o formato:

```java
// Step 6: Save the workbook
workbook.save("CustomDateFormatDemo.xlsx");
System.out.println("Workbook saved with custom date format.");
```

Abra `CustomDateFormatDemo.xlsx` e você deverá ver as datas renderizadas de acordo com o padrão que definimos. Se notar alguma discrepância, verifique novamente se nenhum estilo a nível de célula está sobrescrevendo a configuração global (veja a seção “Casos Limítrofes” abaixo).

## Casos Limítrofes e Variações

### 1. Sobrescrevendo o Formato Global no Nível da Célula

Se uma célula já possui um estilo com um formato numérico específico, a configuração global é ignorada para essa célula. Para forçar o formato global, limpe o estilo da célula:

```java
cells.get("A1").getStyle().setNumber(0); // Reset number format to default
```

### 2. Alterando o Locale da Pasta de Trabalho sem um Padrão Personalizado

Às vezes você só quer **change workbook locale** para que os formatos de data internos (como `14‑03‑2024`) sigam as convenções regionais. Você pode fazer isso sem um `DateTimeFormatter`:

```java
WorkbookSettings localeSettings = workbook.getSettings();
localeSettings.setCultureInfo(new CultureInfo("fr-FR")); // French (France)
```

Agora qualquer estilo de data padrão aparecerá como `21/04/2025` em vez de `04/21/2025`.

### 3. Usando Múltiplos Formatos Personalizados em uma Única Pasta de Trabalho

Aspose Cells permite definir vários formatos personalizados e aplicá‑los seletivamente:

```java
// Define two formatters
DateTimeFormatter usFormatter = new DateTimeFormatter("MM/dd/yyyy", new CultureInfo("en-US"));
DateTimeFormatter jpFormatter = new DateTimeFormatter("ggyy.MM.dd", new CultureInfo("ja-JP"));

// Apply US format globally
settings.setDateTimeFormat(usFormatter);

// Later, apply Japanese format to a specific range
var style = workbook.createStyle();
style.setCustom(usFormatter.getFormatString()); // Or jpFormatter.getFormatString()
cells.get("B1").setStyle(style);
```

### 4. Restaurando o Formato Padrão

Se precisar reverter ao tratamento de data padrão do Aspose, basta passar `null`:

```java
settings.setDateTimeFormat(null); // Clears the custom global format
```

## Perguntas Frequentes Respondidas

- **Isso afeta planilhas existentes?**  
  Sim—qualquer planilha carregada no `Workbook` após você definir o formato global a herdará, a menos que uma célula já possua um estilo explícito.

- **Posso definir o formato depois de escrever os dados?**  
  Absolutamente. O formato global é aplicado no momento da renderização, então você pode preencher as células primeiro e definir o formato depois.

- **E se eu precisar de um calendário específico de locale (por exemplo, Budista Tailandês)?**  
  Use o código `CultureInfo` apropriado (`"th-TH"`), e o formatador respeitará esse calendário automaticamente.

- **Existe alguma penalidade de desempenho?**  
  Negligível. O formatador é armazenado em cache dentro de `WorkbookSettings`, portanto o overhead ocorre apenas uma vez por pasta de trabalho.

## Exemplo Completo em Funcionamento

Abaixo está o programa completo, pronto‑para‑executar, que incorpora cada etapa discutida:

```java
import com.aspose.cells.*;

public class AsposeCellsDateFormatDemo {
    public static void main(String[] args) throws Exception {
        // Apply license if you have one
        // License lic = new License();
        // lic.setLicense("Aspose.Cells.lic");

        // 1️⃣ Create workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Access settings
        WorkbookSettings settings = workbook.getSettings();

        // 3️⃣ Define custom Japanese era format
        DateTimeFormatter jpFormatter = new DateTimeFormatter(
                "ggyy.MM.dd",
                new CultureInfo("ja-JP")
        );

        // 4️⃣ Set as global date format
        settings.setDateTimeFormat(jpFormatter);

        // 5️⃣ Add sample dates
        var sheet = workbook.getWorksheets().get(0);
        var cells = sheet.getCells();

        cells.get("A1").putValue(new java.util.Date());                     // Today
        cells.get("A2").putValue(java.sql.Date.valueOf("2024-12-31"));      // Fixed date
        cells.get("A3").putValue(java.time.LocalDateTime.now());           // Date‑time now

        // 6️⃣ Save to file
        workbook.save("AsposeCellsCustomDateFormat.xlsx");
        System.out.println("Workbook saved with custom Japanese era date format.");
    }
}
```

**Saída esperada no Excel:**

| Célula | Valor Renderizado |
|--------|--------------------|
| A1   | 令和05.04.21   |
| A2   | 令和06.12.31   |
| A3   | 令和05.04.21 14:45:03 (time part may vary) |

Abra o arquivo, e você verá as datas formatadas exatamente como definido.

## Conclusão

Você acabou de aprender como **aspose cells date format** uma pasta de trabalho em Java, desde mudar o locale até aplicar um **set custom date format** que funciona globalmente. Ao utilizar `WorkbookSettings` e `DateTimeFormatter`, você obtém controle preciso sobre como cada data aparece—sem necessidade de estilização manual.

Em seguida, você pode explorar **how to set date format** apenas para colunas específicas, ou combinar formatos numéricos personalizados com formatação condicional para um relatório refinado. Os mesmos princípios se aplicam: defina um formatador, anexe‑o via estilo e deixe o Aspose cuidar do resto.

Feliz codificação, e sinta‑se à vontade para experimentar outros locales—seus usuários agradecerão pelas planilhas elegantes e culturalmente adequadas!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que expandem as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Converter Excel para PDF de Forma Eficiente com Formatos de Data Personalizados Usando Aspose.Cells para Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Dominar a Apresentação de Dados no Excel: Formatação de Números e Datas Personalizadas com Aspose.Cells para Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Como Criar e Formatar Células Excel Usando Aspose.Cells para Java: Um Guia Passo a Passo](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}