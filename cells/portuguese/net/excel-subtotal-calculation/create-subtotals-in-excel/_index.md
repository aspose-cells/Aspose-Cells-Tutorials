---
title: Criar subtotais no Excel
linktitle: Criar subtotais no Excel
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda a criar subtotais no Excel usando o Aspose.Cells para .NET com este tutorial passo a passo fácil.
weight: 10
url: /pt/net/excel-subtotal-calculation/create-subtotals-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar subtotais no Excel

## Introdução
Você está pronto para elevar suas habilidades no Excel e tornar suas planilhas mais dinâmicas? Criar subtotais no Excel pode ajudar você a categorizar e resumir dados de forma eficaz, permitindo melhor interpretação e relatórios de dados. Se você é alguém que frequentemente se vê lutando com montes de números, gerar resumos estruturados é essencial. Hoje, vamos mergulhar em como criar subtotais sem esforço usando o Aspose.Cells para .NET, uma biblioteca poderosa projetada para lidar com todas as suas manipulações de arquivos do Excel.
## Pré-requisitos
Antes de nos aprofundarmos nos detalhes da criação de subtotais no Excel, há alguns pré-requisitos que você deve ter em mente:
1.  Aspose.Cells para .NET instalado: Certifique-se de ter a biblioteca Aspose.Cells configurada em seu ambiente de desenvolvimento. Se você ainda não fez isso, você pode facilmente[baixe aqui](https://releases.aspose.com/cells/net/).
2. Ambiente .NET: Você deve ter um ambiente .NET funcional onde podemos trabalhar com a biblioteca. Seja Visual Studio ou qualquer outro IDE, certifique-se de que você esteja confortável codificando em C#.
3. Conhecimento básico de C#: Familiaridade com C# será benéfica. Os exemplos que forneceremos estão na sintaxe C#, então estar confortável com ela ajudará você a entender o processo.
4.  Planilha Excel: Um arquivo Excel de exemplo para praticar. Usaremos um arquivo chamado`book1.xls` em nosso tutorial.
5.  Acesso à documentação e suporte on-line: familiarizando-se com o[Documentação do Aspose.Cells](https://reference.aspose.com/cells/net/) pode ser incrivelmente útil à medida que você avança no uso da biblioteca.
Agora que estabelecemos a base, vamos para a parte técnica!
## Pacotes de importação
Antes de começar com o código real, precisamos garantir que temos todos os pacotes necessários. Abaixo está como você pode importar o namespace necessário no seu projeto:
```csharp
using System.IO;
using Aspose.Cells;
```
Isso importa tudo o que precisamos da biblioteca Aspose para manipular arquivos do Excel. Agora, vamos dividir o código passo a passo para criar subtotais em uma planilha do Excel.
## Etapa 1: Configurar o caminho do arquivo
Para começar, precisamos definir onde nosso arquivo Excel está localizado. É aqui que informamos ao programa sobre nosso diretório de documentos.
```csharp
string dataDir = "Your Document Directory";
```
 Substituir`"Your Document Directory"` com o caminho real onde seu`book1.xls` é armazenado. Isso informa ao programa onde encontrar o arquivo Excel que manipularemos.
## Etapa 2: Instanciar uma nova pasta de trabalho
Em seguida, criaremos uma nova instância do objeto Workbook. Isso nos permitirá abrir e editar nosso arquivo Excel.
```csharp
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
 Aqui, estamos criando um objeto de`Workbook` e carregá-lo com nosso especificado`book1.xls` arquivo. Este objeto de pasta de trabalho agora contém todas as informações do arquivo Excel e nos permite modificá-las.
## Etapa 3: Acesse a coleção de células
Para operar no conteúdo da planilha do Excel, precisamos acessar a coleção “Células”.
```csharp
Cells cells = workbook.Worksheets[0].Cells;
```
 Isso recupera as células da primeira planilha (índice 0) da nossa pasta de trabalho. O`cells` objeto nos permitirá interagir com as células individuais na planilha.
## Etapa 4: Defina a área da célula para subtotais
Agora é hora de especificar o intervalo de células onde queremos aplicar o subtotal. 
```csharp
CellArea ca = new CellArea();
ca.StartRow = 2; // B3
ca.StartColumn = 1; 
ca.EndRow = 18; // Século XIX
ca.EndColumn = 2;
```
 Aqui, definimos um`CellArea` que especifica o intervalo em que estamos interessados. Neste caso, escolhemos a área de B3 (Linha 2, Coluna 1) a C19 (Linha 18, Coluna 2). É aqui que calcularemos nossos subtotais.
## Etapa 5: Aplicar subtotais
Este é o cerne da nossa operação: aplicar o subtotal à área de célula definida.
```csharp
cells.Subtotal(ca, 0, ConsolidationFunction.Sum, new int[] { 1 });
```
 Nesta linha, chamamos de`Subtotal` método. Os parâmetros definidos são:
- `ca`: O intervalo de células que definimos anteriormente.
- `0`: Este índice se refere à coluna que contém os valores a serem subtotalizados. 
- `ConsolidationFunction.Sum`Isso especifica que queremos somar os valores.
- `new int[] { 1 }`: Isso indica que estamos totalizando os valores da segunda coluna (Coluna C).
## Etapa 6: Salve o arquivo Excel modificado
Por fim, precisamos salvar nossas alterações em um novo arquivo do Excel. 
```csharp
workbook.Save(dataDir + "output.out.xls");
```
 O`Save` método grava as alterações em um novo arquivo chamado`output.out.xls`. Você pode especificar qualquer nome para o arquivo de saída conforme suas necessidades.
## Conclusão
Com essas etapas simples, você criou subtotais com sucesso em sua planilha do Excel usando o Aspose.Cells para .NET! Desde instanciar uma pasta de trabalho até aplicar subtotais e salvar os resultados, cobrimos todas as bases. Esta biblioteca não apenas simplifica suas manipulações do Excel, mas também permite que você manipule dados de forma mais eficaz.
Agora, vá em frente e experimente! Você ficará surpreso com o quanto mais fácil fica gerenciar dados em planilhas quando você sabe como usar as ferramentas certas. 
## Perguntas frequentes
### O que é Aspose.Cells para .NET?
Aspose.Cells para .NET é uma biblioteca poderosa que permite aos desenvolvedores manipular arquivos do Excel em aplicativos .NET programaticamente.
### Preciso instalar algo especial para usar o Aspose.Cells?
 Sim, você precisa baixar e adicionar a biblioteca Aspose.Cells ao seu projeto .NET.[Baixe aqui](https://releases.aspose.com/cells/net/).
### É possível criar outros tipos de recursos do Excel usando Aspose.Cells?
Absolutamente! O Aspose.Cells permite que você execute várias operações do Excel, como criar gráficos, gerenciar planilhas e modificar formatos de células, entre muitas outras.
### Posso usar o Aspose.Cells gratuitamente?
 Você pode[experimente uma avaliação gratuita](https://releases.aspose.com/) do Aspose.Cells para explorar seus recursos antes de decidir comprá-lo.
### Quais opções de suporte estão disponíveis?
 Para qualquer problema, você pode visitar o[Fórum de suporte Aspose](https://forum.aspose.com/c/cells/9) para obter ajuda e compartilhar insights com uma comunidade de usuários e desenvolvedores.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
