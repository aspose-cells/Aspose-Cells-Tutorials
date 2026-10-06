---
category: general
date: 2026-06-08
description: Obtenha a data e hora da célula usando Aspose.Cells Java e aprenda como
  escrever um valor em uma célula do Excel em apenas alguns passos.
draft: false
keywords:
- get datetime from cell
- write value to excel cell
- Aspose.Cells Java date parsing
- Japanese era calendar Excel
- Excel formula recalculation Java
language: pt
og_description: Obtenha data e hora da célula usando Aspose.Cells Java. Este tutorial
  também mostra como escrever valores em uma célula do Excel de forma eficiente.
og_title: Obtenha data e hora da célula no Java Excel – Guia Completo
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Get datetime from cell using Aspose.Cells Java and learn how to write
    value to excel cell in just a few steps.
  headline: Get datetime from cell in Java Excel – Complete Guide
  type: TechArticle
- description: Get datetime from cell using Aspose.Cells Java and learn how to write
    value to excel cell in just a few steps.
  name: Get datetime from cell in Java Excel – Complete Guide
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
title: Obtenha data e hora da célula no Java Excel – Guia Completo
url: /pt/java/cell-operations/get-datetime-from-cell-in-java-excel-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Obter datetime de célula em Java Excel – Guia Completo

Já precisou **obter datetime de célula** mas o valor parece uma string de era japonesa? Você não está sozinho. Em muitas planilhas legadas as datas são armazenadas como “Reiwa 3/04/01”, e extrair um `java.time.LocalDateTime` adequado disso pode parecer decodificar uma mensagem secreta.  

Felizmente, o Aspose.Cells for Java pode lidar com a conversão para você, e aproveitando, também mostraremos como **escrever valor em célula Excel** para que você possa fazer round‑trip de dados sem quebrar a lógica da planilha.

Neste tutorial você aprenderá:

* Como criar um workbook e direcionar uma planilha específica.  
* Os passos exatos para habilitar o calendário de era japonesa para análise.  
* Por que você deve recalcular fórmulas antes de ler a data.  
* Como escrever um novo valor de volta em uma célula sem perder a formatação.  

Sem ferramentas externas, sem mágica — apenas código Java puro que você pode inserir em qualquer projeto Maven hoje.

---

## Pré-requisitos

* **Java 8+** (o exemplo usa a moderna API `java.time`).  
* **Aspose.Cells for Java** ≥ 23.9.0 – adicione a dependência via Maven ou Gradle.  
* Familiaridade básica com conceitos do Excel (planilhas, células, fórmulas).  

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

---

## Etapa 1: Criar um novo workbook e acessar a primeira planilha

Para começar, precisamos de um novo objeto `Workbook`. Pense nele como abrir um novo arquivo Excel na memória.

