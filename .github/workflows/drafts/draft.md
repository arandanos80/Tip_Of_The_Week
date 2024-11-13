---
layout: post
title: "Tip 7:  Uso de Span<T> y Memory<T>"
---

#  Uso de `Span<T>` y `Memory<T>`

💡 Uso de `Span<T>` y `Memory<T>` para Manipulación Eficiente de Datos en Memoria<br />
Introducidos en .𝗡𝗘𝗧 𝗖𝗼𝗿𝗲 𝟮.𝟭, los tipos `Span<T>` y `Memory<T>` ofrecen una forma eficiente de trabajar con subconjuntos de datos en memoria sin realizar copias adicionales. Estos tipos permiten manipular subconjuntos de arrays, cadenas de texto y buffers sin el coste de la asignación de memoria adicional, ayudando a evitar el garbage collection excesivo.

🟢 Ejemplo 1: Uso de `Span<T>` en arrays<br/>
`Span<T>` permite referenciar una porción de un array, permitiendo trabajar con segmentos de datos sin crear subarrays adicionales:

```c#
int[] numbers = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };

// Crear un Span que apunte a una parte del array original
Span<int> slice = numbers.AsSpan(2, 5);

foreach (var number in slice)
{
    Console.WriteLine(number); // Salida: 3, 4, 5, 6, 7
}
```

✅ Ventaja:
Este enfoque evita la creación de subarrays (Array.Copy o SubArray), optimizando el rendimiento al reducir asignaciones de memoria.

🟢 Ejemplo 2: Manipulación de Cadenas con `Span<char>`
```c#
string text = "Hello, .NET Developers!";
ReadOnlySpan<char> spanText = text.AsSpan();

ReadOnlySpan<char> greeting = spanText.Slice(0, 5);
ReadOnlySpan<char> title = spanText.Slice(7, 3);

Console.WriteLine(greeting.ToString()); // Salida: Hello
Console.WriteLine(title.ToString());    // Salida: .NE
```
✅ Ventaja:
Con `ReadOnlySpan<char>`, no se crean nuevas cadenas de texto, lo que hace más eficiente el manejo de strings, especialmente en aplicaciones de alto rendimiento.

🟢 Ejemplo 3: Uso de `Memory<T>` para Trabajos Asíncronos<br />
Cuando trabajamos con operaciones asíncronas que requieren la persistencia de un segmento en memoria, `Memory<T>` es más adecuado que `Span<T>`, ya que puede ser almacenado en el heap.

```c#
Memory<byte> memoryBuffer = new byte[1024];

// Operación simulada de llenado del buffer
await FillBufferAsync(memoryBuffer);
```
✅ Ventaja:
A diferencia de `Span<T>`, `Memory<T>` se puede usar en métodos asíncronos y permite un uso eficiente de la memoria para operaciones largas sin bloquear el hilo.

<b>Comparativa de Sustitución</b><br />
![image](https://github.com/user-attachments/assets/927030b8-161c-417d-985f-90f34ae21624)
<br />
🚀 Ventajas de `Span<T>` y `Memory<T>`<br />
Reducción de Asignaciones: No se crean copias de datos, lo que mejora el rendimiento y reduce el consumo de memoria.<br />
Mejoras en el Garbage Collection: Menos presión de recolección de basura, ya que `Span<T>` y `Memory<T>` permiten trabajar con datos existentes en memoria.<br />
Optimización en Subconjuntos: Se pueden manipular secciones de datos grandes de forma segura y eficiente.<br />
Estos tipos de datos son especialmente útiles en aplicaciones de alto rendimiento o en servicios donde la eficiencia de memoria es crítica. ¡Espero que este tip te sea útil!
