## Interfaces mas importantes

IEnumerable\<T>\
La más importante.
Representa una colección que puede recorrerse.
 ```csharp title="C#"
IEnumerable<int> numeros = new List<int>()
{
1,2,3,4
};
```
Puedes hacer
 ```csharp title="C#"
foreach(var n in numeros)
{
    Console.WriteLine(n);
}
```
Características
✅ Solo lectura (desde la perspectiva de la interfaz).
✅ Se puede recorrer.
✅ Muy usada con LINQ.

 
________________________________________
ICollection\<T>\
Hereda de IEnumerable.
Además, permite:
```csharp title="C#"
Add()
Remove()
Count()
```
Ejemplo
```csharp title="C#"
ICollection<int> numeros = new List<int>();
```
________________________________________
IList\<T>\
Hereda de ICollection.
Además, permite acceder por índice.
```csharp title="C#"
IList<int> numeros = new List<int>();

Console.WriteLine(numeros[0]);
```





________________________________________
IReadOnlyList\<T>\
Lista de solo lectura.
No puedes hacer
```csharp title="C#"
Add()
Remove()
```
Solo leer.
________________________________________
IReadOnlyCollection\<T>\
Colección únicamente de lectura.
 
________________________________________
IQueryable\<T>\
Muy importante si trabajas con Entity Framework.
Ejemplo
```csharp title="C#"
var productos = context. Productos
                        .Where(p => p.Stock > 0);
```
El tipo es
```csharp title="C#"
IQueryable<Producto>
```

La consulta todavía no se ejecuta.
Solo cuando haces
```csharp title="C#"
ToList()
First()
Count()
```

Entity Framework genera el SQL.
 
________________________________________
Diferencia entre IEnumerable e IQueryable
IEnumerable
```csharp title="C#"
var productos = lista.Where(x => x.Stock > 0);
```

El filtrado ocurre en memoria.
________________________________________
IQueryable
```csharp title="C#"
var productos = context.Productos
                       .Where(x => x.Stock > 0);
```

Entity Framework genera algo como:
```csharp title="C#"
SELECT *
FROM Productos
WHERE Stock > 0
```
Muchísimo más eficiente.
 
________________________________________
IEnumerable vs List
Pregunta clásica.
List
```csharp title="C#"
List<int>
```

Tiene
```csharp title="C#"
Add()
Remove()
Insert()
Sort()
```

________________________________________
IEnumerable
IEnumerable\<int>\
Solo permite recorrer.
No existe
```csharp title="C#"
Add()
```
 
________________________________________
object
Es la clase base de todos los tipos.
```csharp title="C#"
object x = 10;
object y = "Hola";
```

Todo deriva de object.
________________________________________
dynamic
El tipo se determina en tiempo de ejecución.
```csharp title="C#"
dynamic x = 10;
x = "Hola";
x = true;
```
________________________________________
Nullable\<T>\
Permite null en tipos por valor.
```csharp title="C#"
int? edad = null;
```
 
________________________________________
Span\<T>\
Muy usado en aplicaciones de alto rendimiento.
Permite trabajar con memoria sin copiar datos.
```csharp title="C#"
Span<int> datos = stackalloc int[10];
```

Suele aparecer en entrevistas de nivel intermedio o avanzado.
________________________________________
Memory\<T>\
Parecido a Span.
Puede vivir en el heap.
Muy utilizado en aplicaciones de alto rendimiento y procesamiento de datos.
________________________________________
ReadOnlySpan\<T>\
Versión de solo lectura.
Muy común para optimizar cadenas (string) sin crear nuevas copias.
________________________________________
Tipos genéricos
```csharp title="C#"
List<T>
Dictionary<TKey,TValue>
Queue<T>
Stack<T>
HashSet<T>
IEnumerable<T>
IQueryablable<T>
```
Los genéricos permiten reutilizar código para distintos tipos de datos.
________________________________________
¿Cuál es la diferencia entre IEnumerable, ICollection, IList e IQueryable?
Puedes responder:
•	IEnumerable\<T>\: permite recorrer una colección y es la base para trabajar con LINQ. No expone operaciones para modificar la colección. 
•	ICollection\<T>\: agrega operaciones como Add, Remove y la propiedad Count. 
•	IList\<T>\: además de lo anterior, permite acceder y modificar elementos por índice ([0]). 
•	IQueryable\<T>\: representa una consulta que puede traducirse a otro lenguaje (como SQL en Entity Framework). La consulta se ejecuta de forma diferida cuando se materializa con métodos como ToList(), First() o Count().
________________________________________
 
