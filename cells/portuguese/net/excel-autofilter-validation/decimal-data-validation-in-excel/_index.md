---
title: Validação de dados decimais no Excel
linktitle: Validação de dados decimais no Excel
second_title: API de processamento do Aspose.Cells .NET Excel
description: Descubra como implementar validação de dados decimais no Excel usando Aspose.Cells para .NET com nosso guia fácil de seguir. Melhore a integridade dos dados sem esforço.
weight: 11
url: /pt/net/excel-autofilter-validation/decimal-data-validation-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Validação de dados decimais no Excel

## Introdução

Criar planilhas com dados precisos é essencial para uma comunicação clara em qualquer negócio. Uma maneira de garantir a precisão dos dados é por meio do uso da validação de dados no Excel. Neste tutorial, vamos aproveitar o poder do Aspose.Cells para .NET para criar um mecanismo de validação de dados decimais que mantém seus dados confiáveis e limpos. Se você está procurando melhorar seu jogo no Excel, você está no lugar certo!

## Pré-requisitos

Antes de mergulhar no código, certifique-se de ter tudo configurado para uma experiência de navegação tranquila:

1. Visual Studio: Baixe e instale o Visual Studio se você ainda não o fez. É o ambiente perfeito para desenvolver aplicativos .NET.
2.  Aspose.Cells para .NET: Você precisará ter a biblioteca Aspose.Cells adicionada ao seu projeto. Você pode baixá-la via[este link](https://releases.aspose.com/cells/net/).
3. Conhecimento básico de C#: embora expliquemos tudo passo a passo, ter um conhecimento fundamental de programação em C# lhe dará uma melhor compreensão dos conceitos.
4. .NET Framework: certifique-se de ter instalado o .NET Framework necessário que seja compatível com o Aspose.Cells.
5. Bibliotecas: faça referência à biblioteca Aspose.Cells no seu projeto para evitar erros de compilação.

Agora que abordamos o básico, vamos para a parte mais emocionante: a codificação.

## Pacotes de importação

Para começar, você precisa importar os pacotes necessários no seu arquivo C#. Isso permite que você acesse as funcionalidades do Aspose.Cells.

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Ao incluir essa linha no topo do seu arquivo, você está dizendo ao C# para procurar a funcionalidade Aspose.Cells que permite manipular arquivos do Excel.

Agora que definimos o cenário, vamos seguir as etapas necessárias para criar a validação de dados decimais em uma planilha do Excel.

## Etapa 1: configure seu diretório de documentos

Antes de salvar qualquer arquivo, você precisa garantir que seu diretório de documentos esteja configurado corretamente:

```csharp
string dataDir = "Your Document Directory";
```

 Substituir`"Your Document Directory"` com o caminho onde você deseja salvar seus arquivos do Excel.

## Etapa 2: verificar a existência do diretório

Este snippet verifica se o diretório existe e o cria caso não exista:

```csharp
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

Este passo é como certificar-se de que seu espaço de trabalho está pronto antes de começar um novo projeto. Sem bagunça, sem estresse!

## Etapa 3: Criar um objeto de pasta de trabalho

Em seguida, vamos criar um novo objeto de pasta de trabalho, que é essencialmente um arquivo do Excel:

```csharp
Workbook workbook = new Workbook();
```

Pense em uma pasta de trabalho como uma tela em branco para seus dados. Neste ponto, ela não tem conteúdo, mas está pronta para ser pintada.

## Etapa 4: Crie e acesse a planilha


Agora, vamos criar uma planilha e acessar a primeira planilha na pasta de trabalho:

```csharp
Worksheet ExcelWorkSheet = workbook.Worksheets[0];
```

Assim como um livro tem várias páginas, uma pasta de trabalho pode ter várias planilhas. No momento, estamos focando na primeira.

## Etapa 5: Obtenha a coleção de validações

Agora, vamos extrair a coleção de validação da planilha, pois é aqui que gerenciaremos nossas regras de validação de dados:

```csharp
ValidationCollection validations = ExcelWorkSheet.Validations;
```

Esta etapa é semelhante a verificar a caixa de ferramentas antes de começar um projeto.

## Etapa 6: Defina a área da célula para validação

Precisamos definir a área onde a validação se aplica:

```csharp
CellArea ca = new CellArea();
ca.StartRow = 0;
ca.EndRow = 0;
ca.StartColumn = 0;
ca.EndColumn = 0;
```

Aqui, estamos estipulando que a validação de dados será aplicada a uma única célula, especificamente, a primeira célula da planilha (A1).

## Etapa 7: Criar e adicionar validação

Vamos criar nosso objeto de validação e adicioná-lo à coleção de validações:

```csharp
Validation validation = validations[validations.Add(ca)];
```

Agora temos um objeto de validação que vamos configurar para impor nossas condições decimais.

## Etapa 8: Defina o tipo de validação

Em seguida, especificaremos o tipo de validação que queremos:

```csharp
validation.Type = ValidationType.Decimal;
```

Ao definir o tipo como Decimal, estamos instruindo o Excel a esperar valores decimais na célula validada.

## Etapa 9: Especifique o operador

Agora, especificaremos a condição para valores permitidos. Queremos garantir que os dados inseridos caiam entre dois intervalos:

```csharp
validation.Operator = OperatorType.Between;
```

Pense nisso como desenhar uma linha de limite. Qualquer número fora desse intervalo será rejeitado, mantendo seus dados limpos!

## Etapa 10: Estabeleça limites para validação

Em seguida, definiremos os limites inferior e superior para nossa validação:

```csharp
validation.Formula1 = Decimal.MinValue.ToString();
validation.Formula2 = Decimal.MaxValue.ToString();
```

Com esses limites, qualquer número decimal, não importa quão grande ou pequeno, é aceito, desde que seja válido!

## Etapa 11: Personalizando a mensagem de erro

Vamos garantir que os usuários saibam por que sua entrada foi rejeitada adicionando uma mensagem de erro:

```csharp
validation.ErrorMessage = "Please enter a valid integer or decimal number";
```

Isso resulta em uma experiência amigável ao usuário, pois fornece orientação sobre o que inserir.

## Etapa 12: Defina a área de validação

Agora, vamos especificar as células que suportarão essa validação:

```csharp
CellArea area;
area.StartRow = 0;
area.EndRow = 9;
area.StartColumn = 0;
area.EndColumn = 0;
```

Nessa configuração, estamos dizendo que a validação se aplica da célula A1 a A10.

## Etapa 13: Adicione a área de validação

Agora que definimos nossa área de validação, vamos aplicá-la:

```csharp
validation.AddArea(area);
```

Sua validação agora está firmemente estabelecida, pronta para capturar quaisquer entradas inapropriadas!

## Etapa 14: Salve a pasta de trabalho

Por fim, vamos salvar a pasta de trabalho com nossa validação de dados decimais em vigor:

```csharp
workbook.Save(dataDir + "output.out.xls");
```

E aí está! Você criou com sucesso uma pasta de trabalho com validação de dados decimais usando Aspose.Cells for .NET.

## Conclusão

Implementar validação de dados decimais no Excel usando Aspose.Cells para .NET é moleza quando você segue estas etapas simples. Você não apenas garante que os dados permaneçam limpos e estruturados, mas também melhora a integridade geral dos dados em suas planilhas, tornando-as confiáveis e fáceis de usar.
Não importa se você está em finanças, gerenciamento de projetos ou qualquer área que utilize relatórios de dados, dominar essas habilidades aumentará sua produtividade significativamente. Então vá em frente, experimente! Suas planilhas agradecerão por isso.

## Perguntas frequentes

### O que é validação de dados no Excel?
A validação de dados no Excel é um recurso que restringe o tipo de dados que podem ser inseridos em uma célula ou intervalo específico, garantindo a integridade dos dados.

### Posso personalizar a mensagem de erro na validação de dados?
Sim! Você pode fornecer mensagens de erro personalizadas para orientar os usuários quando entradas de dados incorretas forem feitas.

### O Aspose.Cells é gratuito?
 O Aspose.Cells oferece um teste gratuito, mas você precisará de uma licença para uso de longo prazo. Você pode encontrar mais informações sobre como adquirir uma licença temporária[aqui](https://purchase.aspose.com/temporary-license/).

### Que tipos de dados posso validar no Excel?
Com o Aspose.Cells, você pode validar vários tipos de dados, incluindo números inteiros, decimais, datas, listas e fórmulas personalizadas.

### Onde posso encontrar mais documentação do Aspose.Cells?
 Você pode explorar a extensa documentação[aqui](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
