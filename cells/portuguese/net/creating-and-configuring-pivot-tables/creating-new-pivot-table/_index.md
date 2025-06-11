---
"description": "Aprenda a criar uma tabela dinâmica programaticamente em .NET usando Aspose.Cells com nosso guia passo a passo. Analise seus dados com eficiência."
"linktitle": "Crie uma nova tabela dinâmica programaticamente no .NET"
"second_title": "API de processamento do Excel Aspose.Cells .NET"
"title": "Crie uma nova tabela dinâmica programaticamente no .NET"
"url": "/pt/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Crie uma nova tabela dinâmica programaticamente no .NET

## Introdução
Criar uma tabela dinâmica pode parecer uma tarefa intimidadora, especialmente quando feita programaticamente. Mas não se preocupe! Com o Aspose.Cells para .NET, montar uma tabela dinâmica não é apenas simples, mas também bastante poderoso para análise de dados. Neste tutorial, guiaremos você passo a passo sobre como criar uma nova tabela dinâmica em um aplicativo .NET. Seja adicionando dados para vendas, esportes ou qualquer outra métrica de negócios, este guia ajudará você a colocar suas tabelas dinâmicas em funcionamento rapidamente.

## Pré-requisitos
Antes de começar, vamos garantir que você tenha tudo pronto. Veja o que você precisa fazer:

1. Instalar o .NET Framework: Certifique-se de ter o .NET Framework instalado em sua máquina. O Aspose.Cells suporta várias versões, mas é melhor usar a mais recente.
2. Biblioteca Aspose.Cells: Você precisa ter a biblioteca Aspose.Cells. Você pode [baixe aqui](https://releases.aspose.com/cells/net/) ou pegue um [licença temporária](https://purchase.aspose.com/temporary-license/) para avaliação.
3. Configuração do IDE: tenha um IDE compatível com C# pronto, como o Visual Studio, onde você pode iniciar um novo projeto.
4. Conhecimento básico de C#: a familiaridade com a programação em C# ajudará você a acompanhar sem ficar muito atolado.

Tudo pronto? Ótimo! Vamos começar a importar os pacotes necessários.

## Pacotes de importação
Primeiro, você precisa importar os namespaces necessários para o seu projeto C#. Abra o arquivo C# e adicione as seguintes diretivas:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Esses namespaces fornecem acesso às funcionalidades de pasta de trabalho, planilha e tabela dinâmica que usaremos neste tutorial.

## Etapa 1: Criar um objeto de pasta de trabalho
Criar uma pasta de trabalho é o início da sua jornada. Vamos começar instanciando uma nova pasta de trabalho e acessando a primeira planilha.

```csharp
// O caminho para o diretório de documentos.
string dataDir = "Your Document Directory";
// Instanciando um objeto Workbook
Workbook workbook = new Workbook();

// Obtendo a referência da planilha recém-adicionada
Worksheet sheet = workbook.Worksheets[0];
```

Nesta etapa, criamos uma `Workbook` instância que representa nosso arquivo Excel e pegue a primeira planilha, que será nosso playground para a tabela dinâmica.

## Etapa 2: inserir dados nas células
Em seguida, vamos preencher nossa planilha com alguns dados de exemplo. Vamos inserir linhas para diferentes esportes, trimestres e números de vendas para dar à nossa tabela dinâmica algo para resumir.

```csharp
Cells cells = sheet.Cells;

// Definindo o valor para as células
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

Aqui, estamos definindo os cabeçalhos das colunas e inserindo valores em cada cabeçalho. Esses dados servirão de fonte para a nossa tabela dinâmica, portanto, certifique-se de que estejam organizados! Siga este bloco e você criará um conjunto de dados abrangente.

## Etapa 3: Adicionando uma Tabela Dinâmica
Com nossos dados prontos, é hora de criar a tabela dinâmica. Usaremos a coleção de tabelas dinâmicas da planilha para adicionar nossa nova tabela dinâmica.

```csharp
Aspose.Cells.Pivot.PivotTableCollection pivotTables = sheet.PivotTables;

// Adicionar uma Tabela Dinâmica à planilha
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```

Neste trecho, adicionamos uma tabela dinâmica à planilha que faz referência ao nosso intervalo de dados (neste caso, as células A1 a C8). Colocamos a tabela dinâmica começando na célula E3 e a chamamos de "Tabela Dinâmica2". Bem simples, não é?

## Etapa 4: personalizar a tabela dinâmica
Agora que temos nossa tabela dinâmica, vamos personalizá-la para exibir resumos significativos. Podemos controlar o que aparece nas linhas, colunas e áreas de dados da tabela dinâmica.

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

Nesta etapa, instruímos a tabela dinâmica a ocultar os totais gerais das linhas e, em seguida, especificamos quais campos devem ser incluídos nas áreas de linha, coluna e dados. Os nomes dos esportes preencherão as linhas, os trimestres preencherão as colunas e os números de vendas fornecerão os resumos.

## Etapa 5: Salve a pasta de trabalho
Por fim, queremos salvar nossa pasta de trabalho recém-criada para ver os frutos do nosso trabalho.

```csharp
// Salvando o arquivo Excel
workbook.Save(dataDir + "pivotTable_test_out.xls");
```

Basta fornecer um caminho adequado e você terá a saída da tabela dinâmica salva em um arquivo Excel que você pode abrir e revisar.

## Conclusão
Criar tabelas dinâmicas programaticamente usando o Aspose.Cells para .NET pode economizar bastante tempo, especialmente ao lidar com grandes conjuntos de dados. Você aprendeu a configurar seu projeto, importar os pacotes necessários, preencher os dados e criar uma tabela dinâmica personalizável do zero. Então, da próxima vez que você estiver se afogando em números, lembre-se deste tutorial e deixe o Aspose.Cells fazer o trabalho pesado para você.

## Perguntas frequentes
### O que é Aspose.Cells?
Aspose.Cells é uma poderosa biblioteca .NET para criar e gerenciar planilhas do Excel programaticamente.

### Existe um teste gratuito do Aspose.Cells?
Sim, você pode obter um teste gratuito [aqui](https://releases.aspose.com/).

### Posso personalizar a aparência da tabela dinâmica?
Com certeza! Você pode personalizar a formatação, o layout e até mesmo os estilos da tabela dinâmica conforme suas necessidades.

### Onde posso encontrar mais exemplos e documentação sobre Aspose.Cells?
Você pode verificar o [documentação](https://reference.aspose.com/cells/net/) para guias e exemplos abrangentes.

### Como obtenho suporte para o Aspose.Cells?
Você pode obter suporte através do [Fórum Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}