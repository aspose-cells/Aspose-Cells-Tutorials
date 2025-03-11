---
title: Desagrupar filas y columnas en Excel con Aspose.Cells
linktitle: Desagrupar filas y columnas en Excel con Aspose.Cells
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Aprenda a desagrupar filas y columnas en Excel con Aspose.Cells para .NET con esta guía completa. Simplifique la manipulación de datos en Excel.
weight: 15
url: /es/net/row-and-column-management/ungrouping-rows-and-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Desagrupar filas y columnas en Excel con Aspose.Cells

## Introducción
Cuando se trata de manejar archivos de Excel, es posible que te encuentres en situaciones en las que necesites desagrupar filas y columnas. Ya sea que estés limpiando una hoja de cálculo o reformateando datos para una mejor presentación, Aspose.Cells para .NET es una herramienta fantástica que simplifica el proceso. En este tutorial, te guiaré a través de los pasos para desagrupar filas y columnas en Excel usando Aspose.Cells. Al final, tendrás una sólida comprensión de cómo trabajar con archivos de Excel de manera programática.
## Prerrequisitos
Antes de sumergirnos en el código, asegurémonos de que tienes todo configurado. Esto es lo que necesitarás:
1.  Visual Studio: Debe tener una versión funcional de Visual Studio instalada en su equipo. Si aún no la tiene, puede descargarla desde[Sitio de Visual Studio](https://visualstudio.microsoft.com/).
2. Aspose.Cells para .NET: Necesitará descargar la biblioteca Aspose.Cells. Puede descargarla desde el sitio web[Página de lanzamientos de Aspose](https://releases.aspose.com/cells/net/) Asegúrese de tener las licencias necesarias, que se pueden comprar u obtener a través de un[licencia temporal](https://purchase.aspose.com/temporary-license/).
3. Conocimientos básicos de C#: una comprensión básica de la programación en C# le ayudará a seguir el proceso más fácilmente.
Una vez que tengas todo listo, podemos pasar a la parte divertida: ¡el código!
## Importar paquetes
Para comenzar, debe importar los paquetes necesarios en su proyecto de C#. A continuación, le indicamos cómo hacerlo:
1. Abra su proyecto en Visual Studio.
2. Agregue una referencia a la biblioteca Aspose.Cells. Puede hacerlo haciendo clic derecho en las Referencias en su proyecto y seleccionando Agregar referencia. Busque la ubicación donde guardó la DLL Aspose.Cells.
3. En la parte superior de su archivo C#, agregue las siguientes directivas using:
```csharp
using System.IO;
using Aspose.Cells;
```
Ahora que todo está configurado, veamos los pasos para desagrupar filas y columnas en su hoja de Excel. 
## Paso 1: Definir el directorio del documento
En primer lugar, debe especificar el directorio en el que se encuentra su archivo de Excel. Puede configurarlo de la siguiente manera:
```csharp
// La ruta al directorio de documentos.
string dataDir = "Your Document Directory";
```
 Reemplazar`"Your Document Directory"` con la ruta real en su computadora donde está guardado el archivo Excel. 
## Paso 2: Crear un flujo de archivos
continuación, debe crear una secuencia de archivos para abrir el archivo de Excel. Puede hacerlo de la siguiente manera:
```csharp
// Creación de un flujo de archivos que contiene el archivo Excel que se va a abrir
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
 Aquí estás abriendo el archivo llamado`book1.xls`Asegúrese de que este archivo exista en el directorio especificado; de lo contrario, se encontrará con un error de archivo no encontrado.
## Paso 3: Crear una instancia de un objeto de libro de trabajo
Ahora, carguemos el archivo de Excel en un objeto Workbook. Esto le permitirá manipular el libro de trabajo mediante programación:
```csharp
// Creación de una instancia de un objeto Workbook
// Abrir el archivo Excel a través del flujo de archivos
Workbook workbook = new Workbook(fstream);
```
Con esta línea de código, ha cargado correctamente el archivo Excel en la memoria y está listo para trabajar con él.
## Paso 4: Acceda a la hoja de trabajo
Una vez que tenga el libro de trabajo, el siguiente paso es acceder a la hoja de trabajo específica en la que desea desagrupar filas y columnas. A continuación, le indicamos cómo hacerlo:
```csharp
// Acceder a la primera hoja de cálculo del archivo Excel
Worksheet worksheet = workbook.Worksheets[0];
```
En este caso, accedemos a la primera hoja de cálculo. Si los datos están en una hoja diferente, puedes cambiar el índice según corresponda.
## Paso 5: Desagrupar filas
¡Ahora viene la parte emocionante! Desagruparemos las primeras seis filas (de la fila 0 a la fila 5). Utilicemos el siguiente código:
```csharp
// Desagrupando las primeras seis filas (de 0 a 5)
worksheet.Cells.UngroupRows(0, 5);
```
Este método elimina cualquier agrupación que se haya aplicado a las filas especificadas. ¡Así de fácil!
## Paso 6: Desagrupar columnas
Al igual que las filas, también puedes desagrupar columnas. A continuación, te indicamos cómo desagrupar las primeras tres columnas (de la columna 0 a la columna 2):
```csharp
// Desagrupando las primeras tres columnas (de 0 a 2)
worksheet.Cells.UngroupColumns(0, 2);
```
## Paso 7: Guarde el archivo Excel modificado
 Una vez que haya desagrupado las filas y columnas, el siguiente paso es guardar los cambios nuevamente en un archivo de Excel. Puede hacerlo utilizando el`Save` método:
```csharp
// Guardando el archivo Excel modificado
workbook.Save(dataDir + "output.xls");
```
 En este ejemplo, guardamos el archivo modificado como`output.xls`Puedes cambiar el nombre del archivo por el que prefieras.
## Paso 8: Cerrar el flujo de archivos
Por último, para liberar recursos, debes cerrar el flujo de archivos:
```csharp
// Cerrar el flujo de archivos para liberar todos los recursos
fstream.Close();
```
Esta es una buena práctica para garantizar que su aplicación no retenga los identificadores de archivos por más tiempo del necesario.
## Conclusión
¡Y ya está! Aprendió a desagrupar filas y columnas en un archivo de Excel con Aspose.Cells para .NET. Con solo unas pocas líneas de código, puede realizar cambios significativos en sus archivos de Excel mediante programación. Ya sea que esté automatizando informes o preparando datos para análisis, dominar estas técnicas puede ahorrarle mucho tiempo.
## Preguntas frecuentes
### ¿Qué es Aspose.Cells?
Aspose.Cells es una potente biblioteca para trabajar con archivos Excel en aplicaciones .NET, lo que permite una fácil manipulación, conversión y creación de hojas de cálculo.
### ¿Puedo desagrupar filas y columnas en Excel usando otras bibliotecas?
Sí, hay otras bibliotecas disponibles para la manipulación de Excel en .NET, pero Aspose.Cells ofrece amplias funciones y facilidad de uso.
### ¿Hay alguna forma de deshacer los cambios después de guardarlos?
Una vez que guarde un archivo Excel, no se podrá restaurar el estado anterior a menos que tenga una copia de seguridad del archivo original.
### ¿Cómo puedo obtener soporte para Aspose.Cells?
 Puede encontrar ayuda visitando el sitio[Foro de soporte de Aspose](https://forum.aspose.com/c/cells/9), donde podrás hacer preguntas y encontrar soluciones.
### ¿Puedo utilizar Aspose.Cells sin una licencia?
Sí, puedes usar Aspose.Cells de forma gratuita con ciertas limitaciones, y puedes comenzar con una[licencia temporal](https://purchase.aspose.com/temporary-license/) para una funcionalidad completa.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
