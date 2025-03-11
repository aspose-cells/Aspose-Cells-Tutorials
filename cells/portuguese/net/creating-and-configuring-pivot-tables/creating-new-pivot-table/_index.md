---
title: Crie uma nova tabela dinâmica programaticamente no .NET
linktitle: Crie uma nova tabela dinâmica programaticamente no .NET
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda a criar uma tabela dinâmica programaticamente em .NET usando Aspose.Cells com nosso guia passo a passo. Analise seus dados com eficiência.
weight: 13
url: /pt/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crie uma nova tabela dinâmica programaticamente no .NET

## Introdução
Criar uma tabela dinâmica pode parecer uma tarefa intimidadora, especialmente quando você está fazendo isso programaticamente. Mas não tenha medo! Com o Aspose.Cells para .NET, montar uma tabela dinâmica não é apenas simples, mas também bastante poderoso para análise de dados. Neste tutorial, nós o guiaremos passo a passo sobre como criar uma nova tabela dinâmica em um aplicativo .NET. Quer você esteja adicionando dados para vendas, esportes ou qualquer outra métrica de negócios, este guia ajudará você a colocar suas tabelas dinâmicas em funcionamento em pouco tempo.

## Pré-requisitos
Antes de mergulhar, vamos garantir que você tenha tudo pronto para ir. Aqui está o que você precisa fazer:

1. Instalar .NET Framework: Certifique-se de ter o .NET Framework instalado na sua máquina. O Aspose.Cells suporta várias versões, mas é melhor ficar com a mais recente.
2.  Biblioteca Aspose.Cells: Você precisa ter a biblioteca Aspose.Cells. Você pode[baixe aqui](https://releases.aspose.com/cells/net/)ou pegue um[licença temporária](https://purchase.aspose.com/temporary-license/) para avaliação.
3. Configuração do IDE: tenha um IDE compatível com C# pronto, como o Visual Studio, onde você pode iniciar um novo projeto.
4. Conhecimento básico de C#: A familiaridade com a programação em C# ajudará você a acompanhar sem ficar muito atolado.

Tudo pronto? Ótimo! Vamos começar a importar os pacotes necessários.

## Pacotes de importação
Primeiro, você precisa importar os namespaces necessários para seu projeto C#. Abra seu arquivo C# e adicione as seguintes diretivas using:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Esses namespaces fornecem acesso às funcionalidades de pasta de trabalho, planilha e tabela dinâmica que usaremos ao longo deste tutorial.

## Etapa 1: Criar um objeto de pasta de trabalho
Criar uma pasta de trabalho é o começo da sua jornada. Vamos começar instanciando uma nova pasta de trabalho e acessando a primeira planilha.

```csharp
// O caminho para o diretório de documentos.
string dataDir = "Your Document Directory";
// Instanciando um objeto Workbook
Workbook workbook = new Workbook();

// Obtendo a referência da planilha recém-adicionada
Worksheet sheet = workbook.Worksheets[0];
```

 Nesta etapa, criamos um`Workbook`instância que representa nosso arquivo Excel e pegue a primeira planilha, que será nosso playground para a tabela dinâmica.

## Etapa 2: Insira dados nas células
Em seguida, vamos preencher nossa planilha com alguns dados de amostra. Vamos inserir linhas para diferentes esportes, trimestres e números de vendas para dar à nossa tabela dinâmica algo para resumir.

```csharp
Cells cells = sheet.Cells;

// Definir o valor para as células
Cell cell = cells["A1"];
cell.PutValue("Sport");
cell = cells["B1"];
cell.PutValue("Quarter");
cell = cells["C1"];
cell.PutValue("Sales");

// Preenchendo datacell = cells["A2"];
cell.PutValue("Golf");
// ... Mais entradas de dados
```

Aqui, estamos definindo nossos cabeçalhos de coluna e inserindo valores sob cada cabeçalho. Esses dados atuarão como a fonte para nossa tabela dinâmica, então certifique-se de que ela esteja organizada! Siga este bloco e você criará um conjunto de dados abrangente.

## Etapa 3: Adicionar uma tabela dinâmica
Com nossos dados prontos, é hora de criar a tabela dinâmica. Usaremos a coleção de tabelas dinâmicas da planilha para adicionar nossa nova tabela dinâmica.

```csharp
Aspose.Cells.Pivot.PivotTableCollection pivotTables = sheet.PivotTables;

// Adicionar uma tabela dinâmica à planilha
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```

Neste snippet, adicionamos uma tabela dinâmica à planilha que faz referência ao nosso intervalo de dados (neste caso, células A1 a C8). Colocamos a tabela dinâmica começando na célula E3 e a nomeamos "PivotTable2". Bem simples, certo?

## Etapa 4: personalizar a tabela dinâmica
Agora que temos nossa tabela dinâmica, vamos personalizá-la para mostrar resumos significativos. Podemos controlar o que aparece nas linhas, colunas e áreas de dados da tabela dinâmica.

```csharp
// Acessando a instância da Tabela Dinâmica recém-adicionada
Aspose.Cells.Pivot.PivotTable pivotTable = pivotTables[index];

// Não exibindo totais gerais para linhas.
pivotTable.RowGrand = false;

// Arrastando o primeiro campo para a área da linha.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Row, 0);

// Arrastando o segundo campo para a área da coluna.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Column, 1);

// Arrastando o terceiro campo para a área de dados.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Data, 2);
```

Nesta etapa, dizemos à tabela dinâmica para ocultar totais gerais para linhas e, em seguida, especificamos quais campos vão para as áreas de linha, coluna e dados. Os nomes dos esportes preencherão as linhas, os trimestres preencherão as colunas e os números de vendas fornecerão os resumos.

## Etapa 5: Salve a pasta de trabalho
Por fim, queremos salvar nossa pasta de trabalho recém-criada para ver os frutos do nosso trabalho.

```csharp
// Salvando o arquivo Excel
workbook.Save(dataDir + "pivotTable_test_out.xls");
```

Basta fornecer um caminho adequado e você terá a saída da tabela dinâmica salva em um arquivo Excel que você pode abrir e revisar.

## Conclusão
Criar tabelas dinâmicas programaticamente usando o Aspose.Cells para .NET pode economizar muito seu tempo, especialmente ao lidar com grandes conjuntos de dados. Você aprendeu como configurar seu projeto, importar pacotes necessários, preencher dados e criar uma tabela dinâmica personalizável do zero. Então, da próxima vez que você estiver se afogando em números, lembre-se deste tutorial e deixe o Aspose.Cells fazer o trabalho pesado para você.

## Perguntas frequentes
### O que é Aspose.Cells?
Aspose.Cells é uma poderosa biblioteca .NET para criar e gerenciar planilhas do Excel programaticamente.

### Existe um teste gratuito do Aspose.Cells?
 Sim, você pode obter uma avaliação gratuita[aqui](https://releases.aspose.com/).

### Posso personalizar a aparência da tabela dinâmica?
Absolutamente! Você pode personalizar a formatação, o layout e até mesmo os estilos da tabela dinâmica conforme suas necessidades.

### Onde posso encontrar mais exemplos e documentação sobre Aspose.Cells?
 Você pode verificar o[documentação](https://reference.aspose.com/cells/net/) para guias e exemplos abrangentes.

### Como obtenho suporte para o Aspose.Cells?
 Você pode obter suporte através do[Fórum Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