```java
// Step 1: Initialize workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

*Por que isso importa:*  
Criar o workbook programaticamente lhe dá controle total sobre as configurações antes que quaisquer dados toquem o sistema de arquivos. A primeira planilha (`index 0`) é onde demonstraremos tanto a leitura quanto a escrita.

---

## Etapa 2: Escrever uma string de data de era japonesa na célula A1

Agora vamos **escrever valor em célula Excel** A1. Isso reflete um cenário real onde um usuário inseriu manualmente “Reiwa 3/04/01”.

```java
// Step 2: Write the era date string into A1
Cell cell = worksheet.getCells().get("A1");
cell.putValue("Reiwa 3/04/01"); // raw string, not yet a date
```

*Dica rápida:* `putValue` é versátil — aceita strings, números, datas e até fórmulas. Quando você passa uma string simples, o Aspose a armazena exatamente como está, o que é perfeito para nossa demonstração.

---

## Etapa 3: Habilitar o calendário de era japonesa para análise de datas

Por padrão, o Aspose.Cells usa o calendário gregoriano. Para entender “Reiwa”, alternamos uma configuração.

```java
// Step 3: Turn on Japanese era calendar support
WorkbookSettings settings = workbook.getSettings();
settings.setUseJapaneseEraCalendar(true);
```

*Por que habilitar isso?*  
O calendário de era japonesa mapeia nomes de eras (Reiwa, Heisei, Showa) para seus equivalentes gregorianos. Sem essa flag, a biblioteca trataria a string como texto simples, e você nunca obteria um objeto `DateTime` adequado.

---

## Etapa 4: Recalcular fórmulas para que a string de era seja convertida para uma data gregoriana

O Aspose não analisa automaticamente a string para uma data. Em vez disso, trata a célula como resultado de fórmula após uma passagem de cálculo.

```java
// Step 4: Force a recalculation to convert the era string
workbook.calculateFormula(); // processes all cells, including A1
System.out.println(cell.getDateTime()); // → 2021‑04‑01
```

Quando `calculateFormula()` é executado, o motor reconhece o padrão de era, aplica o calendário japonês e armazena internamente a data gregoriana resultante. A chamada `getDateTime()` então retorna um `java.util.Date` (ou você pode converter para `java.time`).

**Expected output**

```
2021-04-01T00:00:00.000+00:00
```

---

## Etapa 5: Escrever um novo valor de volta na mesma célula (ou em outra célula)

Suponha que você precise sobrescrever a string original com uma data ISO‑8601 limpa. Aqui está como **escrever valor em célula Excel** com segurança, preservando o estilo da célula.

```java
// Step 5: Overwrite A1 with a formatted date string
java.time.LocalDateTime now = java.time.LocalDateTime.now();
cell.putValue(now); // Aspose will store it as a proper Excel date
// Optional: apply a date format style
Style style = cell.getStyle();
style.setNumber(14); // built‑in "m/d/yyyy" format
cell.setStyle(style);
```

*O que está acontecendo?*  
`putValue` detecta o tipo `LocalDateTime` e o converte para a representação numérica serial do Excel. Definir o formato numérico garante que a célula exiba a data exatamente como você espera ao abrir no Excel.

---

## Exemplo Completo Funcional

Juntando tudo, aqui está uma única classe Java que você pode compilar e executar. Ela cria um workbook, escreve uma string de era, a converte e, finalmente, salva o arquivo.

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

Execute isso com `java -cp aspose-cells-23.9.jar;. JapaneseEraDateDemo` e abra **output.xlsx**. Você verá a célula A1 exibindo a data atual, enquanto o console registra o valor convertido “2021‑04‑01”.

---

## Lidando com Casos de Borda & Perguntas Frequentes

### E se a célula já contiver uma data verdadeira do Excel?

Se `cell.getType()` retornar `CellValueType.IS_DATE_TIME`, você pode pular a etapa de recalculação e ler o valor diretamente:

```java
if (cell.getType() == CellValueType.IS_DATE_TIME) {
    System.out.println("Already a date: " + cell.getDateTime());
}
```

### Como processar uma coluna inteira de strings de era?

Percorra o intervalo usado e aplique as mesmas configurações uma única vez:

```java
Range used = worksheet.getCells().getMaxDisplayRange();
for (int row = 0; row < used.getRowCount(); row++) {
    Cell c = used.getCell(row, 0); // column A
    c.putValue(c.getStringValue()); // re‑assign to trigger parsing
}
workbook.calculateFormula();
```

### Posso desativar o tratamento de era japonesa mais tarde?

Sim — basta reverter a flag:

```java
settings.setUseJapaneseEraCalendar(false);
```

Lembre-se de recalcular novamente se você mudar a configuração após escrever os dados.

---

## Dicas Profissionais & Armadilhas

* **Performance:** Habilitar o calendário de era japonesa adiciona uma pequena sobrecarga. Se você precisar dele apenas para algumas células, considere ativar a configuração, processar e depois desativá‑la.  
* **Locale awareness:** A string de era deve corresponder exatamente ao padrão “EraName yy/MM/dd”. Erros de digitação em “Reiwa” (ex.: “Rewa”) deixarão a célula como texto simples.  
* **Saving format:** `Workbook.save("output.xlsx")` grava um arquivo XLSX. Use `"output.xls"` se precisar do formato binário antigo, mas observe que alguns recursos (como análise de era) podem ser limitados.

---

## Conclusão

Agora você sabe como **obter datetime de célula** quando a fonte usa uma notação de era japonesa, e também viu uma forma limpa de **escrever valor em célula Excel** com formatação adequada. Ao alternar `setUseJapaneseEraCalendar(true)` e forçar a recalculação de fórmulas, o Aspose.Cells preenche a lacuna entre strings de era legadas e datas gregorianas modernas — tudo com algumas linhas de Java.

O que vem a seguir? Experimente estender esse padrão para outros calendários culturais (Tailandês, Hijri) ou processar em lote grandes workbooks usando a mesma abordagem. Os mesmos princípios — habilitar o calendário correto, recalcular, então ler/escrever — se aplicam em todas as situações.

Tem um formato de data complicado que você não consegue decifrar? Deixe um comentário abaixo e vamos solucionar juntos. Feliz codificação!  

![Get datetime from cell example](https://example.com/images/get-datetime-from-cell.png "Get datetime from cell example")

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Domine o Sistema de Data 1904 no Excel Usando Aspose.Cells Java para Operações de Célula Eficazes](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Como Implementar Cálculo Recursivo de Células no Aspose.Cells Java para Automação Avançada do Excel](/cells/english/java/calculation-engine/aspose-cells-java-recursive-cell-calculations/)
- [Como Converter Nomes de Células Excel para Índices Usando Aspose.Cells para Java: Um Guia Passo a Passo](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}