# Interfaces y tipos más importantes en C#

Este documento resume las interfaces y tipos genéricos más usados en .NET, especialmente en entrevistas técnicas y desarrollo con ASP.NET Core y Entity Framework.

---

# 1. IEnumerable\<T>

## ¿Qué es?
Es la interfaz más básica para representar una colección que puede recorrerse.

## ¿Para qué sirve?
Para **leer o recorrer datos**.

## Ejemplo

```csharp
IEnumerable<int> numeros = new List<int>()
{
    1, 2, 3, 4
};

foreach (var n in numeros)
{
    Console.WriteLine(n);
}
```

## Características

- Solo lectura (desde la interfaz).
- Permite recorrer elementos.
- Muy usada con LINQ.

---

# 2. ICollection\<T>

## ¿Qué es?
Hereda de `IEnumerable<T>` y permite modificar la colección.

## Métodos principales

- Add()
- Remove()
- Count

## Ejemplo

```csharp
ICollection<int> numeros = new List<int>();

numeros.Add(1);
numeros.Remove(1);
```

---

# 3. IList\<T>

## ¿Qué es?
Hereda de `ICollection<T>` y permite acceso por índice.

## Ejemplo

```csharp
IList<int> numeros = new List<int>();

Console.WriteLine(numeros[0]);
numeros[0] = 100;
```

## Características

- Acceso por índice.
- Inserción y eliminación por posición.

---

# 4. IReadOnlyCollection\<T>

## ¿Qué es?
Colección de solo lectura.

## Características

- No permite modificar.
- Solo permite recorrer y contar.

---

# 5. IReadOnlyList\<T>

## ¿Qué es?
Versión de solo lectura con acceso por índice.

## Ejemplo

```csharp
IReadOnlyList<int> numeros = new List<int>();

Console.WriteLine(numeros[0]);
```

## Características

- Solo lectura.
- Permite acceso por índice.

---

# 6. IQueryable\<T>

## ¿Qué es?
Representa una consulta que aún no se ejecuta.

## Ejemplo

```csharp
var productos = context.Productos
    .Where(p => p.Stock > 0);
```

## Importante

La consulta se ejecuta cuando llamas:

- ToList()
- First()
- Count()

## Ejemplo con SQL generado

```sql
SELECT *
FROM Productos
WHERE Stock > 0
```

## Uso principal

- Entity Framework Core
- Consultas a bases de datos
- LINQ diferido

---

# 7. List\<T>

## ¿Qué es?
La implementación más común en memoria.

## Ejemplo

```csharp
List<int> numeros = new List<int>();

numeros.Add(1);
numeros.Remove(1);
numeros.Sort();
```

## Características

- Muy flexible.
- Uso general en memoria.

---

# 8. Dictionary<TKey, TValue>

## ¿Qué es?
Colección clave-valor.

## Ejemplo

```csharp
Dictionary<int, string> empleados = new();

empleados.Add(1, "Raúl");

Console.WriteLine(empleados[1]);
```

## Uso

- Cachés
- Configuración
- Búsquedas rápidas

---

# 9. Queue\<T>

## ¿Qué es?
Cola FIFO (First In, First Out).

## Ejemplo

```text
Cliente 1
Cliente 2
Cliente 3
```

## Uso

- Tickets
- Impresoras
- Procesamiento de tareas

---

# 10. Stack\<T>

## ¿Qué es?
Pila LIFO (Last In, First Out).

## Ejemplo

```text
Página A
Página B
Página C
```

## Uso

- Undo / Redo
- Navegación
- Backtracking

---

# 11. HashSet\<T>

## ¿Qué es?
Colección que NO permite duplicados.

## Ejemplo

```csharp
HashSet<int> ids = new();

ids.Add(1);
ids.Add(1);
ids.Add(1);

// Resultado: 1
```

## Uso

- Eliminar duplicados
- Verificación rápida de existencia

---

# Jerarquía

```text
IEnumerable<T>
    ↓
ICollection<T>
    ↓
IList<T>
```

Cada nivel agrega más funcionalidades.

---

# IQueryable vs IEnumerable

| Característica | IEnumerable | IQueryable |
|----------------|------------|------------|
| Ejecución | En memoria | Base de datos |
| Rendimiento | Menor en grandes datos | Mejor en BD |
| Traducción SQL | ❌ No | ✅ Sí |
| Uso típico | Listas en memoria | Entity Framework |

---

# Ejemplo práctico (Entity Framework)

## Repository

```csharp
public IEnumerable<Producto> ObtenerProductos()
{
    return _context.Productos.ToList();
}
```

## Servicio

```csharp
ICollection<Producto>
```

## Vista

```csharp
IList<Producto>
```

## EF Core

```csharp
IQueryable<Producto>
```

---

# Tipos adicionales importantes

## object

Base de todos los tipos en C#.

```csharp
object x = 10;
object y = "Hola";
```

---

## dynamic

Tipo en tiempo de ejecución.

```csharp
dynamic x = 10;
x = "Hola";
```

---

## Nullable\<T>

Permite valores null en tipos valor.

```csharp
int? edad = null;
```

---

## Span\<T>

Alto rendimiento, sin asignación en heap.

```csharp
Span<int> datos = stackalloc int[10];
```

---

## Memory\<T>

Similar a Span pero puede vivir en el heap.

---

## ReadOnlySpan\<T>

Versión de solo lectura optimizada.

---

# ¿Cuáles preguntan más en entrevistas?

- IEnumerable\<T>
- List\<T>
- IQueryable\<T>
- Dictionary<TKey, TValue>

---

# Respuesta típica de entrevista

> "IEnumerable se usa para recorrer colecciones, ICollection agrega capacidad de modificación, IList permite acceso por índice, e IQueryable se usa en Entity Framework para construir consultas que se traducen a SQL y se ejecutan de forma diferida en la base de datos."

---

# Regla práctica

| Necesidad | Tipo recomendado |
|-----------|------------------|
| Solo leer datos | IEnumerable |
| Modificar colección | ICollection |
| Acceso por índice | IList |
| Consultas a BD | IQueryable |
| Uso general | List |
| Búsqueda rápida | Dictionary |