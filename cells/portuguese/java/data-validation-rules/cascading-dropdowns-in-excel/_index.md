---
title: Menus suspensos em cascata no Excel
linktitle: Menus suspensos em cascata no Excel
second_title: API de processamento Java Excel Aspose.Cells
description: Aprenda a criar menus suspensos em cascata no Excel usando Aspose.Cells para Java. Este guia passo a passo fornece código-fonte e dicas de especialistas para manipulação eficiente de planilhas do Excel.
weight: 13
url: /pt/java/data-validation-rules/cascading-dropdowns-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menus suspensos em cascata no Excel


## Introdução aos menus suspensos em cascata no Excel

No mundo da manipulação de planilhas, o Aspose.Cells para Java se destaca como um poderoso kit de ferramentas que capacita os desenvolvedores a trabalhar com arquivos do Excel de forma eficiente. Um dos recursos intrigantes que ele oferece é a capacidade de criar menus suspensos em cascata no Excel, permitindo que os usuários selecionem opções dinamicamente com base em uma seleção anterior. Neste guia passo a passo, vamos mergulhar no processo de implementação de menus suspensos em cascata usando o Aspose.Cells para Java. Então, vamos começar!

## Pré-requisitos

Antes de embarcar nessa jornada, certifique-se de ter os seguintes pré-requisitos em vigor:

-  Aspose.Cells para Java: Baixe e instale em[aqui](https://releases.aspose.com/cells/java/).
- Ambiente de desenvolvimento Java: você deve ter um ambiente de desenvolvimento Java configurado em sua máquina.
- Noções básicas do Excel: familiaridade com o Excel e seus conceitos básicos será útil.

## Preparando o cenário

Nosso objetivo é criar uma planilha do Excel com menus suspensos em cascata. Imagine um cenário em que você tem uma lista de países e, quando seleciona um país, uma lista de cidades naquele país deve estar disponível para seleção. Vamos dividir as etapas para conseguir isso.

## Etapa 1: Criando a pasta de trabalho do Excel

Primeiro, vamos criar uma pasta de trabalho do Excel usando Aspose.Cells para Java. Adicionaremos duas planilhas: uma para a lista de países e outra para a lista de cidades.

```java
// Código Java para criar uma pasta de trabalho do Excel
Workbook workbook = new Workbook();
Worksheet countrySheet = workbook.getWorksheets().get(0);
countrySheet.setName("Countries");
Worksheet citySheet = workbook.getWorksheets().add("Cities");
```

## Etapa 2: Preenchendo dados

Agora, precisamos preencher nossas planilhas com dados. Na planilha "Países", listaremos os países, e na planilha "Cidades", inicialmente deixaremos em branco, pois preencheremos dinamicamente mais tarde.

```java
//Código Java para preencher a planilha "Países"
countrySheet.getCells().get("A1").putValue("Country");
countrySheet.getCells().get("A2").putValue("USA");
countrySheet.getCells().get("A3").putValue("Canada");
countrySheet.getCells().get("A4").putValue("UK");
// Adicione mais países conforme necessário
```

## Etapa 3: Criando os menus suspensos

Em seguida, criaremos listas suspensas para as colunas de país e cidade. Essas listas suspensas serão vinculadas de forma que, quando um país for selecionado, a lista suspensa de cidade será atualizada de acordo.

```java
// Código Java para criar listas suspensas
DataValidationCollection validations = countrySheet.getDataValidations();
DataValidation validation = validations.get(validations.add(1, 1, countrySheet.getCells().getMaxDataRow(), 1));
validation.setType(DataValidationType.LIST);
validation.setFormula1("Countries!$A$2:$A$4"); // Referência à lista de países
```

## Etapa 4: Implementando menus suspensos em cascata

Agora vem a parte emocionante: implementar dropdowns em cascata. Usaremos Aspose.Cells para Java para atualizar dinamicamente o dropdown da cidade com base no país selecionado.

```java
// Código Java para implementar menus suspensos em cascata
countrySheet.getCells().setCellObserver(new ICellObserver() {
    @Override
    public void cellChanged(Cell cell) {
        if (cell.getName().equals("B2")) {
            // Limpar menu suspenso da cidade anterior
            citySheet.getCells().get("B2").setValue("");
            
            // Determinar o país selecionado
            String selectedCountry = cell.getStringValue();
            
            // Com base no país selecionado, preencha o menu suspenso da cidade
            switch (selectedCountry) {
                case "USA":
                    validation.setFormula1("Cities!$A$2:$A$4"); // Povoar com cidades dos EUA
                    break;
                case "Canada":
                    validation.setFormula1("Cities!$B$2:$B$4"); // Povoar com cidades do Canadá
                    break;
                case "UK":
                    validation.setFormula1("Cities!$C$2:$C$4"); // Povoar com cidades do Reino Unido
                    break;
                // Adicionar mais casos para outros países
            }
        }
    }
});
```

## Conclusão

Neste guia abrangente, exploramos como criar menus suspensos em cascata no Excel usando o Aspose.Cells para Java. Começamos configurando os pré-requisitos, criando a pasta de trabalho do Excel, preenchendo os dados e, em seguida, nos aprofundamos nas complexidades da criação de menus suspensos e implementando o comportamento dinâmico em cascata. Como desenvolvedor, agora você tem o conhecimento e as ferramentas para aprimorar seus arquivos do Excel com menus suspensos interativos, proporcionando uma experiência de usuário perfeita.

## Perguntas frequentes

### Como posso adicionar mais países e cidades aos menus suspensos?

Para adicionar mais países e cidades, você precisa atualizar as respectivas planilhas na sua pasta de trabalho do Excel. Basta expandir as listas nas planilhas "Países" e "Cidades", e os menus suspensos incluirão automaticamente as novas entradas.

### Posso usar essa técnica em conjunto com outros recursos do Excel?

Claro! Você pode combinar menus suspensos em cascata com vários recursos do Excel, como formatação condicional, fórmulas e gráficos para criar planilhas poderosas e interativas, adaptadas às suas necessidades específicas.

### O Aspose.Cells para Java é adequado para projetos de pequena e grande escala?

Sim, o Aspose.Cells para Java é versátil e pode ser usado em projetos de todos os tamanhos. Não importa se você está trabalhando em um pequeno utilitário ou em um aplicativo empresarial complexo, o Aspose.Cells para Java pode simplificar suas tarefas relacionadas ao Excel.

### Preciso de habilidades avançadas de programação para implementar menus suspensos em cascata com o Aspose.Cells para Java?

Embora um entendimento básico de Java seja útil, o Aspose.Cells for Java fornece documentação e exemplos extensivos para guiá-lo pelo processo. Com alguma dedicação e prática, você pode dominar esse recurso.

### Onde posso encontrar mais recursos e documentação para Aspose.Cells para Java?

 Você pode acessar documentação e recursos abrangentes para Aspose.Cells para Java em[aqui](https://reference.aspose.com/cells/java/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
