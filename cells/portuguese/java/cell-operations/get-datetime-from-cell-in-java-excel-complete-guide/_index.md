---
category: general
date: 2026-10-07
description: Aprenda a ler datas do Excel de células em Java usando Aspose.Cells e
  também a gravar valores de volta ao Excel de forma eficiente.
draft: false
keywords:
- how to read excel
- write value to excel
- get datetime from excel
- extract datetime from cell
- Aspose.Cells Java date parsing
lastmod: 2026-10-07
og_description: Como ler datas do Excel de células em Java usando Aspose.Cells. Este
  guia também mostra como gravar valores em células do Excel de forma eficiente.
og_image_alt: 'Developer guide: reading and writing Excel dates with Aspose.Cells
  Java'
og_title: Como ler datas do Excel de células em Java usando Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to read Excel dates from cells in Java using Aspose.Cells
    and write values back.
  headline: How to read Excel dates from cells in Java using Aspose.Cells
  type: TechArticle
- description: Learn how to read Excel dates from cells in Java using Aspose.Cells
    and write values back.
  name: How to read Excel dates from cells in Java using Aspose.Cells
  steps:
  - name: What if the cell already contains a true Excel date?
    text: 'If `cell.getType()` returns `CellValueType.IS_DATE_TIME`, you can skip
      the recalculation step and read the value directly:'
  - name: How to process a whole column of era strings?
    text: 'Loop through the used range and apply the same settings once:'
  - name: Can I disable the Japanese era handling later?
    text: 'Yes—just flip the flag back:'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- date parsing
- Excel automation
title: Como ler datas do Excel de células em Java usando Aspose.Cells
url: /pt/java/cell-operations/get-datetime-from-cell-in-java-excel-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como ler datas do Excel de células em Java usando Aspose.Cells

Se você precisa **how to read Excel** valores que são armazenados como strings de era japonesa, está no lugar certo. Muitos livros de trabalho legados contêm datas como “Reiwa 3/04/01”, e extrair um `java.time.LocalDateTime` adequado pode parecer decifrar um código. Aspose.Cells for Java entende essas notações de era, e também permite que você **write value to excel** células sem perder a formatação. Neste guia você obterá um walkthrough completo, passo a passo, que pode colar em qualquer projeto Maven hoje.

## Respostas rápidas
- **Can Aspose.Cells parse Japanese era dates?** Sim – habilite a flag do calendário de era japonesa e recalcule as fórmulas.  
- **Do I need to recalculate formulas manually?** Absolutamente; sem uma passagem de cálculo a string da era permanece como texto.  
- **How many Excel formats does Aspose.Cells support?** Mais de 50 formatos de entrada e saída, incluindo XLSX, XLS, CSV e ODS.  
- **Is the library compatible with Java 8+?** Sim, funciona com Java 8 e versões mais recentes do runtime.  
- **Can I write a Gregorian date back to the same cell?** Use `putValue` com um `LocalDateTime` e defina o formato numérico para exibir ISO‑8601.

## O que é how to read Excel dates from cells?
A frase **how to read Excel** refere-se à extração do conteúdo das células — especialmente datas — para tipos de programação nativos como `java.time.LocalDateTime`. Aspose.Cells abstrai o parsing de baixo nível, permitindo que você se concentre na lógica de negócios em vez das peculiaridades dos números seriais do Excel. Essa abordagem simplifica a manutenção do código e reduz a chance de erros de conversão ao lidar com planilhas legadas.

## Por que usar Aspose.Cells para conversão de era japonesa?
Aspose.Cells suporta **50+** formatos de arquivo e pode processar livros de trabalho com **centenas de páginas** sem carregar o arquivo inteiro na memória. Habilitar o calendário de era japonesa adiciona apenas um custo de desempenho insignificante, tornando-o ideal para processamento em lote de planilhas legadas. A biblioteca também preserva estilos de célula e fórmulas durante a conversão, garantindo que a saída tenha a mesma aparência do livro de trabalho original.

## Pré-requisitos

* **Java 8+** – os exemplos usam a moderna API `java.time`.  
* **Aspose.Cells for Java ≥ 23.9.0** – adicione a dependência Maven/Gradle do repositório oficial.  
* Conhecimento básico dos conceitos do Excel (planilhas, células, fórmulas).  

Se você não tem a biblioteca, obtenha-a no repositório oficial da Aspose:

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9.0</version>
    <classifier>jdk17</classifier>
</dependency>
```

## Como criar uma workbook e acessar a primeira worksheet?
`Workbook` representa um arquivo Excel carregado na memória. `Worksheet` representa uma única planilha dentro dessa workbook.  
Crie um objeto `Workbook`, que representa um arquivo Excel na memória, e então obtenha a primeira `Worksheet`. Isso lhe dá controle total antes que quaisquer dados toquem o disco. Ao inicializar a workbook primeiro, você pode configurar definições — como o tratamento de calendário — antes que quaisquer valores de célula sejam lidos ou escritos.

```java
// Step 1: Initialize workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

