---
layout: post
title: "Tip 9: Primary Constructors para Clases y Structs"
---
# Primary Constructors para Clases y Structs
🚀 **¿Qué son los Primary Constructors?**\
En **C# 12**, los *Primary Constructors* se extienden a clases y structs (inicialmente introducidos en *record* en **C# 9**).\
Con esta característica, puedes definir directamente los parámetros del constructor en la declaración de la clase o struct. Estos valores estarán disponibles en todo el cuerpo de la clase, simplificando la inicialización y reduciendo el código redundante.  

✅ **Ventajas**
1. **Sintaxis Concisa:**\
Se eliminan declaraciones adicionales de propiedades y constructores explícitos.
2. **Legibilidad Mejorada:**\
Es claro qué valores necesita un objeto al momento de su creación.
3. **Menos Código Boilerplate:**\
No necesitas escribir manualmente el constructor y las asignaciones de propiedades.
4. **Ideal para Dependency Injection:**\
Facilita la inyección de dependencias en aplicaciones modernas.  

🔧 **Requisitos Previos**\
Para usar esta característica, necesitas:
- .NET 8 o superior.
- C# 12 o posterior habilitado en tu proyecto.

✅ **Ejemplo Básico con Clases**

```c#
using System;

public class Persona(string nombre, int edad)
{
    public void Presentarse()
    {
        Console.WriteLine($"Hola, mi nombre es {nombre} y tengo {edad} años.");
    }
}

class Program
{
    static void Main()
    {
        var persona = new Persona("Ana", 30);
        persona.Presentarse();

        // Salida: Hola, mi nombre es Ana y tengo 30 años.
    }
}

```

✅ **Ejemplo con Structs**
```c#
using System;

public struct Punto(int x, int y)
{
    public double DistanciaAlOrigen() => Math.Sqrt(x * x + y * y);
}

class Program
{
    static void Main()
    {
        var punto = new Punto(3, 4);
        Console.WriteLine($"Distancia al origen: {punto.DistanciaAlOrigen()}");

        // Salida: Distancia al origen: 5
    }
}

```
✅ **Ejemplo Avanzado con Dependency Injection**
```c#
using System;

public interface IRepositorio
{
    void Guardar(string mensaje);
}

public class Repositorio : IRepositorio
{
    public void Guardar(string mensaje) => Console.WriteLine($"Guardado: {mensaje}");
}

public class Servicio(IRepositorio repositorio)
{
    public void Ejecutar()
    {
        repositorio.Guardar("Ejecutando lógica de negocio...");
    }
}

class Program
{
    static void Main()
    {
        var repositorio = new Repositorio();
        var servicio = new Servicio(repositorio);
        servicio.Ejecutar();

        // Salida: Guardado: Ejecutando lógica de negocio...
    }
}

```
🌟 **Comparativa con Métodos Anteriores**  
<table>
    <thead>
        <tr style="background-color: #e5e5e5">
            <th>Método anterior</th>
            <th>Con Primary Constructors</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Declarar propiedades explícitamente</td>
            <td>Declarar parámetros en la definición de la clase</td>
        </tr>
        <tr>
            <td>Escribir un constructor para inicializar propiedades</td>
            <td>Constructor implícito con parámetros en la clase</td>
        </tr>
        <tr>
            <td>Código más extenso y repetitivo</td>
            <td>Código más conciso y limpio</td>
        </tr>
    </tbody>
</table>  

**Código Anterior (Sin Primary Constructors)** 
```c#
public class Persona
{
    public string Nombre { get; }
    public int Edad { get; }

    public Persona(string nombre, int edad)
    {
        Nombre = nombre;
        Edad = edad;
    }
}
```
**Código Actual (Con Primary Constructors)**  
```c#
public class Persona(string nombre, int edad) { }
```

🔥 **Casos de Uso**  
- Simplificar clases simples o DTOs (Data Transfer Objects).
- Facilitar el trabajo con DI en aplicaciones modernas.
- Reducir la complejidad en clases que solo necesitan inicializar sus propiedades.
