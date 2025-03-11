---
title: Configuración del tiempo de creación de PDF en .NET
linktitle: Configuración del tiempo de creación de PDF en .NET
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Aprenda a configurar el tiempo de creación de un PDF en .NET con Aspose.Cells. Siga nuestra guía paso a paso para realizar una conversión sin problemas de Excel a PDF.
weight: 11
url: /es/net/xps-and-pdf-operations/setting-pdf-creation-time/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Configuración del tiempo de creación de PDF en .NET

## Introducción
En la era digital actual, la capacidad de convertir documentos a distintos formatos es crucial para muchas aplicaciones. Una necesidad común es convertir hojas de cálculo de Excel en archivos PDF. Esto no solo conserva el formato, sino que también facilita enormemente la impresión y el uso compartido. Si eres un desarrollador que trabaja con .NET, Aspose.Cells es una biblioteca fantástica que simplifica este proceso. En este tutorial, analizaremos en profundidad cómo configurar el tiempo de creación de PDF al convertir un archivo de Excel a PDF utilizando Aspose.Cells para .NET.
## Prerrequisitos
Antes de adentrarnos en los detalles del código, asegurémonos de que tienes todo lo que necesitas para comenzar.
### Lo que necesitas
1. Visual Studio: Asegúrate de tener Visual Studio instalado en tu equipo. Este será tu entorno de desarrollo.
2.  Aspose.Cells para .NET: Descargue la biblioteca Aspose.Cells desde[sitio web](https://releases.aspose.com/cells/net/)También puedes empezar con una prueba gratuita para probar sus funcionalidades.
3. Conocimientos básicos de C#: la familiaridad con la programación en C# le ayudará a comprender mejor los fragmentos de código.
4.  Archivo de Excel: tenga un archivo de Excel listo para la conversión. Para este ejemplo, usaremos un archivo llamado`Book1.xlsx`.
Ahora que ya tienes los requisitos previos resueltos, ¡pasemos a la parte divertida: importar los paquetes necesarios y escribir el código!
## Importar paquetes
Para comenzar, debe importar los espacios de nombres necesarios en su archivo C#. Esto es fundamental, ya que le permite acceder a las clases y métodos que ofrece la biblioteca Aspose.Cells.
### Abra su proyecto C#
Abra Visual Studio y cree un nuevo proyecto o abra uno existente donde desee implementar la función de conversión de PDF.
### Añadir referencia de Aspose.Cells
Puede agregar la biblioteca Aspose.Cells a su proyecto haciendo clic derecho en su proyecto en el Explorador de soluciones, seleccionando “Administrar paquetes NuGet” y buscando “Aspose.Cells”. Instale el paquete.
### Importar espacios de nombres
En la parte superior de su archivo C#, incluya los siguientes espacios de nombres:
```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Charts;
```
Estos espacios de nombres le darán acceso a la clase Workbook y otras funcionalidades esenciales.

Ahora que hemos importado nuestros paquetes, analicemos el proceso de conversión de un archivo Excel a PDF mientras configuramos el tiempo de creación.
## Paso 1: Definir el directorio del documento
En primer lugar, debe especificar el directorio en el que se almacenan sus documentos. Aquí es donde se encuentra su archivo de Excel y donde se guardará el PDF resultante.
```csharp
string dataDir = "Your Document Directory"; // Especifique el directorio de su documento
```
 Reemplazar`"Your Document Directory"` con la ruta real donde se encuentra`Book1.xlsx` Se encuentra el archivo. Esta ruta ayudará a la aplicación a localizar el archivo para su procesamiento.
## Paso 2: Cargue el archivo Excel
 A continuación, cargará el archivo Excel en un`Workbook` objeto. Aquí es donde Aspose.Cells brilla, ya que le permite trabajar con archivos de Excel sin esfuerzo.
```csharp
string inputPath = dataDir + "Book1.xlsx"; // Ruta a su archivo Excel
Workbook workbook = new Workbook(inputPath); // Cargar el archivo Excel
```
 El`Workbook` La clase se utiliza para cargar y manipular archivos de Excel. Al pasar la ruta de entrada, le estás indicando a la aplicación con qué archivo trabajar.
## Paso 3: Crear PdfSaveOptions
 Ahora, es el momento de crear una instancia de`PdfSaveOptions`Esta clase le permite especificar varias opciones para guardar su libro de trabajo como PDF, incluido el tiempo de creación.
```csharp
PdfSaveOptions options = new PdfSaveOptions(); // Crear una instancia de PdfSaveOptions
options.CreatedTime = DateTime.Now; // Establezca la hora de creación en ahora
```
 Mediante la configuración`options.CreatedTime` a`DateTime.Now`, estás asegurando que el PDF reflejará la fecha y hora actuales en que fue creado.
## Paso 4: Guarde el libro de trabajo como PDF
Finalmente, guardará el libro de trabajo como un archivo PDF utilizando las opciones que acaba de definir.
```csharp
workbook.Save(dataDir + "output.pdf", options); //Guardar como PDF
```
 Esta línea de código toma el libro de trabajo y lo guarda en formato PDF en la ubicación especificada.`options` Se pasa el parámetro para incluir la hora de creación en los metadatos del PDF.

## Conclusión
¡Y ya está! Has convertido con éxito un archivo de Excel en un PDF con Aspose.Cells para .NET, con una marca de tiempo de creación incluida. Esta función puede resultar increíblemente útil cuando necesitas hacer un seguimiento de las versiones de un documento o cuando quieres proporcionar a los destinatarios información sobre cuándo se creó el documento.
 Si desea explorar más funciones de Aspose.Cells, no dude en consultar el[documentación](https://reference.aspose.com/cells/net/).
## Preguntas frecuentes
### ¿Qué es Aspose.Cells?
Aspose.Cells es una potente biblioteca para .NET que permite a los desarrolladores crear, manipular y convertir archivos Excel.
### ¿Puedo utilizar Aspose.Cells gratis?
 Sí, puedes comenzar con una prueba gratuita disponible en el[Sitio web de Aspose](https://releases.aspose.com/).
### ¿Cómo configuro otras propiedades del PDF?
 Puede configurar varias propiedades de PDF utilizando el`PdfSaveOptions` clase, como tamaño de página, compresión y más.
### ¿Es posible convertir varios archivos Excel a la vez?
Sí, puedes recorrer una lista de archivos y aplicar el mismo proceso de conversión a cada uno.
### ¿Dónde puedo obtener soporte para Aspose.Cells?
 Puede obtener ayuda de la comunidad Aspose en su[foro de soporte](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
