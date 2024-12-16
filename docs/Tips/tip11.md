---
layout: post
title: "Tip 11: Inline Arrays"
---
# Inline Arrays
### 🔑 **Introducción**  
En C# 12, la anotación ```[InlineArray]``` introduce una forma de declarar arrays en línea, que permiten el almacenamiento optimizado de datos dentro de estructuras (```struct```) o clases, directamente en la memoria del objeto contenedor. Esto es útil en escenarios donde la eficiencia de memoria y el rendimiento son esenciales.

Con Inline Arrays, puedes trabajar con buffers de tamaño fijo sin necesidad de manejar arrays dinámicos en el heap. Esto es ideal para sistemas embebidos, gráficos y procesamiento de datos intensivos.  
### ✅ **Características clave**  
🔷 **Declaración de Arrays Embebidos**  
- Usando el atributo ```[System.Runtime.CompilerServices.InlineArray]```, defines un array de tamaño fijo dentro de una estructura.
- Los datos se almacenan directamente en la estructura, eliminando referencias adicionales al heap.
```c#
[System.Runtime.CompilerServices.InlineArray(50)]
public struct Buffer
{
    private int _element; // Representa los elementos embebidos.
}
```

🔷 **Acceso Seguro y Eficiente**  
- Aunque el almacenamiento es más compacto, puedes acceder a los elementos del array como si fueran parte de un array regular.

### ✅ **Ejemplo completo**
**Declaración:**  
```c#
using System.Runtime.CompilerServices;

[InlineArray(10)] // Define un array de tamaño fijo con 10 elementos.
public struct IntBuffer
{
    private int _element; // Este campo representa los 10 elementos del array.
}

public class Example
{
    public IntBuffer Buffer; // Usa el Inline Array dentro de la clase.

    public void FillBuffer()
    {
        for (int i = 0; i < 10; i++)
        {
            Buffer[i] = i * 2; // Almacena valores en el array.
        }
    }

    public void PrintBuffer()
    {
        for (int i = 0; i < 10; i++)
        {
            Console.WriteLine(Buffer[i]); // Imprime los valores.
        }
    }
}
```

**Uso:**
```c#
var example = new Example();
example.FillBuffer();
example.PrintBuffer();

// Salida esperada:
// 0
// 2
// 4
// 6
// 8
// 10
// 12
// 14
// 16
// 18

```

### ✅ **Ventajas**
<table>
    <thead>
        <tr style="background-color: #e5e5e5">
            <th>Característica</th>
            <th>Beneficio</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Almacenamiento en memoria contigua.</td>
            <td>Mayor eficiencia en el uso de memoria.</td>
        </tr>
        <tr>
            <td>Sin overhead del heap.</td>
            <td>Ideal para sistemas de bajo nivel o embebidos.</td>
        </tr>
        <tr>
            <td>Acceso eficiente.</td>
            <td>Rendimiento similar al de arrays tradicionales.</td>
        </tr>
        <tr>
            <td>Control de tamaño fijo.</td>
            <td>Reduce errores asociados a tamaños dinámicos.</td>
        </tr>
    </tbody>
</table>

### 🆚 **Comparativa con arrays tradicionales**  
<table>
    <thead>
        <tr style="background-color: #e5e5e5">
            <th>Inline Arrays (C# 12)</th>
            <th>Arrays Tradicionales</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Embebidos en el struct o clase.</td>
            <td>Referenciados en el heap.</td>
        </tr>
        <tr>
            <td>Tamaño fijo, definido en tiempo de compilación.</td>
            <td>Tamaño dinámico definido en tiempo de ejecución.</td>
        </tr>
        <tr>
            <td>Sin referencias adicionales.</td>
            <td>Necesitan punteros adicionales en memoria.</td>
        </tr>
        <tr>
            <td>Mejor rendimiento en memoria contigua.</td>
            <td>Menor eficiencia en operaciones de bajo nivel.</td>
        </tr>
    </tbody>
</table>

### 🌟 Escenarios de Uso  
1. **Buffers de datos pequeños y frecuentes:** Ejemplo, almacenamiento de vértices para gráficos.
2. **Sistemas embebidos:** Donde cada byte de memoria cuenta.
3. **Procesamiento intensivo:** Como en algoritmos que operan en bloques de datos contiguos.

### 🚀 Conclusión  
Los Inline Arrays con ```[InlineArray]``` son una herramienta poderosa en **C# 12** para optimizar memoria y rendimiento en aplicaciones críticas. Su uso es intuitivo y combina lo mejor de los arrays tradicionales con la eficiencia de estructuras compactas.
