---
layout: post
title: "Tip 10: Diferencias entre Const y Readonly"
---
# Diferencias entre Const y Readonly  
### 🔑 **Introducción**  
Las palabras clave **const** y **readonly** en **C#** tienen como objetivo evitar modificaciones en las variables después de su inicialización, pero su uso y propósito tienen diferencias importantes.  

### ✅ **Características clave**  
🔷 **const**  
1. **Valor fijo en tiempo de compilación:**  
- Su valor debe estar disponible y calculado en tiempo de compilación.
2. **Declaración obligatoria con un inicializador:**
- Es obligatorio asignar un valor en su declaración.
3. **Implícitamente estático:**
- No necesita ser declarado como ```static```, ya que lo es por defecto.
4. **Restricciones de tipo:**
- Solo se permite con tipos primitivos como int, bool, string y double.
- No admite tipos definidos por el usuario, como clases o structs.

```c#
const double Pi = 3.14159;  // Valor fijo en tiempo de compilación.
const int MaxConnections = 10;  // Implícitamente estático.
```
🔷 **readonly**
1. **Valor fijo en tiempo de ejecución:**  
- Su valor puede ser asignado en la declaración o en el constructor.
2. **Flexibilidad en tipos:**
- Puede usarse con cualquier tipo, incluidos tipos por referencia como clases, arrays, y structs.
3. **Puede ser ```static``` o de instancia:**
- No es implícitamente estático; debes declararlo explícitamente si deseas ese comportamiento.

```c#
readonly DateTime CreatedOn = DateTime.Now;  // Asignado en tiempo de ejecución.
readonly string[] Names;  // Admite tipos complejos como arrays.

public MyClass(string[] names)
{
    Names = names;  // Se permite asignar en el constructor.
}
```

### 🆚 **Comparativa**
<table>
    <thead>
        <tr style="background-color: #e5e5e5">
            <th>Aspecto</th>
            <th>const</th>
            <th>readonly</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td style='font-weight: bold;'>Inicialización</td>
            <td>En tiempo de compilación.</td>
            <td>En tiempo de ejecución o constructor.</td>
        </tr>
        <tr>
            <td style='font-weight: bold;'>Modificación posterior</td>
            <td>No se puede modificar.</td>
            <td>No se puede modificar tras asignación inicial o en el constructor.</td>
        </tr>
        <tr>
            <td style='font-weight: bold;'>Alcance de tipos</td>
            <td>Solo tipos primitivos (int, bool, string).</td>
            <td>Admite cualquier tipo, incluidos objetos y arrays.</td>
        </tr>
        <tr>
            <td style='font-weight: bold;'>Estático por defecto</td>
            <td>Sí, implícitamente estático.</td>
            <td>No, debe ser declarado explícitamente si es estático.</td>
        </tr>
        <tr>
            <td style='font-weight: bold;'>Uso con tipos definidos por el usuario</td>
            <td>No</td>
            <td>Sí</td>
        </tr>
    </tbody>
</table>

### **✅ Ejemplo Comparativo**
```c#
using System;

class Program
{
    // Constantes
    const double Pi = 3.14159;         // Tiempo de compilación.
    const string WelcomeMessage = "¡Bienvenido!";

    // Variables readonly
    readonly DateTime CreatedOn;       // Asignado en tiempo de ejecución.
    readonly string[] Names;

    public Program(string[] names)
    {
        CreatedOn = DateTime.Now;      // Permitido en el constructor.
        Names = names;                 // Arrays también permitidos.
    }

    static void Main()
    {
        Console.WriteLine($"Valor de Pi: {Pi}"); // Siempre fijo.
        Console.WriteLine($"Mensaje: {WelcomeMessage}");

        var program = new Program(new[] { "Ana", "Luis", "Carlos" });
        Console.WriteLine($"Creado el: {program.CreatedOn}");

        foreach (var name in program.Names)
            Console.WriteLine($"Nombre: {name}");
    }
}
```

### **🌟 Ventajas y Casos de Uso**
<table>
    <thead>
        <tr style="background-color: #e5e5e5">
            <th>Escenario</th>
            <th>Usar const</th>
            <th>Usar readonly</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Valores conocidos y fijos en tiempo de compilación.</td>
            <td>✅ Ejemplo: Pi, velocidad de la luz, etc.</td>
            <td>🚫 No necesario.</td>
        </tr>
        <tr>
            <td>Valores dinámicos que dependen de lógica o tiempo.</td>
            <td>🚫 No se puede usar.</td>
            <td>✅ Ejemplo: Fechas, objetos dinámicos.</td>
        </tr>
        <tr>
            <td>Tipos complejos como clases o arrays.</td>
            <td>🚫 No permitido.</td>
            <td>✅ Admite cualquier tipo.</td>
        </tr>
    </tbody>
</table>

### 🚀 **Conclusión**
- Usa const cuando los valores sean constantes y conocidos en tiempo de compilación.
- Usa readonly cuando necesites mayor flexibilidad para asignar valores en tiempo de ejecución o usar tipos complejos.
  
¡Conocer estas diferencias te ayudará a escribir código más claro y eficiente! 🎯
