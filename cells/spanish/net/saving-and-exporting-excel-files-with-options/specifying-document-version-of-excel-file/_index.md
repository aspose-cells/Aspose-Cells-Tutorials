---
title: Especificación de la versión del documento de un archivo Excel mediante programación en .NET
linktitle: Especificación de la versión del documento de un archivo Excel mediante programación en .NET
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Aprenda a especificar propiedades de documentos como versión, autor y título en un archivo Excel mediante programación utilizando Aspose.Cells para .NET con instrucciones paso a paso.
weight: 12
url: /es/net/saving-and-exporting-excel-files-with-options/specifying-document-version-of-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Especificación de la versión del documento de un archivo Excel mediante programación en .NET

## Introducción
Aspose.Cells para .NET es una potente biblioteca que permite a los desarrolladores manipular archivos Excel mediante programación con facilidad. Ya sea que desee crear archivos Excel desde cero o modificar los existentes, Aspose.Cells ofrece una API integral para lograr sus objetivos. Una de esas funciones es la especificación de propiedades del documento, como la versión, el autor o el título. Este tutorial le mostrará cómo especificar la versión del documento de un archivo Excel mediante programación utilizando Aspose.Cells para .NET.
## Prerrequisitos
Antes de profundizar en los detalles, asegurémonos de que tienes todo lo que necesitas para seguir este tutorial:
1. Aspose.Cells para .NET: puedes descargar la última versión[aquí](https://releases.aspose.com/cells/net/) Si aún no ha adquirido una licencia, puede optar por una[licencia temporal](https://purchase.aspose.com/temporary-license/) para explorar las características.
2. Entorno de desarrollo .NET: puede utilizar Visual Studio o cualquier IDE compatible con .NET.
3. Conocimientos básicos de C#: comprender la programación en C# hará que sea más fácil seguirla.
## Importar paquetes
Antes de comenzar a codificar, debe importar los espacios de nombres necesarios de la biblioteca Aspose.Cells. Esto le dará acceso a las clases y métodos necesarios para la manipulación de archivos de Excel.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Estos dos espacios de nombres serán esenciales para interactuar con el libro de trabajo y sus propiedades de documento integradas.
Ahora, analicemos el proceso de especificación de propiedades de documentos en un archivo Excel, incluida la versión, el título y el autor.
## Paso 1: Inicializar el objeto del libro de trabajo
 El primer paso es crear una nueva instancia del`Workbook` objeto. Este objeto representa el archivo Excel completo con el que trabajará.
```csharp
Workbook wb = new Workbook();
```
 El`Workbook`La clase proporciona una representación de un archivo de Excel. Al crear una instancia de ella, creamos un libro de Excel en blanco que podemos manipular.
## Paso 2: Acceda a las propiedades integradas del documento
 Aspose.Cells ofrece propiedades de documento integradas, que incluyen campos como título, autor y versión del documento. Puede acceder a estas propiedades a través de la`BuiltInDocumentProperties`recopilación.
```csharp
Aspose.Cells.Properties.BuiltInDocumentPropertyCollection bdpc = wb.BuiltInDocumentProperties;
```
 El`BuiltInDocumentPropertyCollection` La clase proporciona acceso a una colección de propiedades de documento integradas, como el título, el autor y otros metadatos normalmente asociados con el documento.
## Paso 3: Establezca el título del documento de Excel
A continuación, estableceremos el título del documento de Excel. Estos metadatos ayudan a identificar y administrar el archivo más adelante.
```csharp
bdpc.Title = "Aspose File Format APIs";
```
La configuración del título es importante para la organización del documento. Estos metadatos se pueden ver en las propiedades del archivo y pueden ser utilizados por sistemas externos para catalogar o identificar el documento de manera más eficaz.
## Paso 4: Especifique el autor
También se puede especificar el autor del documento para reflejar quién creó o modificó el archivo.
```csharp
bdpc.Author = "Aspose APIs Developers";
```
Este paso ayuda a atribuir el documento a su creador, proporcionando metadatos adicionales para la gestión de documentos o escenarios de colaboración.
## Paso 5: Especifique la versión del documento
Una de las propiedades más importantes que abordamos en este tutorial es la versión del documento. Este paso le permite especificar la versión del documento, lo que resulta útil cuando se trabaja en entornos que requieren control de versiones.
```csharp
bdpc.DocumentVersion = "Aspose.Cells Version - 18.3";
```
La configuración de la versión del documento permite saber con claridad qué versión del documento o de la biblioteca se utilizó para crear el archivo. Esto es especialmente importante en entornos que necesitan realizar un seguimiento de las revisiones de archivos o de la compatibilidad con diferentes versiones de bibliotecas.
## Paso 6: Guarde el archivo Excel
 Por último, puedes guardar el archivo de Excel con todas las propiedades que acabas de configurar. Aspose.Cells te permite guardar el archivo en varios formatos, pero para este ejemplo, nos quedaremos con el`.xlsx` formato.
```csharp
wb.Save("outputSpecifyDocumentVersionOfExcelFile.xlsx", SaveFormat.Xlsx);
```
 El`Save` El método se utiliza para guardar el archivo en el directorio especificado. Aquí, lo guardamos como un archivo de Excel en el directorio`.xlsx`formato. Si es necesario, Aspose.Cells también admite formatos como`.xls`, `.csv` , y`.pdf`, proporcionando flexibilidad en función de las necesidades de su proyecto.
## Conclusión
En este tutorial, explicamos cómo especificar las propiedades de un documento, en particular la versión del documento, en un archivo de Excel mediante Aspose.Cells para .NET. Aspose.Cells es una herramienta extremadamente flexible y potente que permite manipular archivos de Excel mediante programación, lo que la convierte en un recurso excelente para cualquier desarrollador de .NET que trabaje con hojas de cálculo.
## Preguntas frecuentes
### ¿Puedo modificar otras propiedades integradas usando Aspose.Cells?  
Sí, puedes modificar otras propiedades integradas como el asunto, las palabras clave y los comentarios, entre otras.
### ¿Qué formatos de archivos admite Aspose.Cells?  
 Aspose.Cells admite una amplia variedad de formatos, incluidos`.xls`, `.xlsx`, `.csv`, `.pdf`, y mucho más.
### ¿Necesito una licencia para usar Aspose.Cells para .NET?  
 Puedes explorar Aspose.Cells con un[prueba gratis](https://releases.aspose.com/) o solicitar una[licencia temporal](https://purchase.aspose.com/temporary-license/) para pruebas extendidas.
### ¿Puedo utilizar Aspose.Cells en una aplicación web?  
Sí, Aspose.Cells se puede utilizar tanto en aplicaciones de escritorio como web. Es muy versátil y se integra bien con los marcos web .NET.
### ¿Dónde puedo obtener soporte para Aspose.Cells?  
 Puede acceder a la comunidad y al soporte a través de[Foro de soporte de Aspose.Cells](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
