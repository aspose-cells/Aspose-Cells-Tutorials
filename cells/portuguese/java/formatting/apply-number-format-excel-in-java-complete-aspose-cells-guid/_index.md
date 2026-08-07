---
category: general
date: 2026-07-20
description: Aplicar formatação numérica no Excel usando Java e Aspose.Cells. Aprenda
  como aplicar estilo de moeda no Excel, criar uma pasta de trabalho Excel em Java
  e importar DataTable para o Excel de forma eficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- apply currency style excel
- create excel workbook java
- import datatable to excel
language: pt
lastmod: 2026-07-20
og_description: Aplicar formato numérico no Excel com Java. Este guia mostra como
  aplicar o estilo de moeda no Excel, criar uma pasta de trabalho Excel em Java e
  importar uma tabela de dados para o Excel passo a passo.
og_image_alt: Screenshot of an Excel workbook where apply number format excel has
  been applied to a currency column
og_title: Aplicar Formato Numérico no Excel em Java – Tutorial Completo do Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Apply number format excel using Java and Aspose.Cells. Learn how to
    apply currency style excel, create excel workbook java, and import datatable to
    excel efficiently.
  headline: Apply Number Format Excel in Java – Complete Aspose.Cells Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Open the workbook with `new Workbook("Existing.xlsx")`, fetch
      the target worksheet, and follow steps 3‑5 to apply the style array to new data.
    question: Can I apply the number format to an existing workbook?
  - answer: Use a different built‑in number index (`14` for short date, `22` for long
      date) or a custom format like `yyyy‑mm‑dd`. The workflow stays the same.
    question: What if I need to format dates instead of currency?
  - answer: 'Yes. Just change the file extension in `workbook.save("MyFile.xls")`.
      Aspose will automatically switch to the binary format. ## Wrap‑Up – What We
      Achieved We have **applied number format excel** to a column of monetary values,
      demonstrated how to **apply currency style excel**, shown the simplest wa'
    question: Does this work with older Excel versions (.xls)?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Aplicar Formato de Número do Excel em Java – Guia Completo do Aspose.Cells
url: /pt/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aplicar Formato de Número no Excel em Java – Guia Completo do Aspose.Cells

Já se perguntou como **aplicar formato de número excel** diretamente a partir do código Java? Talvez você esteja gerando relatórios financeiros ou precise de uma maneira rápida de formatar uma coluna de valores sem abrir o Excel manualmente. A boa notícia? Com o Aspose.Cells você pode fazer isso em poucas linhas, e ainda aprenderá a **aplicar estilo de moeda excel**, **criar workbook excel java**, e **importar datatable para excel** tudo em uma rotina organizada.

Neste tutorial vamos percorrer um exemplo do mundo real: uma lista de valores armazenada em um `List<Map<String,Object>>` é importada para uma nova planilha, a primeira coluna recebe um formato de moeda embutido, e o arquivo é salvo pronto para distribuição. Pronto para ver como é fácil? Vamos começar.

## Pré-requisitos – O que Você Precisa

Antes de iniciar, certifique‑se de que você tem:

- **Java Development Kit (JDK) 8+** – o código roda em qualquer JDK recente.
- Biblioteca **Aspose.Cells for Java** (o artefato Maven `com.aspose:aspose-cells`) – este é o motor que nos permite manipular arquivos Excel sem precisar do Office instalado.
- Uma **IDE favorita** (IntelliJ IDEA, Eclipse, VS Code…) – qualquer editor serve, mas uma IDE acelera a depuração.
- Familiaridade básica com **coleções Java** – usaremos um `List` de `Map`s para simular um DataTable.

É isso. Nenhum serviço externo, nenhuma instalação do Excel, apenas Java puro.

## Etapa 1: Criar Workbook Excel Java – Instanciando o Workbook

A primeira coisa que precisamos é um objeto workbook. Pense nele como a tela vazia onde tudo vai viver.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook(); // creates an in‑memory Excel file
```

Por que criar o workbook primeiro? O Aspose.Cells funciona totalmente na memória, então você pode adicionar planilhas, estilos e dados antes de tocar no disco. Essa abordagem é rápida e mantém seu código testável.

## Etapa 2: Preparar Dados – Importar Datatable para Excel Usando uma Lista de Maps

Em muitas aplicações corporativas os dados vêm dos bancos de dados como tabelas. Aqui simulamos isso com um `List<Map<String,Object>>`. Cada mapa representa uma linha, e a chave `"Amount"` mapeia para um valor numérico.

```java
// Step 2: Build a DataTable‑like structure (list of maps)
List<Map<String, Object>> dataRows = new ArrayList<>();