________________________________________
1. IEnumerable\<T>\
¿Qué es?
Es la interfaz más básica para representar una colección que puede recorrerse.
¿Para qué sirve?
Cuando solo necesitas leer o recorrer datos.
Ejemplo:
```csharp title="C#"
IEnumerable<Producto> productos = repository.ObtenerProductos();

foreach(var p in productos)
{
    Console.WriteLine(p.Nombre);
}
```

¿Por qué usarlo?
Porque quien consume el método no necesita saber si los datos vienen de:
•	List 
•	Array 
•	HashSet 
•	Entity Framework 
•	Un archivo 
•	Una API 
Solo necesita recorrerlos.
 
Ejemplo de entrevista
```csharp title="C#"
public IEnumerable<Producto> ObtenerProductos()
{
    return _context.Productos.ToList();
}
```
La persona que consume el método no puede hacer:
```csharp title="C#"
Productos.Add(...);
```

Eso protege la colección.
________________________________________
2. ICollection\<T>\
¿Qué es?
Es una colección que ya permite modificar sus elementos.
Tiene métodos como:
```csharp title="C#"
Add()
Remove()
Clear()
Count()
```
Ejemplo
```csharp title="C#"
ICollection<string> nombres = new List<string>();

nombres.Add("Raúl");
nombres.Remove("Pedro");
``` 

¿Para qué sirve?
Cuando necesitas agregar o eliminar elementos, pero no te interesa acceder por índice.
Muy utilizada en Entity Framework para representar relaciones.
Ejemplo:
```csharp title="C#"
public class Cliente
{
    public ICollection<Pedido> Pedidos { get; set; }
}
```
Porque un cliente puede tener muchos pedidos.
________________________________________
3. IList\<T>\
¿Qué es?
Es una lista completa.
Tiene todo lo anterior más:
```csharp title="C#"
[0]
Insert()
RemoveAt()
```

Ejemplo
```csharp title="C#"
IList<int> numeros = new List<int>();

numeros[0] = 100;
```

¿Para qué sirve?
Cuando necesitas trabajar por posición.
Ejemplo
```csharp title="C#"
var primerProducto = productos[0];
```
________________________________________
4. IReadOnlyCollection\<T>\
Solo permite leer.
No puedes modificar.
Ideal cuando quieres proteger una colección.
```csharp title="C#"
public IReadOnlyCollection<Producto> Productos
{
    get;
}
```
________________________________________
5. IReadOnlyList\<T>\
Igual que la anterior, pero además permite acceder por índice.
```csharp title="C#"
producto = productos [5];
```
Sin permitir:
```csharp title="C#"
Add()
Remove()
```
________________________________________
6. IQueryable\<T>\
Esta es una de las más preguntadas.
¿Qué es?
Representa una consulta que todavía no se ha ejecutado.
Ejemplo
```csharp title="C#"
var productos = context.Productos
                    .Where(p => p.Stock > 0);
``` 
Hasta aquí no ocurre nada.
La consulta se ejecuta cuando haces:
```csharp title="C#"
ToList();
o
First()
```
________________________________________
¿Para qué sirve?
Para que Entity Framework genere SQL.
Ejemplo
```csharp title="C#"
var productos = context.Productos
    .Where(p => p.Stock > 0)
    .OrderBy(p => p.Nombre)
    .Take (10)
    .ToList();
```
SQL generado:
```csharp title="C#"
SELECT TOP 10
FROM Productos
WHERE Stock > 0
ORDER BY Nombre
```
Muchísimo más eficiente.
________________________________________
7. List\<T>\
Es la implementación más utilizada.
```csharp title="C#"
List<Producto>
```
Sirve para todo.
```csharp title="C#"
Add()
Remove()
Insert()
Sort()
Reverse()
```
 ________________________________________
 
