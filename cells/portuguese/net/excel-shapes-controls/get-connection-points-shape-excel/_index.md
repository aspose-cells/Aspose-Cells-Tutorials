---
title: Obter pontos de conexão de forma no Excel
linktitle: Obter pontos de conexão de forma no Excel
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda como obter pontos de conexão de forma no Excel com Aspose.Cells para .NET. Siga nosso guia passo a passo para extrair e exibir pontos de forma facilmente, programaticamente.
weight: 11
url: /pt/net/excel-shapes-controls/get-connection-points-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Obter pontos de conexão de forma no Excel

## Introdução
Ao trabalhar com arquivos do Excel programaticamente, muitas vezes precisamos interagir com formas incorporadas nas planilhas. Uma das tarefas mais avançadas que você pode executar é extrair pontos de conexão de uma forma. Os pontos de conexão são usados para anexar formas com conectores e gerenciar seu layout com mais precisão. Se você está procurando obter os pontos de conexão de uma forma no Excel, o Aspose.Cells for .NET é a ferramenta que você precisa. Neste tutorial, nós o guiaremos por um processo passo a passo para conseguir isso.
## Pré-requisitos
Antes de mergulhar no código, certifique-se de ter os seguintes pré-requisitos:
- Aspose.Cells para .NET: Você precisará ter o Aspose.Cells instalado em seu ambiente de desenvolvimento. Se você ainda não o tem, você pode[baixe a última versão aqui](https://releases.aspose.com/cells/net/).
- Ambiente de desenvolvimento: certifique-se de ter uma instalação funcional do Visual Studio ou qualquer outro IDE compatível com .NET.
- Conhecimento básico de C#: Este tutorial pressupõe que você tenha um conhecimento básico de programação em C# e princípios de orientação a objetos.
 Você também pode se inscrever para um[teste gratuito do Aspose.Cells](https://releases.aspose.com/) se você ainda não o fez. Isso lhe dará acesso a todos os recursos necessários para este guia.

## Pacotes de importação
Para trabalhar com Aspose.Cells no seu projeto, você precisa incluir os namespaces necessários. As seguintes instruções de importação devem ser colocadas no topo do seu código:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Esses namespaces dão acesso à funcionalidade principal do Aspose.Cells e permitem que você manipule planilhas e formas.

## Guia passo a passo para obter pontos de conexão de uma forma
Nesta seção, mostraremos como extrair os pontos de conexão de uma forma dentro de uma planilha do Excel. Siga cada passo cuidadosamente para um entendimento claro.
## Etapa 1: Instanciar uma nova pasta de trabalho
 Primeiramente, precisamos criar uma instância do`Workbook` class. Isso representa um arquivo Excel em Aspose.Cells. Se você não tiver um arquivo existente, não tem problema — você pode começar com uma pasta de trabalho em branco.
```csharp
// Instanciar uma nova pasta de trabalho
Workbook workbook = new Workbook();
```
 Nesta etapa, criamos uma pasta de trabalho vazia do Excel, mas você também pode carregar uma existente passando o caminho do arquivo para o`Workbook` construtor.
## Etapa 2: Acesse a primeira planilha
Em seguida, precisamos acessar a planilha onde queremos trabalhar com formas. Neste caso, usaremos a primeira planilha da pasta de trabalho.
```csharp
// Obtenha a primeira planilha na pasta de trabalho
Worksheet worksheet = workbook.Worksheets[0];
```
 Esta linha acessa a primeira planilha da coleção de planilhas na pasta de trabalho. Se você estiver trabalhando com uma planilha específica, poderá substituir o índice`0` com o índice desejado.
## Etapa 3: Adicionar uma nova caixa de texto (forma)
Agora, vamos adicionar uma nova forma à planilha. Criaremos uma caixa de texto, que é um tipo de forma. Você também pode adicionar outros tipos de formas, mas, para simplificar, usaremos uma caixa de texto neste tutorial.
```csharp
// Adicionar uma nova caixa de texto à coleção
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
Aqui está o que fizemos:
-  Adicionada uma caixa de texto na linha`2` , coluna`1`.
-  Defina as dimensões da caixa de texto para`160` unidades de largura e`200` unidades de altura.
## Etapa 4: acesse a forma na coleção de formas
 Depois de adicionarmos a caixa de texto, ela se torna parte da coleção de formas da planilha. Agora, acessaremos essa forma usando o`Shapes`coleção.
```csharp
// Acesse a forma (caixa de texto) da coleção de formas
Shape shape = workbook.Worksheets[0].Shapes[0];
```
Nesta etapa, recuperamos a primeira forma (nossa caixa de texto) da coleção. Se você tiver várias formas, pode especificar o índice ou até mesmo encontrar a forma pelo nome.
## Etapa 5: recuperar pontos de conexão
Agora que temos nossa forma, vamos extrair seus pontos de conexão. Esses pontos são usados para anexar conectores à forma. O`ConnectionPoints` propriedade da forma retorna todos os pontos de conexão disponíveis.
```csharp
// Coloque todos os pontos de conexão nesta forma
var connectionPoints = shape.ConnectionPoints;
```
Isso nos dá uma coleção de todos os pontos de conexão disponíveis para aquela forma.
## Etapa 6: Exibir pontos de conexão
Por fim, queremos exibir as coordenadas de cada ponto de conexão. É aqui que fazemos um loop pelos pontos de conexão e os imprimimos no console.
```csharp
// Exibir todos os pontos de forma
foreach (var pt in connectionPoints)
{
    System.Console.WriteLine(string.Format("X = {0}, Y = {1}", pt.X, pt.Y));
}
```
 Este loop itera sobre cada ponto de conexão e imprime o`X` e`Y` coordenadas. Isso pode ser útil para depurar ou confirmar visualmente os pontos de conexão de uma forma.
## Etapa 7: Executar e concluir
Depois de configurar todos os passos acima, você pode executar o código. Aqui está a linha final que garante que o processo seja concluído com sucesso:
```csharp
System.Console.WriteLine("GetShapeConnectionPoints executed successfully.");
```
Esta linha simplesmente registra uma mensagem no console indicando que o processo foi concluído.

## Conclusão
Neste tutorial, abordamos como recuperar pontos de conexão de uma forma no Excel usando Aspose.Cells para .NET. Ao dividir a tarefa em etapas pequenas e digeríveis, exploramos o processo de criação de uma pasta de trabalho, adição de uma forma e extração dos pontos de conexão.
Ao entender como manipular formas programaticamente, você desbloqueia um mundo de possibilidades para construir planilhas dinâmicas e interativas do Excel. Não importa se você está construindo relatórios, projetando dashboards ou criando diagramas, esse conhecimento será útil.
## Perguntas frequentes
### O que é um ponto de conexão em uma forma?
Um ponto de conexão é um ponto específico em uma forma onde você pode anexar conectores ou vinculá-lo a outras formas.
### Posso recuperar pontos de conexão para todas as formas em uma planilha?
Sim, o Aspose.Cells permite que você recupere pontos de conexão para qualquer forma que os suporte. Basta percorrer a coleção de formas na planilha.
### Preciso de uma licença para usar o Aspose.Cells?
Sim, embora você possa experimentá-lo gratuitamente, uma licença é necessária para todos os recursos. Você pode[compre uma licença aqui](https://purchase.aspose.com/buy)ou pegue um[licença temporária](https://purchase.aspose.com/temporary-license/).
### Como posso adicionar diferentes tipos de formas no Aspose.Cells?
Você pode usar o`Add` método para formas como retângulos, elipses e mais. Cada forma tem parâmetros específicos que você pode personalizar.
### Como carrego um arquivo Excel existente em vez de criar um novo?
 Para carregar um arquivo existente, passe o caminho do arquivo para o`Workbook` construtor, assim:  
```csharp
Workbook workbook = new Workbook("path_to_file.xlsx");
```
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
