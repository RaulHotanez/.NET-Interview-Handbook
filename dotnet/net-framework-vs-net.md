## Diferencias Framework vs Core

## Diferencias entre .NET Framework y .NET Core / .NET

| Característica | .NET Framework | .NET Core / .NET (5+) |
|----------------|----------------|-------------------------|
| **Lanzamiento** | 2002 | 2016 (.NET Core), unificado como .NET 5+ en 2020 |
| **Sistema operativo** | Solo Windows | Windows, Linux y macOS |
| **Licencia** | Originalmente de código cerrado | Open Source |
| **Rendimiento** | Bueno, pero menor que .NET moderno | Más rápido y optimizado |
| **Multiplataforma** | ❌ No | ✅ Sí |
| **Contenedores (Docker)** | Soporte limitado | Soporte nativo y optimizado |
| **Despliegue** | Requiere que .NET Framework esté instalado | Puede ser Self-contained o Framework-dependent |
| **Servidor web** | Principalmente IIS | IIS, Kestrel, Nginx y Apache |
| **Microservicios** | Poco recomendable | Diseñado para microservicios |
| **Cloud** | Soporte limitado | Optimizado para la nube |
| **Actualizaciones** | Solo mantenimiento y parches de seguridad | Desarrollo activo con nuevas versiones |
| **Última versión** | 4.8.1 | .NET 9 (STS) / .NET 8 (LTS) |
| **Uso recomendado** | Mantener aplicaciones existentes | Nuevos proyectos y desarrollo moderno |

### Resumen

- **.NET Framework**
  - Solo funciona en Windows.
  - Ya no recibe nuevas funcionalidades, únicamente mantenimiento.
  - Ideal para mantener aplicaciones antiguas como Windows Forms, WPF o ASP.NET clásico.

- **.NET Core / .NET**
  - Es multiplataforma (Windows, Linux y macOS).
  - Es Open Source.
  - Ofrece mejor rendimiento.
  - Tiene soporte nativo para Docker y Kubernetes.
  - Es la opción recomendada para APIs REST, aplicaciones web, microservicios y aplicaciones en la nube.

### ¿Cuál elegir?

| Escenario | Recomendación |
|-----------|---------------|
| Proyecto nuevo | ✅ .NET 8 (LTS) o la versión LTS vigente |
| API REST | ✅ .NET |
| Microservicios | ✅ .NET |
| Docker | ✅ .NET |
| Linux | ✅ .NET |
| Aplicación antigua en Windows Forms o ASP.NET clásico | ✅ .NET Framework (si no se planea migrar) |

¿Cuál es la diferencia entre C# y .NET?
C# es el lenguaje; .NET es la plataforma de ejecución que proporciona el CLR, el runtime y las bibliotecas.
________________________________________
¿Qué versión de C# utilizas?
Una buena respuesta sería:
"He trabajado principalmente con C# 12 sobre .NET 8. Utilizo con frecuencia LINQ, expresiones lambda, async/await, records, pattern matching, nullable reference types, global using y primary constructors."
________________________________________
¿Qué versión de .NET has usado?
Con base en lo que hemos hablado en conversaciones anteriores sobre tu proyecto de inventario, una respuesta sólida sería:
"He trabajado principalmente con .NET 8 desarrollando APIs REST usando Clean Architecture, CQRS, MediatR, Entity Framework Core, JWT y SQL Server. También conozco las diferencias con .NET Framework y sé que .NET 8 es la versión LTS recomendada para nuevos desarrollos."
________________________________________
Para tu examen o entrevista, memoriza esta línea del tiempo
Año	C#	Característica destacada	Plataforma
2002	C# 1.0	Primera versión	.NET Framework 1.0
2005	C# 2.0	Generics	.NET Framework 2.0
2007	C# 3.0	LINQ, var, lambdas	.NET Framework 3.5
2010	C# 4.0	dynamic	.NET Framework 4.0
2012	C# 5.0	async/await	.NET Framework 4.5
2017	C# 7.x	Tuplas, Pattern Matching	.NET Core 2.x
2019	C# 8.0	Nullable Reference Types	.NET Core 3.1
2020	C# 9.0	Records	.NET 5
2021	C# 10	Global Using	.NET 6 (LTS)
2022	C# 11	required, Raw Strings	.NET 7
2023	C# 12	Primary Constructors, Collection Expressions	.NET 8 (LTS)
