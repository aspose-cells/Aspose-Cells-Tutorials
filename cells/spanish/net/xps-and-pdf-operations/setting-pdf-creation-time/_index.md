---
"description": "Aprenda a configurar la hora de creación de un PDF en .NET con Aspose.Cells. Siga nuestra guía paso a paso para una conversión fluida de Excel a PDF."
"linktitle": "Configuración del tiempo de creación de PDF en .NET"
"second_title": "API de procesamiento de Excel Aspose.Cells .NET"
"title": "Configuración del tiempo de creación de PDF en .NET"
"url": "/es/net/xps-and-pdf-operations/setting-pdf-creation-time/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Configuración del tiempo de creación de PDF en .NET

## Introducción
En la era digital actual, la capacidad de convertir documentos a diferentes formatos es crucial para muchas aplicaciones. Una necesidad común es convertir hojas de cálculo de Excel a archivos PDF. Esto no solo conserva el formato, sino que también facilita enormemente compartir e imprimir. Si eres desarrollador y trabajas con .NET, Aspose.Cells es una fantástica biblioteca que simplifica este proceso. En este tutorial, explicaremos en detalle cómo configurar el tiempo de creación de un PDF al convertir un archivo de Excel a PDF con Aspose.Cells para .NET.
## Prerrequisitos
Antes de profundizar en los detalles del código, asegurémonos de que tienes todo lo que necesitas para comenzar.
### Lo que necesitas
1. Visual Studio: Asegúrate de tener Visual Studio instalado en tu equipo. Este será tu entorno de desarrollo.
2. Aspose.Cells para .NET: Descargue la biblioteca Aspose.Cells desde [sitio web](https://releases.aspose.com/cells/net/)También puedes empezar con una prueba gratuita para probar sus funcionalidades.
3. Conocimientos básicos de C#: la familiaridad con la programación en C# le ayudará a comprender mejor los fragmentos de código.
4. Archivo de Excel: Tenga un archivo de Excel listo para la conversión. Para este ejemplo, usaremos un archivo llamado `Book1.xlsx`.
Ahora que ya tienes todos los prerrequisitos resueltos, ¡pasemos a la parte divertida: importar los paquetes necesarios y escribir el código!
## Importar paquetes
Para comenzar, debe importar los espacios de nombres necesarios en su archivo de C#. Esto es crucial, ya que le permite acceder a las clases y métodos proporcionados por la biblioteca Aspose.Cells.
### Abra su proyecto de C#
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
Primero, debe especificar el directorio donde se almacenan sus documentos. Aquí se encuentra su archivo de Excel y donde se guardará el PDF resultante.
```csharp
string dataDir = "Your Document Directory"; // Especifique el directorio de sus documentos
```
Reemplazar `"Your Document Directory"` con el camino real donde se encuentra `Book1.xlsx` Se encuentra el archivo. Esta ruta ayudará a la aplicación a localizarlo para su procesamiento.
## Paso 2: Cargue el archivo Excel
A continuación, cargará el archivo de Excel en un `Workbook` Aquí es donde Aspose.Cells destaca, ya que permite trabajar con archivos de Excel sin esfuerzo.
```csharp
string inputPath = dataDir + "Book1.xlsx"; // Ruta a su archivo de Excel
Workbook workbook = new Workbook(inputPath); // Cargar el archivo Excel
```
El `Workbook` La clase se usa para cargar y manipular archivos de Excel. Al pasar la ruta de entrada, se le indica a la aplicación con qué archivo trabajar.
## Paso 3: Crear opciones para guardar PDF
Ahora, es el momento de crear una instancia de `PdfSaveOptions`Esta clase le permite especificar varias opciones para guardar su libro de trabajo como PDF, incluida la hora de creación.
```csharp
PdfSaveOptions options = new PdfSaveOptions(); // Crear una instancia de PdfSaveOptions
options.CreatedTime = DateTime.Now; // Establezca la hora de creación en ahora
```
Mediante la configuración `options.CreatedTime` a `DateTime.Now`, te aseguras de que el PDF reflejará la fecha y hora actuales en que fue creado.
## Paso 4: Guarde el libro de trabajo como PDF
Finalmente, guardará el libro de trabajo como un archivo PDF utilizando las opciones que acaba de definir.
```csharp
workbook.Save(dataDir + "output.pdf", options); // Guardar como PDF
```
Esta línea de código toma el libro de trabajo y lo guarda en formato PDF en la ubicación especificada. `options` Se pasa el parámetro para incluir la hora de creación en los metadatos del PDF.

## Conclusión
¡Y listo! Has convertido correctamente un archivo de Excel a PDF con Aspose.Cells para .NET, con marca de tiempo de creación incluida. Esta función puede ser increíblemente útil si necesitas realizar un seguimiento de las versiones del documento o si quieres proporcionar a los destinatarios información sobre su fecha de creación.
Si desea explorar más funciones de Aspose.Cells, no dude en consultar el [documentación](https://reference.aspose.com/cells/net/).
## Preguntas frecuentes
### ¿Qué es Aspose.Cells?
Aspose.Cells es una poderosa biblioteca para .NET que permite a los desarrolladores crear, manipular y convertir archivos Excel.
### ¿Puedo utilizar Aspose.Cells gratis?
Sí, puedes comenzar con una prueba gratuita disponible en el [Sitio web de Aspose](https://releases.aspose.com/).
### ¿Cómo configuro otras propiedades de PDF?
Puede configurar varias propiedades de PDF utilizando el `PdfSaveOptions` clase, como tamaño de página, compresión y más.
### ¿Es posible convertir varios archivos de Excel a la vez?
Sí, puedes recorrer una lista de archivos y aplicar el mismo proceso de conversión a cada uno.
### ¿Dónde puedo obtener soporte para Aspose.Cells?
Puede obtener ayuda de la comunidad Aspose en su [foro de soporte](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}