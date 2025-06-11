---
"description": "Atualize facilmente itens de fórmula do Power Query no Excel usando o Aspose.Cells para .NET. Guia passo a passo para otimizar seus processos de manipulação de dados."
"linktitle": "Atualizar item de fórmula do Power Query"
"second_title": "Referência da API Aspose.Cells para .NET"
"title": "Atualizar item de fórmula do Power Query"
"url": "/pt/net/excel-workbook/update-power-query-formula-item/"
"weight": 160
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Atualizar item de fórmula do Power Query

## Introdução

Se você já trabalhou com o Excel, sabe o quão poderoso ele pode ser — especialmente quando você começa a se aprofundar nas Consultas do Power. Elas são o ingrediente secreto que permite transformar, limpar e analisar seus dados sem esforço. Uma maneira bacana de manipular suas fórmulas do Power Query no Excel é usando o Aspose.Cells para .NET. Hoje, vamos guiá-lo passo a passo pela atualização de itens de fórmula do Power Query. Então, pegue seu chapéu de programação e vamos começar!

## Pré-requisitos

Antes de mergulhar no código, há algumas coisas que você precisa configurar:

1. Visual Studio: Você precisará de um ambiente de desenvolvimento integrado (IDE) para escrever e executar seu código .NET. O Visual Studio é a melhor opção.
2. Biblioteca Aspose.Cells: Certifique-se de ter a biblioteca Aspose.Cells disponível em seu projeto. Você pode baixá-la do [site](https://releases.aspose.com/cells/net/).
3. Conhecimento básico de C#: embora façamos isso juntos, ter algum conhecimento básico de C# certamente ajudará, especialmente ao navegar por diferentes classes e métodos.
4. Arquivos Excel de exemplo: Você precisará dos arquivos Excel mencionados no trecho de código. Certifique-se de ter:
   - `SamplePowerQueryFormula.xlsx`
   - `SamplePowerQueryFormulaSource.xlsx`

5. .NET Framework: certifique-se de que seu projeto tenha como alvo uma versão compatível do .NET Framework.

Agora que temos nosso kit pronto, podemos prosseguir para a parte divertida: escrever o código!

## Pacotes de importação

Antes de mais nada, você precisa importar os namespaces necessários. Veja como fazer isso:

```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```

Ao adicionar esses namespaces, você informa ao compilador que pretende usar as classes e métodos da biblioteca Aspose.Cells. Esta etapa é crucial, pois estabelece a base para o código a seguir.

Vamos analisar o trecho de código que você forneceu. Este tutorial guiará você por cada parte, garantindo que você entenda o que está acontecendo.

## Etapa 1: Configurar diretórios de trabalho

Nesta etapa, definiremos onde nossos arquivos de origem e de saída estarão localizados. Isso garante que o Aspose saiba onde procurar seus arquivos do Excel.

```csharp
// Diretórios de trabalho
string SourceDir = "Your Document Directory";
string outputDir = "Your Output Directory";
```

## Etapa 2: Carregar a pasta de trabalho

Agora, vamos carregar o arquivo do Excel onde o Power Query reside.

```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
O `Workbook` class é o seu ponto de entrada no arquivo Excel. Ao passar o caminho do nosso arquivo de origem, estamos criando uma instância que nos permite manipulá-lo. Imagine como se estivesse abrindo um livro — você está se preparando para ler (ou editar) seu conteúdo.

## Etapa 3: Acesse o Mashup de Dados

Em seguida, acessaremos as fórmulas do Power Query armazenadas no Data Mashup da pasta de trabalho.

```csharp
DataMashup mashupData = workbook.DataMashup;
```
O `DataMashup` A classe contém todas as fórmulas do Power Query associadas à sua pasta de trabalho. É aqui que faremos o trabalho pesado, assim como quando você abre uma caixa de ferramentas para reparos.

## Etapa 4: percorrer as fórmulas do Power Query

Agora vem a parte em que iteramos pelas fórmulas do Power Query para encontrar aquela específica que queremos atualizar.

```csharp
foreach (PowerQueryFormula formula in mashupData.PowerQueryFormulas)
{
    foreach (PowerQueryFormulaItem item in formula.PowerQueryFormulaItems)
    {
        if (item.Name == "Source")
        {
            item.Value = "Excel.Workbook(File.Contents(\"" + SourceDir + "SamplePowerQueryFormulaSource.xlsx\"), null, true)";
        }
    }
}
```

- Nós fazemos um loop em cada um `PowerQueryFormula` em `mashupData`.
- Dentro desse ciclo, mergulhamos em cada `PowerQueryFormulaItem`.
- Verificamos se o nome do item corresponde a "Source". Se corresponder, atualizamos seu valor para vincular ao nosso novo arquivo de origem.

Isso é semelhante a encontrar a página certa em um manual e fazer as atualizações necessárias: é um processo simples e meticuloso.

## Etapa 5: Salve a pasta de trabalho atualizada

Depois de fazer as atualizações, é hora de salvar as alterações.

```csharp
// Salve a pasta de trabalho de saída.
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
O `Save` método grava a pasta de trabalho atualizada no diretório de saída especificado. É como selar suas edições em uma nova versão do manual, pronta para uso por outros!

## Conclusão

Parabéns! Você atualizou com sucesso um item de fórmula do Power Query usando o Aspose.Cells para .NET. Com esse método, você pode automatizar a modificação de fórmulas do Power Query em seus arquivos do Excel, economizando tempo e esforço valiosos.

## Perguntas frequentes

### O que é Aspose.Cells?
Aspose.Cells é uma biblioteca poderosa para manipular arquivos do Excel em aplicativos .NET sem precisar instalar o Microsoft Excel.

### Preciso do Microsoft Excel para executar o Aspose.Cells?
Não, o Aspose.Cells permite que você crie e edite arquivos do Excel programaticamente, sem precisar do Excel no seu servidor ou máquina de desenvolvimento.

### Com quais tipos de arquivos do Excel posso trabalhar usando o Aspose.Cells?
Você pode trabalhar com .xlsx, .xls, .xlsm e vários outros formatos do Excel usando o Aspose.Cells.

### Existe uma versão de teste disponível para o Aspose.Cells?
Sim, você pode baixar uma versão de teste gratuita no [Página de lançamento do Aspose Cells](https://releases.aspose.com/).

### Como posso obter suporte para o Aspose.Cells?
Você pode acessar o suporte através do [Fórum Aspose](https://forum.aspose.com/c/cells/9), onde você pode fazer perguntas e encontrar respostas da comunidade e da equipe da Aspose.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}