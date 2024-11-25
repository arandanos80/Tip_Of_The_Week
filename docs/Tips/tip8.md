---
layout: post
title: "Tip 8: Default values para Tipos Genéricos"
---
# Default values para Tipos Genéricos
En C# 12, ahora puedes asignar valores predeterminados a los parámetros de tipo genéricos de tus métodos, clases o interfaces. Esta característica simplifica el uso de genéricos y mejora la legibilidad y flexibilidad del código.<br />
🚀 **Antes de C# 12** <br />
Antes, para usar un valor predeterminado en un parámetro genérico, debías establecerlo manualmente en cada instancia o utilizar verificaciones adicionales dentro del método. <br /><br />
**Ejemplo:**
```c#
public T MetodoGenerico<T>(T valor = default(T)) // ❌ Esto no era válido
{
    return valor;
}
```
El código anterior genera un error porque no se permitían valores predeterminados explícitos para tipos genéricos.

🆕 **C# 12: Default values para Tipos Genéricos**<br/>
Ahora puedes asignar un valor predeterminado directamente al parámetro genérico. Esto simplifica el diseño y reduce la cantidad de código redundante.<br /><br />
**Ejemplo**
```c#
public T MetodoGenerico<T = int>(T valor = default)
{
    return valor;
}
```
Con esta sintaxis:
- Si el usuario no proporciona un tipo, T será int por defecto.
- Si no proporciona un valor, valor será 0 (el valor predeterminado para int). <br /><br />

🔧 **Ejemplo Práctico** <br /><br />
**Definición:**<br />
```c#
// Uso en un método
public T MetodoGenerico<T = string>(T valor = default)
{
    return valor;
}
```
**Uso:** <br />
```c#
// Caso 1: Se usa el tipo predeterminado (string)
var resultado1 = MetodoGenerico(); // Resultado: null

// Caso 2: Se proporciona un tipo explícito
var resultado2 = MetodoGenerico<int>(); // Resultado: 0

// Caso 3: Se proporciona un valor explícito
var resultado3 = MetodoGenerico("Hola Mundo"); // Resultado: "Hola Mundo"
```
💡 **Ventajas** <br />
**1. Menos Código Redundante:** No necesitas inicializar manualmente valores predeterminados en cada instancia.<br />
**2. Mayor Flexibilidad:** Puedes definir comportamientos predecibles sin requerir sobrecargas adicionales.<br />
**3. Mejor Legibilidad:** Los valores predeterminados ayudan a entender las intenciones del código.<br />
<table>
    <thead>
        <tr style="background-color: #e5e5e5">
            <th>Funcionalidad</th>
            <th>C# 11 y Anteriores</th>
            <th>C# 12</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><strong>Valores predeterminados</strong></td>
            <td>No permitidos para parámetros genéricos</td>
            <td>Permitidos, usando <code>=</code> en la declaración</td>
        </tr>
        <tr>
            <td><strong>Cantidad de código requerido</strong></td>
            <td>Más código para inicializar y manejar sobrecargas</td>
            <td>Menos código gracias a valores predeterminados</td>
        </tr>
        <tr>
            <td><strong>Flexibilidad</strong></td>
            <td>Requiere sobrecargas o lógica adicional</td>
            <td>Más intuitivo y eficiente</td>
        </tr>
    </tbody>
</table>


✨ **Tip Adicional:** <br />
Aunque esta funcionalidad es poderosa, úsala con precaución para evitar que los valores predeterminados oculten comportamientos no deseados. Siempre documenta claramente el propósito de estos valores en tus métodos y clases.
