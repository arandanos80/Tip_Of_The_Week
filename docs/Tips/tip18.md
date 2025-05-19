---
layout: post
title: "Tip 18: Novedades clave en .NET 10 Preview 4"
---
# Novedades clave en .NET 10 Preview 4  

### 🚀 El 13 de mayo de 2025, Microsoft ha anunciado la cuarta versión preliminar de .NET 10, introduciendo mejoras significativas en diversas áreas del ecosistema .NET. 
[Microsoft for Developers](https://devblogs.microsoft.com/dotnet/dotnet-10-preview-4)  

🧠 **Runtime**  
- **Análisis de escape para campos de estructuras locales:** Optimiza la asignación de memoria al determinar si los objetos referenciados en campos de estructuras pueden sobrevivir al método padre, permitiendo su asignación en el heap en lugar de la pila.
- **Mejoras en la inlining:** Incrementa el rendimiento al optimizar la inserción de métodos durante la compilación Just-In-Time (JIT). [Thurrott.com](https://www.thurrott.com/dev/320900/microsoft-delivers-net-10-preview-4)

📚 **Bibliotecas**  
- **Soporte de trazas fuera de proceso para eventos y enlaces de actividad:** Facilita la observabilidad y el diagnóstico en aplicaciones distribuidas.
- **Soporte para muestreo de trazas con limitación de tasa:** Permite controlar la cantidad de datos de trazas recopilados, mejorando el rendimiento y reduciendo la sobrecarga.
- **Nuevas APIs asincrónicas para archivos ZIP:** Responde a una solicitud común de la comunidad, permitiendo operaciones de compresión y descompresión de archivos ZIP de manera asincrónica.
- **Mejoras de rendimiento en GZipStream para flujos concatenados:** Optimiza la descompresión de múltiples flujos GZip concatenados.

🌐 **ASP.NET Core y Blazor**  
- **Mejoras en la gestión de páginas no encontradas en Blazor:** Proporciona una mejor experiencia de usuario al manejar rutas no existentes.
- **Precarga de activos web estáticos en Blazor:** Reduce los tiempos de carga inicial al precargar recursos necesarios.

📱 **.NET MAUI**  
- **Actualizaciones en MediaPicker y DatePicker:** Moderniza y mejora la experiencia de usuario en la selección de medios y fechas.
- **Mejoras de calidad en plataformas móviles y de escritorio:** Incluye mejoras para .NET en Android, iOS, Mac Catalyst, macOS y tvOS, aumentando la estabilidad y el rendimiento.

🧪 **SDK y C#**  
- **Sin nuevas características en esta preview:** No se han introducido nuevas funcionalidades en el SDK ni en el lenguaje C# en esta versión preliminar.

Para más detalles y descargar la Preview 4 de .NET 10, visita el anuncio oficial en el blog de Microsoft:
[Preview](https://devblogs.microsoft.com/dotnet/dotnet-10-preview-4)
