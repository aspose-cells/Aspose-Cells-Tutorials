---
title: Criando validação de dados personalizada
linktitle: Criando validação de dados personalizada
second_title: API de processamento Java Excel Aspose.Cells
description: Aprenda a criar validação de dados personalizada usando Aspose.Cells para Java. Guia passo a passo com código-fonte.
weight: 10
url: /pt/java/data-validation-rules/creating-custom-data-validation/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criando validação de dados personalizada


## Introdução

validação de dados ajuda a manter a integridade dos dados, evitando que os usuários insiram dados incorretos ou inválidos em planilhas do Excel. Embora o Excel ofereça opções de validação de dados integradas, há cenários em que você precisa definir regras de validação personalizadas. O Aspose.Cells para Java permite que você faça isso de forma eficiente.

## Pré-requisitos

Antes de mergulhar no código, certifique-se de ter os seguintes pré-requisitos:

-  Aspose.Cells para Java: Baixe e instale a biblioteca de[aqui](https://releases.aspose.com/cells/java/).

## Etapa 1: Configurando seu projeto Java

Para começar, crie um novo projeto Java no seu Integrated Development Environment (IDE) preferido. Adicione a biblioteca Aspose.Cells for Java ao classpath do seu projeto.

## Etapa 2: Criando uma pasta de trabalho do Excel

Vamos começar criando uma nova pasta de trabalho do Excel usando o Aspose.Cells para Java.

```java
// Código Java para criar uma nova pasta de trabalho do Excel
Workbook workbook = new Workbook();
```

## Etapa 3: Adicionar uma planilha

Agora, vamos adicionar uma planilha à pasta de trabalho onde aplicaremos nossa validação de dados personalizada.

```java
// Código Java para adicionar uma planilha
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Etapa 4: Definindo critérios de validação personalizados

Nesta etapa, definiremos os critérios de validação personalizados aos quais nossos dados devem aderir. Digamos que queremos restringir a idade inserida em uma célula para estar entre 18 e 60.

```java
// Código Java para definir critérios de validação personalizados
Validation validation = worksheet.getValidations().add();
validation.setType(ValidationType.WHOLE);
validation.setOperator(OperatorType.BETWEEN);
validation.setFormula1("18");
validation.setFormula2("60");
validation.setShowError(true);
validation.setAlertStyle(ValidationAlertType.STOP);
validation.setErrorTitle("Invalid Age");
validation.setErrorMessage("Age must be between 18 and 60.");
```

## Etapa 5: Aplicando validação de dados a um intervalo

Agora que definimos nossos critérios de validação personalizados, vamos aplicá-los a um intervalo específico de células.

```java
// Código Java para aplicar validação de dados a um intervalo
CellArea area = new CellArea();
area.startRow = 0;
area.startColumn = 0;
area.endRow = 9; // Aplicar validação às dez primeiras linhas
area.endColumn = 0;

validation.addArea(area);
```

## Etapa 6: Salvando o arquivo Excel

Por fim, salve o arquivo Excel com as regras de validação de dados personalizadas aplicadas.

```java
// Código Java para salvar o arquivo Excel
workbook.save("CustomDataValidation.xlsx");
```

## Conclusão

Neste tutorial, exploramos como criar regras de validação de dados personalizadas usando Aspose.Cells para Java. Seguindo essas etapas, você pode garantir que seus dados do Excel aderem a critérios específicos, aprimorando a integridade e a precisão dos dados.

## Perguntas frequentes

### Como faço para baixar o Aspose.Cells para Java?

 Você pode baixar Aspose.Cells para Java no site em[aqui](https://releases.aspose.com/cells/java/).

### Posso aplicar validação de dados personalizada a vários intervalos na mesma planilha?

Sim, você pode aplicar validação de dados personalizada a vários intervalos na mesma planilha repetindo a Etapa 5 para cada intervalo desejado.

### Existem outros tipos de validação de dados suportados pelo Aspose.Cells para Java?

Sim, o Aspose.Cells para Java suporta vários tipos de validação de dados, incluindo números inteiros, decimais, data, hora, comprimento de texto e muito mais.

### Como posso personalizar a mensagem de erro exibida quando a validação de dados falha?

 Você pode personalizar a mensagem de erro modificando o`setErrorMessage` método na Etapa 4, onde você define os critérios de validação.

### O Aspose.Cells para Java funciona com arquivos Excel em diferentes formatos?

Sim, o Aspose.Cells para Java suporta uma ampla variedade de formatos de arquivo do Excel, incluindo XLS, XLSX, XLSM e muito mais.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
