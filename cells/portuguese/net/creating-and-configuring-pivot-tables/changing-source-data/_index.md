---
title: Alterar dados de origem da tabela dinâmica programaticamente no .NET
linktitle: Alterar dados de origem da tabela dinâmica programaticamente no .NET
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda como alterar os dados de origem da tabela dinâmica programaticamente usando o Aspose.Cells para .NET com nosso tutorial passo a passo abrangente.
weight: 10
url: /pt/net/creating-and-configuring-pivot-tables/changing-source-data/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Alterar dados de origem da tabela dinâmica programaticamente no .NET

## Introdução
No mundo da análise de dados, poucas ferramentas brilham tanto quanto o Microsoft Excel. Todos os dias, inúmeros usuários dependem do Excel para gerenciar e analisar dados, mas, nos bastidores, é muito mais complexo do que apenas clicar e arrastar. Se você já quis manipular arquivos do Excel programaticamente — especificamente, para alterar os dados de origem de uma tabela dinâmica — você está no lugar certo! Neste guia, exploraremos como você pode conseguir isso usando o Aspose.Cells para .NET. Seja você um desenvolvedor experiente ou apenas mergulhando os pés no mar da programação, você encontrará este tutorial repleto de informações valiosas e fáceis de seguir.
## Pré-requisitos
Antes de começarmos nossa jornada de alteração dos dados de origem de uma tabela dinâmica, vamos garantir que você tenha tudo configurado e pronto para uso:
1. Visual Studio: certifique-se de ter uma cópia do Microsoft Visual Studio instalada, pois escreveremos nosso código aqui.
2. Biblioteca Aspose.Cells: Você precisará ter a biblioteca Aspose.Cells baixada e referenciada em seu projeto. Você pode baixá-la[aqui](https://releases.aspose.com/cells/net/).
3. Conhecimento básico de C#: embora este tutorial seja simplificado, ter um conhecimento básico de C# ajudará você a entender melhor o código.
4. Arquivo Excel: Você deve ter um arquivo Excel de exemplo (como "Book1.xlsx") contendo uma tabela dinâmica que podemos manipular.
Tudo bem, com esses pré-requisitos verificados, podemos prosseguir com a importação dos pacotes necessários e começar a codificação!
## Pacotes de importação
Primeiro as coisas mais importantes — vamos importar os pacotes que precisaremos. Abra seu projeto C# no Visual Studio e adicione as seguintes diretivas using no topo do seu arquivo de código:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Esses namespaces darão acesso às classes essenciais necessárias para trabalhar com arquivos do Excel e manipular seu conteúdo usando Aspose.Cells.

Agora, vamos dividir o processo em etapas gerenciáveis. Vamos percorrer a abertura de um arquivo Excel, modificar a planilha, alterar a fonte de dados da tabela dinâmica e salvar os resultados.
## Etapa 1: Defina seu diretório de documentos
 Primeiro, você precisa especificar onde seu arquivo Excel está localizado. Modifique o`dataDir` variável para apontar para a pasta que contém seu "Book1.xlsx".
```csharp
// O caminho para o diretório de documentos.
string dataDir = "Your Document Directory";
```
Esta linha configura o diretório onde seu arquivo Excel é armazenado, facilitando seu acesso posterior.
## Etapa 2: especifique o caminho de entrada
Em seguida, vamos criar uma string para especificar o caminho completo para seu arquivo de entrada do Excel:
```csharp
string InputPath = dataDir + "Book1.xlsx";
```
Isso ajuda a otimizar o acesso aos arquivos; você não precisará digitar o mesmo caminho várias vezes no código.
## Etapa 3: Crie um fluxo de arquivos
 Agora é hora de abrir o arquivo Excel. Vamos criar um`FileStream` que permite ler o conteúdo do arquivo Excel:
```csharp
// Criando um fluxo de arquivo contendo o arquivo Excel a ser aberto
FileStream fstream = new FileStream(InputPath, FileMode.Open);
```
Esta linha abre o arquivo em modo de leitura, permitindo-nos acessar seus dados.
## Etapa 4: Carregue a pasta de trabalho
Com o fluxo de arquivos em funcionamento, o próximo passo é carregar a pasta de trabalho:
```csharp
// Abrindo o arquivo Excel através do fluxo de arquivos
Workbook workbook = new Workbook(fstream);
```
 Este comando pega seu arquivo Excel e o carrega em um`Workbook` objeto. Uma vez carregado, você pode manipular o arquivo conforme necessário.
## Etapa 5: Acesse a planilha
Hora de mergulhar nos detalhes. Acessaremos a primeira planilha na pasta de trabalho:
```csharp
// Acessando a primeira planilha no arquivo Excel
Worksheet worksheet = workbook.Worksheets[0];
```
Isso lhe dá acesso direto aos dados da primeira planilha, facilitando sua modificação.
## Etapa 6: preencher novos dados
Em seguida, queremos inserir novos dados nas células. Neste exemplo, adicionaremos alguns dados de amostra:
```csharp
// Preenchendo novos dados nas células da planilha
worksheet.Cells["A9"].PutValue("Golf");
worksheet.Cells["B9"].PutValue("Qtr4");
worksheet.Cells["C9"].PutValue(7000);
```
 Aqui, estamos colocando os valores "Golf", "Qtr4" e`7000` em células específicas. Você pode alterar esses valores para o que for mais adequado às suas necessidades.
## Etapa 7: Alterar o intervalo nomeado
Agora, vamos alterar o intervalo nomeado ao qual a tabela dinâmica se refere. Isso envolve criar ou atualizar um intervalo:
```csharp
// Alterando o intervalo nomeado "DataSource"
Range range = worksheet.Cells.CreateRange(0,0,9,3);
range.Name = "DataSource";
```
Ao definir um novo intervalo, garantimos que a tabela dinâmica use esses novos dados quando for atualizada.
## Etapa 8: Salve o arquivo Excel modificado
Depois de todas as mudanças, é crucial salvar seu trabalho! Vamos salvar a pasta de trabalho modificada:
```csharp
// Salvando o arquivo Excel modificado
workbook.Save(dataDir + "output.xls");
```
Este comando salva a pasta de trabalho em um novo arquivo, para que você não substitua o arquivo original, a menos que queira!
## Etapa 9: Feche o fluxo de arquivos
Por fim, é essencial fechar o fluxo de arquivos para liberar quaisquer recursos que você esteja usando:
```csharp
// Fechando o fluxo de arquivos para liberar todos os recursos
fstream.Close();
```
Esta etapa garante que seu aplicativo não vaze memória e permaneça eficiente.
## Conclusão
Parabéns! Você acabou de alterar com sucesso os dados de origem de uma tabela dinâmica programaticamente no .NET usando Aspose.Cells. Essa funcionalidade abre muitas possibilidades para automatizar tarefas do Excel e melhorar seu fluxo de trabalho. Não importa se você está atualizando relatórios financeiros, rastreando dados de vendas ou mesmo apenas brincando com conjuntos de dados, ter a capacidade de fazer isso programaticamente pode economizar muito tempo e reduzir o risco de erros.

## Perguntas frequentes
### O que é Aspose.Cells?
Aspose.Cells é uma poderosa biblioteca .NET para trabalhar com arquivos do Excel, permitindo aos usuários criar, modificar e manipular documentos do Excel programaticamente.
### Posso alterar os dados de origem de tabelas dinâmicas existentes usando este método?
Absolutamente! Este método permite que você atualize a fonte de dados para tabelas dinâmicas existentes dentro da sua pasta de trabalho do Excel.
### Preciso ter o Office instalado para usar o Aspose.Cells?
Não! Aspose.Cells é uma biblioteca autônoma, o que significa que você não precisa do Microsoft Office instalado para trabalhar com arquivos do Excel.
### O Aspose.Cells é gratuito?
 Aspose.Cells oferece uma versão de teste gratuita, mas para funcionalidade completa, você terá que comprar uma licença. Você pode encontrar os detalhes[aqui](https://purchase.aspose.com/buy).
### Onde posso encontrar mais exemplos e suporte?
 Para mais exemplos e suporte, confira o[Documentação do Aspose.Cells](https://reference.aspose.com/cells/net/) e seu fórum comunitário[aqui](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
