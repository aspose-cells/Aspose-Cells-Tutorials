---
title: Encuentre el máximo de filas y columnas admitidas por los formatos XLS y XLSX
linktitle: Encuentre el máximo de filas y columnas admitidas por los formatos XLS y XLSX
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Descubra la cantidad máxima de filas y columnas que admiten los formatos XLS y XLSX con Aspose.Cells para .NET. Maximice la gestión de datos de Excel con este completo tutorial.
weight: 11
url: /es/net/workbook-settings/find-maximum-supported-rows-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Encuentre el máximo de filas y columnas admitidas por los formatos XLS y XLSX

## Introducción
En el mundo de Excel, administrar grandes conjuntos de datos puede ser una tarea abrumadora, especialmente cuando se trata de manejar la cantidad máxima de filas y columnas admitidas por diferentes formatos de archivo. Este tutorial lo guiará a través del proceso de búsqueda de la cantidad máxima de filas y columnas admitidas por los formatos XLS y XLSX mediante la biblioteca Aspose.Cells para .NET. Al final de este artículo, comprenderá en profundidad cómo utilizar esta poderosa herramienta para manejar sus tareas relacionadas con Excel de manera eficiente.
## Prerrequisitos
Antes de sumergirnos en el tutorial, asegúrese de tener los siguientes requisitos previos:
1. [Marco .NET](https://dotnet.microsoft.com/en-us/download) o[.NET Core](https://dotnet.microsoft.com/en-us/download) instalado en su sistema.
2. [Aspose.Cells para .NET](https://releases.aspose.com/cells/net/) Biblioteca descargada y referenciada en su proyecto.
 Si aún no lo ha hecho, puede descargar la biblioteca Aspose.Cells para .NET desde[sitio web](https://releases.aspose.com/cells/net/) o instalarlo a través de[NuGet](https://www.nuget.org/packages/Aspose.Cells/).
## Importar paquetes
Para comenzar, deberá importar los paquetes necesarios de la biblioteca Aspose.Cells para .NET. Agregue las siguientes instrucciones using en la parte superior de su archivo C#:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Paso 1: Encuentra el máximo de filas y columnas admitidas por el formato XLS
Comencemos explorando el máximo de filas y columnas que admite el formato XLS (Excel 97-2003).
```csharp
// Imprimir mensaje sobre el formato XLS.
Console.WriteLine("Maximum Rows and Columns supported by XLS format.");
// Crear libro de trabajo en formato XLS.
Workbook wb = new Workbook(FileFormatType.Excel97To2003);
// Imprima el máximo de filas y columnas admitidas por el formato XLS.
int maxRows = wb.Settings.MaxRow + 1;
int maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
Console.WriteLine();
```
En este paso:
1. Imprima un mensaje para indicar que estamos trabajando con el formato XLS.
2.  Crear uno nuevo`Workbook` instancia utilizando el`FileFormatType.Excel97To2003` enumeración, que representa el formato XLS.
3.  Recupere el máximo de filas y columnas admitidas por el formato XLS utilizando el`Workbook.Settings.MaxRow` y`Workbook.Settings.MaxColumn`propiedades, respectivamente. Sumamos 1 a estos valores para obtener los números máximos reales de filas y columnas (ya que están basados en cero).
4. Imprima el máximo de filas y columnas en la consola.
## Paso 2: Encuentra el máximo de filas y columnas admitidas por el formato XLSX
A continuación, exploremos el máximo de filas y columnas que admite el formato XLSX (Excel 2007 y posteriores).
```csharp
// Imprimir mensaje sobre el formato XLSX.
Console.WriteLine("Maximum Rows and Columns supported by XLSX format.");
// Crear libro de trabajo en formato XLSX.
wb = new Workbook(FileFormatType.Xlsx);
// Imprima el máximo de filas y columnas admitidas por el formato XLSX.
maxRows = wb.Settings.MaxRow + 1;
maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
```
En este paso:
1. Imprima un mensaje para indicar que estamos trabajando con el formato XLSX.
2.  Crear uno nuevo`Workbook` instancia utilizando el`FileFormatType.Xlsx` enumeración, que representa el formato XLSX.
3.  Recupere el máximo de filas y columnas admitidas por el formato XLSX utilizando el`Workbook.Settings.MaxRow` y`Workbook.Settings.MaxColumn`propiedades, respectivamente. Sumamos 1 a estos valores para obtener los números máximos reales de filas y columnas (ya que están basados en cero).
4. Imprima el máximo de filas y columnas en la consola.
## Paso 3: Mostrar un mensaje de éxito
Por último, mostremos un mensaje de éxito para indicar que el ejemplo "FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats" se ha ejecutado correctamente.
```csharp
Console.WriteLine("FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats executed successfully.");
```
Este paso simplemente imprime un mensaje de éxito en la consola.
## Conclusión
En este tutorial, aprendió a usar la biblioteca Aspose.Cells para .NET para encontrar la cantidad máxima de filas y columnas admitidas por los formatos de archivo XLS y XLSX. Al comprender las limitaciones de estos formatos, puede planificar y administrar mejor sus proyectos basados en Excel, lo que garantiza que sus datos se ajusten a los rangos admitidos.
## Preguntas frecuentes
### ¿Cuál es el número máximo de filas que admite el formato XLS?
El número máximo de filas admitido por el formato XLS (Excel 97-2003) es 65.536.
### ¿Cuál es el número máximo de columnas que admite el formato XLS?
El número máximo de columnas admitidas por el formato XLS (Excel 97-2003) es 256.
### ¿Cuál es el número máximo de filas que admite el formato XLSX?
El número máximo de filas admitido por el formato XLSX (Excel 2007 y posteriores) es 1.048.576.
### ¿Cuál es el número máximo de columnas que admite el formato XLSX?
El número máximo de columnas admitidas por el formato XLSX (Excel 2007 y posteriores) es 16.384.
### ¿Puedo utilizar la biblioteca Aspose.Cells para .NET para trabajar con otros formatos de archivos de Excel?
 Sí, la biblioteca Aspose.Cells para .NET admite una amplia gama de formatos de archivos de Excel, incluidos XLS, XLSX, ODS y más. Puede explorar[documentación](https://reference.aspose.com/cells/net/) para conocer las características y funcionalidades disponibles.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
