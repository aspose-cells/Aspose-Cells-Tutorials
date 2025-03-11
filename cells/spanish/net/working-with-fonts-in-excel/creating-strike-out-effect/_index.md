---
title: Cómo crear un efecto de tachado en el texto de Excel
linktitle: Cómo crear un efecto de tachado en el texto de Excel
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Aprenda a aplicar un efecto de tachado en el texto en Excel con Aspose.Cells para .NET en este detallado tutorial paso a paso.
weight: 15
url: /es/net/working-with-fonts-in-excel/creating-strike-out-effect/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo crear un efecto de tachado en el texto de Excel

## Introducción
En Excel, los elementos visuales son tan importantes como los datos en sí. Ya sea que esté resaltando cambios importantes o marcando elementos que ya no son relevantes, el efecto tachado en el texto es una forma clásica de administrar la representación visual en las hojas de cálculo. En esta guía, lo guiaremos a través del proceso de implementación de un efecto tachado en el texto en Excel con Aspose.Cells para .NET. Este tutorial no solo cubrirá los requisitos previos necesarios, sino que también proporcionará un enfoque paso a paso para garantizar que pueda replicar este efecto con facilidad.
## Prerrequisitos
Antes de sumergirse en el tutorial, asegúrese de cumplir los siguientes requisitos previos:
1. Entorno de desarrollo: debe tener configurado un entorno de desarrollo .NET. Puede ser Visual Studio o cualquier otro IDE que prefiera que admita el desarrollo .NET.
2. Aspose.Cells para .NET: Asegúrate de tener Aspose.Cells instalado en tu proyecto. Puedes descargarlo desde el siguiente enlace:[Descargar Aspose.Cells](https://releases.aspose.com/cells/net/).
3. Conocimientos básicos de C#: es útil tener una comprensión fundamental de la programación en C#, ya que los ejemplos se codificarán en C#.
4. .NET Framework: asegúrese de que su proyecto tenga como objetivo una versión compatible de .NET Framework, normalmente .NET Core o .NET Framework 4.5 y superiores.
## Importar paquetes
Antes de escribir cualquier código, debe importar los espacios de nombres necesarios desde Aspose.Cells. Esto es fundamental para acceder a las distintas funciones que ofrece la biblioteca. A continuación, se muestra cómo importar los espacios de nombres necesarios:
```csharp
using System.IO;
using Aspose.Cells;
```
Con estas importaciones, tendrá acceso a las clases Libro de trabajo, Hoja de trabajo y Estilo que se utilizarán a lo largo de este tutorial.
Ahora que hemos preparado el terreno, vamos a dividir el proceso en pasos manejables. Cada paso estará acompañado de instrucciones claras que lo guiarán en la creación de un efecto de tachado en el texto en Excel.
## Paso 1: Definir el directorio del documento
Comience por definir la ruta donde se almacenarán sus documentos de Excel. Esta será la ubicación donde guardará los archivos de salida.
```csharp
// La ruta al directorio de documentos.
string dataDir = "Your Document Directory";
```
 Reemplazar`"Your Document Directory"` con la ruta del directorio real donde desea guardar el archivo de Excel. Esto configura el directorio para la salida.
## Paso 2: Crear el directorio
A continuación, debe asegurarse de que el directorio que especificó en el paso anterior exista. Si no existe, puede crearlo mediante programación.
```csharp
// Crear directorio si aún no está presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Este código comprueba si el directorio existe y lo crea en caso contrario. Esto ayuda a evitar errores cuando intentes guardar el archivo más adelante.
## Paso 3: Crear una instancia de un objeto de libro de trabajo
Ahora es el momento de crear un nuevo objeto de libro de trabajo. Esta es la base de su archivo de Excel, donde agregará datos y aplicará formatos.
```csharp
// Creación de una instancia de un objeto Workbook
Workbook workbook = new Workbook();
```
 El`Workbook` La clase representa un archivo de Excel. Al crear una instancia de esta clase, básicamente estás creando un nuevo documento de Excel.
## Paso 4: Agregar una nueva hoja de trabajo
Cada libro de trabajo puede contener varias hojas de trabajo. Vamos a crear una nueva hoja de trabajo en su libro de trabajo.
```csharp
// Agregar una nueva hoja de cálculo al objeto de Excel
int i = workbook.Worksheets.Add();
```
 El`Add` método de la`Worksheets` La colección agrega una nueva hoja de trabajo al libro y devuelve su índice. 
## Paso 5: Obtener la referencia de la nueva hoja de cálculo
Una vez que haya creado la hoja de trabajo, deberá utilizarla como referencia para operaciones futuras.
```csharp
// Obtener la referencia de la hoja de trabajo recién agregada pasando su índice de hoja
Worksheet worksheet = workbook.Worksheets[i];
```
Aquí, estás obteniendo la hoja de trabajo recién creada usando su índice (`i`). Esto le da acceso para manipular la hoja de trabajo.
## Paso 6: Acceder a una celda
 Deberá acceder a una celda específica en su hoja de cálculo donde aplicará el formato de tachado. En este ejemplo, estamos usando la celda`A1`.
```csharp
// Acceder a la celda "A1" desde la hoja de cálculo
Aspose.Cells.Cell cell = worksheet.Cells["A1"];
```
 En Excel, las celdas se mencionan por sus identificadores de columna y fila (por ejemplo, "A1"). Estamos obteniendo una referencia a la celda`A1` para una mayor manipulación.
## Paso 7: Agregar valor a la celda
 A continuación, insertemos algo de texto en la celda. Escribiremos “¡Hola Aspose!” en la celda.`A1`.
```csharp
// Añadiendo algún valor a la celda "A1"
cell.PutValue("Hello Aspose!");
```
 El`PutValue` El método se utiliza para asignar un valor de cadena a la celda. Puede modificar esta cadena para que se muestre como desee.
## Paso 8: Obtener el estilo de la celda
Ahora que tenemos texto en nuestra celda, es momento de acceder al estilo de la celda para aplicar el formato deseado, incluido el efecto de tachado.
```csharp
// Obtención del estilo de la celda
Style style = cell.GetStyle();
```
 El`GetStyle` El método recupera el estilo actual de la celda, lo que le permite modificar propiedades como el tipo de fuente, el tamaño y los efectos.
## Paso 9: Establezca el efecto de tachado
Apliquemos el efecto de tachado al texto de la celda. Modificaremos el estilo de fuente de la celda.
```csharp
// ExStart:Establecer tachado
// Configuración del efecto tachado en la fuente
style.Font.IsStrikeout = true;
// ExFin:EstablecerPonche
```
 Mediante la configuración`IsStrikeout` Si es verdadero, le estás indicando a Excel que tache visualmente el texto en la celda seleccionada, de forma muy similar a marcar visualmente algo de una lista.
## Paso 10: Aplicar el estilo a la celda
Después de modificar el estilo, debes volver a aplicarlo a la celda para reflejar los cambios.
```csharp
// Aplicar el estilo a la celda
cell.SetStyle(style);
```
 El`SetStyle` El método actualiza la celda con el nuevo estilo, que ahora incluye el formato de tachado.
## Paso 11: Guarde el archivo Excel
 Finalmente, es momento de guardar el libro de trabajo en el directorio especificado. En este ejemplo, guardaremos el archivo con el nombre`book1.out.xls`.
```csharp
// Guardando el archivo Excel
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
 El`Save`El método escribe el libro de trabajo en el disco en formato Excel 97-2003. Puede especificar formatos diferentes si es necesario.
## Conclusión
Crear un efecto de tachado en el texto de Excel con Aspose.Cells para .NET es un proceso sencillo si lo desglosamos paso a paso. Si sigue esta guía, ahora tendrá las habilidades necesarias para mejorar sus hojas de cálculo con indicaciones visuales, lo que hará que sus datos no solo sean informativos sino también visualmente atractivos.
## Preguntas frecuentes
### ¿Qué es Aspose.Cells?
Aspose.Cells es una potente biblioteca para administrar archivos de Excel en aplicaciones .NET, que le permite crear, manipular y convertir documentos de Excel mediante programación.
### ¿Puedo utilizar Aspose.Cells gratis?
 Sí, puedes usarlo gratis durante un período de prueba. Hay una versión de prueba gratuita disponible en[Prueba gratuita de Aspose.Cells](https://releases.aspose.com/).
### ¿Cómo compro Aspose.Cells?
 Puede comprar una licencia para Aspose.Cells a través de su sitio web[Comprar Aspose.Cells](https://purchase.aspose.com/buy).
### ¿Hay ejemplos disponibles para utilizar Aspose.Cells?
 Sí, puedes encontrar muchos ejemplos y fragmentos de código en el[Documentación de Aspose.Cells](https://reference.aspose.com/cells/net/).
### ¿Dónde puedo obtener soporte para Aspose.Cells?
 Puede obtener apoyo y ayuda de la comunidad en[Foro de Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
