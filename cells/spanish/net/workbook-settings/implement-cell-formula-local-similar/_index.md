---
"description": "Descubra cómo implementar una fórmula de celda similar a la función local de fórmula de rango en Aspose.Cells para .NET. Aprenda a personalizar los nombres de las funciones integradas de Excel y mucho más."
"linktitle": "Implementar fórmula de celda local similar a fórmula de rango local"
"second_title": "API de procesamiento de Excel Aspose.Cells .NET"
"title": "Implementar fórmula de celda local similar a fórmula de rango local"
"url": "/es/net/workbook-settings/implement-cell-formula-local-similar/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Implementar fórmula de celda local similar a fórmula de rango local

## Introducción
Aspose.Cells para .NET es una API potente y flexible para la manipulación de hojas de cálculo que permite crear, manipular y convertir archivos de Excel mediante programación. Una de las muchas funciones que ofrece Aspose.Cells es la posibilidad de personalizar el comportamiento de las funciones integradas de Excel, incluyendo la posibilidad de crear sus propios nombres de función locales. En este tutorial, le guiaremos por los pasos para implementar una fórmula de celda similar a la funcionalidad local de fórmula de rango de Aspose.Cells para .NET.
## Prerrequisitos
Antes de comenzar, asegúrese de tener lo siguiente:
1. Microsoft Visual Studio 2010 o posterior instalado en su sistema.
2. La última versión de la biblioteca Aspose.Cells para .NET instalada en su proyecto. Puede descargarla desde [Página de descarga de Aspose.Cells para .NET](https://releases.aspose.com/cells/net/).
## Importar paquetes
Para comenzar, deberá importar los paquetes necesarios en su proyecto de C#. Agregue las siguientes instrucciones "using" al principio de su archivo de código:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Paso 1: Crear una clase de configuración de globalización personalizada
El primer paso es crear un archivo personalizado `GlobalizationSettings` Clase que permite anular el comportamiento predeterminado de las funciones de Excel. En este ejemplo, cambiaremos los nombres de las `SUM` y `AVERAGE` funciones para `UserFormulaLocal_SUM` y `UserFormulaLocal_AVERAGE`, respectivamente.
```csharp
class GS : GlobalizationSettings
{
    public override string GetLocalFunctionName(string standardName)
    {
        //Cambie el nombre de la función SUMA según sus necesidades.
        if (standardName == "SUM")
        {
            return "UserFormulaLocal_SUM";
        }
        //Cambie el nombre de la función PROMEDIO según sus necesidades.
        if (standardName == "AVERAGE")
        {
            return "UserFormulaLocal_AVERAGE";
        }
        return "";
    }
}
```
## Paso 2: Cree un nuevo libro de trabajo y asigne la configuración de globalización personalizada
A continuación, cree una nueva instancia de Libro de trabajo y asígnele la configuración personalizada. `GlobalizationSettings` clase de implementación al libro de trabajo `Settings.GlobalizationSettings` propiedad.
```csharp
//Crear libro de trabajo
Workbook wb = new Workbook();
//Asignar la clase de implementación de GlobalizationSettings
wb.Settings.GlobalizationSettings = new GS();
```
## Paso 3: Acceda a la primera hoja de cálculo y a una celda
Ahora, accedamos a la primera hoja de cálculo del libro y a una celda específica dentro de esa hoja de cálculo.
```csharp
//Acceda a la primera hoja de trabajo
Worksheet ws = wb.Worksheets[0];
//Acceder a alguna celda
Cell cell = ws.Cells["C4"];
```
## Paso 4: Asignar fórmulas e imprimir la fórmula local
Por último, vamos a asignar el `SUM` y `AVERAGE` fórmulas a la celda e imprimir el resultado `FormulaLocal` valores.
```csharp
//Asignar fórmula SUMA e imprimir su FórmulaLocal
cell.Formula = "SUM(A1:A2)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
//Asignar fórmula PROMEDIO e imprimir su FórmulaLocal
cell.Formula = "=AVERAGE(B1:B2, B5)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
```
## Conclusión
En este tutorial, aprendió a implementar una fórmula de celda similar a la función local de fórmula de rango en Aspose.Cells para .NET. Al crear una fórmula personalizada... `GlobalizationSettings` Con la clase, puede anular el comportamiento predeterminado de las funciones de Excel y personalizar los nombres de las funciones locales según sus necesidades. Esto puede ser especialmente útil al trabajar con documentos de Excel localizados o internacionalizados.
## Preguntas frecuentes
### ¿Cuál es el propósito de la `GlobalizationSettings` ¿clase en Aspose.Cells?
El `GlobalizationSettings` La clase en Aspose.Cells le permite personalizar el comportamiento de las funciones integradas de Excel, incluida la capacidad de cambiar los nombres de las funciones locales.
### ¿Puedo anular el comportamiento de funciones distintas a... `SUM` y `AVERAGE`?
Sí, puede anular el comportamiento de cualquier función integrada de Excel modificando la `GetLocalFunctionName` método en su costumbre `GlobalizationSettings` clase.
### ¿Hay alguna manera de restablecer los nombres de las funciones a sus valores predeterminados?
Sí, puede restablecer los nombres de las funciones eliminando la configuración personalizada. `GlobalizationSettings` clase o devolviendo una cadena vacía de la `GetLocalFunctionName` método.
### ¿Puedo utilizar esta función para crear funciones personalizadas en Aspose.Cells?
No, el `GlobalizationSettings` La clase está diseñada para anular el comportamiento de las funciones integradas de Excel, no para crear funciones personalizadas. Si necesita crear funciones personalizadas, puede usar la clase `UserDefinedFunction` clase en Aspose.Cells.
### ¿Esta función está disponible en todas las versiones de Aspose.Cells para .NET?
Sí, el `GlobalizationSettings` La clase y la capacidad de personalizar los nombres de las funciones están disponibles en todas las versiones de Aspose.Cells para .NET.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}