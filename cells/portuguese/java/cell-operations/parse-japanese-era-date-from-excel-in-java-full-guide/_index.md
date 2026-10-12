---
category: general
date: 2026-06-18
description: Analise a data da era japonesa em Java usando Aspose.Cells. Aprenda como
  ler a data de uma célula do Excel e extrair a data e hora da célula do Excel rapidamente.
draft: false
keywords:
- parse japanese era date
- read date from excel cell
- extract datetime from excel cell
language: pt
og_description: Analise a data da era japonesa em Java com Aspose.Cells. Este guia
  mostra como ler a data de uma célula do Excel e extrair a data e hora da célula
  do Excel em apenas alguns passos.
og_title: Analisar data da era japonesa a partir do Excel em Java – Tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Parse Japanese era date in Java using Aspose.Cells. Learn how to read
    date from Excel cell and extract datetime from Excel cell quickly.
  headline: Parse Japanese Era Date from Excel in Java – Full Guide
  type: TechArticle
- description: Parse Japanese era date in Java using Aspose.Cells. Learn how to read
    date from Excel cell and extract datetime from Excel cell quickly.
  name: Parse Japanese Era Date from Excel in Java – Full Guide
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
title: Analisar data da era japonesa do Excel em Java – Guia completo
url: /pt/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Analisar Data de Era Japonesa a partir do Excel em Java – Guia Completo

Já precisou **analisar data de era japonesa** armazenada em uma planilha Excel, mas não sabia como transformá‑la em um `DateTime` gregoriano regular? Você não está sozinho — muitos desenvolvedores encontram esse obstáculo ao lidar com planilhas contábeis japonesas legadas ou formulários governamentais. A boa notícia é que, com algumas linhas de Java e a biblioteca correta, você pode ler a data de uma célula do Excel e extrair datetime de uma célula do Excel sem nenhuma manipulação manual de strings.

Neste tutorial vamos percorrer um exemplo completo e executável que mostra exatamente como **analisar strings de data de era japonesa** como “令和3年5月10日” para um `java.time.LocalDateTime` em Java. Vamos cobrir a dependência Maven necessária, explicar por que você deve habilitar a análise sensível à era, e apontar armadilhas comuns que você pode encontrar. Ao final, você terá um trecho de código sólido, pronto para produção, que pode ser inserido em qualquer projeto Java.

## Pré‑requisitos

- Java 17 ou superior (o código funciona também em Java 8+)
- Sistema de build Maven ou Gradle
- Familiaridade básica com arquivos Excel
- A biblioteca **Aspose.Cells for Java** (versão de teste gratuita serve para experimentação)

Se algum desses itens lhe for desconhecido, não se preocupe — mostrarei exatamente como adicionar a biblioteca e começar.

## Etapa 1: Adicionar Aspose.Cells ao Seu Projeto

Primeiro de tudo: você precisa da biblioteca que entende datas de era japonesa. Aspose.Cells faz o trabalho pesado para você.

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

Depois que a dependência for resolvida, você pode começar a escrever código que *lê data de célula do Excel* e *extrai datetime de célula do Excel*.

## Etapa 2: Criar um Workbook e Selecionar a Primeira Worksheet

Começaremos criando um novo workbook em memória e obtendo a primeira planilha. Isso reproduz as duas primeiras linhas do exemplo original.

```java
import com.aspose.cells.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize workbook and worksheet
        Workbook workbook = new Workbook();               // creates a blank workbook
        Worksheet sheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

Por que iniciar com um workbook novo? Ele garante um ambiente limpo onde podemos controlar cada configuração — crítico quando você habilitar a análise sensível à era mais adiante.

## Etapa 3: Inserir uma String de Data de Era Japonesa na Célula A1

Agora simulamos um arquivo Excel que já contém uma data de era japonesa. Na prática, você provavelmente carregaria um `.xlsx` existente, mas para fins de ilustração vamos **escrever** o valor nós mesmos.

```java
        // Step 3: Insert a Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日"); // Reiwa 3rd year = 2021-05-10
```

A string segue a notação japonesa padrão: *Era* + *Ano* + *Mês* + *Dia*. Sem configuração extra, Aspose.Cells trataria isso como texto simples, não como data.

## Etapa 4: Habilitar a Análise Sensível à Era

Aqui está a parte crucial: dizer ao workbook para **analisar datas de era japonesa** quando encontrá‑las. Isso é feito via a flag `ParseDateUsingJapaneseEra`.

```java
        // Step 4: Turn on era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);
