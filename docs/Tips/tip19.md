---
layout: post
title: "Tip 19: Uso de CallerArgumentExpression"
---
# 💡 Usa ```CallerArgumentExpression``` para validaciones más claras  

🔍 Cuando estás validando argumentos en métodos, a menudo lanzas excepciones como ```ArgumentNullException```, ```ArgumentException```, etc. Pero… ¿y si pudieras capturar automáticamente **la expresión original** que se pasó como argumento, sin tener que escribirla tú mismo? 😮

A partir de **C# 10**, puedes usar el atributo ```[CallerArgumentExpression]``` para lograrlo.  


### ✅ ¿Qué hace?
Permite capturar **la expresión literal que el llamador pasó** a un parámetro, sin necesidad de escribir manualmente el nombre del parámetro o su contenido en los mensajes de error.  

### 🔧 Ejemplo clásico de validación:  
```c#
void Validate(string name)
{
    if (string.IsNullOrWhiteSpace(name))
        throw new ArgumentException("El parámetro 'name' no puede estar vacío");
}
```
⬇️ Esto obliga a escribir "name" manualmente y no es muy flexible.  

### 🔧 Ahora con ```CallerArgumentExpression```:
```c#
using System.Runtime.CompilerServices;

void Validate(string value, [CallerArgumentExpression("value")] string? paramName = null)
{
    if (string.IsNullOrWhiteSpace(value))
        throw new ArgumentException($"El parámetro '{paramName}' no puede estar vacío.");
}
```
### 📌 Llamada:
```c#
Validate(user.Name);
```
### 📌 Salida del error:
```c#
"El parámetro 'user.Name' no puede estar vacío."
```
🔹 ¡Captura literalmente lo que pasaste como argumento! 👏  

### 💡 Ejemplo realista: Validación de múltiples parámetros en un método de negocio  
Supongamos que tienes un servicio que registra un usuario, y necesitas validar varios parámetros:
```c#
public class UserService
{
    public void RegisterUser(string name, string email, string password)
    {
        Guard.NotNullOrWhiteSpace(name);
        Guard.NotNullOrWhiteSpace(email);
        Guard.NotNullOrWhiteSpace(password);

        // Resto de lógica para registrar el usuario...
    }
}
```
⬆️ Nada nuevo hasta aquí. Pero ahora vamos a crear la clase Guard para que use ```[CallerArgumentExpression]```.

### ✅ Implementación de Guard con ```CallerArgumentExpression```:
```c#
using System.Runtime.CompilerServices;

public static class Guard
{
    public static void NotNullOrWhiteSpace(
        string? value,
        [CallerArgumentExpression("value")] string? paramName = null)
    {
        if (string.IsNullOrWhiteSpace(value))
            throw new ArgumentException($"El parámetro '{paramName}' no puede ser nulo ni estar vacío.");
    }
}
```
### 💥 ¿Qué ganamos?
Cuando alguien llame a Guard.NotNullOrWhiteSpace(user.Email) y falle, el mensaje de error será:
```c#
"El parámetro 'user.Email' no puede ser nulo ni estar vacío."
```
Esto hace que los logs, los mensajes de error y el debug sean mucho más claros, especialmente cuando los valores provienen de expresiones complejas (por ejemplo: dto.User.Name).

### 🧠 Bonus: Validación de objetos complejos
Puedes usar este patrón también para validar propiedades dentro de DTOs:
```c#
public void ProcessOrder(OrderDto order)
{
    Guard.NotNull(order);
    Guard.NotNullOrWhiteSpace(order.CustomerId);
    Guard.NotNullOrWhiteSpace(order.ShippingAddress);
}
```
Si ShippingAddress falla, el error dirá:
```c#
"El parámetro 'order.ShippingAddress' no puede ser nulo ni estar vacío."
```

### 🌟 Ventajas  
<table>
  <thead>
    <tr style="background-color: #e5e5e5">
      <th>Característica</th>
      <th>Beneficio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Captura automática del argumento</td>
      <td>No necesitas escribir el nombre del parámetro manualmente</td>
    </tr>
    <tr>
      <td>Mejores mensajes de error</td>
      <td>Más claridad en logs y excepciones</td>
    </tr>
    <tr>
      <td>Útil en librerías reutilizables</td>
      <td>Mejora la trazabilidad cuando múltiples métodos llaman a tus validadores</td>
    </tr>
  </tbody>
</table>


### 🧪 Usos comunes  
- Métodos de validación de argumentos (```ThrowIfNull```, ```ThrowIfEmpty```, etc.)
- Librerías de utilidades compartidas
- APIs públicas que requieren buenos mensajes de error  

### ✅ Conclusión
El atributo ```[CallerArgumentExpression]``` te ayuda a construir mensajes de error más claros y automáticos, mejorando la mantenibilidad y la trazabilidad de tu código — especialmente en librerías o APIs. 💥
