# ¿Cómo identificarías por qué una aplicación está lenta?

En una entrevista, lo más importante es demostrar que **primero identificas el cuello de botella y después optimizas**, en lugar de hacer cambios sin evidencia.

---

# Pasos para diagnosticar el problema

## 1. Medir tiempos de respuesta de la API

Antes de optimizar, mediría cuánto tarda cada endpoint para identificar cuáles presentan problemas de rendimiento.

---

## 2. Revisar logs

Analizaría los logs para identificar:

- Endpoints lentos.
- Excepciones.
- Timeouts.
- Errores frecuentes.

---

## 3. Analizar las consultas SQL

Revisaría las consultas generadas por Entity Framework Core para verificar si son eficientes.

Buscaría problemas como:

- Consultas innecesarias.
- Demasiados JOIN.
- Uso de `SELECT *`.
- Consultas repetidas.

---

## 4. Verificar índices y planes de ejecución

En SQL Server revisaría:

- Índices faltantes.
- Índices no utilizados.
- Execution Plan.
- Table Scans.
- Deadlocks.

---

## 5. Evitar el problema N+1 y usar `AsNoTracking()`

Si solo necesito leer información:

```csharp
_context.Users
    .AsNoTracking()
    .ToListAsync();
```

También verificaría que Entity Framework no esté realizando una consulta por cada registro (problema N+1).

---

## 6. Proyectar únicamente los datos necesarios

En lugar de traer toda la entidad:

```csharp
_context.Users.ToListAsync();
```

Utilizaría:

```csharp
_context.Users
    .Select(u => new UserDto
    {
        Name = u.Name,
        Email = u.Email
    })
    .ToListAsync();
```

Esto reduce el tráfico entre la base de datos y la aplicación.

---

## 7. Implementar paginación

Si la consulta devuelve miles de registros:

```csharp
_context.Users
    .Skip((page - 1) * pageSize)
    .Take(pageSize);
```

Evita consumir memoria innecesariamente.

---

## 8. Evaluar el uso de caché

Si la información cambia poco:

- Memory Cache
- Distributed Cache
- Redis

Evita consultar la base de datos repetidamente.

---

## 9. Monitorear el servidor

Revisaría:

- Uso de CPU.
- Consumo de memoria.
- Disco.
- Pool de conexiones.
- Latencia de red.

Puede que el problema no sea el código.

---

## 10. Medir nuevamente

Después de aplicar cualquier optimización volvería a medir para comprobar que realmente hubo una mejora.

Nunca asumiría que un cambio mejoró el rendimiento sin medir antes y después.

---

# Herramientas útiles

- Visual Studio Profiler
- SQL Server Profiler
- Execution Plan
- Application Insights
- dotnet-trace
- dotnet-counters
- Serilog
- Postman
- Swagger

---

# Respuesta corta para entrevista

> "Primero identificaría el cuello de botella antes de realizar cualquier cambio. Mediría los tiempos de respuesta de la API, revisaría los logs, analizaría las consultas SQL y los índices de la base de datos, verificaría que Entity Framework no esté generando consultas N+1, usaría `AsNoTracking()` para consultas de solo lectura, proyectaría únicamente los datos necesarios con `Select()`, implementaría paginación cuando fuera necesario y evaluaría el uso de caché. Finalmente, volvería a medir para confirmar que la optimización realmente mejoró el rendimiento."

---

# Flujo recomendado

```text
Usuario
    │
    ▼
Medir tiempos
    │
    ▼
Revisar Logs
    │
    ▼
Analizar SQL
    │
    ▼
Optimizar Entity Framework
    │
    ▼
Revisar Servidor
    │
    ▼
Aplicar Caché
    │
    ▼
Volver a medir
```