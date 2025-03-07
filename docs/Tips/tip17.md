---
layout: post
title: "Tip 17: New Guard Clauses in .NET 8"
---
# New Guard Clauses in .NET 8  

### 🔑 **Introducción**
🔥 **.𝗡𝗘𝗧 𝟲** introdujo la verificación de null con ArgumentNullException.ThrowIfNull.  
🔥 **.𝗡𝗘𝗧 𝟳** extendió esta funcionalidad con ArgumentException.ThrowIfNullOrEmpty para manejar cadenas vacías.  
🔥 **.𝗡𝗘𝗧 𝟴** lleva los Guard Clauses al siguiente nivel con una gama más amplia de validaciones preconstruidas.  

Estos nuevos métodos ayudan a reducir código repetitivo y mejorar la legibilidad al validar parámetros de entrada en métodos y constructores.  

### 🚀 **Nuevas funcionalidades en .NET 8**  
✅ **ArgumentException**  

🔹 ```ThrowIfNullOrWhiteSpace(string?, string)``` ➜ Lanza una excepción si el string es null, vacío o solo contiene espacios en blanco.</span>

✅ **ArgumentOutOfRangeException**  

🔹 ```ThrowIfEqual<T>(T, T, string?)``` ➜ Lanza una excepción si los valores son iguales.

🔹 ```ThrowIfNotEqual<T>(T, T, string?)``` ➜ Lanza una excepción si los valores NO son iguales.

🔹 ```ThrowIfGreaterThan<T>(T, T, string?)``` ➜ Lanza una excepción si el primer valor es mayor que el segundo.

🔹 ```ThrowIfGreaterThanOrEqual<T>(T, T, string?)``` ➜ Lanza una excepción si el primer valor es mayor o igual que el segundo.

🔹 ```ThrowIfLessThan<T>(T, T, string?)``` ➜ Lanza una excepción si el primer valor es menor que el segundo.

🔹 ```ThrowIfLessThanOrEqual<T>(T, T, string?)``` ➜ Lanza una excepción si el primer valor es menor o igual que el segundo.

🔹 ```ThrowIfNegative<T>(T, string?)``` ➜ Lanza una excepción si el valor es negativo.

🔹 ```ThrowIfNegativeOrZero<T>(T, string?)``` ➜ Lanza una excepción si el valor es negativo o cero.

🔹 ```ThrowIfZero<T>(T, string?)``` ➜ Lanza una excepción si el valor es cero.  

### 🏆 **Ejemplo de uso**  
```c#
void ProcessPayment(decimal amount)
{
    ArgumentOutOfRangeException.ThrowIfLessThanOrEqual(amount, 0, nameof(amount));

    Console.WriteLine($"Processing payment of {amount:C}");
}

void SetUserName(string? name)
{
    ArgumentException.ThrowIfNullOrWhiteSpace(name, nameof(name));

    Console.WriteLine($"User name set to: {name}");
}
```
🔹 Antes de .NET 8, teníamos que escribir manualmente estas verificaciones.  
🔹 Ahora, con los nuevos **Guard Clauses**, podemos hacerlo de manera más limpia y segura.  

🚀 **Conclusión:** Menos código repetitivo, mejor mantenibilidad y mayor seguridad en la validación de parámetros.
