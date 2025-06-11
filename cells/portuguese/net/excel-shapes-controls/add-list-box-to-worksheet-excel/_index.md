---
"description": "Aprenda a adicionar uma caixa de listagem a uma planilha do Excel usando o Aspose.Cells para .NET. Siga nosso guia passo a passo fácil e torne suas planilhas do Excel interativas."
"linktitle": "Adicionar caixa de listagem à planilha no Excel"
"second_title": "API de processamento do Excel Aspose.Cells .NET"
"title": "Adicionar caixa de listagem à planilha no Excel"
"url": "/pt/net/excel-shapes-controls/add-list-box-to-worksheet-excel/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar caixa de listagem à planilha no Excel

## Introdução
Adicionar elementos interativos às suas planilhas do Excel, como uma caixa de listagem, pode melhorar significativamente o gerenciamento de dados e a apresentação. Seja criando um formulário interativo ou uma ferramenta personalizada de entrada de dados, a capacidade de controlar a entrada do usuário com uma caixa de listagem é inestimável. O Aspose.Cells para .NET oferece uma maneira eficiente de adicionar e gerenciar esses controles em seus arquivos do Excel. Neste guia, mostraremos o processo de adição de uma caixa de listagem a uma planilha usando o Aspose.Cells para .NET.
## Pré-requisitos
Antes de começar a codificação, certifique-se de ter as seguintes ferramentas e recursos disponíveis:
- Biblioteca Aspose.Cells para .NET: Você pode baixá-la do [Página de download do Aspose.Cells para .NET](https://releases.aspose.com/cells/net/).
- Ambiente de desenvolvimento: qualquer IDE que suporte desenvolvimento .NET, como o Visual Studio.
- .NET Framework: certifique-se de que seu projeto esteja direcionado a uma versão compatível do .NET Framework.
Considere também obter um [licença temporária](https://purchase.aspose.com/temporary-license/) se você quiser explorar todos os recursos sem limitações.
## Pacotes de importação
Antes de começar, certifique-se de ter importado os namespaces Aspose.Cells necessários. Veja como fazer isso:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
```
Neste tutorial, dividiremos o processo de adição de uma caixa de listagem em várias etapas simples. Siga cada etapa atentamente para garantir que tudo funcione conforme o esperado.
## Etapa 1: Configurando seu diretório de documentos
Antes de criar qualquer arquivo do Excel, você precisa de um local para salvá-lo. Veja como configurar o diretório:
```csharp
// O caminho para o diretório de documentos.
string dataDir = "Your Document Directory";
// Crie um diretório se ele ainda não existir.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Nesta etapa, você define onde seu arquivo será armazenado. O código verifica se o diretório existe e, caso não exista, cria um para você. Isso garante que você não encontre erros de "arquivo não encontrado" posteriormente.
## Etapa 2: Crie uma nova pasta de trabalho e acesse a primeira planilha
Em seguida, criaremos uma nova pasta de trabalho e acessaremos a primeira planilha onde adicionaremos nossa caixa de listagem.
```csharp
// Crie uma nova pasta de trabalho.
Workbook workbook = new Workbook();
// Obtenha a primeira planilha.
Worksheet sheet = workbook.Worksheets[0];
```
Uma pasta de trabalho é essencialmente um arquivo do Excel. Aqui, estamos criando uma nova pasta de trabalho e acessando a primeira planilha, onde colocaremos nossa caixa de listagem. Pense nisso como criar uma tela em branco onde você pintará os controles.
## Etapa 3: Dados de entrada para a caixa de listagem
Antes de adicionar a caixa de listagem, precisamos preencher alguns dados que a caixa de listagem fará referência.
```csharp
// Obtenha a coleção de células da planilha.
Cells cells = sheet.Cells;
// Insira um valor para o rótulo.
cells["B3"].PutValue("Choose Dept:");
// Defina o rótulo como negrito.
cells["B3"].GetStyle().Font.IsBold = true;
// Valores de entrada para a caixa de listagem.
cells["A2"].PutValue("Sales");
cells["A3"].PutValue("Finance");
cells["A4"].PutValue("MIS");
cells["A5"].PutValue("R&D");
cells["A6"].PutValue("Marketing");
cells["A7"].PutValue("HRA");
```
Aqui, estamos adicionando texto à planilha. O rótulo "Escolher Departamento:" está na célula B3 e sua fonte está definida como negrito. Na coluna A, estamos inserindo valores que servirão como intervalo de entrada para nossa caixa de listagem, representando diferentes departamentos. Esse intervalo de entrada é o que os usuários escolherão ao interagir com a caixa de listagem.
## Etapa 4: adicione a caixa de listagem à planilha
Agora que configuramos os dados, vamos adicionar o próprio controle da caixa de listagem.
```csharp
// Adicione uma nova caixa de listagem.
Aspose.Cells.Drawing.ListBox listBox = sheet.Shapes.AddListBox(2, 0, 3, 0, 122, 100);
```
Este código adiciona a caixa de listagem à planilha. Os parâmetros definem a posição e o tamanho da caixa de listagem. A caixa de listagem é colocada na linha 2, coluna 0, com largura de 122 e altura de 100. Essas são as coordenadas e o tamanho que determinam onde a caixa de listagem aparecerá na planilha.
## Etapa 5: definir propriedades da caixa de listagem
Em seguida, definiremos várias propriedades para a caixa de listagem para torná-la totalmente funcional.
```csharp
// Defina o tipo de posicionamento.
listBox.Placement = PlacementType.FreeFloating;
// Defina a célula vinculada.
listBox.LinkedCell = "A1";
// Defina o intervalo de entrada.
listBox.InputRange = "A2:A7";
// Defina o tipo de seleção.
listBox.SelectionType = SelectionType.Single;
// Defina a caixa de listagem com sombreamento 3D.
listBox.Shadow = true;
```
- PlacementType.FreeFloating: esta propriedade garante que a caixa de listagem permaneça em sua posição, independentemente de como a planilha é modificada.
- LinkedCell: define uma célula (neste caso, A1) onde o valor selecionado na caixa de listagem será exibido.
- InputRange: Isso informa à caixa de listagem onde procurar sua lista de opções (A2 a A7, que definimos anteriormente).
- SelectionType.Single: Isso restringe o usuário a selecionar apenas um item da caixa de listagem.
- Sombra: O efeito de sombra dá à caixa de listagem uma aparência mais tridimensional, tornando-a visualmente atraente.
## Etapa 6: Salve o arquivo do Excel
Por fim, vamos salvar nossa pasta de trabalho com a caixa de listagem incluída.
```csharp
// Salve a pasta de trabalho.
workbook.Save(dataDir + "book1.out.xls");
```
Esta linha de código salva a pasta de trabalho no diretório que configuramos anteriormente. O arquivo se chama "book1.out.xls", mas você pode escolher qualquer nome que combine com o seu projeto.
## Conclusão
pronto! Você adicionou com sucesso uma caixa de listagem a uma planilha do Excel usando o Aspose.Cells para .NET. Com apenas algumas linhas de código, criamos uma caixa de listagem totalmente funcional, tornando a planilha mais interativa e dinâmica. Este tutorial deve fornecer uma base sólida para explorar outros controles e recursos do Aspose.Cells para .NET. Continue experimentando e, em breve, você dominará a vasta funcionalidade da biblioteca!
## Perguntas frequentes
### Posso permitir múltiplas seleções na caixa de listagem?  
Sim, você pode alterar o `SelectionType` para `SelectionType.Multi` para permitir seleções múltiplas.
### Posso alterar a aparência da caixa de listagem?  
Com certeza! O Aspose.Cells permite personalizar a aparência da caixa de listagem, incluindo tamanho, fonte e até cor.
### E se eu precisar remover a caixa de listagem mais tarde?  
Você pode acessar e remover a caixa de listagem do `Shapes` coleção usando `sheet.Shapes.RemoveAt(index)`.
### Posso vincular a caixa de listagem a uma célula diferente?  
Sim, basta mudar o `LinkedCell` propriedade para qualquer outra célula onde você deseja exibir o valor selecionado.
### Como adiciono mais itens à caixa de listagem?  
Basta atualizar o intervalo de entrada inserindo mais valores nas células especificadas, e a caixa de listagem será atualizada automaticamente.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}