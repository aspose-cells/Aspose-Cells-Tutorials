---
title: Áreas de células de consulta mapeadas para caminho de mapa XML usando Aspose.Cells
linktitle: Áreas de células de consulta mapeadas para caminho de mapa XML usando Aspose.Cells
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda como consultar áreas de células mapeadas em XML no Excel usando Aspose.Cells para .NET. Este guia passo a passo ajuda você a extrair dados XML estruturados perfeitamente.
weight: 12
url: /pt/net/xml-map-operations/query-cell-areas-mapped-to-xml-map-path/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Áreas de células de consulta mapeadas para caminho de mapa XML usando Aspose.Cells

## Introdução
Você já se perguntou como trabalhar com dados XML no Excel usando .NET? Com o Aspose.Cells para .NET, uma biblioteca poderosa para manipulação de planilhas, você pode interagir facilmente com mapas XML em seus arquivos Excel. Imagine que você tem um arquivo Excel preenchido com dados estruturados e precisa consultar áreas específicas mapeadas para caminhos XML — é aqui que o Aspose.Cells brilha. Neste tutorial, vamos nos aprofundar na consulta de áreas de células mapeadas para caminhos de mapas XML em arquivos Excel usando o Aspose.Cells para .NET. Quer você esteja procurando criar relatórios dinâmicos ou automatizar a extração de dados, este guia tem tudo o que você precisa com instruções passo a passo.
## Pré-requisitos
Antes de começarmos a codificar, há algumas coisas que você precisa:
1.  Aspose.Cells para .NET: Certifique-se de ter esta biblioteca instalada. Você pode baixá-la[aqui](https://releases.aspose.com/cells/net/) ou obtenha-o via NuGet.
2. Um arquivo Excel mapeado em XML: para este tutorial, você precisará de um arquivo Excel (.xlsx) contendo um mapa XML.
3. Ambiente de desenvolvimento: Este guia pressupõe que você esteja usando o Visual Studio, mas qualquer editor C# deve funcionar bem.
4.  Licença Aspose: Você pode usar uma licença temporária, se necessário, que você pode obter[aqui](https://purchase.aspose.com/temporary-license/).
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
Primeiro, você precisará carregar um arquivo Excel que já contenha mapeamento XML. Esse arquivo atua como fonte de dados.
```csharp
// Defina os caminhos do diretório para origem e saída
string sourceDir = "Your Document Directory";
// Carregue o arquivo Excel
Workbook wb = new Workbook(sourceDir + "sampleXmlMapQuery.xlsx");
```
 Aqui,`Workbook` é a classe que representa todo o arquivo Excel, que você carrega usando o caminho do arquivo. Substituir`"Your Document Directory"` com o caminho do diretório real onde seu arquivo está localizado.
## Etapa 2: Acesse o Mapa XML na Pasta de Trabalho
Depois que o arquivo for carregado, o próximo passo é acessar o mapa XML dentro da pasta de trabalho. Este mapa atua como uma ponte entre sua planilha e os dados XML.
```csharp
//Acesse o primeiro mapa XML na pasta de trabalho
XmlMap xmap = wb.Worksheets.XmlMaps[0];
```
 Aqui, recuperamos o primeiro mapa XML na pasta de trabalho acessando`XmlMaps[0]` do`Worksheets` coleção. Você pode ter vários mapas XML em uma pasta de trabalho, e este tutorial foca no primeiro.
## Etapa 3: Acesse a planilha para consultar
Com o mapa XML pronto, agora você vai querer selecionar a planilha específica onde os dados mapeados estão localizados. Essa é normalmente a primeira planilha, mas depende da configuração do seu arquivo.
```csharp
// Acesse a primeira planilha na pasta de trabalho
Worksheet ws = wb.Worksheets[0];
```
Acessar a planilha onde os dados mapeados em XML residem permite que você direcione células específicas. Aqui, estamos usando a primeira planilha, mas você pode escolher qualquer outra planilha alterando o índice ou especificando o nome.
## Etapa 4: Consultar mapa XML usando um caminho
Agora vem a parte principal: consultar o mapa XML. Aqui, você especificará o caminho XML e recuperará os dados mapeados para esse caminho dentro da planilha.
```csharp
Console.WriteLine("Query Xml Map from Path - /MiscData");
ArrayList ret = ws.XmlMapQuery("/MiscData", xmap);
```
 O`XmlMapQuery` método usa dois parâmetros — o caminho XML e o mapa XML que você recuperou anteriormente. Neste exemplo, estamos consultando o caminho`/MiscData` , que é o caminho de nível superior na estrutura XML. Os resultados são armazenados em um`ArrayList`, facilitando a iteração.
## Etapa 5: Exibir resultados da consulta
 Com os dados consultados, o próximo passo é exibir os resultados. Vamos imprimir cada item do`ArrayList` para o console para uma visão clara de quais dados foram extraídos.
```csharp
// Imprima os resultados da consulta
for (int i = 0; i < ret.Count; i++)
{
    Console.WriteLine(ret[i]);
}
```
 Este loop percorre cada item do`ArrayList` e imprime no console. Você verá os dados extraídos do caminho do mapa XML`/MiscData`.
## Etapa 6: consultar um caminho XML aninhado
 Para refinar sua consulta, vamos detalhar um caminho aninhado dentro da estrutura XML, como`/MiscData/row/Color`.
```csharp
Console.WriteLine("Query Xml Map from Path - /MiscData/row/Color");
ret = ws.XmlMapQuery("/MiscData/row/Color", xmap);
```
 Aqui, estamos consultando um caminho mais específico dentro dos dados XML. Ao restringir para`/MiscData/row/Color` , você direciona apenas as informações de cor sob o`row` nó na estrutura XML.
## Etapa 7: Exibir resultados da consulta de caminho aninhado
Por fim, você desejará imprimir os resultados desta consulta refinada para ver os valores específicos mapeados para`/MiscData/row/Color`.
```csharp
// Imprima os resultados da consulta do caminho aninhado
for (int i = 0; i < ret.Count; i++)
{
    Console.WriteLine(ret[i]);
}
```
Assim como antes, esse loop envia os resultados da consulta para o console, permitindo que você revise os dados específicos recuperados do caminho XML aninhado.
## Conclusão
E aí está! Com o Aspose.Cells para .NET, consultar áreas de células mapeadas para caminhos de mapa XML é simples e altamente eficaz. Esse recurso poderoso é um divisor de águas para desenvolvedores que precisam extrair dados XML específicos de planilhas. Agora você tem a base para implementar consultas XML mais complexas e até mesmo combinar vários mapeamentos XML em seus fluxos de trabalho do Excel. Pronto para levar isso adiante? Explore a documentação do Aspose.Cells para funcionalidades adicionais de mapa XML para aprimorar seus aplicativos!
## Perguntas frequentes
### Posso mapear vários arquivos XML em uma única pasta de trabalho do Excel?  
Sim, o Aspose.Cells permite que você gerencie vários mapas XML em uma pasta de trabalho, permitindo interações de dados complexas.
### que acontece se o caminho XML não existir no mapa?  
 Se o caminho for inválido ou não existir, o`XmlMapQuery` o método retornará um vazio`ArrayList`.
### Preciso de uma licença para usar o Aspose.Cells para .NET?  
 Sim, é necessária uma licença para funcionalidade completa. Você pode tentar um[teste gratuito](https://releases.aspose.com/)ou pegue um[licença temporária](https://purchase.aspose.com/temporary-license/).
### Posso salvar os dados consultados em um novo arquivo do Excel?  
Absolutamente! Você pode extrair dados consultados e gravá-los em outro arquivo Excel ou qualquer outro formato suportado pelo Aspose.Cells.
### É possível consultar mapas XML em formatos diferentes do Excel (.xlsx)?  
O mapeamento XML é suportado em arquivos .xlsx. Para outros formatos, a funcionalidade pode ser limitada ou não suportada.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
