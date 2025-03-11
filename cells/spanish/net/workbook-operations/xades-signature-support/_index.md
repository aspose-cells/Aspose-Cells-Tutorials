---
title: Compatibilidad con XAdESSignature en Workbook mediante Aspose.Cells
linktitle: Compatibilidad con XAdESSignature en Workbook mediante Aspose.Cells
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Aprenda a implementar la compatibilidad con firmas XAdES en libros de Excel con Aspose.Cells para .NET. Siga nuestra guía paso a paso para firmar documentos de forma segura.
weight: 29
url: /es/net/workbook-operations/xades-signature-support/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Compatibilidad con XAdESSignature en Workbook mediante Aspose.Cells

## Introducción
En el mundo digital actual, la integridad y autenticidad de los datos son primordiales. Imagine que está enviando un documento crítico de Excel y desea asegurarse de que el destinatario sepa que no ha sido manipulado. ¡Ahí es donde entran en juego las firmas digitales! Con Aspose.Cells para .NET, puede agregar fácilmente firmas XAdES a sus libros de Excel, lo que garantiza que sus datos permanezcan seguros y confiables. En este tutorial, lo guiaremos paso a paso por el proceso de implementación de la compatibilidad con firmas XAdES en sus archivos de Excel. ¡Vamos a profundizar!
## Prerrequisitos
Antes de comenzar, hay algunas cosas que debes tener en cuenta para seguir este tutorial:
1. Aspose.Cells para .NET: Asegúrate de tener instalada la biblioteca Aspose.Cells. Puedes descargarla[aquí](https://releases.aspose.com/cells/net/).
2. Entorno de desarrollo: un IDE adecuado para el desarrollo .NET, como Visual Studio.
3. Conocimientos básicos de C#: la familiaridad con la programación en C# le ayudará a comprender mejor los fragmentos de código.
4. Certificado Digital: Un archivo PFX (intercambio de información personal) válido que contiene su certificado digital y una contraseña para acceder a él.
¿Lo tienes todo? ¡Genial! Pasemos al siguiente paso.
## Importar paquetes
Para comenzar a utilizar Aspose.Cells, debe importar los espacios de nombres necesarios en su proyecto de C#. Esto le permitirá acceder a las clases y métodos necesarios para agregar firmas digitales. A continuación, le indicamos cómo hacerlo:
### Crear un nuevo proyecto de C#
1. Abra Visual Studio.
2. Crear un nuevo proyecto de aplicación de consola.
3.  Ponle a tu proyecto un nombre reconocible, como`XAdESSignatureExample`.
### Añadir referencia de Aspose.Cells
1.  Haga clic derecho en su proyecto en el Explorador de soluciones y seleccione`Manage NuGet Packages`.
2.  Buscar`Aspose.Cells` e instalar la última versión.
### Importar los espacios de nombres necesarios
 En la parte superior de tu`Program.cs` archivo, agregue las siguientes directivas using:
```csharp
using Aspose.Cells.DigitalSignatures;
using System;
using System.IO;
```
Esto le permitirá utilizar las clases y métodos Aspose.Cells en su proyecto.
Ahora que tiene todo configurado, desglosemos el proceso de agregar una firma XAdES a su libro de trabajo en pasos manejables.
## Paso 1: Configurar los directorios de origen y salida
Antes de comenzar a trabajar con su archivo de Excel, debe definir dónde se encuentra el archivo de origen y dónde desea guardar el archivo de salida.
```csharp
// Directorio de fuentes
string sourceDir = "Your Document Directory";
// Directorio de salida
string outputDir = "Your Document Directory";
```
 Reemplazar`"Your Document Directory"`con la ruta real donde se almacena su archivo de Excel y donde desea guardar el archivo firmado.
## Paso 2: Cargue el libro de trabajo
 A continuación, cargará el libro de Excel que desea firmar. Esto se hace mediante el botón`Workbook` clase de Aspose.Cells.
```csharp
Workbook workbook = new Workbook(sourceDir + "sourceFile.xlsx");
```
 Asegúrese de reemplazar`"sourceFile.xlsx"` con el nombre de su archivo Excel actual.
## Paso 3: Prepare su certificado digital
Para agregar una firma digital, debe cargar su archivo PFX y proporcionar la contraseña correspondiente. A continuación, le indicamos cómo hacerlo:
```csharp
string password = "pfxPassword"; // Reemplace con su contraseña PFX
string pfx = "pfxFile"; // Ruta a su archivo PFX
```
 Asegúrese de reemplazar`"pfxPassword"` con tu contraseña actual y`"pfxFile"` con la ruta a su archivo PFX.
## Paso 4: Crear una firma digital
 Ahora es el momento de crear una firma digital utilizando el`DigitalSignature` clase. Necesitará leer el archivo PFX en una matriz de bytes y luego crear la firma.
```csharp
DigitalSignature signature = new DigitalSignature(File.ReadAllBytes(pfx), password, "testXAdES", DateTime.Now);
signature.XAdESType = XAdESType.XAdES;
```
 Aquí,`"testXAdES"` es el motivo de la firma, y`DateTime.Now` Indica el momento de la firma.
## Paso 5: Agregar la firma al libro de trabajo
 Para agregar la firma a su libro de trabajo, deberá crear una`DigitalSignatureCollection` y añade tu firma.
```csharp
DigitalSignatureCollection dsCollection = new DigitalSignatureCollection();
dsCollection.Add(signature);
```
## Paso 6: Establezca la firma digital en el libro de trabajo
Ahora que tienes lista tu colección de firmas, es hora de configurarla en el libro de trabajo.
```csharp
workbook.SetDigitalSignature(dsCollection);
```
## Paso 7: Guardar el libro de trabajo
Por último, guarde su libro de trabajo con la firma digital aplicada.
```csharp
workbook.Save(outputDir + "XAdESSignatureSupport_out.xlsx");
```
 Reemplazar`"XAdESSignatureSupport_out.xlsx"` con el nombre de archivo de salida deseado.
## Paso 8: Confirmar el éxito
Para garantizar que todo salió bien, puede imprimir un mensaje de éxito en la consola.
```csharp
Console.WriteLine("XAdESSignatureSupport executed successfully.");
```
## Conclusión
 ¡Y ya está! Ha añadido correctamente la compatibilidad con firmas XAdES a su libro de Excel mediante Aspose.Cells para .NET. Esta potente función no solo mejora la seguridad de sus documentos, sino que también ayuda a mantener la integridad de sus datos. Si tiene alguna pregunta o se encuentra con algún problema, no dude en consultar la[Documentación de Aspose.Cells](https://reference.aspose.com/cells/net/) o visite el[foro de soporte](https://forum.aspose.com/c/cells/9) para solicitar ayuda.
## Preguntas frecuentes
### ¿Qué es XAdES?
XAdES (XML Advanced Electronic Signatures) es un estándar para firmas electrónicas que garantiza la integridad y autenticidad de los documentos electrónicos.
### ¿Necesito un certificado digital para utilizar firmas XAdES?
Sí, necesita un certificado digital válido en formato PFX para crear una firma XAdES.
### ¿Puedo utilizar Aspose.Cells para otros formatos de archivo?
Sí, Aspose.Cells funciona principalmente con archivos Excel, pero también admite otros formatos de hojas de cálculo.
### ¿Hay una prueba gratuita disponible para Aspose.Cells?
¡Por supuesto! Puedes obtener una prueba gratuita[aquí](https://releases.aspose.com/).
### ¿Dónde puedo encontrar más ejemplos y tutoriales?
 Puede explorar más ejemplos y documentación detallada en[Sitio web Aspose.Cells](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