```

Por que isso é necessário? Por padrão, Aspose.Cells assume o calendário gregoriano, então “令和3年5月10日” permaneceria como string. Habilitar a flag instrui o motor a convertê‑la para um `java.util.Date` (ou equivalente `java.time`) nos bastidores.

## Etapa 5: Recuperar o Valor DateTime Analisado

Agora que o workbook sabe como interpretar a era, podemos solicitar à célula sua representação `DateTime`.

```java
        // Step 5: Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime(); // returns java.util.Date
        // Convert to java.time.LocalDateTime for modern APIs
        java.time.Instant instant = javaDate.toInstant();
        java.time.ZoneId zone = java.time.ZoneId.systemDefault();
        java.time.LocalDateTime dateTime = java.time.LocalDateTime.ofInstant(instant, zone);
```

Observe que **lêmos data de célula do Excel** usando `cell.getDateTime()`. O método devolve um `java.util.Date`, que convertemos imediatamente para `LocalDateTime` para maior segurança de tipos. Isso satisfaz o requisito de **extrair datetime de célula do Excel** de forma limpa e idiomática.

## Etapa 6: Verificar o Resultado

Por fim, vamos imprimir a data gregoriana para confirmar que a conversão funcionou.

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

Essa saída prova que conseguimos **analisar data de era japonesa**, **ler data de célula do Excel** e **extrair datetime de célula do Excel** em um único fluxo.

## Lidando com Casos de Borda do Mundo Real

### Múltiplas Eras

O Japão teve várias eras (Meiji, Taishō, Shōwa, Heisei, Reiwa). A flag `setParseDateUsingJapaneseEra(true)` cobre todas automaticamente, mas esteja ciente de que datas mais antigas podem ficar fora do intervalo suportado pela biblioteca (geralmente 1868‑presente). Se você encontrar uma data como “昭和45年12月31日”, o mesmo código a converterá para 1970‑12‑31.

### Células Vazias ou Inválidas

Se uma célula estiver vazia ou contiver uma string malformada, `cell.getDateTime()` lança uma `CellsException`. Proteja‑se com uma verificação simples:

```java
if (cell.getType() == CellValueType.IS_DATE) {
    // safe to call getDateTime()
} else {
    System.out.println("Cell does not contain a parsable date.");
}
```

### Componente de Hora

O exemplo inclui apenas data, mas se seu arquivo Excel também armazenar hora (por exemplo, “令和3年5月10日 14:30”), Aspose.Cells preservará a parte horária. O `LocalDateTime` que você receberá incluirá horas, minutos e segundos.

## Exemplo Completo Funcionando

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

## Dicas Profissionais & Armadilhas Comuns

- **Dica:** Sempre chame `setParseDateUsingJapaneseEra(true)` **antes** de ler qualquer valor de célula. Alterar a flag depois de ler uma célula não converte retroativamente o valor.
- **Fique atento ao locale:** A biblioteca analisa strings de era com base em caracteres Unicode, portanto não é necessário definir explicitamente um locale japonês.
- **Nota de desempenho:** Habilitar a análise de era adiciona um pequeno overhead. Se precisar apenas para algumas células, você pode alternar a flag temporariamente, ler as células e depois desativá‑la novamente.
- **Testes:** Use a versão de teste gratuita da Aspose para validar contra um arquivo Excel real que contenha múltiplas datas de era. Isso garante que seu código de produção se comporte como esperado.

## Conclusão

Acabamos de demonstrar como **analisar datas de era japonesa** diretamente de um workbook Excel usando Java e Aspose.Cells. Ao habilitar a análise sensível à era, você pode **ler data de célula do Excel** e **extrair datetime de célula do Excel** de maneira limpa e segura. A abordagem funciona para qualquer era japonesa moderna, lida com componentes de hora e trata graciosamente dados inválidos.

Pronto para o próximo desafio? Experimente carregar um arquivo `.xlsx` real que contenha uma mistura de datas gregorianas e de era japonesa, ou experimente formatar o `LocalDateTime` resultante em strings que correspondam ao seu locale. Você também pode explorar escrever as datas convertidas de volta ao Excel para sistemas downstream que entendem apenas datas gregorianas.

Tem perguntas ou encontrou algum caso de borda curioso? Deixe um comentário abaixo, e feliz codificação!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Domine o Sistema de Data 1904 no Excel Usando Aspose.Cells Java para Operações de Célula Eficientes](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Converta Excel para PDF de Forma Eficiente com Formatos de Data Personalizados Usando Aspose.Cells para Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Como Selecionar Intervalos de Células no Excel Usando Aspose.Cells para Java (Guia 2023)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}