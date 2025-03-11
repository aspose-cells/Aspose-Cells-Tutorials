---
title: Actualizar elemento de fórmula de Power Query
linktitle: Actualizar elemento de fórmula de Power Query
second_title: Referencia de API de Aspose.Cells para .NET
description: Actualice fácilmente los elementos de fórmulas de Power Query en Excel con Aspose.Cells para .NET. Guía paso a paso para optimizar sus procesos de manipulación de datos.
weight: 160
url: /es/net/excel-workbook/update-power-query-formula-item/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Actualizar elemento de fórmula de Power Query

## Introducción

Si alguna vez ha trabajado con Excel, sabe lo poderoso que puede ser, especialmente cuando comienza a sumergirse en Power Queries. Estas son la fórmula secreta que le permite transformar, limpiar y analizar sus datos sin esfuerzo. Una forma ingeniosa de manipular sus fórmulas de Power Query en Excel es a través de Aspose.Cells para .NET. Hoy, lo guiaremos paso a paso en la actualización de los elementos de fórmula de Power Query. ¡Así que, póngase su sombrero de codificador y comencemos!

## Prerrequisitos

Antes de sumergirte en el código, hay algunas cosas que querrás tener configuradas:

1. Visual Studio: necesitará un entorno de desarrollo integrado (IDE) para escribir y ejecutar su código .NET. Visual Studio es la opción ideal.
2.  Biblioteca Aspose.Cells: asegúrese de tener la biblioteca Aspose.Cells disponible en su proyecto. Puede descargarla desde[sitio](https://releases.aspose.com/cells/net/).
3. Conocimientos básicos de C#: Si bien repasaremos esto juntos, tener algunos conocimientos básicos de C# seguramente será de ayuda, especialmente al navegar por diferentes clases y métodos.
4. Archivos de Excel de muestra: necesitará los archivos de Excel mencionados en el fragmento de código. Asegúrese de tener lo siguiente:
   - `SamplePowerQueryFormula.xlsx`
   - `SamplePowerQueryFormulaSource.xlsx`

5. .NET Framework: asegúrese de que su proyecto tenga como objetivo una versión compatible de .NET Framework.

Ahora que tenemos nuestro kit listo, podemos proceder a la parte divertida: ¡escribir código!

## Importar paquetes

Lo primero es lo primero: deberá importar los espacios de nombres necesarios. A continuación, le indicamos cómo hacerlo:

```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```

Al agregar estos espacios de nombres, le estás informando al compilador que tienes la intención de usar las clases y los métodos de la biblioteca Aspose.Cells. Este paso es crucial, ya que sienta las bases para el código que sigue.

Analicemos el fragmento de código que nos proporcionaste. Este tutorial te guiará por cada parte para asegurarte de que entiendes lo que está sucediendo.

## Paso 1: Configurar directorios de trabajo

En este paso, definiremos dónde se encuentran nuestros archivos de origen y de salida. Esto garantiza que Aspose sepa dónde buscar sus archivos de Excel.

```csharp
// Directorios de trabajo
string SourceDir = "Your Document Directory";
string outputDir = "Your Output Directory";
```

## Paso 2: Cargue el libro de trabajo

Ahora, carguemos el archivo Excel donde reside Power Query.

```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
 El`Workbook` La clase es el punto de entrada al archivo de Excel. Al pasar la ruta de nuestro archivo de origen, estamos creando una instancia que nos permite manipularlo. Puedes imaginarlo como abrir un libro: te estás preparando para leer (o editar) su contenido.

## Paso 3: Acceda al Mashup de datos

A continuación, accederemos a las fórmulas de Power Query almacenadas en el Mashup de datos del libro de trabajo.

```csharp
DataMashup mashupData = workbook.DataMashup;
```
 El`DataMashup` La clase contiene todas las fórmulas de Power Query asociadas con su libro de trabajo. Aquí es donde haremos el trabajo pesado, como cuando abre una caja de herramientas para realizar reparaciones.

## Paso 4: Recorrer las fórmulas de Power Query

Ahora viene la parte en la que iteramos a través de las fórmulas de Power Query para encontrar la específica que queremos actualizar.

```csharp
foreach (PowerQueryFormula formula in mashupData.PowerQueryFormulas)
{
    foreach (PowerQueryFormulaItem item in formula.PowerQueryFormulaItems)
    {
        if (item.Name == "Source")
        {
            item.Value = "Excel.Workbook(File.Contents(\"" + SourceDir + "SamplePowerQueryFormulaSource.xlsx\"), null, true)";
        }
    }
}
```

-  Hacemos un bucle a través de cada uno`PowerQueryFormula` en`mashupData`.
- Dentro de ese bucle, nos sumergimos en cada uno de ellos.`PowerQueryFormulaItem`.
- Comprobamos si el nombre del elemento coincide con "Fuente". Si es así, actualizamos su valor para vincularlo a nuestro nuevo archivo fuente.

Esto es similar a encontrar la página correcta en un manual y luego realizar las actualizaciones necesarias: es un proceso sencillo y meticuloso.

## Paso 5: Guardar el libro de trabajo actualizado

Después de realizar las actualizaciones, es hora de guardar nuestros cambios.

```csharp
// Guarde el libro de trabajo de salida.
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
 El`Save` El método escribe el libro de trabajo actualizado en el directorio de salida especificado. ¡Es como sellar tus ediciones en una nueva versión del manual, lista para que otros la usen!

## Conclusión

¡Felicitaciones! Ha actualizado correctamente un elemento de fórmula de Power Query con Aspose.Cells para .NET. Con este método, puede automatizar la modificación de fórmulas de Power Query en sus archivos de Excel, lo que le permitirá ahorrar tiempo y esfuerzo valiosos.

## Preguntas frecuentes

### ¿Qué es Aspose.Cells?
Aspose.Cells es una potente biblioteca para manipular archivos Excel en aplicaciones .NET sin necesidad de tener instalado Microsoft Excel.

### ¿Necesito Microsoft Excel para ejecutar Aspose.Cells?
No, Aspose.Cells le permite crear y editar archivos Excel mediante programación sin necesidad de tener Excel en su servidor o máquina de desarrollo.

### ¿Con qué tipos de archivos de Excel puedo trabajar usando Aspose.Cells?
Puede trabajar con .xlsx, .xls, .xlsm y varios otros formatos de Excel utilizando Aspose.Cells.

### ¿Hay una versión de prueba disponible para Aspose.Cells?
 Sí, puedes descargar una versión de prueba gratuita desde[Página de lanzamiento de Aspose Cells](https://releases.aspose.com/).

### ¿Cómo puedo obtener soporte para Aspose.Cells?
 Puede acceder al soporte a través de[Foro de Aspose](https://forum.aspose.com/c/cells/9), donde podrás hacer preguntas y encontrar respuestas de la comunidad y del equipo de Aspose.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
