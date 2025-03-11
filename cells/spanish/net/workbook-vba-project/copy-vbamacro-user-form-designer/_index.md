---
title: Copiar el almacenamiento del Diseñador de formularios de usuario de VBAMacro al libro de trabajo mediante Aspose.Cells
linktitle: Copiar el almacenamiento del Diseñador de formularios de usuario de VBAMacro al libro de trabajo mediante Aspose.Cells
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: ¡Aprenda a copiar de manera eficiente el Diseñador de formularios de usuario de macros de VBA en Aspose.Cells para .NET con nuestro completo tutorial paso a paso! Descubra el potencial de Excel.
weight: 11
url: /es/net/workbook-vba-project/copy-vbamacro-user-form-designer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copiar el almacenamiento del Diseñador de formularios de usuario de VBAMacro al libro de trabajo mediante Aspose.Cells

## Introducción
¡Bienvenido! Si busca mejorar su experiencia en Excel con macros y formularios de usuario de VBA, ¡está en el lugar correcto! En esta guía, profundizaremos en cómo puede copiar sin problemas un Diseñador de formularios de usuario de macros de VBA de un libro de trabajo a otro utilizando Aspose.Cells para .NET. Ya sea que sea un desarrollador experimentado o recién esté comenzando, lo guiaremos a través de cada paso crucial. Considere esta su guía para dominar el arte de manejar archivos de Excel de manera programática. ¿Listo para sumergirse? ¡Vamos!
## Prerrequisitos
Antes de adentrarnos en los detalles de la codificación, asegurémonos de que tienes todo lo que necesitas:
1. Entorno de desarrollo de C#: debe tener un entorno de trabajo preparado para el desarrollo de C#. Se recomienda encarecidamente Visual Studio.
2.  Biblioteca Aspose.Cells para .NET: asegúrese de tener la biblioteca Aspose.Cells integrada en su proyecto. Puede hacerlo fácilmente[Descárgalo aquí](https://releases.aspose.com/cells/net/).
3. Conocimientos básicos de VBA y macros de Excel: una buena comprensión de VBA y cómo funcionan las macros de Excel le ayudará a navegar por este tutorial con facilidad.
4. Un archivo de Excel con un formulario de usuario: para experimentar, crear u obtener un libro de Excel que contenga un formulario de usuario, preferiblemente con macros habilitadas (como`.xlsm` archivos).
## Importar paquetes
En su proyecto de C#, deberá importar determinados espacios de nombres en la parte superior de su archivo para utilizar las funcionalidades de Aspose.Cells. A continuación, le indicamos cómo hacerlo:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Vba;
```
La inclusión de estos espacios de nombres le permitirá acceder a todas las potentes herramientas integradas en la biblioteca Aspose.Cells. 
Ahora que ya tenemos cubiertos los requisitos previos y los paquetes, es hora de pasar a la parte divertida: ¡codificar! Veamos el proceso paso a paso.
## Paso 1: Defina sus directorios de origen y salida
Primero, debes establecer dónde se encuentran tus archivos:
```csharp
// Directorio de fuentes
string sourceDir = "Your Document Directory";
// Directorio de salida
string outputDir = "Your Document Directory";
```
 Aquí, reemplace`"Your Document Directory"` con la ruta actual donde se almacenan sus archivos. Aquí es donde se obtendrá nuestro libro de trabajo de origen (con el formulario de usuario) y donde se guardará el nuevo libro de trabajo.
## Paso 2: Crear un libro de trabajo de destino vacío
A continuación, crearemos nuestro libro de trabajo de destino donde copiaremos nuestro formulario de usuario y macros:
```csharp
// Crear un libro de trabajo de destino vacío
Workbook target = new Workbook();
```
Esta línea de código inicializa un libro de trabajo nuevo y vacío que podemos llenar con datos. ¡Piense en ello como un lienzo en blanco para su obra maestra!
## Paso 3: Cargue su libro de trabajo de plantilla
Necesitamos cargar el libro de trabajo que contiene el formulario de usuario y las macros:
```csharp
// Cargue el archivo Excel que contiene el formulario de usuario del Diseñador de macros de VBA
Workbook templateFile = new Workbook(sourceDir + "sampleDesignerForm.xlsm");
```
 Asegúrese de cambiar`"sampleDesignerForm.xlsm"` al nombre de tu archivo actual. Este libro de trabajo es como tu libro de recetas: ¡de ahí sacaremos nuestros ingredientes!
## Paso 4: Copiar hojas de trabajo al libro de trabajo de destino
Ahora, comencemos a copiar hojas de trabajo desde nuestra plantilla al libro de trabajo de destino:
```csharp
// Copiar todas las hojas de trabajo de plantilla al libro de trabajo de destino
foreach (Worksheet ws in templateFile.Worksheets)
{
    if (ws.Type == SheetType.Worksheet)
    {
        Worksheet s = target.Worksheets.Add(ws.Name);
        s.Copy(ws);
        // Coloque el mensaje en la celda A2 de la hoja de cálculo de destino
        s.Cells["A2"].PutValue("VBA Macro and User Form copied from template to target.");
    }
}
```
En este paso, recorreremos cada hoja de trabajo de la plantilla y las copiaremos en nuestro libro de trabajo de destino. Si lo piensas, es como transferir tus mejores recetas de un libro de cocina a otro.
## Paso 5: Copiar macros VBA desde la plantilla
continuación, copiaremos las macros de VBA, incluidos los módulos UserForm Designer, a nuestro nuevo libro de trabajo:
```csharp
// Copiar el UserForm del Diseñador de macros de VBA desde la plantilla al destino
foreach (VbaModule vbaItem in templateFile.VbaProject.Modules)
{
    if (vbaItem.Name == "ThisWorkbook")
    {
        // Copiar el código del módulo ThisWorkbook
        target.VbaProject.Modules["ThisWorkbook"].Codes = vbaItem.Codes;
    }
    else
    {
        // Copiar el código y los datos de otros módulos
        System.Diagnostics.Debug.Print(vbaItem.Name);
        int vbaMod = 0;
        Worksheet sheet = target.Worksheets.GetSheetByCodeName(vbaItem.Name);
        if (sheet == null)
        {
            vbaMod = target.VbaProject.Modules.Add(vbaItem.Type, vbaItem.Name);
        }
        else
        {
            vbaMod = target.VbaProject.Modules.Add(sheet);
        }
        target.VbaProject.Modules[vbaMod].Codes = vbaItem.Codes;
        if ((vbaItem.Type == VbaModuleType.Designer))
        {
            // Obtener los datos del formulario de usuario, es decir, el almacenamiento del diseñador
            byte[] designerStorage = templateFile.VbaProject.Modules.GetDesignerStorage(vbaItem.Name);
            // Agregue el almacenamiento del diseñador al proyecto VBA de destino
            target.VbaProject.Modules.AddDesignerStorage(vbaItem.Name, designerStorage);
        }
    }
}
```
Este gran fragmento de código se encarga de comprobar cada módulo VBA en el archivo de plantilla. Estamos copiando el diseño del formulario de usuario y sus códigos asociados. ¡Es como asegurarse de que no solo obtenga la famosa receta de tarta de la abuela, sino también sus técnicas exactas de horneado!
## Paso 6: Guardar el libro de trabajo de destino
Después de que tengamos todas nuestras copias, es hora de guardar nuestro arduo trabajo:
```csharp
// Guardar el libro de trabajo de destino
target.Save(outputDir + "outputDesignerForm.xlsm", SaveFormat.Xlsm);
```
Asegúrese de modificar el nombre del archivo de salida según sea necesario. Una vez que lo guarde, estará creando su propia versión personalizada del libro de trabajo, repleto de macros y formularios de usuario. ¿No es emocionante?
## Paso 7: Confirmar el éxito
Por último, imprimamos un mensaje de éxito en la consola:
```csharp
Console.WriteLine("CopyVBAMacroUserFormDesignerStorageToWorkbook executed successfully.\r\n");
```
Esta pequeña línea te asegura que el proceso se desarrolló sin problemas. ¡Es la guinda del pastel de tu programación!
## Conclusión
¡Felicitaciones! Ha completado la guía paso a paso para copiar un Diseñador de formularios de usuario de macros de VBA de un libro de trabajo a otro usando Aspose.Cells para .NET. Puede parecer un poco abrumador al principio, pero con la práctica, manejará las manipulaciones de libros de trabajo como un profesional. Recuerde, la codificación es cuestión de práctica, así que no dude en probar diferentes cosas en sus archivos de Excel. Si tiene alguna pregunta o se encuentra con algún problema, no dude en consultar los foros o la documentación de Aspose para obtener ayuda.
## Preguntas frecuentes
### ¿Qué versiones de Excel admite Aspose.Cells?
Aspose.Cells admite una amplia gama de formatos de Excel, incluidos XLSX, XLSM, CSV y más.
### ¿Puedo utilizar Aspose.Cells gratis?
 ¡Sí! Puedes empezar con una prueba gratuita, que te permite evaluar la biblioteca:[Prueba gratuita](https://releases.aspose.com/).
### ¿Necesito Visual Studio para ejecutar este código?
Si bien es muy recomendable debido a sus características fáciles de usar, cualquier IDE de C# funcionará siempre que admita el desarrollo .NET.
### ¿Dónde puedo encontrar más ejemplos y documentación?
 Puedes explorar el[Documentación de Aspose.Cells](https://reference.aspose.com/cells/net/) para más ejemplos y explicaciones detalladas.
### ¿Cómo resuelvo problemas al utilizar Aspose.Cells?
 Deberías visitar el[Foro de soporte de Aspose](https://forum.aspose.com/c/cells/9) para solicitar ayuda a la comunidad y al personal de soporte de Aspose.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