## Como escrever uma string de data de era japonesa na célula A1?
`Cell` é o objeto que contém o valor de uma única célula Excel.  
Insira a string de era legada “Reiwa 3/04/01” na célula A1. Isso imita um valor inserido pelo usuário que você converterá posteriormente. Escrever a string primeiro permite demonstrar todo o fluxo de conversão de texto para um objeto de data adequado.

```java
// Step 2: Write the era date string into A1
Cell cell = worksheet.getCells().get("A1");
cell.putValue("Reiwa 3/04/01"); // raw string, not yet a date
```

## Como habilitar o calendário de era japonesa para análise de datas?
`WorkbookSettings.setUseJapaneseEraCalendar(boolean)` alterna o recurso de conversão de era.  
Ative a flag do calendário para que o Aspose.Cells saiba como traduzir nomes de era para anos gregorianos. Habilitar essa flag informa ao motor de cálculo para interpretar strings como “Reiwa” como o ano gregoriano correspondente, o que é essencial para análise precisa de datas.

```java
// Step 3: Turn on Japanese era calendar support
WorkbookSettings settings = workbook.getSettings();
settings.setUseJapaneseEraCalendar(true);
```

## Como recalcular fórmulas para que a string de era seja convertida em uma data gregoriana?
`Workbook.calculateFormula()` força o motor de cálculo a avaliar todas as fórmulas na workbook.  
Execute o motor de cálculo uma vez; ele reconhece o padrão de era, converte e armazena o resultado gregoriano internamente. Depois disso, `getDateTime()` retorna um `java.util.Date`, que você pode converter para `java.time`. Esta etapa é necessária porque a string de era é inicialmente tratada como texto simples até que as fórmulas sejam avaliadas.

```java
// Step 4: Force a recalculation to convert the era string
workbook.calculateFormula(); // processes all cells, including A1
System.out.println(cell.getDateTime()); // → 2021‑04‑01
```

**Saída esperada**

```
2021-04-01T00:00:00.000+00:00
```

## Como escrever um novo valor de volta na mesma célula (ou em outra célula)?
`Cell.putValue(Object)` grava um valor em uma célula, lidando automaticamente com a conversão de tipo.  
Sobrescreva a string de era original com uma data ISO‑8601 limpa, preservando o estilo da célula. `putValue` detecta o tipo `LocalDateTime` e o converte para a representação numérica serial do Excel. Definir o formato numérico garante que a célula exiba a data exatamente como você espera ao abrir no Excel.

```java
// Step 5: Overwrite A1 with a formatted date string
java.time.LocalDateTime now = java.time.LocalDateTime.now();
cell.putValue(now); // Aspose will store it as a proper Excel date
// Optional: apply a date format style
Style style = cell.getStyle();
style.setNumber(14); // built‑in "m/d/yyyy" format
cell.setStyle(style);
```

## Exemplo completo em funcionamento

Todas as etapas acima são combinadas em uma única classe Java que você pode compilar e executar. Ela cria uma workbook, grava uma string de era, converte-a e, finalmente, salva o arquivo.

```java
import com.aspose.cells.*;

public class JapaneseEraDateDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create workbook & get first sheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 2️⃣ Write Japanese era date string to A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue("Reiwa 3/04/01");

        // 3️⃣ Enable Japanese era calendar
        WorkbookSettings settings = workbook.getSettings();
        settings.setUseJapaneseEraCalendar(true);

        // 4️⃣ Recalculate so the string becomes a Gregorian date
        workbook.calculateFormula();
        System.out.println("Converted date: " + cell.getDateTime());

        // 5️⃣ Overwrite with a clean LocalDateTime (optional)
        java.time.LocalDateTime now = java.time.LocalDateTime.now();
        cell.putValue(now);
        Style style = cell.getStyle();
        style.setNumber(14); // m/d/yyyy
        cell.setStyle(style);

        // 6️⃣ Save the workbook
        workbook.save("output.xlsx");
        System.out.println("Workbook saved as output.xlsx");
    }
}
```

Execute a classe com `java -cp aspose-cells-23.9.jar;. JapaneseEraDateDemo` e abra **output.xlsx**. A célula A1 mostrará a data gregoriana convertida, e o console registrará o valor “2021‑04‑01”.

## E se a célula já contiver uma data verdadeira do Excel?
Se a célula já armazenar uma data nativa do Excel, você pode lê-la diretamente sem processamento extra. Isso economiza tempo porque o motor de cálculo não precisa reinterpretar o valor. Basta verificar o tipo da célula e recuperar a data.

```java
if (cell.getType() == CellValueType.IS_DATE_TIME) {
    System.out.println("Already a date: " + cell.getDateTime());
}
```

