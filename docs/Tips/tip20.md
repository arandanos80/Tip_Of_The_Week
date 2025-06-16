---
layout: post
title: "Tip 20: Ejecutar una clase individual con dotnet run"
---
# 💡 Ejecutar una clase individual con ```dotnet run```  

🔥 Una de las nuevas funcionalidades más prácticas introducidas en **.NET 10 Preview 4** es la capacidad de ejecutar directamente **un archivo de clase individual (.cs)** desde la línea de comandos usando ```dotnet run```, **sin necesidad de compilar ni ejecutar el proyecto completo**.

Esto convierte cualquier archivo ```.cs``` en un pequeño **script ejecutable**, ideal para tareas ad-hoc, pruebas o utilidades internas.

### ✅ ¿Cómo se usa?
Supón que tienes el siguiente archivo en tu proyecto:
```c#
// Archivo: Utilities/TempScript.cs
using System.Text.Json;

Console.WriteLine("Procesando archivo JSON...");

string json = File.ReadAllText("data.json");
var data = JsonSerializer.Deserialize<Dictionary<string, string>>(json);

foreach (var (key, value) in data!)
{
    Console.WriteLine($"{key}: {value}");
}
```
Puedes ejecutarlo directamente así:
```
dotnet run Utilities/TempScript.cs
```
📦 Si necesitas pasar argumentos:
```
dotnet run Utilities/TempScript.cs -- arg1 arg2
```

### ✨ ¿Por qué es útil?
✅ No necesitas modificar ```Program.cs``` ni tocar el proyecto  
✅ Perfecto para scripts de mantenimiento, pruebas rápidas, transformaciones de datos, etc.  
✅ Útil en tareas DevOps o cuando experimentas con librerías nuevas  
✅ Compatible con ```top-level statements```, pero también puedes tener ```static void Main()``` si lo deseas  
✅ **Evolución sencilla:** tu script puede convertirse en un proyecto completo con ```dotnet project convert app.cs```.

### 🧩 Directivas en el archivo, sin ```.csproj```:
```c#
#:package Humanizer@2.14.1
#:sdk Microsoft.NET.Sdk
#:property LangVersion preview

using Humanizer;

Console.WriteLine($"Han pasado {TimeSpan.FromDays(1).Humanize()} desde ayer.");
```

Estas directivas permiten:
- Referenciar paquetes NuGet con ```#:package```
- Definir el SDK, como ```Microsoft.NET.Sdk.Web```
- Establecer propiedades MSBuild, como ```LangVersion```

### 🛠️ Ejemplo del "mundo real": script para consultar una API
```c#
#:package Flurl.Http@4.0.2

using Flurl.Http;

var resp = await "https://api.github.com"
    .WithHeader("User-Agent", "dotnet-script")
    .GetJsonAsync<object>();

Console.WriteLine(resp);
```
```bash
dotnet run fetchGithub.cs
```
Este script descarga y serializa datos de GitHub, ¡todo sin crear un proyecto! 

### 📈 Escala a proyecto completo
Cuando el script crece:
```bash
dotnet project convert app.cs
```
Esto generará un proyecto con ```.csproj```, trasladará tu código y convertirá las directivas ```#:``` a configuraciones MSBuild 

### ✨ Ventajas clave
- Inmediatez: tres comandos y ejecutas código, sin necesidad de proyecto.
- Simplicidad: menos archivos, configuración mínima.
- Flexibilidad: desde scripts breves hasta Minimal APIs en un solo archivo.
- Escalable: proyecta hacia un proyecto real cuando sea necesario.

🔔 Requiere tener instalado el **SDK de .NET 10 Preview 4 o superior.**
