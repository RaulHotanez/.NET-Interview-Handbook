# ADO.NET vs Entity Framework Core

ADO.NET y Entity Framework Core son dos formas diferentes de acceder a una base de datos desde aplicaciones .NET.

- **ADO.NET** ofrece acceso de bajo nivel y control total sobre la base de datos.
- **Entity Framework Core** es un ORM que simplifica el acceso a los datos mediante objetos de C#.

---

# ¿Qué es ADO.NET?

ADO.NET es la tecnología de acceso a datos de bajo nivel de .NET.

Con ADO.NET tú:

- Escribes el SQL.
- Abres la conexión.
- Ejecutas la consulta.
- Lees los resultados.
- Cierras la conexión.

## Ejemplo

```csharp
using SqlConnection connection = new SqlConnection(connectionString);

connection.Open();

SqlCommand command = new SqlCommand(
    "SELECT Id, Name FROM Users",
    connection);

SqlDataReader reader = command.ExecuteReader();

while (reader.Read())
{
    Console.WriteLine(reader["Name"]);
}
```

## Con ADO.NET controlas todo

- Abrir la conexión.
- Cerrar la conexión.
- Escribir SQL.
- Leer resultados.
- Manejar transacciones.

---

# Ventajas de ADO.NET

- ✅ Muy rápido.
- ✅ Mayor control.
- ✅ Permite escribir SQL altamente optimizado.
- ✅ Consume poca memoria.

---

# Desventajas de ADO.NET

- ❌ Mucho código repetitivo.
- ❌ Más difícil de mantener.
- ❌ Debes mapear los datos manualmente.

Ejemplo del mapeo:

```csharp
User user = new User();

user.Id = (int)reader["Id"];
user.Name = reader["Name"].ToString();
```

---

# ¿Qué es Entity Framework Core?

Entity Framework Core (EF Core) es un **ORM (Object Relational Mapper)**.

Un ORM convierte automáticamente las tablas de la base de datos en objetos de C#.

En la mayoría de los casos ya no necesitas escribir SQL manualmente.

## Ejemplo

```csharp
var users = await _context.Users.ToListAsync();
```

Internamente EF genera algo parecido a:

```sql
SELECT *
FROM Users
```

Pero el desarrollador no escribe ese SQL.

---

# Insertar datos con Entity Framework

```csharp
var user = new User
{
    Name = "Raúl"
};

_context.Users.Add(user);

await _context.SaveChangesAsync();
```

EF genera internamente:

```sql
INSERT INTO Users(Name)
VALUES('Raúl')
```

---

# ¿Qué hace Entity Framework por ti?

- Convierte tablas en clases.
- Convierte filas en objetos.
- Genera SQL automáticamente.
- Maneja relaciones.
- Maneja transacciones.
- Rastrea cambios (Change Tracking).
- Permite usar LINQ.

---

# Ejemplo comparativo

## ADO.NET

```csharp
SqlCommand cmd = new SqlCommand(
    "SELECT * FROM Users WHERE Age > 18",
    connection);
```

## Entity Framework Core

```csharp
var users = await _context.Users
    .Where(x => x.Age > 18)
    .ToListAsync();
```

Como puedes observar, EF Core requiere mucho menos código.

---

# Comparación

| Característica | ADO.NET | Entity Framework Core |
|----------------|----------|------------------------|
| Escribes SQL | ✅ Sí | ❌ Normalmente no |
| Usa LINQ | ❌ No | ✅ Sí |
| Mapea objetos automáticamente | ❌ No | ✅ Sí |
| Rendimiento | ✅ Muy alto | ⚠️ Muy bueno, con una pequeña sobrecarga |
| Fácil de mantener | ❌ No | ✅ Sí |
| Curva de aprendizaje | Media | Baja a media |
| Control total del SQL | ✅ Sí | ⚠️ Parcial (puedes escribir SQL cuando sea necesario) |

---

# ¿Cuál es más rápido?

Generalmente:

**ADO.NET**

⬇

Mayor rendimiento

⬇

Porque no realiza:

- Change Tracking.
- Conversión automática a objetos.
- Abstracciones adicionales.

Sin embargo, la diferencia suele ser pequeña para la mayoría de las aplicaciones empresariales.

---

# ¿Cuál usan la mayoría de las empresas?

Actualmente, la mayoría de los proyectos utilizan **Entity Framework Core**.

Ejemplos:

- APIs REST.
- Microservicios.
- Aplicaciones empresariales.
- Sistemas de inventario.
- Sistemas administrativos.

ADO.NET sigue utilizándose cuando se requiere el máximo rendimiento o un control muy específico sobre las consultas.

---

# ¿Cuándo usar ADO.NET?

## 1. Consultas extremadamente optimizadas

Por ejemplo:

- Reportes con millones de registros.
- Consultas muy complejas.

---

## 2. Procedimientos almacenados complejos

```sql
EXEC GetSalesReport
```

Aunque EF Core puede ejecutar procedimientos almacenados, ADO.NET ofrece un control más directo.

---

## 3. Importaciones masivas

Por ejemplo:

- Insertar millones de registros.

---

## 4. Máximo rendimiento

Ideal para sistemas como:

- Bancarios.
- Trading.
- Telecomunicaciones.
- Procesamiento masivo de datos.

---

# ¿Cuándo usar Entity Framework Core?

## CRUD

- Crear.
- Leer.
- Actualizar.
- Eliminar.

Es el escenario donde EF Core destaca.

---

## APIs REST

Ejemplo:

```csharp
_context.Products
```

Muy sencillo y fácil de mantener.

---

## Desarrollo rápido

Entity Framework reduce significativamente la cantidad de código.

---

## Mantenimiento

Supongamos que cambias una propiedad:

Antes:

```csharp
Name
```

Después:

```csharp
FullName
```

Visual Studio puede ayudarte a refactorizar el código.

Si el SQL estuviera distribuido por toda la aplicación, el mantenimiento sería más complejo.

---

# ¿Se pueden usar juntos?

Sí.

Es bastante común encontrar proyectos que combinan ambos enfoques.

Ejemplo:

| Uso | Tecnología |
|------|------------|
| 95% de las consultas | Entity Framework Core |
| Reportes muy pesados | ADO.NET |
| Procesos masivos | ADO.NET |
| CRUD | Entity Framework Core |

---

# Respuesta recomendada para una entrevista

> **ADO.NET** es una tecnología de acceso a datos de bajo nivel donde el desarrollador escribe el SQL y administra conexiones, comandos y resultados manualmente. Ofrece mayor control y puede proporcionar un mejor rendimiento en escenarios específicos.
>
> **Entity Framework Core** es un ORM que permite trabajar con objetos de C# y consultas LINQ, generando automáticamente el SQL necesario. Es ideal para la mayoría de las aplicaciones empresariales y APIs por su productividad y facilidad de mantenimiento.
>
> Utilizaría **Entity Framework Core** para el desarrollo diario y **ADO.NET** en escenarios donde se requiera el máximo rendimiento, consultas altamente optimizadas o importaciones masivas de datos.

---

# Como desarrollador de .NET 8

En una entrevista puedes mencionar algo como:

> "Mi experiencia principal ha sido con Entity Framework Core en proyectos desarrollados con .NET 8, Clean Architecture, CQRS y MediatR. Sin embargo, también conozco ADO.NET y entiendo que Entity Framework Core utiliza internamente ADO.NET para comunicarse con la base de datos. Dependiendo del escenario, puedo elegir entre la productividad de EF Core o el control y rendimiento de ADO.NET."