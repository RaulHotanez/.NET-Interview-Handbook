# Tipos de datos más conocidos en C#

Este documento resume los tipos de datos más utilizados en C#, incluyendo primitivos, tipos por referencia y colecciones.

---

# Tipos primitivos

```csharp
int
long
short
byte
bool
char
float
double
decimal
```

## Características

- Son tipos de valor.
- Se almacenan normalmente en el stack.
- Tienen un tamaño fijo en memoria.
- Son muy eficientes.

---

# Tipos por referencia

```csharp
string
object
class
interface
array
delegate
record
```

## Características

- Se almacenan en el heap.
- Las variables guardan una referencia.
- Pueden tener tamaño dinámico.
- Son más flexibles.

---

# Colecciones en C#

## Array

Tamaño fijo.

```csharp
int[] numeros = { 1, 2, 3 };
```

### Características

- Tamaño fijo.
- Acceso muy rápido por índice.
- Estructura simple.

---

## List\<T>

La colección más utilizada en .NET.

```csharp
List<int> numeros = new List<int>();

numeros.Add(5);
```

### Ventajas

- Crece dinámicamente.
- Fácil de usar.
- Muy utilizada con Entity Framework.

---

## Dictionary<TKey, TValue>

Colección clave-valor.

```csharp
Dictionary<int, string> alumnos = new();

alumnos.Add(1, "Raúl");
alumnos.Add(2, "Pedro");
```

### Resultado

```text
1 -> Raúl
2 -> Pedro
```

### Características

- Búsqueda muy rápida por clave.
- Ideal para catálogos y cachés.

---

## Queue\<T>

Estructura FIFO (First In, First Out).

```csharp
Queue<int> cola = new();

cola.Enqueue(1);
cola.Enqueue(2);

cola.Dequeue();
```

### Ejemplo visual

```text
1
2
3
```

Sale primero el 1.

### Uso

- Impresoras
- Colas de tareas
- Procesamiento secuencial

---

## Stack\<T>

Estructura LIFO (Last In, First Out).

```csharp
Stack<int> pila = new();

pila.Push(1);
pila.Push(2);

pila.Pop();
```

### Ejemplo visual

```text
1
2
3
```

Sale primero el 3.

### Uso

- Undo / Redo
- Navegación de páginas
- Backtracking

---

## HashSet\<T>

Colección que no permite duplicados.

```csharp
HashSet<int> numeros = new();

numeros.Add(1);
numeros.Add(1);
```

### Resultado

```text
Solo se almacena un 1
```

### Características

- No permite elementos duplicados.
- Muy eficiente para búsquedas.
- Ideal para validaciones de existencia.

---

# Resumen rápido

| Tipo | Uso principal |
|------|--------------|
| Array | Datos de tamaño fijo |
| List\<T> | Colecciones dinámicas |
| Dictionary<TKey,TValue> | Búsqueda por clave |
| Queue\<T> | Procesamiento FIFO |
| Stack\<T> | Procesamiento LIFO |
| HashSet\<T> | Evitar duplicados |

---

# Uso en entrevistas

Estos tipos son fundamentales en entrevistas de C# porque evalúan:

- Conocimiento de estructuras de datos.
- Optimización de rendimiento.
- Uso correcto de colecciones en escenarios reales.

---

# Regla práctica

| Necesidad | Tipo recomendado |
|-----------|------------------|
| Datos fijos | Array |
| Lista dinámica | List\<T> |
| Búsqueda rápida | Dictionary |
| Cola de procesos | Queue |
| Deshacer acciones | Stack |
| Evitar duplicados | HashSet |