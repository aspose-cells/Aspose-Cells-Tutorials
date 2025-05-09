---
"description": "Aprenda a consultar áreas de células mapeadas em XML no Excel usando o Aspose.Cells para .NET. Este guia passo a passo ajuda você a extrair dados XML estruturados com facilidade."
"linktitle": "Áreas de células de consulta mapeadas para o caminho do mapa XML usando Aspose.Cells"
"second_title": "API de processamento do Excel Aspose.Cells .NET"
"title": "Áreas de células de consulta mapeadas para o caminho do mapa XML usando Aspose.Cells"
"url": "/pt/net/xml-map-operations/query-cell-areas-mapped-to-xml-map-path/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Áreas de células de consulta mapeadas para o caminho do mapa XML usando Aspose.Cells

## Introdução
Você já se perguntou como trabalhar com dados XML no Excel usando o .NET? Com o Aspose.Cells para .NET, uma poderosa biblioteca para manipulação de planilhas, você pode interagir facilmente com mapas XML em seus arquivos do Excel. Imagine que você tem um arquivo do Excel repleto de dados estruturados e precisa consultar áreas específicas mapeadas para caminhos XML — é aqui que o Aspose.Cells se destaca. Neste tutorial, vamos nos aprofundar na consulta de áreas de células mapeadas para caminhos de mapas XML em arquivos do Excel usando o Aspose.Cells para .NET. Seja para criar relatórios dinâmicos ou automatizar a extração de dados, este guia tem instruções passo a passo.
## Pré-requisitos
Antes de começarmos a codificar, você precisa de algumas coisas:
1. Aspose.Cells para .NET: Certifique-se de ter esta biblioteca instalada. Você pode baixá-la [aqui](https://releases.aspose.com/cells/net/) ou obtenha-o via NuGet.
2. Um arquivo Excel mapeado em XML: para este tutorial, você precisará de um arquivo Excel (.xlsx) contendo um mapa XML.
3. Ambiente de desenvolvimento: Este guia pressupõe que você esteja usando o Visual Studio, mas qualquer editor C# deve funcionar bem.
4. Licença Aspose: Você pode usar uma licença temporária, se necessário, que você pode obter [aqui](https://purchase.aspose.com/temporary-license/).
## Pacotes de importação
Para começar, certifique-se de importar os namespaces necessários no seu arquivo de código:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Diagnostics;
using System.Collections;
```
Com esses pacotes, você estará pronto para acessar a pasta de trabalho, manipular planilhas e consultar mapas XML dentro da planilha.
## Etapa 1: Carregue o arquivo Excel contendo um mapa XML
Primeiro, você precisará carregar um arquivo Excel que já contenha o mapeamento XML. Este arquivo atua como fonte de dados.
```csharp
// Defina os caminhos de diretório para origem e saída
string sourceDir = "Your Document Directory";
// Carregar o arquivo Excel
Workbook wb = new Workbook(sourceDir + "sampleXmlMapQuery.xlsx");
```
Aqui, `Workbook` é a classe que representa todo o arquivo Excel, que você carrega usando o caminho do arquivo. Substituir `"Your Document Directory"` com o caminho do diretório real onde seu arquivo está localizado.
## Etapa 2: Acesse o Mapa XML na Pasta de Trabalho
Após o carregamento do arquivo, o próximo passo é acessar o mapa XML na pasta de trabalho. Este mapa funciona como uma ponte entre a planilha e os dados XML.
```csharp
// Acesse o primeiro mapa XML na pasta de trabalho
XmlMap xmap = wb.Worksheets.XmlMaps[0];
```
Aqui, recuperamos o primeiro mapa XML na pasta de trabalho acessando `XmlMaps[0]` do `Worksheets` coleção. Você pode ter vários mapas XML em uma pasta de trabalho, e este tutorial se concentra no primeiro.
## Etapa 3: Acesse a planilha para consultar
Com o mapa XML pronto, agora você precisa selecionar a planilha específica onde os dados mapeados estão localizados. Normalmente, essa é a primeira planilha, mas depende da configuração do seu arquivo.
```csharp
// Acesse a primeira planilha da pasta de trabalho
Worksheet ws = wb.Worksheets[0];
```
Acessar a planilha onde os dados mapeados em XML residem permite que você segmente células específicas. Aqui, estamos usando a primeira planilha, mas você pode escolher qualquer outra planilha alterando o índice ou especificando o nome.
## Etapa 4: Consultar mapa XML usando um caminho
Agora vem a parte principal: consultar o mapa XML. Aqui, você especificará o caminho XML e recuperará os dados mapeados para esse caminho na planilha.
```csharp
Console.WriteLine("Query Xml Map from Path - /MiscData");
ArrayList ret = ws.XmlMapQuery("/MiscData", xmap);
```
O `XmlMapQuery` O método usa dois parâmetros: o caminho XML e o mapa XML que você recuperou anteriormente. Neste exemplo, estamos consultando o caminho `/MiscData`, que é o caminho de nível superior na estrutura XML. Os resultados são armazenados em um `ArrayList`, facilitando a iteração.
## Etapa 5: Exibir resultados da consulta
Com os dados consultados, o próximo passo é exibir os resultados. Vamos imprimir cada item da `ArrayList` para o console para uma visão clara de quais dados foram extraídos.
```csharp
// Imprima os resultados da consulta
for (int i = 0; i < ret.Count; i++)
{
    Console.WriteLine(ret[i]);
}
```
Este loop percorre cada item do `ArrayList` e imprime no console. Você verá os dados extraídos do caminho do mapa XML `/MiscData`.
## Etapa 6: consultar um caminho XML aninhado
Para refinar sua consulta, vamos detalhar um caminho aninhado dentro da estrutura XML, como `/MiscData/row/Color`.
```csharp
Console.WriteLine("Query Xml Map from Path - /MiscData/row/Color");
ret = ws.XmlMapQuery("/MiscData/row/Color", xmap);
```
Aqui, estamos consultando um caminho mais específico dentro dos dados XML. Ao restringir para `/MiscData/row/Color`, você direciona apenas as informações de cores sob o `row` nó na estrutura XML.
## Etapa 7: Exibir resultados da consulta de caminho aninhado
Por fim, você desejará imprimir os resultados desta consulta refinada para ver os valores específicos mapeados para `/MiscData/row/Color`.
```csharp
// Imprima os resultados da consulta de caminho aninhado
for (int i = 0; i < ret.Count; i++)
{
    Console.WriteLine(ret[i]);
}
```
Assim como antes, esse loop envia os resultados da consulta para o console, permitindo que você revise os dados específicos obtidos do caminho XML aninhado.
## Conclusão
pronto! Com o Aspose.Cells para .NET, consultar áreas de células mapeadas para caminhos de mapas XML é simples e altamente eficaz. Este poderoso recurso é revolucionário para desenvolvedores que precisam extrair dados XML específicos de planilhas. Agora você tem a base para implementar consultas XML mais complexas e até mesmo combinar múltiplos mapeamentos XML em seus fluxos de trabalho do Excel. Pronto para ir mais longe? Explore a documentação do Aspose.Cells para obter funcionalidades adicionais de mapas XML para aprimorar seus aplicativos!
## Perguntas frequentes
### Posso mapear vários arquivos XML em uma única pasta de trabalho do Excel?  
Sim, o Aspose.Cells permite que você gerencie vários mapas XML em uma pasta de trabalho, permitindo interações complexas de dados.
### O que acontece se o caminho XML não existir no mapa?  
Se o caminho for inválido ou não existir, o `XmlMapQuery` o método retornará um vazio `ArrayList`.
### Preciso de uma licença para usar o Aspose.Cells para .NET?  
Sim, é necessária uma licença para a funcionalidade completa. Você pode tentar uma [teste gratuito](https://releases.aspose.com/) ou pegue um [licença temporária](https://purchase.aspose.com/temporary-license/).
### Posso salvar os dados consultados em um novo arquivo do Excel?  
Com certeza! Você pode extrair os dados consultados e gravá-los em outro arquivo do Excel ou em qualquer outro formato suportado pelo Aspose.Cells.
### É possível consultar mapas XML em formatos diferentes do Excel (.xlsx)?  
O mapeamento XML é suportado em arquivos .xlsx. Para outros formatos, a funcionalidade pode ser limitada ou incompatível.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}