8. Dictionary<TKey,TValue>
Sirve para buscar información por llave.
Ejemplo
```csharp title="C#"
Dictionary<int,string> empleados = new();

empleados.Add(1, "Raúl");
```
Buscar
```csharp title="C#"
Console.WriteLine(empleados[1]);
```
Muy rápido.
________________________________________
9. Queue\<T>\
Cola. 
FIFO.
Ejemplo
```csharp title="C#"
Cliente 1
Cliente 2
Cliente 3
```
Sale primero el Cliente 1.
Usos
•	Impresoras 
•	Tickets 
•	Atención al cliente 
•	Procesamiento de tareas 
________________________________________
10. Stack\<T>\
Pila.
LIFO.
```csharp title="C#"
Pagina A
Pagina B
Pagina C
```
Si regresas:
```csharp title="C#"
Página C -> Página B
```
Usos
•	Deshacer (Undo) 
•	Navegación 
•	Backtracking 
________________________________________
11. HashSet\<T>\
No acepta repetidos.
Ejemplo
```csharp title="C#"
HashSet<int> ids = new();

ids.Add(1);

ids.Add(1);

ids.Add(1);
```
Resultado: 1
Muy útil para eliminar duplicados y comprobar si un elemento ya existe.
________________________________________
Jerarquía
```csharp title="C#"
IEnumerable -> ICollection -> IList
```
Cada una agrega más funcionalidades.
________________________________________
Ejemplo práctico
Supongamos un sistema de ventas.
El Repository
```csharp title="C#"
public IEnumerable<Producto> ObtenerProductos()
```
Solo quieres devolver datos.
No quieres que alguien haga:
```csharp title="C#"
productos.Add( ... )
```
 ________________________________________
El Servicio
 Necesitas agregar productos.
```csharp title="C#"
ICollection<Producto>
```
________________________________________
La Vista
```csharp title="C#"
IList<Producto>
```
Necesitas mostrar el producto número 3.
________________________________________
Entity Framework
```csharp title="C#"
IQueryable<Producto>
```
Quieres que SQL haga el trabajo.
________________________________________
 
¿Cuál usar en cada caso?
Tipo	¿Para qué sirve?	Caso de uso
IEnumerable\<T>	Recorrer datos	Devolver resultados, LINQ, foreach
ICollection\<T>	Agregar y quitar elementos	Relaciones en EF Core, colecciones modificables
IList\<T>	Trabajar por índice	Listas donde importa la posición
IReadOnlyCollection\<T>	Solo lectura	Exponer colecciones sin permitir cambios
IReadOnlyList\<T>	Solo lectura con índice	Mostrar datos sin modificarlos
IQueryable\<T>	Construir consultas diferidas	Entity Framework, generación de SQL
List\<T>	Implementación general	La colección más usada en memoria
Dictionary<TKey,TValue>	Búsqueda por clave	Catálogos, cachés, configuración
Queue\<T>	FIFO	Colas de impresión, procesamiento de tareas
Stack\<T>	LIFO	Deshacer, historial de navegación
HashSet\<T>	Elementos únicos	Evitar duplicados, búsquedas rápidas
________________________________________
 
Lo que más preguntan en entrevistas
Si la vacante es para ASP.NET Core con Entity Framework, estas cuatro son prácticamente obligatorias:
1.	IEnumerable\<T> → Para exponer y recorrer colecciones. 
2.	List\<T> → La implementación más común para trabajar en memoria. 
3.	IQueryable\<T> → Para consultas eficientes que Entity Framework traduce a SQL. 
4.	Dictionary<TKey,TValue> → Para búsquedas rápidas por clave. 
Una pregunta muy habitual es:
¿Por qué devolver IEnumerable\<T> en lugar de List\<T>\?
Una buena respuesta es:
"Porque programar contra interfaces reduce el acoplamiento. Si un método solo necesita exponer una secuencia de elementos para recorrerla, IEnumerable\<T> expresa esa intención y oculta los detalles de la implementación. Así, en el futuro puedo cambiar de List\<T> a otra colección sin afectar el código consumidor."
