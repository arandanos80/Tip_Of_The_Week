---
layout: post
title: "Tip 15: Lazy&lt;T&gt;: Inicialización diferida para mejor rendimiento"
---
# ```Lazy<T>```: Inicialización diferida para mejor rendimiento
### 🔑 **Introducción**
En muchas aplicaciones, hay objetos que consumen muchos recursos y que **no siempre se necesitan** en el momento en que se crea la instancia de una clase. Para estos casos, podemos usar ```Lazy<T>```, que permite **retrasar la creación de un objeto hasta que realmente se necesite**, optimizando así el rendimiento y el uso de memoria.  

### 🚀 **¿Cómo funciona ```Lazy<T>```?**
```Lazy<T>``` envuelve un objeto y **sólo lo inicializa cuando se accede por primera vez a su valor**. Esto es útil en situaciones donde el costo de inicialización es alto, como conexiones a bases de datos, cálculos pesados o carga de datos desde una API externa.

### ✅ Ejemplo sin ```Lazy<T>``` (Carga inmediata)
Aquí el objeto ```ExpensiveObject``` se crea inmediatamente al instanciar ```MyClass```, aunque puede que nunca lo usemos.
```c#
class MyClass
{
    private ExpensiveObject _expensiveObject = new ExpensiveObject();

    public void UseObject()
    {
        Console.WriteLine(_expensiveObject.Data);
    }
}

class ExpensiveObject
{
    public string Data { get; } = "Objeto pesado inicializado";
}
```
**Problema**: El objeto se crea incluso si nunca llamamos a ```UseObject()```, lo que desperdicia memoria y CPU.

### ✅ Ejemplo con ```Lazy<T>``` (Inicialización diferida)
Con ```Lazy<T>```, el objeto se creará **sólo si realmente se necesita.**
```c#
class MyClass
{
    private Lazy<ExpensiveObject> _expensiveObject = new Lazy<ExpensiveObject>();

    public void UseObject()
    {
        Console.WriteLine(_expensiveObject.Value.Data); // Se inicializa aquí si aún no ha sido creado
    }
}

class ExpensiveObject
{
    public string Data { get; } = "Objeto pesado inicializado";
}
```
**Ventaja**: Si nunca se llama a ```UseObject()```, el ```ExpensiveObject``` **nunca se creará**, ahorrando memoria y tiempo de CPU.  

### 🌟 Ejemplo con ```Lazy<T>``` y Funciones Personalizadas
También podemos **personalizar la lógica de inicialización** usando un delegado ```Func<T>```.
```c#
class MyClass
{
    private Lazy<ExpensiveObject> _expensiveObject = new Lazy<ExpensiveObject>(() =>
    {
        Console.WriteLine("Inicializando ExpensiveObject...");
        return new ExpensiveObject();
    });

    public void UseObject()
    {
        Console.WriteLine(_expensiveObject.Value.Data);
    }
}
```
Aquí la inicialización imprime "Inicializando ExpensiveObject...", pero sólo cuando realmente se accede al objeto.

### 🔷 Comparación con inicialización normal  
<table>
  <thead>
    <tr style="background-color: #e5e5e5">
      <th>Método</th>
      <th>Carga inmediata</th>
      <th>Usando Lazy&lt;T&gt;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="font-weight: bold;">Cuando se inicializa</td>
      <td>Al instanciar la clase</td>
      <td>Al acceder por primera vez</td>
    </tr>
    <tr>
      <td style="font-weight: bold;">Uso de memoria</td>
      <td>Siempre ocupa espacio</td>
      <td>Sólo cuando se usa</td>
    </tr>
    <tr>
      <td style="font-weight: bold;">Mejor para</td>
      <td>Objetos livianos o siempre usados</td>
      <td>Objetos costosos o rara vez usados</td>
    </tr>
  </tbody>
</table>   

### 🔧 Cuándo Usar ```Lazy<T>```
✅ Cuando el objeto es **pesado de inicializar** y puede que **nunca se use**.  
✅ Cuando queremos **optimizar el rendimiento y el uso de memoria** en aplicaciones con recursos limitados.  
✅ Cuando queremos asegurar que un objeto **se crea de forma segura en entornos multi-hilo**, ya que ```Lazy<T>``` maneja esto automáticamente.  

### 💡 Conclusión
```Lazy<T>``` es una herramienta poderosa para mejorar el **rendimiento y la eficiencia de memoria**, asegurando que los objetos sólo se creen **cuando realmente se necesitan**. Si trabajas con objetos costosos en términos de CPU o memoria, esta técnica puede ayudarte a optimizar tu código. 

**❓ ¿Has usado ```Lazy<T>``` antes? ¿En qué situaciones crees que sería útil en tu código? 😃**
