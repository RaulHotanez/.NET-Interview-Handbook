## Variables anónimas
________________________________________
En C#, una variable anónima normalmente se refiere a una variable que almacena un tipo anónimo (Anonymous Type).
Un tipo anónimo es un objeto que se crea sin definir previamente una clase.
Fue introducido en C# 3.0, junto con LINQ.
________________________________________
Ejemplo
Sin tipo anónimo:
```csharp title="C#"
public class Persona{
    public string Nombre { get; set; }
    public int Edad { get; set; }
}
Persona persona = new Persona
{
    Nombre = "Raul",
    Edad = 28
};
```
Aquí tuviste que crear una clase.
________________________________________
Con tipo anónimo:
```csharp title="C#"
var persona = new
{
    Nombre = "Raúl",
    Edad = 28
};
```
No existe una clase llamada Persona.
El compilador crea una clase internamente.
________________________________________
¿Por qué se usa var?
Porque el tipo no tiene nombre.
No puedes escribir algo como:
```csharp title="C#"
PersonaAnonima persona = ...
```
No existe.
Entonces el compilador infiere el tipo:
```csharp title="C#"
var persona = new
{
    Nombre = "Raúl",
    Edad = 28
};
```
 ________________________________________
¿Cómo acceder a las propiedades?
Como cualquier objeto:
```csharp title="C#"
Console.WriteLine(persona.Nombre);
Console.WriteLine(persona.Edad);
```
Salida:
Raúl
28
 
________________________________________
¿Para qué sirve?
Principalmente para proyecciones en LINQ.
Ejemplo:
```csharp title="C#"
var usuarios = _context.Users
    .Select(u => new
    {
        u.Nombre,
        u.Email
    })
    .ToList();
```
Cada elemento tiene únicamente:
Nombre
Email
No trae toda la entidad.
Esto mejora el rendimiento porque solo recuperas las columnas necesarias.
________________________________________
Otro ejemplo
Supongamos esta clase:
```csharp title="C#"
public class Empleado
{
    public int Id { get; set; }
    public string Nombre { get; set; }
    public decimal Salario { get; set; }
    public string Departamento { get; set; }
}
``` 

Solo necesitas el nombre:
```csharp title="C#"
var empleados = _context.Empleados
    .Select(e => new
    {
        e.Nombre
    })
    .ToList();
```
Cada objeto tendrá únicamente:
```csharp title="C#"
{
    Nombre = "Juan"
}
```
 ________________________________________
¿Son de solo lectura?
Sí.
Después de crearlo:
```csharp title="C#"
var persona = new
{
    Nombre = "Raúl"
};
```

No puedes hacer:
```csharp title="C#"
persona.Nombre = "Pedro";
```
Da error porque las propiedades son de solo lectura (read-only).
________________________________________
Diferencia entre var y tipo anónimo
Muchos los confunden.
Esto NO es un tipo anónimo:
```csharp title="C#"
var nombre = "Raúl";
```
El compilador sabe que nombre es un string.
Equivale a:
```csharp title="C#"
string nombre = "Raúl";
```
Aquí solo hay inferencia de tipos.
________________________________________
Esto SÍ es un tipo anónimo:
```csharp title="C#"
var persona = new
{
    Nombre = "Raúl",
    Edad = 28
};
```

Porque el objeto no tiene una clase definida.
________________________________________
¿Cuándo usar tipos anónimos?
✅ En consultas LINQ.
```csharp title="C#"
var resultado = _context.Productos
    .Select(p => new
    {
        p.Nombre,
        p.Precio
    });
```

✅ Cuando necesitas agrupar algunos datos temporalmente.
```csharp title="C#"
var datos = new
{
    Total = 100,
    Fecha = DateTime.Now
};
```

________________________________________
¿Cuándo NO usarlos?
No los uses cuando el objeto deba:
•	Pasarse entre capas de la aplicación. 
•	Devolverse desde una API. 
•	Reutilizarse en varios métodos. 
En esos casos es mejor crear una clase o un DTO.
Por ejemplo:
```csharp title="C#"
public class ProductoDto
{
    public string Nombre { get; set; }
    public decimal Precio { get; set; }
}
```

________________________________________
Pregunta típica de entrevista
¿Qué es un tipo anónimo en C#?
Una buena respuesta sería:
"Un tipo anónimo es un objeto cuyo tipo es generado automáticamente por el compilador y no tiene un nombre definido por el desarrollador. Se crea utilizando la palabra clave new junto con var y se utiliza principalmente en consultas LINQ para proyectar únicamente las propiedades necesarias, evitando crear clases temporales."

