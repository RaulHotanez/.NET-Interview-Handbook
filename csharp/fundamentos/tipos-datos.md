## Tipos de dato más conocidos
________________________________________
### Tipos primitivos
```csharp title="C#"
• int
• long
• short
• byte
• bool
• char
• float
• double
• decimal
```
________________________________________
### Tipos por referencia
```csharp title="C#"
• string
• object
• class
• interface
• array
• delegate
• record (C# moderno)
```
________________________________________
###  Colecciones
Array
Tamaño fijo.
```csharp title="C#"
int[] numeros = {1,2,3};
```
Acceso muy rápido.

________________________________________
### List\<T> 
La colección más utilizada.

```csharp title="C#"
List<int> numeros = new List<int>();

numeros.Add(5);
```

Ventajas
•	Crece automáticamente 
•	Fácil de recorrer 
•	Muy utilizada con Entity Framework 

________________________________________
### Dictionary<TKey,TValue>
Guarda datos por llave.
```csharp title="C#"
Dictionary<int, string> alumnos = new();

alumnos.Add(1, "Raúl");
```
Resultado
1 -> Raúl
2 -> Pedro
Búsquedas muy rápidas por clave.

________________________________________
### Queue<T>
FIFO
First In First Out
1
2
3
Sale primero el 1.

```csharp title="C#"
Queue<int> cola = new();
cola. Enqueue (1);
cola. Enqueue (2);
cola.Dequeue();
```
 ________________________________________
### Stack<T>
LIFO
Last In First Out
1
2
3
```csharp title="C#"
Stack<int> pila = new();
pila.Push(1);
pila.Push(2);
pila.Pop();
```
________________________________________
### HashSet<T>
No permite duplicados.
```csharp title="C#"
HashSet<int> numeros = new();
numeros. Add(1);
numeros.Add(1);
```
Solo queda un elemento.