// Row 1
dataRows.add(new HashMap<>() {{
    put("Amount", 1234.56);
}});
// Row 2
dataRows.add(new HashMap<>() {{
    put("Amount", 7890.12);
}});
```

Você pode perguntar: “Por que não usar um `ResultSet` ou POJOs?” O método `importDataTable` aceita qualquer coleção que se comporte como um DataTable, e uma lista de maps é a forma mais direta de demonstrar o conceito sem trazer dependências extras.

## Etapa 3: Definir o Formato de Número – Aplicar Estilo de Moeda Excel

Agora vem o coração do tutorial: **aplicar formato de número excel**. O Aspose.Cells vem com formatos de número embutidos; o formato de moeda está no índice 5. Pegamos o estilo padrão da primeira planilha, ajustamos seu formato de número e o armazenamos para uso posterior.

```java
// Step 3: Get the default style and set a currency number format
Style currencyStyle = workbook.getWorksheets().get(0).getCells().getDefaultStyle();
currencyStyle.setNumber(5); // 5 = built‑in currency format ($#,##0.00)
```

Por que usar o estilo padrão como base? Ele já contém a fonte padrão da workbook, alinhamento e outras configurações, então você só precisa mudar o que importa — neste caso, o formato de número. Se precisar de um formato personalizado (por exemplo, “€#,##0.00”), pode chamar `currencyStyle.setCustom("#,##0.00 €")` em vez disso.

## Etapa 4: Configurar Opções de Importação – Vinculando o Array de Estilos

O Aspose.Cells permite que você passe um array de objetos `Style` que correspondem às colunas sendo importadas. Como nossos dados têm apenas uma coluna, fornecemos um array de um único elemento contendo o estilo de moeda.

```java
// Step 4: Configure import options with the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(new Style[] { currencyStyle });
```

Se precisar estilizar várias colunas de forma diferente, basta expandir o array: `new Style[] { styleForCol1, styleForCol2, … }`. A ordem dos estilos corresponde à ordem das colunas nos dados de origem.

## Etapa 5: Importar Dados – Inserindo o Datatable na Planilha

Com a workbook pronta, os dados preparados e os estilos definidos, finalmente **importamos datatable para excel**. Começamos na célula `A1`, incluímos os cabeçalhos das colunas (`true`) e passamos o `ImportTableOptions`.

```java
// Step 5: Perform the import
Worksheet worksheet = workbook.getWorksheets().get(0);
worksheet.getCells().importDataTable(dataRows, true, "A1", importOptions);
```

Observe a flag `true` — o Aspose.Cells gerará automaticamente uma linha de cabeçalho baseada nas chaves do map (`"Amount"`). Se você definir como `false`, o cabeçalho será omitido, dando mais controle sobre o layout final.

## Etapa 6: Salvar o Arquivo – Criar Workbook Excel Java no Disco

A última peça do quebra‑cabeça é persistir a workbook em memória em um arquivo físico. Você pode escolher qualquer formato suportado pelo Aspose (`.xlsx`, `.xls`, `.csv`, …). Aqui salvamos como um arquivo XLSX.

```java
// Step 6: Save the workbook to disk
String outputPath = "DataTableWithCurrencyStyle.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Depois de executar o programa, abra o arquivo gerado. Você verá a coluna `"Amount"` formatada com o símbolo de dólar, duas casas decimais e separadores de milhar adequados — exatamente o que se espera ao **aplicar formato de número excel** para valores monetários.

## Resultado Esperado

| Valor |
|-------|
| $1,234.56 |
| $7,890.12 |

O cabeçalho “Valor” aparece em negrito (estilo padrão) e cada célula abaixo mostra o formato de moeda que definimos. Nenhuma formatação manual no Excel é necessária.

## Dicas Profissionais e Armadilhas Comuns

- **Reutilizar Estilos com Sabedoria** – Estilos são leves, mas criar um novo `Style` para cada célula pode prejudicar o desempenho. Sempre reutilize um objeto de estilo ao aplicar o mesmo formato a muitas células, como fizemos com `currencyStyle`.
- **Formatos Personalizados** – Se sua localidade usa um símbolo de moeda diferente, substitua `currencyStyle.setNumber(5)` por `currencyStyle.setCustom("€#,##0.00")`. Teste o formato no Excel para confirmar que ele se comporta como esperado.
- **Conjuntos de Dados Grandes** – Para milhares de linhas, considere usar `importDataTable` com a flag `ImportTableOptions.setImportDataOnly(true)` para pular a geração de cabeçalhos e acelerar a importação.
- **Segurança em Threads** – Os objetos do Aspose.Cells **não** são thread‑safe. Crie uma `Workbook` separada por thread se estiver gerando relatórios em paralelo.

## Perguntas Frequentes

**Q: Posso aplicar o formato de número a uma workbook existente?**  
A: Claro. Abra a workbook com `new Workbook("Existing.xlsx")`, obtenha a planilha alvo e siga as etapas 3‑5 para aplicar o array de estilos aos novos dados.

**Q: E se eu precisar formatar datas em vez de moeda?**  
A: Use um índice de número embutido diferente (`14` para data curta, `22` para data longa) ou um formato personalizado como `yyyy‑mm‑dd`. O fluxo de trabalho permanece o mesmo.

**Q: Isso funciona com versões antigas do Excel (.xls)?**  
A: Sim. Basta mudar a extensão do arquivo em `workbook.save("MyFile.xls")`. O Aspose mudará automaticamente para o formato binário.

## Conclusão – O Que Conquistamos

Aplicamos **formato de número excel** a uma coluna de valores monetários, demonstramos como **aplicar estilo de moeda excel**, mostramos a maneira mais simples de **criar workbook excel java**, e usamos o Aspose.Cells para **importar datatable para excel** sem tocar na interface. Tudo isso foi feito em um programa conciso e autocontido que você pode copiar, colar e executar.

O que vem a seguir? Experimente estender o exemplo:

- Adicione mais colunas (por exemplo, “Date”, “Description”) e atribua estilos diferentes por coluna.
- Exporte os mesmos dados para CSV e compare como os formatos numéricos são perdidos.
- Integre o código a um serviço Spring Boot que retorne a workbook como resposta HTTP para download.

Sinta‑se à vontade para experimentar e, se encontrar algum obstáculo, deixe um comentário abaixo. Boa codificação!

## O Que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [How to Apply Styles to Excel Cells Using Aspose.Cells for Java - Complete Guide](/cells/english/java/formatting/apply-styles-excel-aspose-cells-java/)
- [Merge Cells & Apply Styles in Excel using Aspose.Cells for Java - A Complete Guide](/cells/english/java/formatting/merge-cells-apply-styles-aspose-cells-java/)
- [Aspose.Cells for Java&#58; How to Create and Format Excel Workbooks Efficiently](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}