## Como processar uma coluna inteira de strings de era?
Quando muitas células contêm strings de era, itere sobre o intervalo usado e aplique a mesma lógica de conversão a cada célula. Essa abordagem em lote reduz a sobrecarga em comparação ao tratamento de células individualmente. Lembre-se de habilitar o calendário de era japonesa antes do loop e recalcular uma vez após o processamento.

```java
Range used = worksheet.getCells().getMaxDisplayRange();
for (int row = 0; row < used.getRowCount(); row++) {
    Cell c = used.getCell(row, 0); // column A
    c.putValue(c.getStringValue()); // re‑assign to trigger parsing
}
workbook.calculateFormula();
```

## Posso desativar o tratamento de era japonesa depois?
Você pode desativar a flag de conversão de era depois de terminar o processamento das células relevantes. Desativá‑la restaura o comportamento padrão de parsing para quaisquer operações subsequentes. Isso é útil se precisar trabalhar com datas padrão mais tarde na mesma workbook.

Lembre-se de recalcular novamente se mudar a configuração após gravar os dados.

```java
settings.setUseJapaneseEraCalendar(false);
```

## Dicas profissionais & armadilhas

* **Performance:** Habilitar o calendário de era japonesa adiciona uma sobrecarga mínima. Ative‑o apenas para as células que precisam de conversão, depois desative.  
* **Locale awareness:** A string de era deve seguir o padrão exato “EraName yy/MM/dd”. Erros de ortografia (por exemplo, “Rewa”) mantêm a célula como texto simples.  
* **Saving format:** `Workbook.save("output.xlsx")` grava um arquivo XLSX. Use `"output.xls"` para o formato binário mais antigo, mas observe que alguns recursos avançados — como parsing de era — podem ser limitados.

## Perguntas frequentes

**Q: Essa abordagem funciona com outros calendários culturais (Tailandês, Hijri)?**  
A: Sim — Aspose.Cells fornece flags semelhantes para os calendários Budista Tailandês e Hijri; habilite a configuração apropriada e recalcule.

**Q: Posso ler datas de uma workbook protegida por senha?**  
A: Carregue a workbook com o parâmetro de senha, então siga os mesmos passos; a flag de calendário funciona inalterada.

**Q: Existe um limite para o número de linhas que posso processar?**  
A: Aspose.Cells pode lidar com milhões de linhas; ele transmite os dados para manter o uso de memória baixo, especialmente quando `setUseJapaneseEraCalendar` é alternado por lote.

**Q: Como preservo os estilos de célula existentes ao sobrescrever a data?**  
A: Recupere o objeto `Style` da célula antes de chamar `putValue`, então reaplique‑o após a operação de gravação.

**Q: Preciso de uma licença comercial para uso em produção?**  
A: Sim, uma licença válida do Aspose.Cells é necessária para implantações em produção; um teste gratuito está disponível para avaliação.

## Conclusão

Agora você sabe **how to read Excel** datas que usam notação de era japonesa e como **write value to excel** células com formatação adequada. Ao habilitar `setUseJapaneseEraCalendar(true)` e forçar uma recalculação de fórmulas, o Aspose.Cells conecta strings de era legadas a datas gregorianas modernas em apenas algumas linhas de Java. Experimente estender esse padrão para outros calendários culturais ou processar em lote grandes workbooks — o mesmo fluxo enable‑recalculate‑read/write se aplica universalmente.

Tem um formato de data complicado que você não consegue decifrar? Deixe um comentário abaixo, e vamos solucionar juntos. Feliz codificação!

![Obter data e hora da célula exemplo](https://example.com/images/get-datetime-from-cell.png "Obter data e hora da célula exemplo")
[Obter data e hora da célula exemplo](https://example.com/images/get-datetime-from-cell.png "Obter data e hora da célula exemplo")

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Domine o Sistema de Data 1904 no Excel Usando Aspose.Cells Java para Operações de Célula Eficazes](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Como Implementar Cálculo Recursivo de Células no Aspose.Cells Java para Automação Avançada do Excel](/cells/english/java/calculation-engine/aspose-cells-java-recursive-cell-calculations/)
- [Como Converter Nomes de Células do Excel em Índices Usando Aspose.Cells para Java: Um Guia Passo a Passo](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)

---

**Last Updated:** 2026-10-07  
**Tested With:** Aspose.Cells 23.9.0  
**Author:** Aspose

## Tutoriais Relacionados

- [Desempenho do aspose cells: Recuperar Dados de Células Excel com Java](/cells/java/cell-operations/aspose-cells-java-data-retrieval-excel/)
- [Alterar o sistema de data 1904 do Excel com Aspose.Cells para Java](/cells/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Domine o Manipulação de Arquivos Java com Aspose.Cells: Ler, Gravar e Processar Dados de Forma Eficiente](/cells/java/workbook-operations/java-file-handling-aspose-cells-read-write-process/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}