---
layout: post
title: "Tip 16: Keyed Services en .NET 8: Dependency Injection Avanzada"
---
# Keyed Services en .NET 8: Dependency Injection Avanzada  

🔥 **Keyed Services** es una nueva funcionalidad introducida en **.NET 8** que mejora la **Dependency Injection (DI)** permitiendo registrar **múltiples implementaciones** de una misma interfaz, pero diferenciadas mediante **claves (keys).**  
Esto es útil en escenarios donde necesitas una implementación específica de un servicio según el contexto, sin depender de condicionales o fábricas personalizadas.  

🔹 **Ejemplo de uso:** Si una aplicación soporta múltiples formas de notificación **(Email, SMS, Push)**, puedes registrarlas todas bajo la misma interfaz ```INotificationService```, asignándoles una clave para seleccionar la que necesitas en cada caso.  

### 🔹 Registro de Keyed Services en .NET 8
Para definir servicios con una clave específica, se utilizan los nuevos métodos en ```IServiceCollection```:  
<table>
  <thead>
    <tr style="background-color: #e5e5e5">
      <th>Método</th>
      <th>Ciclo de vida</th>
      <th>Uso</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>AddKeyedSingleton&lt;TService&gt;(key, implementation)</td>
      <td>Singleton</td>
      <td>Instancia única para toda la aplicación.</td>
    </tr>
    <tr>
      <td>AddKeyedScoped&lt;TService&gt;(key, implementation)</td>
      <td>Scoped</td>
      <td>Nueva instancia en cada petición (web request o scope).</td>
    </tr>
    <tr>
      <td>AddKeyedTransient&lt;TService&gt;(key, implementation)</td>
      <td>Transient</td>
      <td>Nueva instancia cada vez que se resuelve el servicio.</td>
    </tr>
  </tbody>
</table>
        
📌 **Ejemplo: Registro de múltiples implementaciones de ```INotificationService```**
```c#
var builder = WebApplication.CreateBuilder(args);

// Registramos dos implementaciones distintas bajo la misma interfaz
builder.Services.AddKeyedSingleton<INotificationService, EmailNotificationService>("Email");
builder.Services.AddKeyedSingleton<INotificationService, SmsNotificationService>("SMS");

var app = builder.Build();
```
### 🔹 Inyección de Keyed Services en Controladores y APIs 
🔸 **Opción 1: Usando ```[FromKeyedServices]``` en controladores**  
En ASP.NET Core, puedes inyectar un servicio específico en un **controlador** o **Minimal API** con el atributo ```[FromKeyedServices]```:
```c#
[ApiController]
[Route("api/notifications")]
public class NotificationController : ControllerBase
{
    // Inyectamos específicamente la implementación de Email
    public IActionResult SendNotification([FromKeyedServices("Email")] INotificationService service)
    {
        service.Send("Hola desde Keyed Services!");
        return Ok();
    }
}
```
✅ **Ventaja:** No necesitas modificar la lógica de la aplicación ni escribir código adicional para seleccionar la implementación.  

🔸 **Opción 2: Resolviendo manualmente desde ```IServiceProvider```**  
También puedes recuperar una implementación específica en cualquier parte del código usando ```GetKeyedService<T>```:
```c#
var notificationService = app.Services.GetKeyedService<INotificationService>("SMS");
notificationService?.Send("Mensaje enviado por SMS");
```
✅ **Ventaja:** Puedes elegir la implementación en tiempo de ejecución sin usar estructuras condicionales como if o switch.  

### 🔹 Comparación con Implementaciones Clásicas
Antes de .NET 8, la forma típica de gestionar múltiples implementaciones de una misma interfaz en DI era:

1️⃣ **Mediante Factories o Func&lt;T&gt;**
```c#
public class NotificationServiceFactory
{
    private readonly IServiceProvider _serviceProvider;

    public NotificationServiceFactory(IServiceProvider serviceProvider)
    {
        _serviceProvider = serviceProvider;
    }

    public INotificationService GetService(string type)
    {
        return type switch
        {
            "Email" => _serviceProvider.GetRequiredService<EmailNotificationService>(),
            "SMS" => _serviceProvider.GetRequiredService<SmsNotificationService>(),
            _ => throw new NotImplementedException()
        };
    }
}
```
📌 **Problema:** Código más extenso y propenso a errores, requiere manejar ```IServiceProvider``` manualmente.  

2️⃣ **Usando Diccionarios o Condicionales**
```c#
if (type == "Email")
    _notificationService = new EmailNotificationService();
else if (type == "SMS")
    _notificationService = new SmsNotificationService();
```
📌 **Problema:** Menos flexible, difícil de escalar cuando hay muchas implementaciones.  

🔹 **Con Keyed Services en .NET 8, estas soluciones ya no son necesarias** porque DI se encarga de todo.  
📌 **Resumen de las ventajas:**
<table>
  <thead>
    <tr style="background-color: #e5e5e5">
      <th>Enfoque</th>
      <th>Mantenimiento</th>
      <th>Escalabilidad</th>
      <th>Facilidad de uso</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Factory o Diccionario</td>
      <td>Difícil de mantener</td>
      <td>Difícil de escalar</td>
      <td>Requiere código extra</td>
    </tr>
    <tr>
      <td>Condicionales (if)</td>
      <td>No recomendado</td>
      <td>No escalable</td>
      <td>Código desordenado</td>
    </tr>
    <tr>
      <td>Keyed Services</td>
      <td>Más limpio y mantenible</td>
      <td>Escalable con claves</td>
      <td>Fácil de usar</td>
    </tr>
  </tbody>
</table>

### 🔹 Otros Casos de Uso de Keyed Services
📌 1️⃣ **Multi-tenant Applications**  
Si una aplicación necesita usar diferentes servicios según el tenant o cliente que lo usa, puedes definir distintas implementaciones y resolverlas dinámicamente según la configuración del usuario.
```c#
builder.Services.AddKeyedScoped<IDataAccess, SqlDataAccess>("SQL");
builder.Services.AddKeyedScoped<IDataAccess, NoSqlDataAccess>("NoSQL");
```
Dependiendo del tipo de base de datos requerida, se puede obtener el servicio correcto sin condicionales.  

📌 2️⃣ **Estrategias de Caché o Storage**  
Un sistema que necesita cambiar su almacenamiento entre **memoria, disco o cloud** podría beneficiarse de Keyed Services:
```c#
builder.Services.AddKeyedSingleton<IStorageService, InMemoryStorage>("Memory");
builder.Services.AddKeyedSingleton<IStorageService, DiskStorage>("Disk");
builder.Services.AddKeyedSingleton<IStorageService, CloudStorage>("Cloud");
```
Esto facilita la selección dinámica de la estrategia sin modificar el código base.

### 📌 Conclusión
**Keyed Services** en **.NET 8** ofrecen una solución elegante para manejar múltiples implementaciones de un mismo servicio en **Dependency Injection**, evitando estructuras condicionales y mejorando la mantenibilidad del código.  
✅ **Ventajas clave:**  
✔ Permite **registrar y resolver múltiples implementaciones** con un sistema de claves.  
✔ Reduce la necesidad de **factories o lógica condicional** para la inyección de dependencias.  
✔ Se integra perfectamente con **Minimal APIs y Controllers** en ASP.NET Core.  
✔ Proporciona **una forma más escalable y flexible** de gestionar dependencias en proyectos complejos.  

🚀 **¿Ya estás usando Keyed Services en tus proyectos? ¡Cuéntame tu experiencia!** 😃
